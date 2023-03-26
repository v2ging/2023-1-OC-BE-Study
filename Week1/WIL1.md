# 1주차 정리

**Section0. 강의 소개**

스프링을 공부하는 방법:

- 처음부터 끝까지 직접 코딩

**Section1. 프로젝트 환경설정**

1. 프로젝트 생성
    - Java 11 이상 설치; 19 설치
    - [start.spring.io](http://start.spring.io/) - 스프링부트 template project 만들기
    - IDA: IntelliJ 설치
    - 프로젝트 선택
        
        Project: **Gradle - Groovy** Project Spring Boot: 제일 최신 버전(M1, SNAPSHOT: 정식버전 ❌)
        Language: Java
        Packaging: Jar
        
        groupId: hello
        
        artifactId: hello-spring Dependencies: Spring Web, Thymeleaf
        
- [ ]  스프링 부트 3.0 사용시 주의!
스프링 부트 3.0을 선택하게 되면 다음 부분을 꼭 확인해주세요.
    
    **1. Java 17 이상**을 사용해야 합니다. -> java 19 설치
    
    **2. javax 패키지 이름을 jakarta로 변경**해야 합니다.
    
    오라클과 자바 라이센스 문제로 모든 javax 패키지를 jakarta로 변경하기로 했습니다. 
    
    **3. H2 데이터베이스를 2.1.214 버전 이상 사용해주세요.**
    
    - 동작 확인
    - 기본 메인 클래스 실행
    - 스프링 부트 메인 실행 후 에러페이지로 간단하게 동작 확인( [http://localhost:8080](http://localhost:8080) )
        
        IntelliJ Gradle 대신에 자바 직접 실행
        최근 IntelliJ 버전은 Gradle을 통해서 실행 하는 것이 기본 설정이다. buy 이렇게 하면 실행속도가 느리다.
        
        다음과 같이 변경하면 자바로 바로 실행해서 실행속도가 더 빠르다.
        
        Preferences Build, Execution, Deployment Build Tools Gradle
        
        Build and run using: Gradle -> IntelliJ IDEA
        Run tests using: Gradle -> IntelliJ IDEA
        
    
    - 프로젝트 환경 설정 성공
        
        메인메소드 실행 -> run -> 클래스 작동 -> @ application 실행 -> 내장된 톰캐시놀 웹서버 실행 (아직 이해 안딤 ;;)
        
    
    - 라이브러리 살펴보기
        - Gradle은 의존관계가 있는 라이브러리를 함께 다운로드 한다.
            - 스프링 부트 다이어리
                
                - spring-boot-starter-web
                
                - spring-boot-starter-tomcat: 톰캣(웹서버)
                
                - spring-webmvc: 스프링 웹 MVC
                
                - spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View)
                
                - spring-boot-starter(공통): 스프링부터 + 스프링코어 + 로깅 - 알아보기
                
                - spring-boot
                
                - spring-core
                
                - spring-boot-starter-logging
                
                -logback, slf4j
                
                텍스트 라이브러리
                
                - spring-boot-starter-test
                
                - unit: 테스트 프레임워크
                
                - mockito: 목 라이브러리
                
                - asserts: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
                
                - spring-test: 스프링 통합 테스트 지원
                
    - 로그(log)
        - 로그란?
            
            : IT에서 발생되는 모든 행위와 이벤트 정보를 시간에 따라 남겨둔 데이터를 지칭하는 말
            
            사고나 장애 발생 시, 원인을 평가하고 대처할 수 있는 근거를 찾을 수 있기 때문에 로그를 수집 및 분석하면 기업의 소중한 정보 자산으로 활용할 수 있음
            
            현업 실무에서 많이 사용
            

- 터미널에서 빌드하고 실행하기
    1. ./gradlew build
    2. cd build/libs
    3. java -jar hello-spring-0.0.1-SNAPSHOT.jar
    4. 실행확인

**Section2. 스프링 웹 개발 기초**

1. 정적 컨텐츠
    - 스프링부트는 정적 컨텐츠 기능
    - 파일을 그대로 웹 브라우저에 내려주는 방식
    - 정적 컨텐츠 이미지
        
        ![스크린샷 2023-03-26 오후 5.37.04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5b49d89-29b5-4a18-a416-af085bdf9cbc/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-03-26_%EC%98%A4%ED%9B%84_5.37.04.png)
        
        웹 브라우저에서 [localhost:8080/hello-static.html](http://localhost:8080/hello-static.html) 주소를 입력함 
        
        → 내장 톰켓 서버가 요청을 받음 
        
        → 톰켓서버가 스프링 컨테이너에 주소가 왔음을 알림 
        
        → 스프링컨테이너:
        
        1. controller 쪽에서 hello-static 관련 컨트롤러가 있는지 확인
        2. 컨트롤러가 없다면 resource:static/hello-static.html 를 찾음
        3. 있다면 웹 브라우저에 반환!

1. MVC와 템플릿 엔진
    - 서버에서 변형 후 html을 바꾸어 내려주는 방식
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65918f1e-13ab-40c2-a93a-b95e07d33c16/Untitled.png)
    
    - MVC: Model-View-Controller
        - 사용자 인터페이스, 데이터 및 논리 제어를 구현하는데 널리 사용되는 소프트웨어 디자인 패턴 / 구성요소를 세 가지로 분리
        - 사용자가 controller를 조작하면 controller는 model을 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달
        - 왜 사용해야 하는가?
            - 유지보수성, 애플리케이션의 확장성, 유연성 증가, 중복 코딩이라는 문제점 사라짐
            
            ### WEB에 적용 시!
            
            1. 사용자가 웹사이트에 접속 (Users)
            2. Controller는 사용자가 요청한 웹페이지를 서비스하기 위해서 모델을 호출 (Manipulates)
            3. Model은 데이터베이스나 파일과 같은 데이터 소스를 제어한 후 그 결과를 Return
            4. Controller는 Model이 리턴한 결과를 View에 반영 (Updates)
            5. 데이터가 반영된 View는 사용자에게 보여짐 (Sees)
            
        
        - **📲 모델 (Model)**
            
            데이터를 가진 객체를 모델이라고 지칭
            
            데이터는 내부의 상태에 대한 정보를 가질 수도 있고, 모델을 표현하는 이름 속성으로 가질 수 있다. 모델의 상태에 변화가 있을 때 컨트롤러와 뷰에 이를 통보한다. 이와 같은 통보를 통해 뷰는 최신의 결과를 보여줄 수 있고, 컨트롤러는 모델의 변화에 따른 적용 가능한 명령을 추가, 제거, 수정할 수 있다.
            
            **모델의 규칙**
            
            - 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야만 함
            - 뷰나 컨트롤러에 대해서 어떠한 정보도 알지 말아야 함
            - 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야 함
            
        - **🖥️ 뷰 (View)**
            
            클라이언트 측 기술 HTML/CSS/Javascript를 모아둔 컨테이너 
            
            사용자가 볼 결과물을 생성하기 위해 모델로부터 정보를 얻어옴
            
            **뷰의 규칙**
            
            - 모델이 가지고 있는 정보를 따로 저장해서는 안됨
            - 모델이나 컨트롤러와 같이 다른 구성 요소를 몰라야 함
            - 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야 함
        - **🕹️ 컨트롤러 (Controller)**
            
            사용자가 접근한 URL에 따라 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를 Model을 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려줌.
            
            모델에 명령을 보냄으로써 뷰의 상태를 변경할 수 있음 → 컨트롤러가 관련된 모델에 명령을 보냄으로써 뷰의 표시 방법을 바꿀 수 있음
            
            **컨트롤러의 규칙**
            
            - 모델이냐 뷰에 대해서 알고 있어야 함
            - 모델이나 뷰의 변경을 모니터링해야 함
    
    - [http://localhost:8080/hello-mvc?name=spring!!!](http://localhost:8080/hello-mvc?name=spring!!!)
        - hello controller / hello-mvc의 name에 “spring!!!” 값 들어감
        - -> hello-template.html의 의 name에도 값이 넘어감
        
    - MVC, 템플릿 엔진 이미지
        
        ![스크린샷 2023-03-26 오후 5.39.04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d81422e6-2b8d-4fd1-af27-925e5d77d4f7/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-03-26_%EC%98%A4%ED%9B%84_5.39.04.png)
        
        - 웹 브라우저에서 [localhost:8080/hello-static.html](http://localhost:8080/hello-static.html) 주소를 입력함
            
            → 내장 톰켓 서버가 요청을 받음 
            
            → 톰켓서버가 스프링 컨테이너에 주소가 왔음을 알림 
            
            → hellocontroller에 메소드가 맵핑이 돼 있다면 메소드를 호출함 
            
            → view resolver: 리턴의 스트링 네임과 똑같은 네임을 찾아서 thyme leaf 템플릿 엔진에게 처리해달라고 넘김 
            
            → 템플릿 엔진 렌더링
            
            → 변환된 HTML을 웹브라우저에 반환
            
    
    - 정적 컨텐츠와의 차이: 정적 컨텐츠는 템플릿 엔진에서 변환하지 않고 웹브라우저에 그대로 넘겨줌

1. API(Application Programming Interface)
    - 애플리케이션 소프트웨어를 빌드하고 통합하기 위한 정의 및 프로토콜 세트
    - Android , iOS : json 데이터 구조포맷을 클라이언트한테 데이터를 전달해줌
    - @ResponseBody : http에서 body에 데이터에 내용을 그대로 직접 넣어주겠다!!!! (html 구조x)
    - JSON(JavaScript Object Notation)
        - json이란?
            
            : JavaScript 객체 리터럴, 배열, 스칼라 데이터를 표현하는 텍스트 기반의 방식
            
        - 과거 xml, json 혼용했지만, 현재는 대다수가 무겁고 열고 닫기 해야하는 단점을 가진 xml보다 심플하고 가벼운 json 방식 사용
        - 구조: {”key” : “value”}
        
    
    - 서버(server)
        - 서버란?
            
            : 인터넷(Internet)을 통해 클라이언트(Client)에게 서비스나 정보를 제공하는 역할을 수행하는 컴퓨터
            
        - 하나의 고성능 컴퓨터; 다수의 사용자에게 '서비스를 제공하는 역할을 수행하는 컴퓨터’
        - 서버 ↔ 클라이언트: '서비스를 요청하는 컴퓨터’
    
    - REST(Representational State Transfer)
        - 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것
            - 즉, 자원(resource)의 표현(representation) 에 의한 상태 전달
                - a. 자원(resource)의 표현(representation)
                    - 자원: 해당 소프트웨어가 관리하는 모든 것
                    -> Ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등
                    - 자원의 표현: 그 자원을 표현하기 위한 이름
                    -> Ex) DB의 학생 정보가 자원일 때, ‘students’를 자원의 표현으로 정함
                
                - b. 상태(정보) 전달
                    - 데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달
                    - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적
                    - 
            - 월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
                - REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일
                - REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나
    
    - REST API
        - REST API란?
            
            : REST 기반으로 서비스 API를 구현한 것
            
        - 최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공
        - 특징
            - 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있음
            - REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있음
            즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있으
    
    - Restful
        - Restful이란?
            
            : 일반적으로 REST라는 아키텍쳐를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어
            
            REST API를 제공하는 웹 서비스를 RESTful하다고 할 수 있음
            
        - 목적
            - 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
        
    - **@ResponseBody 사용 원리**
        
        ![스크린샷 2023-03-26 오후 5.40.04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/48e71390-ab63-4dd8-9354-9d68498b87c4/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2023-03-26_%EC%98%A4%ED%9B%84_5.40.04.png)
        
        - HTTP의 BODY에 문자 내용을 직접 반환
        - 웹 브라우저에서 [localhost:8080/hello-static.html](http://localhost:8080/hello-static.html) 주소를 입력함
            
            → 내장 톰켓 서버가 요청을 받음 
            
            → 톰켓서버가 스프링 컨테이너에 주소가 왔음을 알림
            
            → @**ResponseBody** 붙어있을 때
            
            1. httpmessageconverter가 동작
            
            2-1. 단순문자: string converter 작동 → html에 바로 넘김
            
            2-2. 객체: json converter 작동 → json 스타일로 바꾸어 http 응답에 반환
            
        - viewResolver 대신에 HttpMessageConverter 가 동작
        - 기본 문자처리: StringHttpMessageConverter
        - 기본 객체처리: MappingJackson2HttpMessageConverter
        - byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음
        - 클라이언트의 HTTP Accept 해더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해서 HttpMessageConverter 가 선택된다. (추후 설명)

- [ ]  **단축키**

**cmd + p: option**

**cmd + n: generate**

**cmd + shift + enter: 문장완성**