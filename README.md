# MSA-project 목차
1. MicroService와 Spring Cloud 소개
2. Service Discovery
3. API Gateway Service


# MicroService와 Spring Cloud 소개

### 2010년 이후

- 탄력적, 안티 프레즐,클라우드 네이티브 아키텍처로 시스템 구축
- 로컬 환경에서 클루우드로 이전
- 확장성,안정성 강화됨
- 지속적 개선 및 변경사항이 생겨도 시스템 운영 가능하도록 구축
- DevOps 문화 생김

### 안티 프레즐 특징

- 자동 확장성 가짐

- 마이크로 서비스 - 클라우드 네이티브 아키텍처의 핵심

전체 서비스를 구축하고 있는 모듈이나 기능을 독립적으로 개발하고 배포 운용할 수 있는 서비스

- 카오스 엔지니어링

시스템 변동 내에서도 안정적인 서비스를 제공할 수 있도록 구축되어야 한다는 규칙

- 배포 파이프라인

수십 수백개의 서비스들을 빌드하고 테스트하고 배포하는 작업을 자동화된 시스템을 구축하고

하나의 작업에서 다른 작업으로 연계되는 과정을 파이프라인으로 연결시키면 빠르게 적용 가능

## 클라우드 네이티브 아키텍처

- 확장 가능한 아키텍처

확장된 서버로 시스템의 부하 분산, 가용성 보장

가상 서버의 기술이 핵심적으로 필요

서버 가상화 기술과 더불어 컨테이너 가상화도 같이 사용

클라우드 네이티브에 구축된 가상 서버와 리소스들은 다양한 모니터링 도구를 이용해

시스템 상황 및 리소스 사용량 확인

- 탄력적 아키텍처

CI/CD를 통해 비즈니스 환경변화에 대응 시간 단축

분할된 서비스 구조 - 전체 어플리케이션을 구성하고 있는 도메인 특성에 따라 서비스 경계를 잘 구분해야함

서로 분리된 서비스 간에 원활한 통신을 위해 각각의 서비스들은 종속성을 최소화하고 상태를 갖지 않는 서비스를 제공하려고 노력해야함

전체 어플리케이션을 구축하는 마이크로 서비스들은 자신들이 배포될때 자신들의 위치가 어디에 있는지 등록해야 함 ⇒ 다른 서비스들이나 외부에 연결되어있는 타 시스템에서도 해당 서비스를 검색하고 사용할 수 있음

마이크로 서비스들의 존재는 디스커버리 서비스라는 곳에 등록되고 삭제되는 작업을 하게 된다.

- 장애 복구에 뛰어남

하나의 마이크로 서비스에서 생기는 문제나 오류사항은 다른 쪽 서비스로의 영향을 최소화 할 수 있음.

특정 부분에 대해 수정해도 전체 서비스를 다시 배포해야 하지 않음 

## 클라우드 네이티브 어플리케이션

클라우드 네이티브 아키텍처 특징과 안티 프레즐 특징을 가짐

- 마이크로 서비스로 개발된다.
- CI/CD 시스템에 의해 자동으로 통합되고 빌드 테스트 배포 함.
- 마이크로 서비스에 문제가 생겼을 경우에 바로바로 수정해서 배포하는 과정 반복 ⇒ DevOps

⇒ 고객이 원하는 최선의 결과물을 만드는 데 그 목적을 두고 있음

- 컨테이너 가상화 기술 사용

### 1.CI/CD 지속적인 통합, 지속적인 배포

- 지속적인 통합

결과물을 통합하기 위한 형상관리, 통합된 코드를 빌드하고 테스트하는 과정

Jenkins, Team CI, Travis CI  ⇒깃과 연동해서 사용

CI 시스템에 파이프라인을 잘 연동하게 되면 개발자가 어떤 코드를 완성한 후에 깃과 같은 형상관리 시스템에 해당 코드를 커밋함과 동시에 빌드,테스트,실행해서 다른 쪽 코드와 문제가 발생하는지 여부를 바로 확인

- 지속적인 배포

