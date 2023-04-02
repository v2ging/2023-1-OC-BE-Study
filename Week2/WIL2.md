**컨트롤러, 서비스, 리포지토리의 역할**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4b78b66f-d206-40f1-9bd6-93e5dfabf501/Untitled.png)

- **🕹️ 컨트롤러 (Controller)**

`모델(Model)`과 `뷰(View)` 사이를 이어주는 `브릿지(Bridge` 역할

사용자가 접근한 URL에 따라 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를 Model을 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려줌 

+ 컨트롤러가 관련된 모델에 명령을 보냄으로써 뷰의 표시 방법을 바꿀 수 있음

- 사용하는 이유?
    - Controller라는 중간 제어자를 만들어 **역할**에 따라 설계 및 코딩 시 개발 비용 또는 유지보수 비용이 대폭 줄어듦

- **@Controller(Spring MVC Controller)**
    - 전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 View를 반환하기 위해 사용
    - @ResponseBody 어노테이션과 같이 사용하면 RestController와 똑같은 기능 수행 가능
    
- **@RestController(Spring Restful Controller)Permalink**
    - RestController는 Controller에서 @ResponseBody 어노테이션이 붙은 효과를 지님
    - JSON/XML형태로 객체 데이터 반환을 목적
    

- **✔️ 서비스 (Service)**
    
    데이터를 받아 비즈니스 로직을 처리 (글을 쓰거나, 글을 읽거나, 글을 지우거나 하는 모든 것들)
    
    Service 에 request나 response와 같은 객체를 매개변수로 받아선 안됨 (컨트롤러의 역할)
    
    DB의 활용이 필요한 경우 해당 처리를 하는 DAO를 호출
    
    **DAO : Data Access Object (Database의 data에 접근을 위한 객체)*
    
    - 서비스의 역할
        - 자신을 어떤 컨트롤러가 호출하든 상관X
        - 필요한 매개변수만 주면 자신의 비즈니스 로직을 처리
        - 모듈화를 통해 어디서든 재사용이 가능한 파일

- 📁 **리포지토리 (Repository)**
    
    Entity에 의해 생성된 DB에 접근하는 메서드 들을 사용하기 위한 인터페이스
    
    DB 연결, 해제, 자원을 관리하고 CRUD 작업을 처리
    

**TDD란? 왜 하는가?**

- **TDD**(Test-Driven Development) **테스트 주도 개발**
    
    소프트웨어 개발 방법론 중의 하나로, 선 개발 후 테스트 방식이 아닌 선 테스트 후 개발 방식의 프로그래밍 방법
    
    다시 말해, 먼저 자동화된 테스트 코드를 작성한 후 테스트를 통과하기 위한 코드를 개발하는 방식의 개발 방식을 말함
    
    - TDD 이용한 개발 방법
        1. 테스트 케이스 작성
        2. 테스트 케이스를 통과하는 코드 작성
            1. 반드시 실패를 포함하는 테스트 코드의 작성이 앞서야 함
            2. 테스트 케이스를 통과하는 코드를 작성
                1.  작성된 코드는 개선될 수 있는 많은 여지를 포함한 코드여야 함
                2. 리팩토링 과정에서 이를 개선
        3. 작성한 코드 리팩토링
        
    - TDD의 장점
        - 객체 지향적인 코드 개발
            - 코드의 재사용 보장을 명시하므로 TDD를 통한 소프트웨어 개발 시 기능별로 모듈화가 이루어짐. 이는 의존성과 종속성이 낮은 모듈로 조합된 소프트웨어 개발을 가능하게 하며, 필요에 따라 모듈을 추가하거나 제거해도 소프트웨어 전체 구조에 영향을 미치지 않게 됨’
            
        - 설계 수정시간의 단축
            - 테스트코드를 먼저 작성하기 때문에 최초 설계안을 만족하게 하며 입출력 구조와 기능의 정의를 명확하게 하게 되므로 설계의 구조적 문제를 바로 찾아낼 수 있음
        
        - 유지보수(리팩토링)의 용이성
            - 기본적으로 단위 테스트 기반의 테스트 코드를 작성하기 때문에 추후 문제가 발생하였을 때 각각의 모듈별로 테스트를 진행해보면 문제의 지점을 쉽게 찾을 수 있음
        
        - 테스트 문서의 대체 가능
            - 대부분의 개발 프로젝트에서 테스트를 진행하는 경우 단순 통합 테스트에 지나지 않음TDD를 하게 될 때 테스팅을 자동화시킴과 동시에 더욱 정확한 테스트 근거를 산출해 정의서를 작성할 수 있음
    
    - TDD의 단점
        - 사전준비 기간
            - TDD를 프로젝트에 도입하려면 사전에 필요한 지식을 습득하고 개발 환경을 구축해야 함. TDD를 효과적으로 사용할 수 있는 수준으로 개발자를 교육하는 데 보통 1~6개월간의 시간이 필요함.
        - 생산성 저하
            - 프로젝트를 진행할 때 경험 때문에 어떤 예외상황이 발생할지 눈에 뻔히 보이는 경우가 종종 있음. 이러한 단발성 개발은 개발 기간이 타이트하게 잡히는 경우가 많은데, 이럴 때 TDD를 이용해 테스트 코드를 작성하고 그에 통과하기 위한 코드를 작성한다면 비효율적일 것임.
        
    - TDD Tools
        - JUnit
            - 전 세계적으로 널리 사용되는 JAVA의 표준 단위 테스트 프레임워크
            - 에릭 감마와 켄트 백이 개발하였으며, JUnit을 시작으로 XUnit 프레임워크가 탄생하게 됐음