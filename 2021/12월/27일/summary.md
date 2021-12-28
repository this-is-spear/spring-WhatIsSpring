# 스프링 기본편 정리
## 스프링이 무엇인지, 왜 세상에 나왔는 지

### 스프링

스프링은 복잡하고 컨테이너 안에서만 동작할 수 있는 객체 구조인 EJB 컨테이너를 대체하기 위해 나온 기술이며, 객체 지향 언어의 특징을 살려내 애플리케이션을 개발할 수 있도록 도와주는 프레임워크이다.

**스프링 프레임워크의 핵심 기술은 스프링 DI 컨테이너이다.**

#### EJB

EJB는 인스턴스 풀링을 이용해 객체들을 미리 메모리에 저장해 많은 동접자수에 대해 안정성을 지원하고 자동으로 컨테이너가 모든 처리 메서드에 트랜잭션을 처리해준다. 그리고 빈즈의 상태를 사용여부에 따라 메모리에 저장할지 안할지를 고민하는 퍼시스턴스 관리를 할 수 있다. 그에 반해 단점은 복잡하고, 특정 환경에 종속적인 코드이며, 컨테이너 안에서만 동작할 수 있는 객체 구조라는 점이다.

#### 왜 EJB가 아니라 스프링인가?

EJB를 사용하여 개발하게 되면 기술 구조 변경시에 서버 환경에 종속되는 경우가 있다. 스프링과 같이 POJO 중심의 개발 방식을 기술적으로 지원해 특정 컴포넌트 모델에 종속적이지 않게 개발하는 것이 추세이며, 대부분의 회사들이 구조적인 유연성을 중시하게 되면서 보다 유연한 애플리케이션을 만들기 원한다.

#### POJO란?

POJO를 해석하면 순수한 자바 오브젝트이다. 말 그대로 순수한 자바 오브젝트에 도메인 로직을 넣어 사용해 보자는 생각에서 나온 방법이다.


### 스프링 부트

스프링을 조금 더 간편하게 사용하기 위해 스프링 부트가 나왔다. 스프링 부트는 스프링에서 톰켓과 같은 웹 서버를 내장해 별도의 웹 서버를 설치하지 않아도 된다.
starter 종속성을 제공해 빌드를 편리하게 할 수 있도록 도와주며, 메트릭과 상태확인 그리고 외부 구성과 같은 프로덕션 준비 기능을 제공한다.

## 객체 지향 원리를 적용해 프로그래밍하는 방법

### 객체 지향의 특징

<details>
<summary>1. 추상화</summary>
불필요한 정보는 숨기고 중요한 정보만을 표현하며 공통의 속성이나 기능을 묶는 것을 말한다.
</details>

<details>
<summary>2. 캡슐화</summary>
기능과 특성의 모음을 클래스라는 캡슐에 분류해서 넣는 것이다.
</details>

<details>
<summary>3. 상속</summary>
부모의 속성과 기능을 그대로 이어받아 사용할 수 있게 도와주고 기능의 일부분을 변경해 자식이 사용할 수 있도록 하는 것을 말한다.
</details>

<details>
<summary>4. 다형성</summary>
하나의 객체나 변수가 상황에 따라 다른 의미로 해석될 수 있는 것이다.
</details>


### 다형성을 왜 사용할까? 

> 인터페이스와 구현객체를 이용해 애플리케이션을 설계하면 클라이언트는 사용하려는 기능의 명세서만 보고도 사용할 수 있고, 상세 구현한 클래스의 내용을 알지 않아도 된다. 제일 중요한 강점은 구현 대상인 클래스의 내용을 변경해도 영향을 받지 않아 유연하게 구현체인 클래스를 변경할 수 있다.


### 좋은 객체 지향 설계의 5가지 원칙 - SOLID

- SRP - 단일 책임 원칙
- OCP - 개방-폐쇄 원칙
- LSP - 리스코프 치환 원칙
- ISP - 인터페이스 분리 원칙
- DIP - 의존 관계 역전 원칙


아래는 위의 5가지 원칙을 정리해봤다.

### SRP - 단일 책임 원칙

<details>
<summary>한 클래스는 하나의 책임만 가져야 한다.</summary>
단일 책인 원칙에서 중요한 기준은 변경이다. 변경이 있을 때, 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것이다. 객체의 생성과 사용을 분리한다면 파급 효과가 적도록 설계할 수 있다.

스프링에서 이용한다면 구현 객체를 생성해 객체를 생성하고 역할을 명시한 인터페이스를 사용하도록 하는 것이다.

</details>

### OCP - 개방-폐쇄 원칙

<details>
<summary>소프트웨어 요소의 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.</summary>
새로운 기능을 구현하는 객체를 만들기 위해서는 인터페이스를 상속받는 새로운 클래스를 하나 만들어 구현하게 만든다. 다형성을 활용하면 역할과 구현의 분리를 통한 확장에는 열려 있게 만들 수 있고, 변경에는 닫혀 있게 만들 수 있다. 하지만 구현 객체를 변경하려면 클라이언트 코드를 변경해야 하고, 다형성 원칙으로 OCP 원칙을 전부 지킬 수 없다.

내가 생각하는 가장 중요한 원칙 중 하나이다. 스프링에 원래 생성되어 있는 기능들의 변경을 하지 않고, 새로운 객체를 생성함으로 확장에는 자유로워야 한다. 다형성의 원칙으로는 OCP 원칙을 다 지킬 수 없는 부분은 스프링의 DI와 DI 컨테이너를 이용해 단점을 보완할 수 있다.
</details>

### LSP - 리스코프 치환 원칙

<details>
<summary>프로그램 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.</summary>
다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것이다. 다형성을 지원하기 위한 원칙, 인터페이스로 구현한 구현체를 믿고 사용하려면 이 원칙이 필요하다.

객체 지향 설계를 위해서 기능을 구현한 인터페이스의 신뢰가 필요하다. 그렇기에 단순히 컴파일에 성공하는 것을 넘어서 해당 인스턴스 설계 의도대로 움직이고 있는지를 확인하는 LSP 원칙을 잘 지키고 있는지 확인할 필요가 있다.
</details>

### ISP - 인터페이스 분리 원칙

<details>
<summary>특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.</summary>
인터페이스 분리 원칙은 클라이언트가 자신이 이용하지 않는 메서드에 의존하지 않아야 한다는 원칙이다. 인터페이스 분리 원칙은 범용적인 큰 덩어리 인터페이스 분리 원칙은 큰 덩어리의 인터페이스들을 구체적이고 작은 단위들로 분리시킴으로써 특정 클라이언트들이 꼭 필요한 메서드들만 이용할 수 있게 한다.

스프링이나 어느 객체 지향 설계를 위해서는 모든 기능을 포괄하는 범용 인터페이스보다 각각의 특징을 살린 특정 클라이언트들을 위한 인터페이스를 여러 개 만드는 것이 좋다고 생각한다.
</details>

### DIP - 의존 관계 역전 원칙

<details>
<summary>추상화에 의존해야지 구체화에 의존하면 안 된다.</summary>
상위 계층이 하위 계층에 의존하는 전통적인 의존관계를 역전시킴으로 상위 계층이 하위 계층의 구현으로부터 독립되게 할 수 있다. 즉, 상위 모듈은 하위 모듈에 의존해서는 안되며 상위 모듈과 하위 모듈 모두 추상화에 의존해야 한다. 그리고 추상화는 세부 사항에 의존해서는 안되며 세부 사항이 추상화에 의존하게 만들어야 한다.