지속적 전달, 지속적 배포

깃과 같은 곳에 저장된 코드를 가지고 와서 패키지화된 형태 결과물을 실행환경에 어떻게 배포하는지에 따라 전달이냐 배포냐가 달라짐

변경된 시스템을 무조건 새로 반영하기 보다는 기존 시스템과 같이 운용해줌으로써 사용자에게 발생할 수 있는 이질감, 문제점 최소화 하는 것이 필요

배포 전략

- 카나리 배포

95퍼센트 사용자는 이전 버전 서비스를 사용하게 하고 5퍼센트 사용자만 새 버전 서비스를 사용

- 블루그린 배포

이전버전 사용자 트래픽을 점진적으로 새 버전으로 옮김

### 2.DevOps

개발 조직과 운영 조직의 통합

이러한 통합으로 고객의 요구사항 빠르게 반영하고 만족도 높은 결과물을 제시하는 것이 목적

고객의 요구사항은 언제든 변경될 수 있다. ⇒ 바로바로 수정할 수 있는 구조가 적합

클라우드 네이티브 어플리케이션은 서비스의 구조를 작은 단위로 분할 함으로써 더 자주 통합,테스트, 배포 할 수 있는 구조

### 3.컨테이너 가상화

적은 비용으로 탄력성 있는 시스템 구축하게 된 배경이 컨테이너 가상화 기술

기존 개발 방식 :   하드웨어 ⇒ 운영체제 ⇒ 앱

가상화를 통한 개발 방식: 하드웨어 ⇒ 운영체제 ⇒ 하이퍼바이저 ⇒ 가상머신(독립적인 운영체제 가지고 실행될 수 있음 ⇒ 각각의 가상머신에 어플리케이션 운용할 수 있음)

⇒ 가상머신에서 작동되는 어플리케이션은 호스트 운영체제에 많은 부하를 주고 시스템 확장에 한계가 있음

컨테이너 가상화를 통한 개발 방식: 하드웨어 ⇒ 운영체제 ⇒ 컨테이너 런타임(공통적인 라이브러리나 리소스 공유) ⇒ 컨테이너(각자 필요한 부분만 독립적인 영역에 실행) ⇒ 리소스가 적어 가볍게 빠르게 운용 가능

## 클라우드 네이티브 애플리케이션을 구축함에 있어 고려해야할 12가지 항목

1. 코드 베이스
2. 종속성
3. 구성정보
4. 서비스 지원
5. 빌드,배포,실행환경 분리
6. 프로세스
7. 포트 바인딩
8. 동시성
9. 삭제가능
10. 개발과 제품 구분
11. 로깅
12. 관리도구

+

1. API first
2. 모든 지표 수치화 
3. 인증 필수

## 모노리틱 VS 마이크로 서비스

- 모노리틱

모든 업무 로직이 하나의 애플리케이션 형태로 패키지되어 서비스

시스템 일부만 수정해도 전체를 다시 빌드하고 테스트하고 패키징해야하는 단점

- 마이크로 서비스

함께 작동하는 작은 규모의 서비스들

유지보수나 변경사항 적용 유리

최소한의 중앙 집중식 관리가 되어야하고 다른 언어와 다른 데이터 저장기술 사용가능하다.

디바이스가 다양해짐 ⇒ 사용자의 요청정보를 처리하는 서버 사이드 기술도 다양한 형태로 서비스 되어야 함

서비스 요청에 대한 통일된 게이트웨이,서비스들의 부하 분산, 분리된 서비스들을 동기화하기 위한 매커니즘들이 필요

마이크로 서비스 개발하는 방법 뿐만 아니라 마이크로 서비스를 운영,관리하기 위해 필요한 기술도 알아햐한다.

## 마이크로 서비스 특징

## SOA vs MSA

- 서비스 지향한다는 것은 공통적인 부분

SOA는 재사용을 통한 비용 절감이 주 목적

MSA는 서비스 간의 결합도를 낮추어 변화에 능동적으로 대응하는 것이 주 목적

- 기술방식

