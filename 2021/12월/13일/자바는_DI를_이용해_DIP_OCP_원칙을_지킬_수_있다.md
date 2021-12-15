
## 스프링 없이 SOLID 원칙을 잘 해결할 수 있을까? 
본론부터 말하자면 외부에서 의존 관계를 설정해준다면 해결할 수 있다고 생각한다. 각 구현체들은 의존 관계를 설정해주는 클래스에 의해 
외부에서 참조 객체들을 선택받아 생성할 수 있다. 그렇게 되면 우리는 해당 구현 객체를 수정하지 않고도 참조 객체를 마음대로 교체할 수 있다.

내가 어느 부분에서 SOLID 원칙을 지키지 않았고, 그 부분을 어떻게 해결했는지 아래에 설명했다.
### 의존성 주입을 하지 않은 나는 SRP, DIP, OCP 원칙에 어긋나는 설계를 하고 있다.
> 인터페이스를 이용해 역할과 기능을 분리했는데...
 
우리가 추구하는 객체 지향 프로그래밍에서 세가지의 원칙을 어기고 있다.
우리가 어긴 세가지 원칙은 SRP, DIP 그리고 OCP 원칙이다.
1. SRP 원칙에 어긋남
   > 해당 클라이언트 코드는 구현 객체를 참조해야 하고, 실행하는 역할까지 두 개의 책임을 맡은 클라이언트 코드가 된다.
2. DIP 원칙에 어긋남
   > 인터페이스를 의존하고 있지만 인터페이스로 구현한 객체까지도 의존하고 있는 상황이 된다.
3. OCP 원칙에 어긋남
   > 변경에는 닫혀 있어야 하는 OCP 원칙에 어긋난다.


이전까지 우리는 클라이언트 클래스가 생성될 때 마다 구현 객체를 참조해 생성자를 생성해주며 다양한 메서드를 실행했다.

인터페이스를 통해 우리는 인터페이스에 있는 메서드를 참조해 사용할 수 있어서 실제 동작에 필요한 구현 객체가 아무리 변해도 우리는
클라이언트의 코드를 크게 변경 시켜줄 필요가 없는 상황이다. **하지만 동작에 필요한 구현 객체를 바꿔야 하는 상황이 온다면 우리는
필수 불가결하게 클라이언트 코드를 변경해줘야 한다.**

 ```java
public class MemberServiceImpl implements MemberService{
    //해당 구현 객체가 참조하는 객체
    private final MemberRepository memberRepository = new MemoryRepository();
//    다양한 메서드...
}
```
우리가 위화 같은 클라이언트 코드들을 가지고 있고, 구현 객체를 참조하는 클라이언트 코드들이 많다면,
참조하는 클라이언트를 교체해야 할때, 클라이언트 코드들을 다 수정해야하는 상황이 온다. 😖😖
이런 상황을 해결하기 위해 우리는 참조 객체를 외부에서 주입할 수 있는 방법을 통해 구현 객체를 수정하지 않고 참조 객체를 수정할 수 있는 방법을
찾았다.

## 자바를 이용해 SRP, DIP, OCP 원칙을 지킬 수 있을까?

### AppConfig 클래스의 출현 그리고 **DI 등장**
> AppConfig 클래스가 우리에게 어떤 편리함을 제공해 줄까?

AppConfig 클래스는 애플리케이션의 실제 동작에 필요한 구현 객체를 생성하고, 생성한 객체 인스턴스의 참조(레퍼런스)를 생성자를 통해서 주입(연결) 해준다.
생성자 주입을 하기 위해서는 구현 객체에서 생성자를 생성해 주입하려는 인스턴스의 레퍼런스를 인자로 넣어주면 된다.

<br>

아래의 생성자 주입을 통해 해당 ServiceImpl 클래스는 MemoryMemberRepository 참조 객체를 의존하지 않게되어
DIP 원칙과 OCP 원칙에 위배되지 않게 된다. 이러한 생성자 주입은 생성자를 통해서 어떤 구현 객체를 주입할지는 오직 외부
AppConfig 클래스에서 결정하므로 의존관계에 대한 고민은 AppConfig 클래스에 맡기고 설계에만 집중할 수 있다.