스프링에서 의존 관계 역전 원칙을 이용하기 위해서 인터페이스가 구현 클래스에 의존하지 않고 구현 클래스가 인터페이스에 의존해야 한다는 의미이다. 즉, 상위 개념인 인터페이스가 하위 개념인 구현 클래스에 의존하지 않도록 설계해야 하며, 인터페이스가 구현 객체의 구현으로부터 독립되게 설계해야 한다.

객체 지향의 핵심은 다형성이지만, 다형성 만으로는 객체 지향 프로그램을 쉽게 개발할 수 없다. 구현 객체를 반영할 때, 클라이언트 코드도 함께 변경된다. 다형성 만으로는 OCP, DIP를 지키기 힘들기에 다른 방법을 강구해야 한다. 위와 같은 OCP와 DIP를 지키기 위해 스프링에서는 의존성 주입과 DI컨테이너와 같은 기능들을 제공한다. 객체 지향 설계를 완벽하게 도와주는 기능들을 스프링에서 제공한다.

스프링을 완벽하게 제어하고 스프링의 장점을 잘 사용하기 위해서는 SOLID의 원칙을 잘 알고 다형성에 대한 기본적인 지식이 필요하다고 생각해 블로그 글을 작성했다.
</details>

#### 스프링 프레임워크 없이 SOLID 원칙들을 잘 지킬 수 있을까?

> 본론부터 말하자면 외부에서 의존 관계를 설정해준다면 해결할 수 있다고 생각한다. 
웹 MVC 패턴을 이용해 각 구현체들은 의존 관계를 설정한 클래스에 의해 외부에서 참조 객체들을 선택받아 생성한다. 그렇게 되면 해당 구현 객체를 수정하지 않고도 참조 객체를 마음대로 교체할 수 있다.

#### 스프링 프레임워크의 DI 컨테이너를 사용하지 않는다면

**스프링 프레임워크에서 DI 컨테이너를 이용하지 않고 순수한 자바 코드로만 의존성 주입을 하게 된다면 의존성 주입을 요청할 때마다 객체를 생성한다.** 만약 이렇게 된다면 각기 다른 클래스에서 부른 구현체가 달라 동시성 문제가 생길 수 있다.

### 객체 지향 프로그래밍을 더 잘하는 방법은 무엇일까

1. 구현보다 역할을 더 중요하게 생각하자
2. SOLID 원칙을 지키며 설계하자
3. 구현 객체에 대한 의존성 주입을 통해 구현체에게 의존적이지 않은 설계를 하자

## **스프링 DI를 이용해 스프링 프레임워크를 활용하는 방법**

### 스프링을 이용해 의존성 주입하는 방법

### 자바를 이용해 외부에서 의존성 주입을 할 수 있는데 왜 스프링을 사용하는가?

스프링은 객체 지향 언어의 특징을 잘 살려내 애플리케이션을 개발할 수 있도록 도와주는 프레임워크이다. 외부에서 의존성을 주입하는 역할을 하는 클래스를 스프링 컨테이너에 등록하지 않고도 사용할 수 있도록 만들었기에 처음에는 굳이 스프링 컨테이너에 등록하기 위해 여러 어노테이션을 붙여가며 스프링 빈을 만들어야 할까 라는 생각을 많이 했다. 처음 만든 AppConfig 클래스 만으로 외부에서 의존성 주입해 객체 지향 설계를 할 수 있지 않을까라는 생각을 했고, AppConfig 클래스에 존재하는 DI 컨테이너들을 스프링 컨테이너에 등록하는 이유가 궁금했다. 그 궁금증에 답은 스프링 컨테이너를 이용해 스프링 빈을 관리하면 동시성 문제를 해결할 수 있기 때문에 스프링 컨테이너를 사용한다는 것이다.

### 스프링 컨테이너

#### 왜 스프링 컨테이너를 이용해 의존성 주입을 할까

대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 웹이 아니어도 개발할 수 있지만, 
웹 애플리케이션은 보통 여러 고객이 동시 요청을 하는 데에서 싱글톤 패턴을 이용하지 않으면 문제가 생긴다.

**스프링 없는 순수한 DI 컨테이너인 AppConfig는 요청을 할 때 마다 객체를 새로 생성하기 때문에 동시성 문제가 생긴다.** 해결방안은 해당 객체가 한개만 생성되고 공유할 수 있도록 설정한다. 그리고 **스프링 컨테이너는 싱글톤 방식으로 스프링 빈들을 관리하기 때문에 이러한 문제없이 사용할 수 있다.**

#### 싱글톤 패턴

> 클래스의 인스턴스가 딱 하나만 생성되도록 하는 것을 보장하는 패턴이며, 객체 인스턴스를 2개 이상 생성하지 못하도록 막는다.
> pirvate 생성자를 사용해 외부에서 임의로 new 키워드를 사용하지 못하도록 막아야 한다.


#### 싱글턴 패턴을 만드는 방법은 어떤 방법들이 있을까?

> 싱글턴 패턴을 적용하면 고객의 요청이 올 때 마다 객체를 생성하는 것이 아니라,이미 만들어진 객체를 공유해서 효율적으로 사용할 수 있다. **하지만, 싱글톤 패턴은 다음과 같은 수 많은 문제점들을 가지고 있다.**

#### 싱글톤 패턴의 문제점

구체 클래스에서 구현한 getInstance() 메서드를 호출해야 하기 때문에, 구체 클래스를 호출할 수 밖에 없다.

- 싱글톤 패턴을 구현하는 코드 자체가 많이 들어간다.
- 의존관계상 클라이언트가 구체 클래스에 의존한다. - DIP 위반
- 클라이언트가 구체 클래스에 의존해 OCP 원칙을 위반할 가능성이 높다. - OCP 위반
- 테스트하기 어렵다.
- 내부 속성을 변경하거나 초기화하기 어렵다.
- private 생성자로 자식 클래스를 만들기 어렵다.
- 결론적으로 유연성이 떨어진다.
- 안티패턴으로 불리기도 한다.

#### 싱글톤 컨테이너

스프링 컨테이너는 싱글톤 패턴의 문제점을 해결하면서, 객체 인스턴스를 싱글톤으로 관리한다.
지금까지 우리가 학습한 스프링 빈이 바로 싱글톤으로 관리되는 빈이다.

- 스프링 컨테이너는 싱글톤 패턴을 적용하지 않아도, 객체 인스턴스를 싱글톤으로 관리한다.
- 스프링 컨테이너는 싱글톤 컨테이너 역할을 하고 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라 한다.
- 스프링 컨테이너의 이런 기능 덕분에 싱글톤 패턴의 모든 단점을 해결하면서 객체를 싱글톤으로 유지할 수 있다.

싱글톤 컨테이너 적용 후
스프링 컨테이너 덕분에 고객의 요청이 올 때 마다 객체를 생성하는 것이 아니라, 이미
만들어진 객체를 공유해서 효율적으로 재사용 할 수 있다.

> 스프링의 기본 빈 등록 방식은 싱글톤 방식이지만, 싱글톤 방식만 
> 지원하는 것은 아니다. 프로토타입 스코프도 존재하고, 웹 스코프도 존재한다.

#### 싱글톤 방식의 주의점

- 객체 인스턴스를 하나만 생성해서 공유하는 싱글톤 방식은 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 상태를 유지(stateful)하게 설계하면 안된다.
- 무상태인 statefule로 설계해야 한다.
  - 특정 클라이언트에 의존적인 필드가 있으면 안된다.
  - 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다.
  - 가급적 읽기만 가능해야 한다.
  - 필드 대신에 자바에서 공유되지 않는, 지역변수, 파라미터, TreadLocal 등을 사용해야 한다.

