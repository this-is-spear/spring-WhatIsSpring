
### Configuration and Singleton

아래의 AppConfig.class 에서 memberService() 메서드와 orderService() 메서드에서
memoryRepository() 메서드를 두번 실행하면서 return new MemoryMemberRepository(); 명령어가 실행이 된다.
그러면 해당 명령어에 따라 MemoryMemberRepository() 객체가 두개 생성이 되어야 하는데 
스프링은 각기 다른 2개의 객체를 생성하면서 싱글톤이 깨지는 것 처럼 보이는데 스프링 컨테이너는 어떻게 해결할까? 

```java
@Configuration
public class AppConfig {
    @Bean
    public MemberRepository memoryRepository() {
        return new MemoryMemberRepository();
    }

    @Bean
    public DiscountPolicy discountPolicy() {
        return new RateDiscountPolicy();
    }

    @Bean
    public MemberService memberService(){
        return new MemberServiceImpl(memoryRepository());
    }

    @Bean
    public OrderService orderService(){
        return new OrderServiceImpl(memoryRepository(), discountPolicy());
    }
}
```

해당 구현체인 serviceImpl에 들어가 각 memoryRepository() 레퍼런스를 불러와 비교해보자

실제 예상하는 호출 순서

call AppConfig.memoryRepository
call AppConfig.memberService
call AppConfig.memoryRepository <- memberService 안에서 call
call AppConfig.orderService
call AppConfig.memoryRepository <- orderService 안에서 call

스프링은 아래와 같이 실행한다.

call AppConfig.memoryRepository
call AppConfig.memberService
call AppConfig.orderService

스프링은 클래스의 바이트코드를 조작하는 라이브러리를 사용하기 때문에 만든 객체를 다시 만들지 않는다.

####  @Configuration 애너테이션과 바이트코드 조작의 마법
스프링 컨테이너는 싱글톤 레지스트리이다. 따라서 스프링 빈이 싱글톤이 되도록 보장해줘야 한다.
그런데 스프링이 자바코드 까지 어떻게 하기는 어렵다. 위와 같은 호출 형식을 본다면 memoryRepository() 메서드는 3번 호출되야 
맞는 순서이지만 스프링은 그렇지 않다.


#### 만약 @Configuration 애너테이션이 없다면? 

**없더라도 @Bean 애너테이션에 붙은 구현체들은 스프링 빈으로 등록할 수 있지만 같은 기능을 가진 구현체들을 중복해서 만들어 싱글톤 레지스트리에 맞지 않게 호출된 만큼 생성이 된다.**
만약 이렇게 된다면 각기 다른 클래스에서 부른 구현체가 달라 동시성 문제가 생길 수 있다.
