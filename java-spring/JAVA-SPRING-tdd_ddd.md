# TDD (Test-Driven Development)
### 테스트 주도 개발
- 특징
  - 짧은 개발 서클의 반복을 갖는 개발 프로세스
  - 실패하는 테스트 코드를 먼저 작성하고, 그 후 통과하는 소스 코드를 작성
  - 개발 단위는 작은 단위로 작성
  - 궁극적인 목표는 작동하는 깔끔한 코드를 작성하는 것
- 장점
  - 빠른 피드백이 가능
  - 회기 오류를 잡아줄 꾸준한 테스트를 만들 수 있음
  - 기존 기능을 망가뜨리지 않고 새 기능을 추가할 수 있음
- 단점
  - 초기에 테스트 케이스를 작성해야하기 때문에 빠른 생산성이 요구되는 시점에서는 큰 단점
  - 코드를 테스트하기위해서 테스트 코드를 작성해야하는데 이를 위해서 소프트웨어에 대한 이해도가 필요함
- 진행 순서
    1. 실패하는 테스트 코드 작성
       - 테스트 코드를 돌려서 실패가 뜨는 것을 확인. 컴파일조차 안될 수 있음
    2. 통과하는 테스트 코드 작성
       - 테스트를 통과만 할 정도로 간략하게 작성
    3. 코드 리팩토링
       -  리팩토링을 진행하며 중복을 제거
