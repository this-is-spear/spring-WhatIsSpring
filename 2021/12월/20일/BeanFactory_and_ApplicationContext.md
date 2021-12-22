## BeanFactory and ApplicationContext

BeanFactory interface를 상속받는 ApplicationContext interface
ApplicationContext interface를 상속받는 AnnotationConfigApplicationContext 구현 객체

### BeanFactory

- 스프링 컨테이너의 최상위 인터페이스다.
- 스프링 빈을 관리하고 조회하는 역할을 한다.
- 'getBean()'메서드를 제공한다.

### ApplicationContext

- BeanFactory 기능을 모두 상속받아 제공한다.


ApplicationContext는 아래의 다양한 인터페이스들을 상속받고 있다.


## #AnnotationConfigApplicationContext

ApplicationContext 인터페이스를 구현한 구현체이다.



#### ApplicationContext 인터페이스는 빈을 관리하고 검색하는 기능을 BeanFactory가 제공해주는데 같은 기능을 만든 이유가 뭘까? 

  - 애플리케이션을 개발할 때 빈을 관리하고 조회하는 기능을 물론이고 수 많은 부가기능이 필요하다.
  - BeanFactory가 제공하는 기능은 물론 다른 인터페이스에서 제공하는 부가 기능을 제공하기 위해 ApplicationContext 인터페이스가 생겅이 됐다.
  - 그렇기에 보통 BeanFactory를 직접 사용하지 않고 ApplicationContext를 직접 사용한다.
  - 그래서 스프링 컨테이너인 BeanFactory를 상속받아 모든 일을 처리하는 ApplicationContext를 스프링 컨테이너라고 부른다.

#### ApplicationContext는 BeanFactory 기능 말고도 어떤 기능을 제공할까? 

**ApplicationContext가 상속받는 인터페이스**

- EnvironmentCapable 
  - 로컬(개인 컴퓨터) 환경, 개발(테스트 서버) 환경, 스테이시 환경(운영 환경과 밀접한 환경) ,운영 환경들을 구분해서 처리하는 메서드를 제공하는 인터페이스
- ListableBeanFactory 
  - 클라이언트의 요청에 따라 이름으로 하나씩 빈 조회를 시도하는 대신 모든 빈 인스턴스를 열거할 수 있는 BeanFactory 인터페이스를 확장한 인터페이스이다.
  - 제공하는 메서드는 getBeansOfType(Class<T> type) 과 같은 return 값이 <T>map<String, T> 인 메서드들이 다량 존재한다.
- HierarchicalBeanFactory
  - 계층의 일부가 되는 빈을 관리하며, 빈 팩토리에 의해 구현되는 하위 인터페이스이다.
  - 제공하는 method
    - containsLocalBean(String name) : 해당 name의 빈이 지역 빈에 존재하는지 확인할 수 있다. return 값은 boolean 이다.
    - getParentBeanFactory(): 해당 부모 빈 팩토리를 찾는다. return 값은 BeanFactory 이며, 존재하지 않는다면, Null을 리턴한다.(@Nullable 애터테이션 존재)
- MessageSource
  - 메시지 소스를 활용한 국제화 기능을 제공하는 인터페이스
- ApplicationEventPublisher
  - 이벤트를 발행하고 구독하는 모델을 편리하게 지원하는 인터페이스
- ResourcePatternResolver
  - 파일, 클래스 패스, 외부 등에서 리소스를 편리하게 조회하는 기능을 제공하는 인터페이스

#### AnnotationConfigApplicationContext는 어떻게 동작을 하는 것일까? 

기본적으로는 ApplicationContext를 상속받은 AnnotationConfigApplicationContext 클래스에 @Configuration 애너테이션을 상속받은 AppConfig 클래스 파일을 멤버 변수로 넘긴다.
그러면 AnnotationConfigApplicationContext 내에 있는 리더가 이 파일을 읽고 BeanDefinition에 스프링 빈 메타 정보를 생성해 저장한다. 그렇게 되면 BeanFactory 또는 BeanFactory를 상속받은  ApplicationContext 클래스 즉, 스프링 컨테이너에 BeanDefinition에 생성된 스프링 빈 메타 정보를 불러와 하나하나 저장한다. 
