# **스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술**
## 2. **스프링 웹 개발 기초**
### ResponseBody
``` 
@Controller
public class HelloController {
  @GetMapping("hello-api")
  @ResponseBody
  public Hello helloApi(@RequestParam("name") String name) {
    Hello hello = new Hello();
    hello.setName(name);
    return hello;
  }
}
```

#### helloApi에서 hello.setName 메소드만 호출을 하고 return 이 있는 hello.getName 메소드는 호출 하지 않았는데 결과가 {"name":"srping!!"} 나오는 이유
- @ResponseBody를 사용하면 HTTP 응답의 Body에 문자 내용을 직접 반환하게 되고 helloApi()에서의 반환 값은 hello 객체입니다. 이 때 스프링은 HttpMessageConverter의 구현체 중 MappingJackson2HttpMessageConverter를 이용해서 객체를 Http 응답 바디에 적을 수 있도록 직렬화 과정을 거치게 됩니다. 해당 직렬화를 할 때 객체의 getter 메서드를 사용하게 됩니다.
- 출처: [helloApi의 return 값이 이해가 되지 않습니다. - 인프런 커뮤니티 질문&답변](https://www.inflearn.com/community/questions/820021?focusComment=249584)

## 3. **회원 관리 예제** - **백엔드 개발**

### **회원 리포지토리 메모리 구현체**


```
public class MemoryMemberRepository implements MemberRepository {

  private static Map<Long, Member> store = new HashMap<>();//실무에서는 `ConcurrentHashMap` , `AtomicLong` 사용 고려해야 한다.
  private static long sequence = 0L;

  @Override
  public Member save(Member member) {
    member.setId(++sequence);
    store.put(member.getId(), member);
    return member;
  }
}
```
#### AtomicLong이란?
- 여러 스레드가 사용되게 되면 코드의 결과 값이 작동할 때마다 달라져, 일치하지 않게 될 것입니다. 값이 일치하지 않게 된 이유는 ++sequence 로 되어있는 간단한 증감연산 때문입니다. 이 연산은 겉으로 보기에 원자적 연산(한번에 하나씩 수행되는 연산이라고 요약할 수 있습니다)처럼 보일 수 있지만 실제로는 값을 얻고, 얻은 값을 증가시키고, 증가시킨 값(업데이트된 값)을 다시 쓰는 세 가지의 연산이 일어납니다.
- 여러 스레드가 CAS 알고리즘을 통해 동일한 값을 업데이트하려 할 때, 한 스레드가 경합에서 이기고 해당 값을 업데이트 합니다. synchronized를 이용한 lock을 이용하는 경우와 달리 다른 스레드는 해당 값이 업데이트되는 동안에도 일시 중단되지 않습니다. 대신에 다른 스레드들은 해당 값을 업데이트하지 못했다는 것을 알게 됩니다. 이렇게 되면 해당 값을 업데이트하는 스레드를 제외한 다른 스레드들은 추가로 다른 작업을 진행할 수 있으며 스레드 간의 콘텍스트 스위치도 일어나지 않습니다.
- 자바에서는 [AtomicInteger](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/atomic/AtomicInteger.html), [AtomicLong](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/atomic/AtomicLong.html), [AtomicBoolean](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/atomic/AtomicBoolean.html), [AtomicReference](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/atomic/AtomicReference.html) 클래스를 제공합니다.
- 출처: [Long 과 AtomicLong은 어떤 차이가 있을까?](https://simgee.tistory.com/37)

### **회원 서비스 개발**
#### 의존성 주입이란?
- 의존성이란 한 객체가 다른 객체를 사용할 때 의존성이 있다고 한다. 예컨대 MemberService 객체가 MemoryMemberRepository 객체를 사용하고 있는 다음과 같은 경우 ‘MemberService 객체가 MemoryMemberRepository 객체에 의존성이 있다.’고 한다.
- ```
  public class MemberService {
      private final MemberRepository memberRepository = new MemoryMemberRepository();
  }
  ```
  
- MemberService 객체가 MemoryMemberRepository 객체과 강하게 결합되어 있는 문제를 해결하기 위해 의존성 주입(Dependency Injection, DI) 이 필요하다. MemberService 객체가 구체 클래스인  MemoryMemberRepository 대신 인터페이스인 memberRepository를 통해서 리포지토리를 주입을 받도록 한다. 인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하는 것이다.
- ```
  public class MemberService {
  
  	private final MemberRepository memberRepository;
  
  	public MemberService(MemberRepository memberRepository) {
    		this.memberRepository = memberRepository;//DI
  	}
  }
  ```
-  이러한 개념은 제어의 역전(Inversion of Control, IoC)라고 불리기도 한다. 어떠한 객체를 사용할지에 대한 책임은 프레임워크에게 넘어갔고, 자신은 수동적으로 주입받는 객체를 사용하기 때문이다.
- 출처: [\[Spring\] 의존성 주입\(Dependency Injection, DI\)이란? 및 Spring이 의존성 주입을 지원하는 이유](https://mangkyu.tistory.com/150)