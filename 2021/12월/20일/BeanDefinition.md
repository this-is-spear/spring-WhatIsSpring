## BeanDefinition
### 스프링 빈 설정 메타 정보 - BeanDefinition
스프링이 다양한 설정 형식을 지원하는 중심에는 BeanDefinition 추상 클래스가 존재한다.
@Configuration 애너테이션이 붙은 설정 파일을 읽어 빈으로 설정된 구현체들을 BeanDefinition(빈 설정 메타 정보)에 메타 정보가 생성된다.
그리고 BeanDefinition 에 존재하는 메타 정보들을 읽어 스피링 빈을 생성한다.

1. JAVA
   1. AnnotationConfigApplicationContext 호출
   2. AnnotationConfigApplicationContext 안에 있는 reader 인 AnnotatedBeanDefinitionReader 호출
   3. AnnotatedBeanDefinitionReader가 AppConfig.class 읽는다.
   4. BeanDefinition 생성
   5. @Bean 애너테이션이 붙은 구현체들을 BeanDefinition 에 메타 정보 저장
   6. 스프링 컨테이너는 BeanDefinition에 설정된 메타 정보를 이용해 스프링 빈 생성
2. XML
   1. GenericApplicationContext
   2. XmlBeanDefinitionReader
   3. appConfig.xml
   4. BeanDefinition 생성
3. Xxx
   1. 새로운 형식의 설정 정보가 추가 되면 XxxBeanDefinitionReader 생성
   2. BeanDefinition 생성

### BeanDefinition 정보

- BeanClassName
  - 생성할 빈의 클래스명(자바 설정처럼 팩토리 빈을 사용하면 없음)
- factoryBeanName
  - 팩토리 역할의 빈을 사용할 경우
- factoryMethodName
  - 빈을 생성할 팩토리 메서드 지정
- Scope
  - 싱글톤
- lazyInit
  - 스프링 컨테이너를 생성할 때, 빈을 생성하는 것이 아니라, 실제 빈을 사용할 때 까지 최대한 생성을 지연처리 하는지 여부
- InitMethodName
  - 빈을 생성하고, 의존관계를 적용한 뒤에 호출되는 초기화 메서드 명
- DestroyMethodName
  - 빈의 생명주기가 끝나서 제거하기 직전에 호출되는 메서드 명
- Constructor arguments, Properties
  - 의존관계 주입에서 사용(자바 설정처럼 팩토리 역할의 빈을 사용하면 없음)

아래와 같이 getBeanDefinitionNames() 메서드를 호출해서 하나씩 가져오게 된다면 BeanClassName 인자를 가져오게 된다. 그리고 이 BeanClassName 인자를 이용해 getBean() 메서드를 사용하면 위에 있는 BeanDefinition 정보들이 모두 출력이 된다.

```java
    @Test
    @DisplayName("모든 빈 출력하기")
    public void findAllBean () throws Exception{
        //given
        String[] beanDefinitionNames = applicationContext.getBeanDefinitionNames();
        //when
        for(String beanDefinitionName : beanDefinitionNames){
            Object bean = applicationContext.getBean(beanDefinitionName);
            System.out.println("name = " + beanDefinitionName+ " object = " + bean);
        }
        //then
    }
```