AppConfig.java
```java
public class AppConfig {
    public MemberService memberService(){
        return new MemberServiceImpl(new MemoryRepository());
    }
    public OrderService orderService(){
        return new OrderServiceImpl(new MemoryRepository(), new RateDiscountPolicy());
    }
}
```

<br>

그렇게 변경된 MemberServiceImpl 클래스

MemberServiceImpl.java
```java
public class MemberServiceImpl implements MemberService{
    private final MemberRepository memberRepository;

    public MemberServiceImpl(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
//  다양한 메서드들...
}
```

### AppConfig 클래스를 생성하면서 지켜진 원칙들
- SRP

  초기 OrderServiceImpl, MemberServiceImpl 클라이언트 객체들은 직접 구현 객체를 생성하고, 실행하는 다양한 책임을 가지고 있었다.
  > AppConfig 클래스를 생성하면서 구현 객체를 생성하고 연결하는 책임을 AppConfig 클래스로 전가시킴으로 구현 객체에 실행이라는 하나의 책임만을 남겨 SRP 원칙을 지켰다.
- DIP

  새로운 할인 정책을 개발하고 적용시키면 클라이언트 코드들도 함께 변경해야 해서 번거로웠다. 각 서비스들은 DIP 원칙을 지키며 인터페이스에 의존하는 듯 보였지만
  인터페이스와 함께 인터페이스를 구현한 클래스도 함께 의존하는 상황이 발생했다.
    ```java
    public class MemberServiceImpl implements MemberService{
        private final MemberRepository memberRepository = new MemoryRepository();
    }
    ```
  > AppConfig 클래스에 객체 인스턴스를 클라이언트가 직접하는 대신 클라이언트에 의존 관계를 주입하면서 DIP 문제를 해결할 수 있다.

    ```java 
    public class MemberServiceImpl implements MemberService{
       private final MemberRepository memberRepository;
        
       public MemberServiceImpl(MemberRepository memberRepository) {
            this.memberRepository = memberRepository;
       }
    }
    ```
- OCP
  > AppConfig 클래스를 사용해 클라이언트를 변경하지 않고 인스턴스를 AppConfig 클래스에서 의존 관계를 주입하면서 OCP 원칙을 지킬 수 있다.
  이렇게 객체 지향 설계를 하면 새롭게 확장해도 사용 영역의 변경은 닫혀 있게 설계할 수 있다.



## IoC 컨테이너? DI 컨테이너? 그게 뭘까?

### DI - 의존관계 주입
> DI 라고 들어 봤나?

AppConfig 클래스는 구현 객체에서 생성자를 생성해 주입하해주는데, 주입 받는 구현 객체 입장에서 생각하면
마치 외부에서 주입해주는 것을 의존관계 주입(DI)이라 한다.

의존관계는 두 가지로 분리해서 생각해야 한다.
1. 정적인 클래스 의존 관계
    1. 정적인 클래스 의존관계는 클래스가 사용하는 import 코드만 보고 의존관계를 쉽게 판단할 수 있다.
2. 실행 시점에 결정되는 동적인 객체의 의존 관계
    1. 동적인 객체 인스턴스와의 의존 관계는 애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존관계이다.

이렇게 의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있다.


### 제어의 역전(Inversion of Control)
기존 프로그램은 클라이언트 구현 객체가 스스로 필요한 서버 구현 객체를 생성하고, 호출하고 실행했다.
한마디로 프로그램의 흐름을 구현 객체 스스로가 조종했다.

반면에 AppConfig 클래스가 등장한 이후에 구현 객체는 자신의 로직을 실행하는 역할만 담당하면서 제어 흐름을
외부에서 관리하게 된 것을 제어의 역전(IoC)이라고 한다. 

결국 IoC 컨테이너와 DI 컨테이너는 같은 역할을 한다. 제어 흐름을 외부에서 관리하면서 AppConfig 클래스가 IoC 컨테이너가 됐고, 외부에서 의존 
관계 주입을 해주며 AppConfig 클래스가 DI 컨테이너도 되므로 같은 의미라 생각해도 된다. 😊

**AppConfig 클래스는 IoC 컨테이너이며, DI 컨테이너다.**