**스프링 빈의 필드에 공유 값을 설정하면 큰 장애가 발생할 수 있다. 즉, 전역 변수 등 공유 필드는 조심해야 한다.**


### 스프링 빈

#### 자바 빈즈

자바 빈즈는 클래스안에 프로퍼티를 저장한 후 객체를 만들기 위한 클래스이다. 즉, 객체를 만들기 위한 틀인 클래스를 자바빈이라고 부르는 것처럼 보였다. 자바빈에 대해 공부를 하면서 자바 빈이랑 스프링 빈은 같을까 라는 생각이 들었다.

#### 스프링 빈이란

간단하게 말하자면 Spring에서의 빈은 ApplicationContext가 알고있는 객체, 즉 스프링 컨테이너 안에 담고있는 객체를 의미한다. 스프링 빈을 사용하면 스프링이 스프링 컨테이너 안에 해당 구현체를 관리하며, 구현체가 호출이 될 때, 참조하는 레퍼런스를 외부에서 주입해주는 역할이다.

#### 스프링 IoC 컨테이너가 관리하는 자바 객체인 스프링 빈이랑 위에 설명하는 자바 빈즈는 같을까?

자바 빈즈와 유사하지만 다르다는 생각한다. 스프링 빈은 스프링 컨테이너에서 싱글톤 패턴을 통한 의존성 주입으로 동시성 문제를 해결해준다. 스프링 빈도 엄연히 위와 같이 캡슐화를 통해 구현체를 관리하는 것 처럼 보이지만 스프링 프레임워크의 기술 덕에 싱글톤으로 관리할 수 있어 동시성 문제까지 해결해준다.

#### 스프링 빈을 등록하는 방법

1. @Component - 애너테이션을 이용해 스프링 컨테이너에 자동 빈 등록하는 방법
    1. @Component-scan 애너테이션은 @Component-scan 애너테이션이 포함된 클래스부터 하위 패키지 까지 모든 클래스를 조회하여 @Component 애너테이션이 붙은 클래스들을 스프링 빈으로 등록한다.
    2. 즉, @Component나 @Component가 내제되어 있는 애너테이션을 이용해 스프링 컨테이너에 직접적으로 스프링 빈을 등록한다.
2. @Bean - 애너테이션을 이용해 설정 파일을 만들어 스프링 컨테이너에 수동 빈 등록하는 방법
    1. @Configuration 애너테이션이 붙은 설정 파일에 존재하는 @Bean을 스프링 빈으로 등록하는 방법이다.
    2. 우리는 팩토리 빈을 통해서 스프링 빈을 등록할 수 있다.

#### 자동 빈 등록, 수동 빈 등록

자동 빈 등록을 이용해 빈을 편리하게 등록할 수 있다. 하지만 그렇게 되면 수동 빈 등록에 대한 장점이 없는데 어떤 상황에서 사용할 수 있을까?

#### 수동 빈 등록은 언제 사용하면 좋을까?

1. 업무 로직 빈
    - 비즈니스 요사항을 개발할 때 추가되거나 변경된다.
2. 기술 지원 빈
    - 기술적인 문제나 공통 관심사(AOP)를 처리할 때 주로 사용된다. 데이터베이스 연결이나, 공통 로그 처리처럼 업무 로직을 지원하기 위한 하부 기술이나 공통 기술들이다.

> 애플리케이션에 광범위하게 영향을 미치는 기술 지원 객체는 수동 빈으로 등록해서 설정 정보에 바로 나타나게 코드를 짜는 것이 유지보수하기 수월하다.
> **그러나 스프링과 스프링 부트가 자동으로 등록하는 수 많은 빈들은 예외다.**

> 또한 비즈니스 로직 중에서 다형성을 적극 활용할 때 적합하다.

하지만 동일한 타입의 모든 빈들을 조회할 필요가 있을 때, List나 Map으로 관리하려고 할 때, 각 상황마다 어떤 빈들이 주입될 지, 각 빈들의 이름은 무엇인지 코드만 보고
쉽게 파악하는 것은 불가능하다.

이런 경우 수동 빈으로 등록하거나 특정 패키지에 같이 묶어서 관리하는 것이 좋다.

```java
@Configuration
public class DiscountPolicyConfig{
    
    @Bean
    public DiscountPolicy rateDiscountPolicy(){
        return new rateDiscountPolicy();
    }
    
    @Bean
    public DiscountPolicy fixDiscountPolicy(){
        return new fixDiscountPolicy();
    }
}
```

**정리**

- 편리한 자동 기능을 기본으로 사용하자.
- 직접 등록하는 기술 지원 객체는 수동 등록하자.
- 다형성을 적극 활용하는 비즈니스 로직은 수동 등록을 고민하자.

#### 빈 조회하는 방법

기본적으로는 ApplicationContext를 상속받은 AnnotationConfigApplicationContext 클래스에 @Configuration 애너테이션을 사용한 구성 설정 파일을 멤버 변수로 넘긴다.
그러면 AnnotationConfigApplicationContext 내에 있는 리더가 이 파일을 읽고 BeanDefinition에 스프링 빈 메타 정보를 생성해 저장한다. 그렇게 되면 BeanFactory 또는 BeanFactory를 상속받은 ApplicationContext 클래스 즉, 스프링 컨테이너에 BeanDefinition에 생성된 스프링 빈 메타 정보를 불러와 하나하나 저장한다. 

```java
        ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);

```

#### 기본 조회

기본적으로 스프링 빈이 잘 저장되는지 확인하는 테스트를 간단하게 실행했다. 스프링 컨테이너에서 getBeanDefinitionNames() 메서드를 호출해 String 배열 형식의 DefinitionNames 를 가져와 하나씩 출력한다.

```java
    @Test
    @DisplayName("모든 빈 출력하기")
    public void findAllBean () throws Exception{
        String[] beanDefinitionNames = applicationContext.getBeanDefinitionNames();
        for(String beanDefinitionName : beanDefinitionNames){
            Object bean = applicationContext.getBean(beanDefinitionName);
            System.out.println("name = " + beanDefinitionName+ " object = " + bean);
        }
    }
```

### @ComponentScan

#### @Configuration 애너테이션을 사용한 구성 정보에 데이터를 다 넣으면 안되나?

스프링 빈이 너무 많아지면 설정 정보도 커지고 누락하는 문제도 발생한다. 그래서 스프링은 설정 정보가 없어도 자동으로 스프링 빈을 등록하는 컴포넌트 스캔이라는 기능을 제공한다. 또, 의존관계도 자동으로 주입하는 '@Autowired' 애너테이션이라는 기능도 제공한다.

코드로 @ComponentScan 애너테이션과 의존관계 자동 주입을 알아보자

#### @ComponentScan 애너테이션에 등록되는 스프링 이름은 어떻게 저장될까? 

@ComponentScan 애너테이션은 @Component 애너테이션이 붙은 모든 클래스를 스프링 빈으로 등록한다. 이 때, 빈의 기본 이름은 클래스명을 사용하되 맨 앞글자만 소문자를 사용한다.

- 빈 이름 기본 전략
  - MemberServiceImpl 클래스 -> memberServiceImpl
