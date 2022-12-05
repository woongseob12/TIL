## 목차
1. [NGINX란?](#nginx란?)
2. [NGINX 구조](#nginx-구조)
3. [NGINX 설정](#nginx-설정)
4. [NGINX 사용 예시](#nginx-사용-예시)

## NGINX란?

![[nginx structure.png]]

- nginx는 웹서빙, 리버스 프록시, 로드 밸런싱, 캐싱 등을 수행할 수 있는 SW

[nginx 설치 공식문서](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/)

> mac OS의 경우 brew가 설치되어 있다면 쉽게 local test 가능
> 설치 : `brew install nginx`
> ![[nginx local directory.png]]
> 실행 : `brew services start nginx` 
> 설정파일 확인 : `cd {설치된 경로} && cat nginx.conf`
> 브라우저 확인 : 브라우저 `localhost:{port}`
> 프로세스 확인: pstree | grep nginx
> ![[nginx local pstree.png]]
> 

## NGINX-구조

![[nginx process structure.png]]
- **Master Process**
	- 설정, 포트 바인등 등과 같은 권한 작업 수행
	- worker process 관리
- Child Processes
	- Cache Manager:  Cache된 항목에 대한 만료, 크기 등 설정 값에 따라서 Cache를 삭제하는 작업을 수행
		 - `proxy_cache_path`설정이 있을 경우에만 생성
	- Cache Loader: Nginx가 시작시 실행되며, `disk-based cache`를 메모리에 적재
		- `proxy_cache_path`설정이 있을 경우에만 생성
	- **Worker Process**: 네트워크 연결, Disk I/O, upstream servers와 통신 등 client의 요청을 처리하는 프로세스


[nginx 구조 공식 블로그](https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/)

![[usage of webservers.png]]
APACHE SERVER와 차이점:
- Process Driven: 요청이 들어오면 커넥션을 형성하기 위해 프로세스를 할당
- Prefork 방식: 요청이 들어오기 전 미리 프로세스를 생성
- C10K: 동시에 많은 수의 클라이언트를 처리하기 위해 네트워크 소켓을 최적화하는 문제

### EVENT DRIVEN
- Connection의 연결, Client의 Http Request 처리, Connection의 종료까지의 모든 절차를 `Event`로 취급
- Worker Process는 처리해야할 Event를 **Working Queue**를 담고 순차적으로 처리
- **Thread Pool**: 오래 걸리는 작업(ex. Disk I/O)을 처리하는 Thread를 미리 할당
  ![[nginx thread pool.png]]

## NGINX-설정

```nginx
worker_processes auto;

events {
	worker_connections 1024;
}

http {
	include mime.types;
	default_type application/octet-stream;
	sendfile on;
	keepalive_timeout 65;
	
	types {
	    text/html html htm;
	    text/css css;
	    application/xml xml;
	    application/javascript js;
	}
	
	gzip_vary on;
	gzip_proxied any;
	gzip_comp_level 6;
	gzip_types text/html text/css application/xml application/javascript;

	server {
		listen 3000;
		server_name _;
  
		location / {
		    root /home1/irteam/webapp;
		    index index.html index.htm;
		    try_files $uri $uri/ /index.html =404;
		}
	}
}
```

`worker_processes`: Worker Process 수 설정
- CPU 코어당 1개의 Worker process 권장
`worker_connections` : Worker Process가 동시에 처리할 수 있는 커넥션 수 설정
`http`: 웹서버에 대한 동작 설정
`include`: 포함시킬 외부파일 설정
`mime.type`: 파일 확장명과 MIME 타입 목록
`default_type` : 웹서버의 기본 Content-Type 설정
`sendfile`: nginx에서 정적파일을 보내도록 설정
`keepalive_timeout`: 커넥션 연결 유지 시간 설정
`gzip`: gzip 압축 전송 설정
`server`: 하나의 웹사이트를 선언
`listen`: 해당 포트로 들어오는 요청을 해당 `server {}` 블록의 내용에 맞게 처리
`server_name`: 한 개 이상의 호스트명을 지정
- HTTP 요청 헤더의 `Host` 값으로 판단한다.
- 매핑되는 server_name이 없을 경우 처음 혹은 `listen default_server`로 지정한 server로 매핑
`location`: url에 따른 처리 방식 설정
`root`: static 파일 경로
`index`: index 파일 설정
`try_files`:  요청을 처리할 파일이 존재하는지 순서대로 확인하며 존재하는 파일을 제공

## NGINX-사용-예시

#### Proxy Server
- `cvmogligw01.clova`, `cvmogligw02.clova`, `cvmogligw03.clova` 서버에 `kaa`, `beta-kaa`, `dev-kaa`의 Proxy Server(nginx) 존재
- nginx 설정 파일 편집을 통해 CORS 설정 추가

```nginx
server {
        ...
        server_name  beta-kaa.clova.ai;
        ...
        location / {

                if ($request_method = OPTIONS) {
                        add_header 'Access-Control-Allow-Origin' '*';
                        add_header 'Access-Control-Allow-Methods' 'GET,POST,PUT,DELETE,OPTIONS,HEAD';
                        add_header 'Access-Control-Allow-Headers' 'X-KAA-APIAUTH, Authorization, Origin, Access, DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Pragma';
                        return 200;
                }
                if ($http_origin ~* (navercorp\.com$|clova\.ai$)) {
                        add_header 'Access-Control-Allow-Origin' '$http_origin';
                }
                add_header 'Access-Control-Allow-Methods' 'GET,POST,PUT,DELETE,OPTIONS,HEAD';
                ....

        }
}
``````

[Nginx Revese Proxy 문서](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)

#### Load Balancer

```nginx
http {
    upstream backend {
		# no load balancing method is specified for Round Robin
        server backend1.example.com weight=5;
        server backend2.example.com;
        server 192.0.0.1 backup;
    }
    
    server {
        location / {
            proxy_pass http://backend;
        }
    }
}
```

[Nginx Load Balancer 문서](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/)