```java
/* 계산기 기능 */
//1. 실패하는 테스트 코드 작성
public class CalculatorTest {
    
    @Test
    void testAddition() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);  // 2 + 3 = 5
    }
}
// 위 코드를 작성하면 Calculator 클래스가 없다는 컴파일 에러가 발생
```
```java
//2. 통과하는 테스트 코드 작성
// Calculatoro 클래스를 만들어 컴파일 오류 해결
// 통과하기 위한 최소한의 코드 작성
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

```java
// 3. 리팩토링
//현재는 리팩토링할 부분이 없지만, 여러 기능을 추가하면서 개선 가능
//추가적으로 subtract(뺄셈) 기능을 추가할 수도 있음.
@Test
void testSubtraction() {
    Calculator calculator = new Calculator();
    int result = calculator.subtract(5, 2);
    assertEquals(3, result);  // 5 - 2 = 3
}
```
---

# BDD (Behavior-Driven Development)
### 행동 주도 개발
- 특징
  - TDD에서 파생 된 프로그래밍 개발 프로세스
  - 시나리오 기반 테스트 작성
  - 사용자 관점에서 기능 요구 사항을 기술
  - Given-When-Then 형태로 표현하여 주어진 상황에서 어떤 동작을 하고 기대하는 결과가 나오는지를 명시
- 장점
  - 비즈니스 관점에서 테스트를 작성 → 요구사항을 쉽게 이해 가능
  - 비개발자(기획자, QA, 클라이언트)도 테스트를 읽고 참여 가능
  - TDD보다 더 직관적이고 협업이 쉬움
- 단점
  - BDD를 지원하는 소프트웨어 툴은 비교적으로 적다.
  - 개발자들간의 소통시에는 BDD는 다른 개발 방법론들보다 효율성이 적다.



> [!NOTE] Gherkin
> - Cucumber에서 사용하는 테스트 작성 문법 (자연어 기반)<br>
> - Given-When-Then 패턴을 사용하여 시나리오 정의<br>
> - 비개발자도 쉽게 읽고 작성 가능<br>
> - .feature의 확장자<br><br>
> - 구성요소
>   - Feature:	테스트하려는 기능의 이름 (ex 로그인 기능)
>   - Scenario:	개별 테스트 케이스 (올바른 아이디와 비밀번호로 로그인하면 성공한다)
>   - Given	: 초기 상태(설정)를 나타냄 (ex 사용자가 "test@example.com"과 "password123"을 입력했을 때)
>   - When	사용자의 행동(이벤트) (ex 로그인 버튼을 클릭하면)
>   - Then	기대한 결과(검증) (ex 로그인 성공 메시지가 표시되어야 한다)

> [!NOTE] Cucumber
> BDD를 지원하는 테스트 프레임워크<br>
> Java, JavaScript, Python 등 다양한 언어에서 사용 가능<br>
> Gherkin 문법을 사용하여 자연어 기반 테스트 작성 가능<br>
> 개발자뿐만 아니라 기획자, QA, 비개발자도 테스트 이해 가능<br>

> ex) Feature : ATM에서 돈을 인출하는 기능<br>
>Scenario : 계좌에 충분한 잔액이 있을 때 돈을 인출<br>
>  Given : 계좌에 50000원이 들어있다<br>
>  When : 10000원을 출금하면<br>
>  Then : 계좌 잔액은 40000원이 되어야 한다<br><br>
>Scenario: 계좌에 충분한 잔액이 없을 때 출금 시도<br>
>  Given : 계좌에 5000원이 들어있다<br>
>  When : 10000원을 출금하면<br>
>  Then : 출금이 실패해야 한다<br>
>```java
> //Cucumber를 활용
>import static org.junit.jupiter.api.Assertions.*;
>import io.cucumber.java.en.Given;
>import io.cucumber.java.en.When;
>import io.cucumber.java.en.Then;
>public class ATMWithdrawalSteps {
>
>  private int accountBalance;
>  private int withdrawalAmount;
>  private boolean withdrawalSuccess;
>
>  @Given("계좌에 {int}원이 들어있다")
>  public void 계좌에_잔액이_들어있다(int balance) {
>      accountBalance = balance;
>  }
>
>  @When("{int}원을 출금하면")
>  public void 출금을_시도한다(int amount) {
>      withdrawalAmount = amount;
>      if (accountBalance >= withdrawalAmount) {
>          accountBalance -= withdrawalAmount;
>          withdrawalSuccess = true;
>      } else {
>          withdrawalSuccess = false;
>      }
>  }
>
>  @Then("계좌 잔액은 {int}원이 되어야 한다")
>  public void 계좌_잔액_확인(int expectedBalance) {
>      assertEquals(expectedBalance, accountBalance);
>  }
>
>  @Then("출금이 실패해야 한다")
>  public void 출금_실패_확인() {
>      assertFalse(withdrawalSuccess);
>  }
>}
>```



---

# DDD (Domain-Driven Development)
### 도메인 주도 개발
- 특징
  - 일반적으로 많이 사용하는 데이터 중심의 접근법이 아닌, 순수한 도메인의 모델과 로직에 집중
  - 보편적인 언어를 사용하여 도메인 전문가와 개발자 간의 커뮤니케이션 문제를 해결할 수 있음
  - 소프트웨어의 설계와 구조를 도메인 영역에 맞춰 구축하는 개념으로, 비지니스 도메인의 복잡성을 이해하고 그에 맞는 모델과 코드를 개발하여 비지니스 문제를 해결하는 것이 핵심
- 장점
  - 비즈니스 도메인에 집중하여 설계하므로, 개발된 소프트웨어가 실제 비즈니스 요구사항을 정확하게 반영할 수 있음
  - 기획자 혹은 고객과 개발자 간의 공통 언어를 사용하여 의사소통이 원활해짐
- 단점
  - 개념이 많고 익히는 데 시간이 필요하기 때문에 초기 학습 비용이 높음
  - 작은 프로젝트에는 오버 엔지니어링이 될 수 있음 → 단순 CRUD 프로젝트에는 불필요
> ex) 은행 어플리케이션 개발을 한다고 가정했을 때<br>
> Customer(고객) : 고객은 계좌를 가지며, 입출금과 잔액 조회가 가능하다<br>
> Account(계좌) : 계좌는 계좌번호와 잔액 정보를 가지며, 입금과 출금 기능을 제공한다<br>
> Transaction(거래) : 거래는 입금 또는 출금을 나타내며, 거래 내역을 기록한다.<br>
> 이처럼 비지니스 도메인을 중심으로 모델링하여 실제 비지니스 도메인을 반영하는 개념적 모델과 코드를 구현

---

# ATDD (Acceptance Test Driven Development)
### 인수테스트 주도 개발
- 특징
  - 시나리오(사용자 스토리) 기반으로 진행되는 테스트
  - 요구사항에 대한 인수 테스트를 이용하여 요구사항을 명확히 하고 모든 팀원이 요구사항에 대한 공통의 이해를 바탕으로 개발을 진행
  - 개발을 하기전 인수 테스트를 먼저 작성하여 전체적인 가이드 라인을 잡는다. 이후 그 인수 테스트를 충족시키기 위해 개발을 진행
  - BDD와 유사하지만, BDD는 개발자 관점에서 기능의 동작에 더 중점을 두는 반면 ATDD는 사용자 시나리오 관점에서 정확한 요구사항을 개발하는 데 중점
  - 장점
    - TDD의 장점을 가져감
    - 서비스 흐름 파악에 큰 도움
    - 작업의 시작과 끝이 명확함 -> 인수 테스트 통과하면 기능 개발 끝
    > 인수테스트 없이 했을 경우에는 배포해서 기능 동작을 확인해야하는 수동 테스트기 때문에 인수테스트보다 효율이 떨어짐
  - 단점 
    - 초기 설계 및 테스트 작성 시간이 오래 걸림
    - 자동화 테스트 도구(Cucumber, Selenium 등)의 복잡성
  - TDD와의 차이점
    - TDD : 코드 단위의 테스트 / ATDD : 전체 기능 테스트
    - TDD : 코드 품질 향상, 리팩토링 용이가 목적 / ATDD : 사용자 요구사항 충족 확인이 목적
    - TDD : JUnit, Mockito 등 사용 / ATDD : Cucumber, RestAssured 등 사용
- ATDD 개발 프로세스
```java
//Step 정의 (Cucumber + RestAssured 활용)
import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;