- 빈 이름 직접 지정
  - 만약 스프링 빈의 이름을 직접 지정하고 싶으면 @Component("memberService)라고 이름을 직접 부여하면 된다.


### @ComponentScan 스캔의 탐색 위치와 기본 스캔 대상

#### 탐색할 패키지의 시작 위치 지정

모든 자바 클래스를 다 컴포넌트 스캔하면 시간이 오래 걸린다. 그래서 꼭 필요한 위치부터 탐색하도록 시작 위치를 지정할 수 있다.

```java
@ComponentScan(
        basePackages = "hello.core", // 해당 패키지부터 @Component 애너테이션이 붙은 클래스를 찾는다.
        basePackagesClasses = AutoAppConfig.class, //이 클래스 위의 패키지 부터 @Component 애너테이션이 붙은 클래스를 찾는다.
        excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Configuration.class)
)
public class AutoAppConfig {

}
```

- backPackages
  - 탐색할 위치를 지정할 수 있다. 이 패키지를 포함해서 하위 패키지를 모두 탐색한다.
- basePackageClasses
  - 지정한 클래스의 패키지를 탐색 시작 위로 지정한다.
- 만약 지정하지 않으면 @ComponentScan이 붙은 설정 정보 클래스의 패키지가 시작 위치가 된다.

**권장하는 방법**

> 패키지 위치를 지정하지 않고, 설정 정보 클래스의 위치를 프로젝트 최상단에 두는 것이다. 최든 스프링 부트도 이 방법을 기본적으로 제공한다. 그리고 스프링 부트를 사용하면 스프링 부트 대표 시작 정보인 @SpringBootApplication 애너테이션이 붙은 클래스와 같은 시작 루트 위치에 두는 것이 관례이다.

#### 컴포넌트 스캔 대상

- @Component
  - 컴포넌트 스캔에서 사용
- @Controller
  - 스프링 MVC 컨트롤러에서 사용
- @Service
  - 스프링 비즈니스 로직에서 사용
- @Repository
  - 스프링 데이터 계층에서 사용
- @Configuration
  - 스프링 설정 정보에서 사용


#### 그러면 위와 같은 컴포넌트를 만들고 구성 설정 정보를 만들지 않으면 자동으로 스프링 컨테이너가 생성되지 않고, 싱글톤 컨테이너를 이용할 수 없는가?

@Configuration 애너테이션을 통해 수동으로 빈을 등록하지 않고 ComponentScan을 통해 빈을 등록하더라도 싱글톤(스코프를 변경하지 않는 이상)으로 관리된다. **이 방법을 자동 빈 등록이라고 한다.**

> 애너테이션에는 상속 관계가 없다. 애너테이션이 특정 애너테이션을 들고 있는 것을 인식할 수 있는 것은 자바 언어가 지원하는 기능이 아니고 스프링이 지원하는 기능이다.

컴포넌트 스캔의 용도 뿐만 아니라 다음 애너테이션이 있으면 스프링은 부가 기능을 수행한다.

- @Controller
  - 스프링 MVC 컨트롤러로 인식한다.
- @Service
  - 이 애너테이션에는 특별한 처리를 하지 않지만 개발자들은 이 곳에 핵심 비즈니스 로직이 있겠구나라고 인식하는데 도움이 된다.
- @Repository
  - 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다.
- @Configuration
  - 스프링이 설정 정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 추가 처리를 한다.

### @Autowired 의존관계 자동 주입

생성자에 @Autowired 애너테이션을 지정하면 스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아 주입한다. 생성자에서 주는 인자의 해당 타입을 뒤져서 가져온다.
**이름은 달라도 같은 타입이 여러개 있으면 충돌이 일어난다.**


### 다양한 방법으로 의존관계 주입하는 방법

**오류가 나지 않도록, 누군가 외부에서 실수로 주입하면 컴파일 에러가 나도록 외부에서 주입할 수 없도록 설계해야 한다.**

#### 1. 생성자 주입

- 생성자 호출 시점에서 딱 한번만 호출되는 것이 보장된다.
- **불변,필수(final) 의존관계에 사용**
- 안에 데이터를 임의로 넣지 못하도록 설계해야 한다. (불변)
- final을 붙이면 값이 꼭 있어야 한다고 지정하는 것이다. (필수)

> **생성자가 딱 하나만 있으면 @Autowired 애너테이션을 생략해도 자동 주입된다.(물론 스프링 빈에만)**

#### 2. 수정자 주입 (setter)

> 옵션이 필요할 때 사용한다. 즉, 주입할 스프링 빈이 없어도 동작해야 할 때 사용한다.

- setter  필드의 값을 결정하는 수정자 메서드를 통해서 의존관계를 주입하는 방법이다.
- @Autowired 애너테이션을 설정해 줘야 의존 관계 주입이 일어난다.
- 생성자 호출 후 순서대로 setter 메서드 호출한다. 즉, 의존관계 주입 두 번째에서 일어 난다.(첫 번째는 생성자를 빈에 등록(주입))
- **선택, 변경 가능한 의존관계에 사용**
- 자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법이다.

> @Autowired 애너테이션의 기본 동작은 주입할 대상이 없으면 오류가 발생한다. 주입할 대상이 없어도 동작하게 하려면 '@Autowired(required=false)'로 지정해야한다.

> 자바빈 프로퍼티, 자바에서는 과거부터 필드의 값을 직접 변경하지 않고,getter, setter라는 메서드를 통해 값을 읽거나 수정하는 규칙을 만들었는데, 그것이 자바빈 프로퍼티 규약이다.

#### 3. 필드 주입

**필드 주입을 해버리면 불변하지 않는다는 단점과 누락될 수 있다는 단점이 존재하고, 스프링 컨테이너 없이는 테스트가 불가능하다.**

>이름 그대로 필드에 바로 주입하는 방법이다.
- 코드가 간결해서 많은 개발자들을 유혹하지만 외부에서 변경이 불가능해서 테스트 하기 힘들다는 치명적인 단점이 있다.
- DI 프레임워크가 없으면 아무것도 할 수 없다.
- **실제 환경에서 절대 사용 금지!!**
  - 간단한 테스트 코드(애플리케이션과 관계없는 코드)에서만 사용
  - @Configuration 애너테이션이 붙은 설정 파일 같은 특별한 곳만 사용

#### 4. 일반 메서드 주입

>일반 메서드를 통해서 주입할 수 있다.
- 한번에 여러 필드를 주입 받을 수 있다.
- **일반적으로 잘 사용하지 않는다.**

> 어쩌면 당연한 이야기지만 의존관계 자동 주입은 스프링 컨테이너가 관리하는 스프링 빈이어야 동작한다. 스프링 빈이 아닌 코드에서 @Autowired 코드를 적용해도 아무 기능을 하지 않는다.

#### 어떤 의존 관계 주입 방법을 선택해야 할까? 
> 과거에는 수정자 주입과 필드 주입을 많이 사용했지만, 최근에는 스프링을 포함한 DI 프레임워크 대부분이 누락하지 않고 불변할 수 있는 생성자 주입을 권장한다.

#### **불변**

> 대부분의 의존관계 주입은 한 번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 오히려 대부분의 의존관계는 애플리케이션 종료 전까지 변하면 안된다.

final 키워드를 이용해 변하지 않도록 설계할 수 있다. 생성자 주입을 통한 설계를 하면 **final** 키워드를 이용해 실수로 생성자에 멤버 변수를 넣지 않았을 때, 오류가 나서 쉽게 찾을 수 있도록 설계할 수 있다.

#### **누락**

> 프레임워크 없이 순수한 자바 코드를 단위 테스트 하는 경우 setter 메서드를 통해 의존관계를 주입한다면 NPE(Null Point Exception)이 발생하는데, 의존관계가 누락됐기 때문에 생기는 예외이다.
생성자 주입을 사용했을 때, **주입 데이터를 누락하면 컴파일 오류가 발생한다.** 생성자를 이용해 의존성을 주입할 때, 컴파일 오류가 일어나면 오류를 쉽게 찾을 수 있는 방법을 제공해주고, 가장 빠르게 오류를 찾아낸다.

### 중복 등록과 충돌에 대처하는 방법

#### 중복 등록이 되는 상황

1. 자동 빈 등록 vs 자동 빈 등록
2. 수동 빈 등록 vs 자동 빈 등록

#### 1. 자동으로 등록한 빈들끼리 충돌하는 경우

> 컴포넌트 새킨에 의해 자동으로 스프링 빈이 등록 되는데, 이름이 같은 경우 **ConflictingBeanDefinitionException 예외**라는 오류를 발생시킨다.

#### 2. 자동으로 등록한 빈과 수동으로 등록한 빈이 충돌하는 경우

> **이 경우 수동 등록 빈이 우선권을 가진다는 점을 알아야 한다.** (수동 빈이 자동 빈을 오버라이딩 해버린다.)
 
스프링은 친절하게 수동 빈이 자동 빈을 오버라이드시 남는 로그를 남겨준다.

이러한 경우는 개발자가 의도적으로 설정해서 나오는 경우가 아니라 설정들이 꼬여서 이런 결과가 나오는 경우가 대부분이다. **그러면 정말 잡기 어려운 버그가 만들어진다. 항상 잡기 어려운 버는 애매한 버그이다.** 그래서 최근 스프링 부트에서는 수동 빈 등록과
자동 빈 등록이 충돌나면 오류가 발생하도록 기본 값을 바꿨다. (Test 환경에서는 오버라이드 되어 오류가 나지 않는다.)

#### 왜 Test에서 오류가 나지 않는걸까? 

스프링의 코어 모듈은 에러가 나지 않고 오버라이딩을 주지만, 스프링 부트는 default 값을 false로 줘서 오류가 나도록 설정하기 때문이다.

스프링 부트에서의 오류
스프링의 코어 모듈은 에러가 나지 않고 오버라이딩을 주지만, 스프링 부트는 실행 환경의 default 값을 false로 줘서 오류가 나도록
설정했다. 그래서 오버라이딩을 의도적으로 하려면 spring.main.allow-definition-overriding=true 값을 application.properties 설정 파일에 
추가 해줘야 한다. **이 방법은 좋은 방법이 아니니 애매한 상황을 만들어 주변 사람을 혼란하게 만들지 말자.**


### Filter (FilterType)

필터에는 두가지의 타입이 존재한다. 하나는 포함시키는 명령어(includeFilters)이고, 나머지 하나는 제외시키는 명령어(excludeFilters)다. 이 명령어를 사용하면 스프링이 시작할 때, ComponentScan 애너테이션에 있는 Filter 정보를 들려서 사용자가 지정한 타입을 빈으로 추가하거나 배제할 수 있다.

- includeFilters
- excludeFilters

#### FilterType

- ANNOTATION
  - 기본값, 애너태이션을 인식해 동작한다.
- ASSIGNABLE_TYPE
  - 지정한 타입과 자식 타입을 인식해서 동작한다.
- ASPECTJ
  - AspectJ 패턴을 사용한다.
- REGEX
  - 정규 표현식이다.
- CUSTOM
  - 'TypeFilter' 이라는 인터페이스를 구현해 처리한다.

#### MyIncludeComponent 클래스를 빈으로 등록하고 싶으면 includeFilters 명령어를 이용하여 아래와 같이 추가한다.

```java
    @Configuration
    @ComponentScan(
            includeFilters = @Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class)
            }
    )
    static class ComponentFilterAppConifg{

    }
```

#### BeanA 빈을 제외하고 싶은 경우에 ASSIGNABLE_TYPE 타입을 이용한다.

```java
    @Configuration
    @ComponentScan(
            excludeFilters = {
                    @Filter(type = FilterType.ASSIGNABLE_TYPE, classes = BeanA.class)
            }
    )
    static class ComponentFilterAppConifg{

    }
```

### Option

> 주입할 스프링 빈이 없어도 동작해야 할 때가 있다. 그런데, @Autowired 애너테이션만 사용하면 'required' 옵션의 기본값이 true로 되어 있어서 자동 주입 대상이 없으면 오류가 발생한다.

 
#### 자동 주입 대상을 옵션으로 처리하는 방법

- '@Autowired(required=false)'

    자동 주입할 대상이 없으면 수정자 메서드 자체가 호출이 되지 않지만, 'required' 옵션의 기본값이 false로 설정해 자동 주입 대상이 없어도 실행할 수 있도록 설정한다. 그럼 주입 대상이 없으면 오는 값은 아래 와 같다.

- org.springframework.lang.@Nullable
  
    자동 주입할 대상이 없으면 null이 입력된다.

- Optional<>

    자동 주입할 대상이 없으면 Optional.empty가 입력된다.

> Optional, @Nullable은 스프링 전반에 걸쳐 지원한다. 예를 들어 생성자 자동 주입에서 특정 필드만 사용해도 된다.

```java

    static class TestBean{
        @Autowired(required = false)
        public void setNoBean1(Member noBean1){
            System.out.println("noBean1 = " + noBean1);
        }
        @Autowired
        public void setNoBean2(@Nullable Member noBean2){
            System.out.println("noBean2 = " + noBean2);
        }

        @Autowired
        public void setNoBean3(Optional<Member> noBean3){
            System.out.println("noBean3 = " + noBean3);
        }

    }
```

Member 참조 객체는 스프링 빈이 아니기 때문에 (required = false) 이 명령어가 없다면 에러가 난다.
하지만 이 명령어가 있다고 해도 의존관계가 없으면 아래 메소드는 아예 호출이 되지 않는다.
**즉, Member는 스프링 빈이 아니기 때문에 호출이 되지 않는다.**

### @Autowired 애너테이션을 이용할 때, 같은 타입 빈이 두 개 이상 조회되면 생기는 문제

@Autowired 애너테이션은 타입으로 조회한다. 그렇기에 getBean(Class<T> class)와 같이 메서드 이름이 제공되지 않은 getBean() 메서드와 유사하게 동작한다. (실제로는 @Autowired 애너테이션이 더 많은 기능을 제공한다.)

스프링 빈 조회하면서 알 수 있듯이 타입으로 조회할 때, 같은 타입이 두개 이상이면 문제가 발생한다. (NoUniqueBeanDefinitionExceptio 예외가 나온다.)

**반대로 말하면 스프링은 NoUniqueBeanDefinitionException 빈은 throw해 자동 연결에 둘 이상의 빈을 사용할 수 있음을 나타낸다.**

스프링 프레임워크는 어떤 빈을 주입해야 하는지 모르게 때문에 NoUniqueBeanDefinitionException 예외를 던진다. 이러한 상황을 해결하기 위해서 세가지 방법에 대해 알아보겠다.

#### @Autowired 필드 명, @Quilifire, @Primary 애너테이션을 이용해 문제 해결

1. @Autowired 필드 명 매칭
2. @Quilifier -> @Quilifier 끼리 매칭 -> 빈 이름 매칭
3. @Primary 사용 

### 1. @Autowired 필드 명 매칭

> @Autowired 애너테이션 타입 매칭을 시도하고 같은 타입 빈이 여러개 있으면 **파라미터 이름으로 빈 이름을 추가 매칭한다.**

```java
@Component
public class OrderServiceImpl implements OrderService {

    private final MemberRepository memberRepository;
    private final DiscountPolicy discountPolicy;

    @Autowired
    public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy fixDiscountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = fixDiscountPolicy;
    }
}
```

위 OrderServiceImpl 클래스에서 빈 타입은 DiscountPolicy, 파라미터 이름은 fixDiscountPolicy의 빈을 찾는다.

#### 2. @Quilifier -> @Quilifier 끼리 매칭 -> 빈 이름 매칭
<details>
<summary>@Quilifier 자세히 보기</summary>
<div markdown="1">

```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
public @interface Qualifier {

    String value() default "";

}
```

@Quilifier는 인터페이스를 상세하게 
</div>
</details>


> 추가 구분자를 붙여주는 방법이다. 주입시 추가적인 방법을 제공하는 것이지, 빈 이름을 변경하는 것은 아니다.

```java
@Component
@Qualifier("mainDiscountPolicy")
public class RateDiscountPolicy implements DiscountPolicy {}
```

```java
@Autowired
public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {
    this.memberRepository = memberRepository;
    this.discountPolicy = discountPolicy;
}
```

@Qualifier 애너테이션에 파라미터를 "mainDiscountPolicy"를 주기 전 가져오고 싶은 DiscountPolicy 타입의 구현체에  @Qualifier("mainDiscountPolicy") 애너테이션을 붙여줘야 스프링 컨테이너가 매칭을 시켜준다. 해당 빈 이름이 mainDiscountPolicy이라고 바로 매칭되는 것이 아니라 @Qualifier의 인자를 보고 매칭을 시켜준다.

**@Qualifier가 해당 String 값을 못 찾으면 하는 행동**

해당 "mainDiscountPolicy" string 인자로 준 이름의 스프링 빈을 추가로 찾는다. 
하지만, @Qualifier 애너테이션은 @Qualifier 애너테이션 이름이 붙은 빈을 찾는 용도로만 사용하는게 명확하고 좋다.

> 정리하자면 @Qualifier 끼리 매칭이 되고, 없으면 빈 이름이 매칭이 된다. 그것 마저도 없으면 NoSuchBeanDefinitionException 예외가 발생한다.

#### 3. @Primary 사용 <- 자주 사용하는 애너테이션

@Primary 애너테이션은 우선 순위를 지정하는 방법이다. @Autowired 애너테이션을 이용해 의존성 주입이 될 떄, 여러 빈이 매칭이 되면 @Primary 애너테이션을 가진 
구현체가 우선권을 가진다.

주로 메인 DB가 존재하고 보조가 DB이 있으면 메인 DB에 커넥션 빈을 이용해 데이터를 가지고 올때, @Qualifier 애너테이션을 사용하고, 
보조 DB에 커넥션할 때도, @Qualifier 애너테이션을 이용해 사용하면 번거로워진다.
그럼 이때 사용이 많은 메인 DB에 @Primary 애너테이션을 이용해 우선권을 가지게 해서 사용하게 만들면 코드를 깔끔하게 관리할 수 있다.

```java
@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy {
}
```

#### @Primary, @Quilifier 중 누가 먼저 동작할까? 

@Primary 애너테이션이 기본값처럼 동작하고, @Quilifier 애너테이션은 매우 상세하게 동작한다.
스프링은 이러한 좁은 범위의 선택권에 우선권을 주므로, 이런 경우에는 @Quilifier 애너테이션 우선권이 높다.

## 애너테이션 직접 만들기

다양한 상황에 놓인 환경에서 아래와 같이 애너테이션을 직접 생성해서 관리하면 코드가 간결해지고 명확해진다.

애너테이션 재정의
```java
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
@Qualifier("mainDiscountPolicy")
public @interface MainDiscountPolicy {
}
```

@Qualifier 애너테이션을 대체해서 사용
```java
@Component
@MainDiscountPolicy
public class RateDiscountPolicy implements DiscountPolicy {
}
```
@Qualifier 애너테이션을 대체해서 사용
```java
@Component
public class OrderServiceImpl implements OrderService{

    private final MemberRepository memberRepository;
    private final DiscountPolicy discountPolicy;

    @Autowired
    public OrderServiceImpl(MemberRepository memberRepository,@MainDiscountPolicy DiscountPolicy discountPolicy) {
        this.memberRepository = memberRepository;
        this.discountPolicy = discountPolicy;
    }
}
```

애너테이션에는 상속이라는 개념이 없다. 이렇게 여러 애너테이션을 모아 사용하는 기능은 스프링이 지원해주는 기능이다.
@Qualifier 애너테이션 뿐만 아니라 다른 애너테이션도 함께 조합해서 사용할 수 있다. 단적으로 @Autowired 애너테이션도 재정의 할 수 있다.
**물론 스프링이 제공하는 기능을 뚜렷한 목적 없이 무분별하게 재정의 하는 것은 유지보수에 더 혼란만 가중할 수 있다.**

### 조회한 빈을 모두 사용해야 할 때 (List, Map 이용)

할인 서비스를 제공하는데 클라이언트가 할인의 종류(rate, fix)를 선택할 수 있다고 가정할 때, 스프링을 사용하면 소위 말하는 전략 패턴을 이용해 매우 간단하게 
구현할 수 있다.

#### 로직 분석

1. DiscountService는 Map으로 모든 DiscountPolicy 타입의 구현체를 주입받는다. 이때, fixDiscountPolicy, rateDiscountPolicy 구현체가 주입된다.
2. dicount() 메서드는 dicountCode로 fixDiscountPolicy 구현체가 넘어오면 map에서 fixDiscountPolicy 스프링 빈을 찾아 실행한다. 물론, rateDiscountPolicy 구현체가 넘어오면 rateDiscountPolicy 구현체가 실행된다.

#### 주입 분석

- Map<String, DiscountPolicy>
  - map 키에 스프링 빈의 이름을 넣어주고, 그 값으로 DiscountPolicy 타입으로 조회한 모든 스프링 빈을 담는다.
- List<DiscountPolicy>
  - DiscountPolicy 타입으로 조회한 모든 스프링 빈을 담아준다.
- 만약 해당하는 타입의 스프링 빈이 없으면, 빈 컬렉션이나 Map을 주입한다.



### 빈 생명 주기
#### 빈 생명 주기와 콜백

애플리케이션이 시작할 때, 데이터베이스 서버를 많으면 100개 적으면 10개를 미리 잡아 미리 연결해 둬야 안정적으로 돌아간다.위와 같이 데이터베이스 커넥션 풀이나 네트워크 소켓처럼 애플리케이션 시작 시점에 미리 연결하고, 애플리케이션이 종료될 때 안전하게 종료를 해줘야 한다. 즉, 객체의 초기화와 종료 작업이 필요하다.

이러한 정상적으로 종료 처리를 해주는 기능을 스프링이 제공을 한다.

스프링 빈은 객체 생성 후 의존관계 주입의 라이프 사이클을 가진다.(생성자 주입 예외)
스프링 빈은 객체를 생성하고, 의존관계 주입이 다 끝난 다음에 필요한 데이터를 사용할 수 있는 준비가 완료된다. 따라서 초기화 작업은 의존관계 주입이 모두 완료되고 난 다음에
호출해야 한다. 그러면 개발자 시점에서는 어디에서 의존관계를 어디에 호출해야 할까? 

**스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해 초기화 시점을 알려주는 다양한 기능을 제공한다. 또한 스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 준다. 따라서 안전하게 종료 작업을 진행할 수 있다.**

스프링 빈의 이벤트 라이프 사이클

1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존관계 주입
4. 초기화 콜백
5. 사용
6. 소멸전 콜백
7. 스프링 종료

- 초기화 콜백
  - 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출
- 소멸전 콜백
  - 빈이 소멸되기 직전에 호출

#### 객체 생성과 초기화를 분리하자

생성자는 필수 정보(파라미터)를 받고, 메모리를 할당해서 객체를 생성하는 책임을 가진다. 반면에 초기화는 이렇게 생성된 값들을 활용해서 외부 커넥션을 연결하는 등, 무거운 동작을 수행한다.

생성자 안에서 무거운 초기화 작업을 함께 하는 것 보다 객체를 생성하는 부분과 초기화 하는 부분을 명확하게 나누는 것이 유지보수 관점에서 좋다.
물론 초기화 작업이 내부 값들만 약간 변경하는 정도로 단순한 경우에는 생성자에서 한번에 처리하는 것이 더 나을 수 있다.

#### 스프링은 크게 3가지 방법으로 생명주기 콜백을 지원한다.

1. 인터페이스

2. 설정 정보에서 구성

3. 애너테이션 설정

#### 1.  InitializingBean, DisposableBean 인터페이스 오버라이딩

초기화와 소멸하는  InitializingBean, DisposableBean 인터페이스

- InitializingBean
    - afterPropertiesSet() : 메서드 초기화 지원
- DisposableBean : 메서드 소멸을 지원
    - destroy() : 메서드를 안정적으로 종료하는 기능을 지원

- 인터페이스는 스프링 전용 인터페이스다. 해당 코드가 스프링 전용 인터페이스에 의존한다.
- 초기화, 소멸 메서드의 이름을 변경할 수 없다.
- 내가 코드를 고칠 수 없는 외부 라이브러리에 제공할 수 없다.

> 인터페이스를 사용하는 초기화와 종료 방법은 스프링 초창기에 나온 방법들이고, 지금은 더 나은 방법들을 제공하고 있다.

```java
public class NetworkClient  implements InitializingBean, DisposableBean {
    private String url;

    public NetworkClient() {
        System.out.println("생성자 호출 url = " + url);
    }

    public void connect(){
        System.out.println("connect : " + url);
    }

    public void call(String message){
        System.out.println("call : " + url + "message = "+message);
    }

    public void disconnect(){
        System.out.println("close : " + url);
    }

    public void setUrl(String url) {
        this.url = url;
    }

    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("NetworkClient.afterPropertiesSet");
        connect();
        call("초기화 연결 메시지");
    }

    @Override
    public void destroy() throws Exception {
        System.out.println("NetworkClient.destroy");
        disconnect();
    }
}
```

#### 2. 설정 정보에서 구성 - 빈 등록 초기화, 소멸 메서드

설정 정보에서 구성하는 방법 이용한 특징

- 메서드 이름을 자유롭게 사용 가능
- 스프링 빈이 스프링 코드에 의존하지 않는다.
- **코드가 아니라 설정 정보를 사용하기 때문에, 코드를 고칠 수 없는 외부 라이브러리에도 초기화, 종료 메서드를 적용할 수 있다.**

```java
    @Configuration
    static class LifeCycleConfig{
        @Bean(initMethod = "init", destroyMethod = "close")
        public NetworkClient networkClient(){
            NetworkClient networkClient = new NetworkClient();
            networkClient.setUrl("http://hello-spring.dev");
            return networkClient;
        }
    }
```

종료 메서드 destroyMethod 추론
infer-method = "(inferred)"

- 라이브러리는 대부분 'close', 'shutdown' 이라는 이름의 종료 메서드를 사용한다.
- @Bean 의 default는  "(inferred)" 으로 등록되어 있따. 이 추론 기능은 'close', 'shutdown' 이라는 이름의 종료 메서드를 자동으로 호출해준다. 그렇기에 따로 적어두지 않아도 잘 적동한다.
- 만약 사용하기 싫다면 destroyMethod = "" 공백을 주면 된다.

#### 3. 애너테이션을 이용 - @PostConstruct, @PreDestroy

**이 방법을 사용하자!!**

- 최신 스프링에서 가장 권장하는 방법이다.
- 애너테이션 하나만 붙이면 되므로 매우 편리하다.
- 컴포넌트 스캔과 잘 아울린다.
- 유일한 단점은 외부 라이브러리에 적용하지 못한다는 점이다. 외부 라이브러리를 초기화와 종료를 해야 한다면 @Bean의 기능을 사용하자.

#### 정리

- **애너테이션을 이용해 관리하자**
- 코드를 고칠 수 없는 외부 라이브러리를 콜백 해야한다면 구성 설정 정보에서 관리하자

### 빈 스코프

지금까지 우리는 스프링 빈이 스프링 컨테이너의 시작과 함께 생성되어 스프링 컨테이너가 종료될 때 까지 유지된다. 이것은 스프링 빈이 기본적으로 싱글톤 스코프로 생성되기 때문이다.

> 스프링은 다음과 같은 스코프를 지원한다.

- 싱글톤
  - 기본 스코프
- 스코프
  - 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다.
- 웹 관련 스코프
  - request : 웹 요청이 들어오고 나갈때 까지 유지되는 스코프이다.
  - session : 웹 세션이 종료될 떄 까지 유지되는 스코프이다.
  - application : 웹 서블릿 컨텍스와 같은 범위로 유지되는 스코프다.

#### 빈 스코프 지정

- 컴포넌트 스캔 자동 등록 : @Component 애너테이션을 붙인 구현체 위에 @Scope("Scope type") 애너테이션을 붙이다.
- 수동 등록 : 구성 설정 정보에 있는 @Bean 애너테이션이 붙은 구현체에 @Scope("Scope type") 애너테이션을 붙인다.


#### 싱글톤 빈 스코프
#### 프로토타입 빈 스코프
요청 값에 따른 새로운 빈을 생성해 의존관계를 주입하고 나서 리턴하고 나면 종료한다. 

> 프로토타입의 핵심은 스프링 컨테이너는 프로토타입 빈을 생성하고, 의존관계 주입, 초기화까지만 처리한다는 것이다. (그러면 책임을 누가 지냐면 요청한 클라이언트가 책임을 지고 종료를 해줘야 한다.)
> 클라이언트 빈을 반환하고, 이후 스프링 컨테이너는 생성된 프로토 타입 빈을 관리하지 않는다. 프로토타입 빈을 관리할 책임은 프로토타입 빈을 받은 클라이언트에 있다. **그래서 '@PreDestroy' 메서드가 호출되지 않는다.**


#### 싱글톤 빈과 프로토타입 빈의 차이점

- 싱글톤 빈은 스프링 컨테이너 생성 시점에 초기화 메서드가 실행 되지만, 프로토타입 스코프의 빈은 스프링 컨테이너에서 빈을 조회할 때 생성되고, 초기화 메서드도 실행된다.
- 프로토타입 빈을 두 번 조회 했으므로 완전히 다른 스프링 빈이 생성되고, 초기화도 두 번 샐행된 것을 확인할 수 있다.
- 싱글톤 비은 스프링 컨테이너가 관리하기 때문에 스프링 컨테이너가 종료될 때 빈의 종료 메서드가 실행되지만, 프로토타입 비은 스플이 컨테이너가 생성과 의존관계 주입 그리고 초기화 까지만 관여하고 더는 관리하지 않는다. 따라서 프로토타입 빈은 스프링 컨테이너가 종료될 때, @PreDestroy 같은 종료 메서드가 전혀 실행되지 않는다.

#### 프로토타입 특징 정리

- 스프링 컨테이너에 요청할 때 마다 새로 생성된다.
- 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입 그리고 초기화까지만 관여한다.
- **종료 메서드가 호출되지 않는다.**
- 프로토타입 빈은 프로토타입 빈을 조회한 클라이언트가 관리해야 한다. 종료 메서드에 대한 호출도 클라이언트가 직접 해야 한다.

#### 웹 스코프

- 웹 환경에만 동작한다.
- 프로토타입과 다르게 스프링이 해당 스코프의 종료시점까지 관리한다. 따라서 종료 메서드가 호출된다.


#### 웹 스코프 종류

- request
  - HTTP 요청 하나가 들어오고 나갈 때 까지 유지되는 스코프, 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고 관리된다.
- session
  - HTTP Session과 동일한 생명주기를 가지는 스코프
- application
  - 서블릿 컨텍스트(ServletContext)와 동일한 생명주기를 가지는 스코프
- websocket
  - 웹 소켓과 동일한 생명주기를 가지는 스코프

request 요청 -> 특정 클라이언트 전용 빈 생성 (request scope) -> http request 가 같으면 전용 빈 (전용 request scope) 에서 활동
**즉, Http request 에 따라 각각 정보를 제공해준다.**

#### request 스코프 예제 만들어서 이해하기

동시에 여러 HTTP 요청이 오면 어떤 요청이 남긴 로그인지 구분하기 어렵기에 이럴 때 사용하면 좋은 것이 바로 request 스코프이다. 로그 앞에 scope마다 uuid를 사용해서 HTTP 요청을 구분하자.

build.gradle 파일에 스프링 부트 스타터 웹 라이브러리를 넣자

```groovy
    implementation 'org.springframework.boot:spring-boot-starter-web'
```

spring-boot-starter-web 라이브러리를 추가하면 내장 톰켓 서버를 활용해 웹 서버와 스프링을 함께 실행한다.
> 스프링 부트는 웹 라이브러리가 없으면 우리가 지금까지 학습한 AnnotationConfigApplicationContext 구현체를 기반으로 애플리케이션을 구동했지만 웹과 관련된
> 추가 설정과 환경을 이용하려면 AnnotationConfigServletWebServerApplicationContext 구현체를 기반으로 사용해야 한다. (물론 이제부터 이 기능을 이용해 애플리케이션이 구동된다.)


그냥 이렇게 설정하면 error 가 난다 왜냐하면 우리가 요청하는 request scope는 특정한 유저가 응답을 했을 때, 생성이 되고 응답이 끝나면 종료되는 생명 주기를 가지고 있다.
그렇기에 아래와 같이 응답을 받기전에 컨테이너에서 의존관계를 주입하려고 하니 존재하지 않은 빈이라 판단하고 있다.

```java
//오류나는 컨트롤러
@Controller
@RequiredArgsConstructor
public class LogDemoController {

    private final LogDemoService logDemoService;
    private final MyLogger myLogger;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request){
        StringBuffer requestURL = request.getRequestURL();
        myLogger.setRequestURL(String.valueOf(requestURL));
        myLogger.log("Controller test");
        logDemoService.logic("testId");
        return "OK";
    }
}
```


```java
@Service
@RequiredArgsConstructor
public class LogDemoService {
    private final MyLogger myLogger;

    public void logic(String id) {
        myLogger.log("Service id = " + id);
    }
}

```

> 왜 서비스에서 모든 로직을 사용하지 않았냐면 requestURL과 같은 웹과 관련된 정보가 웹과 관련 없는 서비스 계층까지 넘어가면 안된다.
서비스 계층은 웹 기술에 종속되지 않고, 가급적 순수하게 유지하는 것이 유지보수 관점에서 좋다.

#### 1. ObjectProvider를 이용한 방법

ObjectProvider를 이용하면 MyLogger를 찾을 수 있는 DL이 주입이 되면서 에러가 나지 않는다.


> 이런 로직은 컨트롤러 보다 공통 처리가 가능한 스프링 인터셉터와 서블릿 핏터에서 사용하자
 
```java
@Controller
@RequiredArgsConstructor
public class LogDemoController {

    private final LogDemoService logDemoService;
//    private final MyLogger myLogger;
    private final ObjectProvider<MyLogger> myLoggerObjectProvider;

    @RequestMapping("log-demo")
    @ResponseBody
    public String logDemo(HttpServletRequest request){
        MyLogger myLogger = myLoggerObjectProvider.getObject();
        StringBuffer requestURL = request.getRequestURL();
        myLogger.setRequestURL(String.valueOf(requestURL));
        myLogger.log("Controller test");
        logDemoService.logic("testId");
        return "OK";
    }
}
```

#### 2. 프록시를 이용한 방법

@Scope 애너테이션의 proxyMode = ScopedProxyMode.TARGET_CLASS 명령어를 설정하면 스프링 컨테이너는 CGLIB 라는 바이트코드를 조작하는 라이브러리를 사용해 MyLogger를 상속받은 가짜 프록시 객체를 생성한다.

### 프록시

@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
스프링이 조작해서 만든 빈이 등록이 되어있다. 즉 껍데기 구현체를 집어 넣고, 기능이 실제 호출하는 시점에서 진짜 객체를 찾아 넣는 작업을 한다.

CGLIB라는 라이브러리로 내 클래스를 상속 받은 가짜 프록시 객체를 만들어서 주입한다.

- @Scope 애너테이션의 proxyMode = ScopedProxyMode.TARGET_CLASS 명령어를 설정하면 스프링 컨테이너는 CGLIB 라는 바이트코드를 조작하는 라이브러리를 사용해 MyLogger를 상속받은 가짜 프록시 객체를 생성한다.
- 결과를 확인하면 우리가 등록한 순수한 MyLogger 클래스가 등록되는 것이 아닌 스프링이 바이트 코드를 조작한 가짜 프록시 객체가 만들어져 등록되어져 있는 것을 알 수 있다.
- 나중에 빈을 조회해도 프록시 객체가 조회되는 것을 확인할 수 있따.

> 의존관계 주입도 가짜 프록시 객체가 주입되어 실행되게 때문에, 요청이 있어야 실행하는 request 스코프도 오류 없이 실행 시킬 수 있고, 실제 요청이 들어와 작업을 할 필요가 있을 떄, 프록시 객체는 실제 필요한 객체를 가져와 작업을 하도록 도와준다.
**가짜 프록시 객체는 요청이 오면 그때 내부에서 진짜 빈을 요청하는 위임 로직이 들어있다.**

프록시 빈은 내부에서 실제 객체를 찾아오는 방법을 가지고 있다.
클라이언트가 해당 프록시 빈을 호출할 때, 가짜 프록시 객체의 메서드를 호출한 것이고, 이 호출을 받을 떄, 프록시 빈은 requst 스코프를 호출해 해당 작업을 실행한다.

#### 어떻게 이게 가능한가?

**프록시 객체는 원본 클래스를 상속 받아 만들었기 때문에 해당 객체를 사용하는 클라이언트 입장에서는 실제 객체와 동일하게 사용할 수 있는 다형성의 특징을 가지고 있기 때문에 가능한 일이다.**

#### 정리

- 싱글톤을 사용하 듯이 편리하게 request 스코프를 사용할 수 있다.
- 사실 Provider를 사용하든 프록시를 사용하든 핵심 아이디어는 **진짜 객체 조회를 꼭 필요한 시점까지 지연처리 한다는 점이다.**
  - 진짜 HTTP 요청이 올 때까지 버티는 상황이다.
- 단지 애너테이션 설정 변경만으로 원본 객체를 프록시 객체로 대체할 수 있다. 이것이 바로 다형성과 DI 컨테이너가 가진 큰 장점이다.
- 꼭 웹 스코프가 아니더라도 프록시를 사용할 수 있다.

#### 주의점

- 마치 싱글톤을 사용하는 것 같지만 다르게 동작하기 때문에 결국 주의해서 사용해야 한다.
- **이런 특별한 스코프는 꼭 필요한 곳에만 최소화해서 사용하자!! 무분별하게 사용하면 유지보수가 힘들어진다.**
