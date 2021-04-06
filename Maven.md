# Maven

+ 1. 빌드
    - 소스코드 파일을 컴퓨터에서 실행할 수 있는 독립 소프트웨어 가공물로 변환하는 과정 또는 그에 대한 결과물이다.
    - java, xml, jpg, jar 을 JVM, 톰캣 같은 WAS가 인식할 수 있는 구조로 패키징하는 과정 및 결과물

+ 2. 빌드 도구
    - 프로젝트 생성, 테스트 빌드, 배포 등의 작업을 위한 전용 프로그램
    - 빠른 기간 동안 늘어나는 라이브러리 추가, 프로젝트를 진행하며 라이브러리의 버전 동기화의 어려움을 해소하고자 등장
    - 초기에는 java에서는 Ant를 사용. 최근에는 Maven, Gradle 사용


+ 3. MAVEN 이란
    - 자바용 프로젝트 관리 도구. Apache Ant의 대안으로 만들어짐.
    - Ant와 마찬가지로 프로젝트의 라이프 사이클을 관리하는 도구.
    - Maven은 필요한 라이브러리를 특정 문서(pom.xml)에 정의해 놓으면 내가 사용할 라이브러리 뿐만 아니라 해당 라이브러리가 작동하는 데에 필요한 다른 라이브러리까지 관리. 네트워크를 통해 자동으로 다운로드.
    - Maven은 중앙 저장소를 통한 자동 의존성 관리를 중앙 저장소(아파치 재단에서 운영 관리)는 라이브러리를 공유하는 파일 서버라고 볼 수 있고, 메이븐은 자기 회사만의 중앙 저장소를 구축할 수도 있다.
    - 간단한 설정을 통한 배포 관리가 가능.
   

+ 4. Ant vs Maven
    1. Ant는 자유도가 높은 편 (전처리, 컴파일, 패키징, 테스팅, 배포까지 가능)
    2. Maven은 정해진 라이프 사이클에 의하여 작업 수행. 전반적인 프로젝트 관리 기능까지 포함.
    

+ 5. Maven LifeCycle
    1. LifeCycle
        - 미리 정해진 빌드 순서가 있다.
        - 메이븐은 프레임워크. 동작 방식이 정해져 있고, 미리 정의하고 있는 빌드 순서가 존재. 이를 라이프사이클.
            + Default(Build) : 일반적인 빌드 프로세스를 위한 모델
            + Clean : 빌드 시 생성되었던 파일들을 삭제
            + Validate : 프로젝트가 올바른 지 확인하고 필요한 모든 정보를 사용할 수 있는 지 확인하는 단계
            + Compile : 프로젝트의 소스코드를 컴파일 하는 단계
            + Test : 유닛 테스트를 수행하는 단계 (테스트 실패 시 빌드 실패로 처리, 스킵 가능)
            + Package : 실제 컴파일된 소스 코드와 리소스들을 jar, war 등등의 파일 등의 배포를 위한 패키지로 만드는 단계
            + Verify : 통합 테스트 결과에 대한 검사를 실행하여 품질 기준을 충족하는 지 확인하는 단계
            + Install : 패키지를 로컬 저장소에 설치하는 단계
            + Site : 프로젝트 문서와 사이트 작성, 생성하는 단계
            + Deploy : 만들어진 package를 원격 저장소에 release하는 단계
             
            - 최종 빌드 순서는 compile=>test=>package이다.
            1. compile : src/main/java 디렉토리 아래의 모든 소스 코드가 컴파일 된다.
            2. test : src/test/java, src/test/resources 테스트 자원 복사 및 테스트 소스 코드 컴파일 된다.
                (junit: 단위 테스트 프레임워크. 테스트 단계를 거치기 위해 의존 설정을 해준다.)
            3. packaging : 컴파일과 테스트가 완료된 후, jar, war같은 형태로 압축하는 작업.
            
     2. Phase(단계)
         - Build Lifecycle의 각각의 단계를 Phase라고 한다.
         - Phase는 의존관계를 가지고 있어 해당 Phase가 수행되려면 이전 단계의 Phase가 모두 수행되어야 한다.
         - 즉, 모든 빌드단계는 이전 단계가 성공적으로 실행되었을 때 실행 된다는 것이 Dependency이다.
         
     3. Goal
         - 특정 작업, 최소한의 실행 단위(task).
         - 하나의 플러그인에서는 여러 작업을 수행할 수 있도록 지원하며, 플러그인에서 실행할 수 잇는 각각의 기능(명령)을 Goal이라고 한다.
             (각각의 Phase에 연계된 Goal를 실행하는 과정을 Build라고 한다.)
         - 플러그인의 goal을 실행하는 방법은 다음과 같다.
             + - mvn groupId:artifactId:version:goal(아래와 같이 생략 가능)
             + - mvn plugin:goal
             
     4. Maven
         1. settings.xml
             - 메이븐 빌드 툴과 관련한 설정파일
             - MAVEN_HOME/conf 디렉토리에 위치 (메이븐 설치 시 기본 제공)
             - settings.xml의 설정
             
             + 메이븐을 빌드할 때 의존 관계에 있는 라이브러리, 플러그인을 중앙 저장소에서 개발자 PC로 다운로드하는 위치(로컬저장소)의 기본 설정 'USER_HOME/.m2/repository'인데 settings.xml에 원하는 로컬 저장소의 경로를 지정, 변경할 수 있다.
         
         2. POM(프로젝트 객체 모델(Project Object Model))
             - POM은 pom.xml 파일을 말하며 pom.xml은 메이븐을 이용하는 프로젝트의 root에 존재하는 xml 파일이다.
                 (하나의 자바 프로젝트에 빌드 툴을 maven으로 설정하면, 프로젝트 최상위 디렉토리에 "pom.xml"이라는 파일이 생성된다.)
             - Maven의 기능을 이용하기 위해서 POM이 사용된다.
             - 파일은 프로젝트마다 1개이며, pom.xml만 보면 프로젝트의 모든 설정, 의존성 등을 알 수 있다.
             - 다른 파일이름으로 지정가능. 하지만 pom.xml으로 사용하기를 권장
             - 엘리먼트
                 + modelVersion : POM model의 버전
                 + parent : 프로젝트의 계층 정보
                 + groupId : 프로젝트를 생성하는 조직의 고유 아이디를 결정. 일반적으로 도메인 이름을 거꾸로 적는다.
                 + artifactId : 프로젝트 빌드 시 파일 대표이름. groupId 내에서 유일해야 한다. Maven을 이용하여 빌드 시 다음과 같은 규칙으로 파일이 생성된다. artifactId-version.packaging. 밑의 예의 경우 빌드할 경우 bo-0.0.1-SNAPSHAT.war 파일이 생성된다. (하단 예시 파일 참고)
                 + version : 프로젝트의 현재 버전, 프로젝트 개발 중일 때는 SNAPSHAT을 접미사로 사용.
                 + packaging : 패키징 유형(jar,war,ear 등)
                 + name : 프로젝트, 프로젝트 이름
                 + description : 프로젝트에 대한 간략한 설명
                 + url : 프로젝트에 대한 참고 Reference 사이트
                 + propertes : 버전 관리 시 용이하다. ex) 하단 자바 버전을 선언하고 dependencies에서 다음과 같이 활용 가능.
                 +   ``` <version>${java.version}</version>```
                 + dependencies : dependencies 태그 안에는 프로젝트와 의존 관계에 있는 라이브러리들을 관리한다.
                 + build : 빌드에 사용할 플러그인 목록
                 
                 
         
        

