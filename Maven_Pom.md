```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>test</groupId>
	<artifactId>test</artifactId>
	<packaging>war</packaging>
	<version>1.0.0</version>
	<name>test</name>
	<url>http://www.egovframe.go.kr</url>
```

+ General Information
    + 필수 요소
    + Organization : 프로젝트 조직 정보 : 이름, 홈페이지 URL
    + Project Team and Collaborations tools
        - 형상관리 서버, 이슈 트랙커, 통합 빌드 서버 정보 등
       

```
	<licenses>
        <license>
            <name>The Apache Software License, Version 2.0</name>
            <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
        </license>
    </licenses>
```

+ Apache Software License, Version 2.0
    - 아파치 웹서버의 배포를 위해 만들어진 라이선스
    - 아파치 재단이나 재단의 프로젝트에 의해서 만들어진 모든 소프트웨어는 현재 Apach License 2.0로 배포.
    - version : 2.0
    - 관리기관 : 아파치 소프트웨어 재단
    - 관련 라이선스 : Apache 1.1


```
	<properties>
	    <spring.maven.artifact.version>4.3.25.RELEASE</spring.maven.artifact.version>
		<egovframework.rte.version>3.10.0</egovframework.rte.version>
	</properties>
```

+ Properties : maven 내부에서 반복적으로 사용될 상수 값을 정의할 때 사용
    + 현재는 maven artifact version, egovframework.rte.version
    
    


```
<repositories>
        <repository>
            <id>mvn2s</id>
            <url>https://repo1.maven.org/maven2/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
 ```

+ Repository
    + 의존성을 다운로드 받을 위치의 repository
    + 기술되지 않을 시 기본적인 위치 : http://repo.maven.apache.org/maven2
    + 다수의 ```<repository>``` 기술 가능
    + 회사 내부의 repository를 기술 하기도 한다.
    + 현재는 다운로드 받을 url : https://repo1.maven.org/maven2
    + mvn2s 를 url에서 다운받는 데 releases, snapshots 상관 없이 받겠다.

```
<build>
        <defaultGoal>install</defaultGoal>
        <directory>${basedir}/target</directory>
        <finalName>${artifactId}-${version}</finalName>
        <pluginManagement>
            <plugins>
                <plugin>
	                <groupId>org.apache.tomcat.maven</groupId>
	                <artifactId>tomcat7-maven-plugin</artifactId>
	                <version>2.2</version>
	                <configuration>
	                    <port>80</port>
	                    <path>/</path>
	                    <systemProperties>
	                        <JAVA_OPTS>-Xms256m -Xmx768m -XX:MaxPermSize=256m</JAVA_OPTS>
	                    </systemProperties>
	                </configuration>
	            </plugin>
                <plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.1</version>
					<configuration>
						<source>1.8</source>
						<target>1.8</target>
						<encoding>UTF-8</encoding>
						<maxmem>1024m</maxmem>
					</configuration>
				</plugin>
				<plugin>
                	<groupId>org.apache.maven.plugins</groupId>
                	<artifactId>maven-war-plugin</artifactId>
                	<version>2.4</version>
                	<configuration>
                		<failOnMissingWebXml>false</failOnMissingWebXml>
                	</configuration>
                </plugin>
                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>hibernate3-maven-plugin</artifactId>
                    <version>3.0</version>
                    <configuration>
                        <components>
                            <component>
                                <name>hbm2ddl</name>
                                <implementation>annotationconfiguration</implementation>
                            </component>
                        </components>
                    </configuration>
                    <dependencies>
                        <dependency>
                            <groupId>org.hsqldb</groupId>
                            <artifactId>hsqldb</artifactId>
                            <version>2.5.0</version>
                        </dependency>
                    </dependencies>
                </plugin>
                <!-- EMMA -->
                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>emma-maven-plugin</artifactId>
                    <version>1.0-alpha-3</version>
                </plugin>
                <!-- PMD manven plugin -->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-pmd-plugin</artifactId>
                    <version>3.12.0</version>
                </plugin>
            </plugins>
        </pluginManagement>
        <plugins>
            <!-- EMMA -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <configuration>
                    <skipTests>true</skipTests>
                    <forkMode>once</forkMode>
                    <reportFormat>xml</reportFormat>
                    <excludes>
                        <exclude>**/Abstract*.java</exclude>
                        <exclude>**/*Suite.java</exclude>
                    </excludes>
                    <includes>
                        <include>**/*Test.java</include>
                    </includes>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>emma-maven-plugin</artifactId>
                <inherited>true</inherited>
            </plugin>
            <!-- JavaDoc -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-javadoc-plugin</artifactId>
                <version>3.1.1</version>
            </plugin>
        </plugins>
    </build>
```