SOA - 공통의 서비스를 ESB에 모아 공통 서비스 형식으로 서비스 제공

MSA - 각 독립된 서비스가 노출된 REST API를 사용

- RESTful Web Service

사용자 우선

HTTP 장점 최대한 살려서 개발(헤더,request,response 등)

request 메소드 - get,post,put,delete

response 상태 - 200,404,400,201,401 (400번대 클라이언트 오류, 500은 서버오류)

## Spring Cloud Netflix Eureka

마이크로서비스는 스프링 클라우드 넷플릭스 유레카에 등록

유레카가 해주는 역할 : service discovery(외부에서 마이크로 서비스를 검색하기 위해 사용되는 개념⇒전화번호 책⇒ 어떤 서비스가 어디 위치에 있는지를 등록하고 있는 정보)
</br></br></br></br></br></br>


# Service Discovery

## Spring Cloud Netflix Eureka

같은 서버에서 구동하면 서비스들 포트번호 다르게

서버 여러개면 서버 ip다르게 포트는 같아도 된다.

서비스들을 Service Discovery(유레카)에 등록

외부에서 다른 서비스들이 다른 서비스들을 검색하기 위해 사용(전화번호책)

어느 서비스가 어디 위치에 있는지를 저장하고 있음

서비스 디스커버리 역할 : 서비스 등록 및 검색

클라이언트는 자기가 필요한 요청정보를 load balancer또는 Api gateway에 전달

⇒ 서비스 디스커버리에 물어봄 ⇒ 반환받음 ⇒ 반환받은 정보 토대로 서비스 호출하고 요청정보 받음

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled.png)

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%201.png)

### DiscoveryserviceApplication.java

스프링부트가 실행되면 가장 먼저 실행되는 부트스트랩같은 역할을 하는 파일

@SpringBootApplication이라는 어노테이션이 있는 파일을 실행

Eureka 서버 역할을 하기 위해 서버자격으로 등록해야함⇒@EnableEurekaServer 어노테이션 등록

### Application.yml 작성

 

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%202.png)

### 유레카 서버에 등록할 샘플 마이크로 서비스 ⇒userSerive

UserServiceApplication.java에서 @EnableDiscoveryClient 추가

유레카 서버에 등록될 클라이언트 서비스라는 것 명시

yml이 중요

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%203.png)

- fetch-registry는 유레카 서버로부터 인스턴스들의 정보를 주기적으로 가져올 것인지를 설정하는 속성. true로 설정하면 갱신된 정보를 받겠다는 설정
- service-url : 서버의 위치가 어디인지 지정하는 부분(유레카 서버의 위치 지정)
- defaultZone : 서버가 가지고 있는 위치값 지정

등록 후 유레카 서버 화면

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%204.png)

server.port = 0 ⇒ 포트번호 랜덤하게 할당 ⇒ 유레카 서버에서는 동적으로 할당된 포트번호가 아니라 yml에 있는 포트번호를 가져오기 떄문에 여러서비스 실행해도 하나만 뜸

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%205.png)

=⇒ yml에 eureka.instance.instance-id 설정하면 둘다 뜬다.

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%206.png)

application과 터미널에서 bootRun으로 실행시킨 두개의 userService 확인

![Untitled](Service%20Discovery%2065e506d2d98a49e2a623cafbf8c5815d/Untitled%207.png)
</br></br></br></br></br></br>


# API Gateway Service

프록시 역할

시스템의 내부 구조는 숨기고 외부의 요청에 대해서 적절한 형태로 가공해서 응답할 수 있다는 장점

- API gateway가 없다면 클라이언트가 직접 마이크로서비스를 호출하고 마이크로 서비스가 변경된다면 클라이언트 측도 변경되어야함.

## API Gateway Service

- 인증 및 권한 부여
- 서비스 검색 통합
- 응답 캐싱
- 정책, 회로 차단기
- 속도 제한
- 부하 분산
- 로깅,추적
- 헤더, 쿼리 스트링 변환
- IP 허용 목록에 추가

## Netfilx Ribbon, Zuul

