# Build Tool

**Build Tool(빌드 도구)**: **빌드 자동화**를 통해 실행 가능한 프로그램으로 바꿔주는 도구

- 빌드: 소스 코드를 컴파일, 테스트, 정적분석 등을 실행하여 실행 가능한 애플리케이션으로 만들어 주는 과정

- 빌드 자동화: 소스 코드를 실행 가능한 프로그램이 나오기까지의 과정을 자동화 하는 것

- 라이브러리를 자동 추가 및 관리
- 시간이 지남에 따라 아비르러리의 버전을 자동으로 동기화



# Maven

- **공식적인 규약**을 통한 빌드 파일의 표준화
- pom.xml을 통해 필요한 라이브러리를 자동으로 불러오고 관리

```xml
<dependency>
	<groupId>org.springFramework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```



# Gradle

- 동적인 스크립트로 설정 파일을 작성(유연함)

- Groovy 기반의 DSL(Domain Specific Language)을 사용

  > Groovy는 JVM에서 실행되는 스크립트 언어로 문법이 Java와 비슷하며, Java와 호환이 되어 Java 클래스 파일을 그대로 Groovy 클래스로 사용할 수 있음

- Gradle 설치 없이 Gradle Wrapper를 이용하여 빌드 지원

- 성능

  - **Incremental Builds: 빌드 실행 중 마지막 빌드 호출 이후에 task의 입력, 출력 혹은 구현이 변경 됐는지 확인. 최신 상태로 간주하지 않는다면 빌드는 실행되지 않음
  - **Build Cache**: task가 이미 다른 컴퓨터에서 실행된 경우 Gradle은 로컬 실행을 건너뛰고 빌드 캐시로부터 작업의 결과물을 가져올 수 있음
  - **Gradle Daemon**: 빌드하는 인스턴스를 유지, 빌드가 끝난뒤에도 사라지지 않고 백그라운드에서 대기

  

- Build Lifecycle

  1. Initialization(초기화): 빌드 대상 프로젝트를 결정하고 각각에 대한 프로젝트 객체를 생성
     - settings.gralde 파일에서 프로젝트 구성(멀티프로젝트, 싱글프로젝트 구분)
  2. Configuration(구성): 빌드 대상이 되는 모든 프로젝트의 빌드 스크립트를 실행(프로젝트 객체 구성)
     - configured Task 실행

  3. Exectuion(실행): 구성 단계에서 생성하고 설정된 프로젝트의 Task 중에 실행 대상 결정

     - gradle 명령행에서 지정한 Task 이름 인자와 현재 디렉토리를 기반으로 Task를 결정하여 선택된 Task들을 실행

       

- Build 설정 파일

  ![image](https://user-images.githubusercontent.com/55429912/125277478-6e26fa80-e34c-11eb-85ad-7086cba99466.png)

  - gradlew: Linux 또는 MAC OS 용 실행 쉘 스크립트 파일

  - gradlew.bat: Windows용 실행 배치 스크립트 파일

  - settings.gradle: 프로젝트 구성 설정(싱글 프로젝트의 경우 생략 가능)

  - build.gradle: 빌드에 대한 모든 기능 정의

    - ext: build.gradle에서 사용하는 전역변수 설정

      ![image](https://user-images.githubusercontent.com/55429912/125275315-d7593e80-e349-11eb-96c6-e45fdc98fec1.png)

    - repositories: 라이브러리들을 가져올 레파지토리 설정 

      ![image-20210712195843238](C:\Users\woong\AppData\Roaming\Typora\typora-user-images\image-20210712195843238.png)

    - dependencies: 사용할 라이브러리 설정

      ![image](https://user-images.githubusercontent.com/55429912/125276978-d75a3e00-e34b-11eb-9521-1719251da9b4.png)

    