+ build
    + project 태그 바로 하위
    + plugins : 빌드에서 사용할 플러그인
    + 디렉터리 구조
    + 인코 딩 정보 등 빌드 LifeCycle 환경 설정


```
    <reporting>
        <outputDirectory>${basedir}/target/site</outputDirectory>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-project-info-reports-plugin</artifactId>
                <version>3.0.0</version>
                <reportSets>
                    <reportSet>
                        <id>sunlink</id>
                        <reports>
                            <report>javadoc</report>
                        </reports>
                        <inherited>true</inherited>
                        <configuration>
                            <links>
                                <link>http://docs.oracle.com/javase/6/docs/api/</link>
                            </links>
                        </configuration>
                    </reportSet>
                </reportSets>
            </plugin>
            <!-- JUnit Test Results & EMMA Coverage Reporting -->
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>emma-maven-plugin</artifactId>
                <inherited>true</inherited>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>surefire-report-maven-plugin</artifactId>
                <inherited>true</inherited>
                <reportSets>
                    <reportSet>
                        <reports>
                            <report>report-only</report>
                        </reports>
                    </reportSet>
                </reportSets>
            </plugin>
            <!-- Generating JavaDoc Report -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-javadoc-plugin</artifactId>
                <configuration>
                    <minmemory>128m</minmemory>
                    <maxmemory>512m</maxmemory>
                    <encoding>${encoding}</encoding>
                    <docencoding>${encoding}</docencoding>
                    <charset>${encoding}</charset>
                </configuration>
            </plugin>
            <!-- Generating Java Source in HTML -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jxr-plugin</artifactId>
                <configuration>
                    <inputEncoding>${encoding}</inputEncoding>
                    <outputEncoding>${encoding}</outputEncoding>
                    <linkJavadoc>true</linkJavadoc>
                    <javadocDir>apidocs</javadocDir>
                </configuration>
            </plugin>
        </plugins>
    </reporting>
```

+ Reporting
    + 리포트 생성 기능 설정
   

```      
      <dependency>
		    <groupId>taglibs</groupId>
		    <artifactId>standard</artifactId>
		    <version>1.1.2</version>
        </dependency>
```        

+ dependency
    + 프로젝트에서 사용한 라이브러리를 선언하여 Build Path에 포함. Dependency(의존성) 설정 참조
    + taglibs 라이브러리를 쓰겠다. 
    + groupId는 프로젝트를 모든 프로젝트 사이에서 고유하게 식별하게 해주는 것.
        - groupId에는 네이밍 스키마를 적용
        - groupId에는 package 명명 규칙을 따르도록 한다.
        - 즉, 최소한 당신이 컨트롤하는 도메인 네임이어야 한다.
        - 하위 그룹은 얼마든지 추가 가능.
    + artifactId
        - 버전을 생략한 jar 파일의 이름
        - 이름은 원하는 것으로 아무거나 정해도 된다.
        - 단, 소문자로만 작성.
        - 특수문자를 사용하지 않는다.
        - 만약 써드 파티 jar 파일이라면, 할당된 이름을 사용해야한다.


```python

```
