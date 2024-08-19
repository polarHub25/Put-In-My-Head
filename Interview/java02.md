
## Checked Exception과 Unchecked Exception에 대해 설명해주세요. 
스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요?
> Checked Exception
- 컴파일 시점에 체크되는 예외
- 개발자가 명시적으로 처리해야함 ( try-catch-throws )
- Exception 클래스를 직접 상속
- I/O, 파일, 네트워크, DB 작업 등 외부 자원과 관련된 작업에서 발생
- IOException, SQLException, ClassNotFoundException

> Unchecked Exception
- 런타임 시점에 발생하는 예외 
- 컴파일러가 강제하지 않으므로 명시적으로 처리 하지 않아도 됨. 개발자가 코드를 잘 작성하면 피할 수 있는 예외
- RuntimeException 클래스를 상속
- Null 참조, 배열 인덱스 초과, 잘못된 연산 등에서 발생 
- NummPointerException, ArrayIndexOutOfBoundsException, IllegalArgumentException.. 

> 예외( Exception )vs 오류 ( Error ) 
- 예외( Exception )
: 프로그램 실행 중 발생할 수 있는 예상 가능한 문제 

- 오류( Error )
: 시스템 레벨에서 발생하는 문제로, 일반적으로 개발자가 예측하거나 처리할 수 없는 문제. 주로 JVM에서 발생하며, 프로그램의 비정상 종료를 초래할 수 있음

> 스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요?
- Unchecked Exception(RuntimeException)과 Error가 발생할때 트랜잭션을 롤백

> Checked Exception이 발생해도 트랜잭션을 롤백하려면 어떻게 해야 하나요? 
- @Transactional 어노테이션의 rollbackfor 속성을 사용해 롤백 대상 지정 가능 
- @Transactional(rollbackFor = Exception.class) 로 설정하면 롤백 가능

> 스프링 트랜잭션에서 기본적으로 RuntimeException과 Error만 롤백하는 이유는? 
- RuntimeException과 Error는 예측 불가능한 비정상적인 상황을 나타내므로, 데이터의 일관성을 위해 자동으로 롤백. 
- Checked Exception은 비즈니스 로직의 일부로 발생할 수 있어 롤백 여부를 개발자가 선택할수 있음

> OutOfMemoryError에 대해서 발생시점, 예방 방법, 처리 방법에 대해서 알려주세요 
- JVM의 힙 메모리나 메타스페이스 영역에서 사용할 수 있는 메모리가 부족할 때 발생하는 런타임 오류 
- 발생 시점 
: 메모리 누수 , 메모리 과다 사용 ( 대량의 데이터를 힙 메모리에 적재하거나, 대규모 컬렉션을 무한 확장시 ), 잘못된 객체 관리 ( 무한 루프 ) 
- 예방 방법 
: 사용이 끝난 객체를 명시적으로 참조 해제 , 메모리 효율이 좋은 데이터 구조 사용하여 불필요한 메모리 사용 줄임 , JVM 옵션 ( -Xms, -Xmx ) 를 설정하여 힙 메모리 크기 조정 , 불필요한 객체 생성 피함
- 처리 방법 
: 발생 즉시 큰 객체나 불필요한 참조를 해제하여 메모리 확보 후 작업 재시도 , 메모리 부족이 근본적으로 자원의 한계에서 발생했다면, JVM 힙 메모리 설정을 늘리거나, 분선 처리로 재설계하여 시스템 부담 줄이기, 애플리케이션 재시작


## Java8에서 추가된 기능에 대해서 설명해주세요.
- 람다 표현식
: 함수를 간단하게 표현할 수 있는 방법. 주로 익명 내부 클래스를 대체하기 위해 사용. 

``` java 
List<String> names = Arrays.asList("a", "b", "c");
names.forEach(name -> System.out.println(name)); // 람다 표현식 사용
```

- 스트림 API ( Stream API ) 
: 데이터 처리를 함수형 스타일로 처리할 수 임음. 컬렉션 데이터를 필터링, 매핑, 정렬 등 작업을 수행할 때 유용, 병렬 처리 기능도 제공
``` java 
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::println); // 짝수만 출력
```

- 인터페이스 디폴트 메서드
: 인터페이스에 디폴트 메서드 정의 가능.

- 메서드 참조 
: 기존 메서드를 람다 표현식처럼 사용할 수 있도록 지원. 간결하고 가독성 높은 코드 작성 가능
``` java 
List<String> names = Arrays.asList("a", "b", "c");
names.forEach(System.out::println); // 메서드 참조 사용
```

- Optional class 
: 값이 있을 수도 있고, 없을 수도 있는 상황을 처리하는데 유용. NPE 방지 가능

