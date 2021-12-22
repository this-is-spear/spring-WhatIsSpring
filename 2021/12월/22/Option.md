
### 옵션 처리

> 주입할 스프링 빈이 없어도 동작해야 할 때가 있다.
> 그런데, @Autowired 애너테이션만 사용하면 'required' 옵션의 기본값이 true로 되어 있어서
> 자동 주입 대상이 없으면 오류가 발생한다.
 
자동 주입 대상을 옵션으로 처리하는 방법
- '@Autowired(required=false)'
  - 자동 주입할 대상이 없으면 수정자 메서드 자체가 호출이 안된다.
- org.springframework.lang.@Nullable
  - 자동 주입할 대상이 없으면 null이 입력된다.
- Optional<>
  - 자동 주입할 대상이 없으면 Optional.empty가 입력된다.

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
