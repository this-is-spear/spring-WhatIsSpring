
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

#### BeanA 빈도 제외하고 싶은 경우에 ASSIGNABLE_TYPE 타입을 이용한다.

```java
    @Configuration
    @ComponentScan(
            includeFilters = @Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class),
            excludeFilters = {
                    @Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class),
                    @Filter(type = FilterType.ASSIGNABLE_TYPE, classes = BeanA.class)
            }
    )
    static class ComponentFilterAppConifg{

    }
```
