# FTP

**FTP(File Transfer Protocol)**: 인터넷을 통한 파일 송수신을 위해 고안된 프로토콜(통신규약)

![image](https://user-images.githubusercontent.com/55429912/125189193-d3f28400-e271-11eb-9e68-f5262ac87cbf.png)

- 호스트 간에 두 개의 연결을 설정(데이터 전송, 제어)

- Well Known Port(0~ 1023번): 20, 21번 사용

  | 포트 | TCP/UDP | 설명                                                         |
  | ---- | ------- | ------------------------------------------------------------ |
  | 20   | TCP     | FTP 데이터 전송을 위한 데이터 포트<br> - 파일 전송 때마다 설정, **전송이 완료되면 폐쇄** |
  | 21   | TCP     | FTP 명령, 인증 등 제어를 위한 제어 포트<br> - FTP세션 동안 계속 **연결 상태를 유지** |

  

**FTP 종류**

1. Active mode

   ![image](https://user-images.githubusercontent.com/55429912/125189084-72cab080-e271-11eb-955d-41f5e795b671.png)

   - 서버에서 클라이언트로 접속하여 데이터를 전송하는 방식
     - 클라이언트 PC에 방화벽이 설치되어 외부에서 접속을 허용하지 않을 경우, FTP 접속은 되지만 데이터 채널 연결이 되지 않아 파일을 받을 수 없는 문제 발생

   - 동작 순서

     ```
     ① Client에서 Server의 21번 포트로 접속 후, Client가 사용한 데이터 전송용 포트를 서버에 알려줌
     ② Server는 이에 대해 Ack로 응답
     ③ Server의 20번 포트는 Client가 알려준 데이터 전송용 포트에 접속을 시도
     ④ Client가 Ack로 응답
     ```

     

2. Passive mode

   ![image](https://user-images.githubusercontent.com/55429912/125189106-84ac5380-e271-11eb-81fd-264957aab09b.png)

   - 클라이언트에서 서버로 접속하여 데이터를 전송하는 방식

     - 서버의 비특권(unpriviledged) 포트를 모두 열어두어야 함
     - Passive mode로 접속 시 사용할 수 있는 포트를 제한 설정할 수 있는 기능 지원

   - 일반 웹브라우저들의 Default 설정

   - 동작 순서

     ```
     ① Client에서 Server의 21번 포트로 접속 시도
     ② Server는 이에 대해 Server가 사용할 데이터 전송용 포트(2042)로 응답
     ③ Client는 다른 포트를 열어 Server가 알려준 데이터 전송용 포트(2042)로 접속을 시도
     ④ Server가 Ack로 응답
     ```

     