```
<?xml version="1.0" encoding="UTF-8"?> <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd"> 
<modelVersion>4.0.0</modelVersion> <!--POM model의 버전--> 

<parent> <!--프로젝트의 계층 정보--> 
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId> 
    <version>2.2.4.RELEASE</version> <relativePath/> <!-- lookup parent from repository --> 
    
</parent> 
<groupId>com.god</groupId> <!--프로젝트를 생성하는 조직의 고유 아이디를 결정한다. 일반적으로 도메인 이름을 거꾸로 적는다.--> 
<artifactId>bo</artifactId> <!--프로젝트 빌드시 파일 대표이름 이다. groupId 내에서 유일해야 한다.Maven을 이용하여 빌드시 다음과 같은 규칙으로 파일이 생성 된다. artifactid-version.packaging. 위 예의 경우 빌드할 경우 bo-0.0.1-SNAPSHOT.war 파일이 생성된다.-->

<version>0.0.1-SNAPSHOT</version> <!--프로젝트의 현재 버전, 프로젝트 개발 중일 때는 SNAPSHOT을 접미사로 사용-->
<packaging>war</packaging> <!--패키징 유형(jar, war, ear 등)-->
<name>bo</name> <!--프로젝트, 프로젝트 이름--> 
<description>Demo project for Spring Boot</description>
<!--프로젝트에 대한 간략한 설명--> 
<url>http://goddaehee.tistory.com</url> <!--프로젝트에 대한 참고 Reference 사이트-->
<properties> <!-- 버전관리시 용이 하다. ex) 하당 자바 버전을 선언 하고 dependencies에서 다음과 같이 활용 가능 하다. <version>${java.version}</version> -->
    <java.version>1.8</java.version> 
</properties> 

<dependencies> <!--dependencies태그 안에는 프로젝트와 의존 관계에 있는 라이브러리들을 관리 한다.-->
    <dependency> 
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId> 
    </dependency> 
    <dependency> 
        <groupId>org.springframework.boot</groupId> 
        <artifactId>spring-boot-starter-tomcat</artifactId> 
        <scope>provided</scope> 
    </dependency> 
    <dependency> 
        <groupId>org.springframework.boot</groupId> 
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
        <exclusions> 
            <exclusion>
                <groupId>org.junit.vintage</groupId> 
                <artifactId>junit-vintage-engine</artifactId>
            </exclusion>
        </exclusions>
    </dependency> 
</dependencies>

<build> <!--빌드에 사용할 플러그인 목록--> 
    <plugins> 
        <plugin>
            <groupId>org.springframework.boot</groupId> 
            <artifactId>spring-boot-maven-plugin</artifactId> 
        </plugin>
    </plugins> 
</build>
</project>
```