public class UserRegistrationSteps {

  private String requestBody;

  @Given("회원 가입을 위한 정보가 주어졌을 때")
  public void 회원_가입_정보_준비() {
      requestBody = """
          {
              "name": "홍길동",
              "email": "hong@example.com",
              "password": "1234"
          }
      """;
  }

  @When("회원 가입 API를 호출하면")
  public void 회원_가입_API_호출() {
      given()
          .contentType(MediaType.APPLICATION_JSON_VALUE)
          .body(requestBody)
      .when()
          .post("/users")
      .then()
          .statusCode(HttpStatus.CREATED.value()); // HTTP 201 Created 기대
  }

  @Then("회원 정보가 정상적으로 저장되어야 한다")
  public void 회원_정보_검증() {
      given()
      .when()
          .get("/users?email=hong@example.com")
      .then()
          .statusCode(HttpStatus.OK.value()) // HTTP 200 OK 기대
          .body("name", equalTo("홍길동"))
          .body("email", equalTo("hong@example.com"));
  }
}
```
```java
//회원 가입 API 구현
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {
    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @PostMapping
    public ResponseEntity<User> registerUser(@RequestBody User user) {
        User savedUser = userService.register(user);
        return ResponseEntity.status(201).body(savedUser);
    }

    @GetMapping
    public ResponseEntity<User> getUserByEmail(@RequestParam String email) {
        User user = userService.findByEmail(email);
        return ResponseEntity.ok(user);
    }
}
```

  
### 용어간 차이
- 테스트
  - 구현 -> 테스트
  - 구현한 후 테스트의 용도(하루를 끝내고 지내온 일에 대해 일기를 쓰는것)
- TDD
  - 테스트(요구사항) -> 구현
  - 구현 할 내용의 요구사항을 명세하기 위해서 사용(하루를 시작 할 때 작성하는 TODO List)
- BDD
  - 행위(요구사항) -> 구현
  - TDD의 T(Test를)를 B(Behavior)로 대체한 느낌.
  - TDD에서의 Test는 명세를 하기위해서 만들어졌는데 테스트라는 용어 자체가 검증의 의미로 많이 사용되다보니까 그 의미가 잘못 해석이 되는 경우가 많아서 행위라는 용어로 대체한게 BDD
- ATDD
  - 인수조건(요구사항) -> 인수테스트
  - 구현 요구사항을 명세하는 방법을 AT(인수테스트)라는 방법으로 정의





<br>
<br>
<br>
<br>
<br>
https://www.youtube.com/watch?v=bRhVW8304zg<br>
https://www.youtube.com/watch?v=ITVpmjM4mUE&t=1322s<br>
https://m.blog.naver.com/rkdudwl/221973507455<br>