Spring Cloud 에서 MSA 간 통신은 

- RestTemplate를 구현하는 방법 ⇒ ip와 포트번호, http메소드로 호출
- Feign Client를 구현하는 방법 ⇒마이크로서비스 이름으로 호출

API GateWay 역할을 하는 Ribbon과 Zuul (현재는 못씀)

Ribbon : Client side Load Balancer ⇒ 비동기 처리 불가(잘 안쓰게됨)

- 서비스 이름으로 호출
- Health check
- 게이트 웨이가 클라이언트 측에 있다고 보면된다.

Zuul: Gateway 역할, 2점대 버전부터는 비동기 처리 가능하지만 스프링 라이브러리 호환 문제로 안쓰게됨

ZuulFilter : 마이크로 서비스가 요청될때 사전작업,사후작업 처리

## Spring Cloud Gateway

기존 zuul 서비스를 대신한다. 비동기 처리 가능

dependencies는 DevTools, Lombok, Eureka Discovery Client, Gateway 추가

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled.png)

비동기로 처리되기 때문에 tomcat이 아니라 Netty로 실행

## Spring Cloud Gateway - Filter

- Pre Filter : 사전 필터
- Post Filter : 사후 필터

요청 ⇒ Gateway Handler Mapping 요청 받기 => Predicate 조건 분기(어디로 갈지) ⇒ 사전 필터 ⇒ 서비스 ⇒ 사후 필터 ⇒ Gateway Handler Mapping ⇒ 응답

Filter 적용의 두가지 방법

- java코드

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%201.png)

자바 코드로 진행시에는 yml 파일에 게이트웨이 주석처리할것

- yml파일

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%202.png)

yml 파일 진행시에는 FilterConfig에 @Configuration과 @Bean 주석처리 할것

## CustomFilter

사용자 정의 필터, 로그출력, 인증 등 등록가능

@Componenet,@Slf4j

반드시 AbstractGatewayFilterFactory<내부클래스>를 상속받아야한다.

apply 메소드 오버라이드하여 작성

yml에 CustomFilter 넣어주기

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%203.png)

yml

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%204.png)

# Global Filter

공통 필터

- Custom 필터와 차이점 : custimFilter는 각 라우트마다 등록해줘야함.
- 가장 먼저 시작되고 가장 마지막에 종료된다

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%205.png)

yml

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%206.png)

# Logging Filter

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%207.png)

- Ordered.HIGHEST_PRECEDENCE 옵션을 주면 가장 먼저 실행되고 가장 마지막에 종료됨

yml

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%208.png)

필터가 두개 이상이면 name 붙여줘야함

# Load Balancer

### 게이트웨이와 서비스들

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%209.png)

dependencies에 유레카 클라이언트 있어야 함.

### 게이트 웨이

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%2010.png)

uri에 lb://{서비스 이름}

요청 ⇒ 게이트 웨이 서비스 ⇒> 디스커버리 서비스(유레카 서버)에서 해당 서비스 이름 찾고 게이트웨이한테 알려줌⇒ 게이트웨이에서 서비스 직접 찾아가서 요청하고 데이터 받음

같은 서비스를 여러개 기동한다면 요청을 보냈을때 어느 서비스로 가는지 모른다.

⇒포트를 0으로(랜덤포트) 설정 ⇒ 같은 서비스 여러개 실행시켜도 유레카 대시보드에는 0 하나만 뜸⇒ 인스턴스 아이디 값을 부여하자

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%2011.png)

같은 서비스 여러개 기동했을 때 어떤 서비스가 호출되는지 확인 하기 위해 포트번호 출력해보기

![Untitled](API%20Gateway%20Service%20996d89dec6ba4a66ab1c9fa7245e6e48/Untitled%2012.png)

결과: 게이트웨이가 라운드 로빈방식으로 서비스를 번갈아가며 호출한다. (로드 밸런싱)

게이트 웨이를 사용하게 되면 라우팅 기능과 로드 밸런싱 기능까지 포함해서 사용할 수 있다.