``` java 
Optional<String> optionalName = Optional.ofNullable(null);
System.out.println(optionalName.isPresent()); // false 출력
optionalName.ifPresent(System.out::println); // 값이 없으면 아무것도 출력되지 않음
```

- 날짜와 시간 API ( java.time 패키지 ) 
: 기존의 java.util.Date와 Calendar의 단점을 보완한 새로운 API 도입 . 불변 객체를 기반으로 하며 직관적인 날짜와 시간 처리 가능
- 기존 API : 불변성이 없으며, 스레드 안전하지 않음. 월이 0부터 시작, 시간대와의 통합 불편
- 변경된 API : 불변 객체, 스레드 안전. 월이 1부터 시작, 시간대 관련(ZoneDateTime) 제공
``` java 
LocalDate today = LocalDate.now();
System.out.println(today);
``` 

> 스트림 API의 장점은 무엇이며, 실무에서 어떻게 활용해봤나요? 
- 스트림 API는 데이터 처리 로직을 간결하게 구현할 수 있고, 실무에서 스트림 API를 활용하여 컬렉션 데이터를 효율적으로 처리한 경험이 있습니다. 
예를 들어, SubscriptionList라는 리스트안에 각 리스트의 요소는 Subscription 객체였고, 각 Subscription 객체는 Subscriptiontool 객체를 포함한 또 다른 리스트를 가지고 있었습니다. 
즉, 리스트 안에 데이터가 리스트로 들어가 있는 중첩된 형태였습니다. 기존에는 중첩 반복문과 조건문을 사용해 데이터를 처리헀지만, 스트림API의 flatMap() 를 활용해 리스트의 리스트를 평탄화하여( 하나의 리스트 형태로 ) 효율적으로 데이터를 처리할 수 있었습니다. 

> flatMap()의 동작원리 설명해주세요 
- 스트림의 각 요소를 함수로 매핑한 후, 반환된 여러 하위 스트림을 하나의 스트림으로 평탄화하여 단일 스트림을 생성하는 메서드. 주로 리스트 안의 리스트와 같은 중첩된 데이터를 처리할 때 사용

## try-with-resource에 대해서 설명해주세요.
- Java 7에서 도입된 기능으로 자동으로 자원을 해제(Close)해주는 구문
- 파일, DB 연결, 네트워크 소켓 등과 같이 자원을 명시적으로 해제해줘야 하는 경우 사용 
- try-catch-finally 구조에서 자원을 수동으로 해제해야 하는 번거로움과 자원 해제 누락으로 인한 문제를 해결하기 위해 도입
- 자원 해제를 자동으로 처리해 코드가 간결해지며, 예외가 발생해도 자원이 안젼하게 해제. 자원 누수 문제 방지
- try 블록에서 사용하는 자원이 AutoCloseable 인터페이스를 구현하고 있어야함 
- java의 자원 클래스들은 대부분 AutoCloseable을 이미 구현함 
ex) InputStream, OutputStream, Reader, Writer, Connection, BufferReader, FileReader.. 
- AutoCloseable을 구현하면 try 블록이 끝날 때, 자원이 자동으로 해제되도록 close()메서드 호출

> try-with-resource에서 여러 자원을 다룰 때 자원 해제 순서는 어떻게 되나요? 
- 여러 자원을 선언하면, 선언된 순서의 역순으로 자원이 해제되며, 이는 자원들 간의 의존성 문제를 안전하게 처리하기 위함

## 강한 결합과 느슨한 결합이 무엇인지 설명해주세요.
> 강한 결합 ( Tight Coupling )
- 클래스가 서로의 구체적은 구현에 의존하며, 하나의 클래스가 변경되면 그 클래스를 의존하는 다른 클래스들도 변경 해야함. 시스템 확장이나 유지보수가 어려워짐

> 느슨한 결합 (Loose Coupling ) 
- 클래스나 모듈간의 의존성을 최소화하며 (인터페이스나 추상화를 통해 의존성을 줄임), 변경에 유연하고 확장성이 뛰어남

> 결합도와 응집도는 어떤 관계가 있나요? 
- 결합도는 클래스나 모듈간의 의존성을 의미하고, 응집도는 클래스나 모듈 내부의 요소들이 얼마나 밀접하게 관련되어 있는지를 나타내는데, 좋은 소프트웨어 설계는 낮은 결합도와 높은 응집도를 목표로 함 
- ex) 하나의 클래스가 단일 책임 원칙 ( SRP )을 따르면서 다른 클래스와의 의존성을 최소화한다면, 이 클래스는 높은 응집도와 낮은 결합도를 가지고 있다고 볼수 있음 
