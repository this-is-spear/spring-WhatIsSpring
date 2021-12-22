
### FilterType
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
