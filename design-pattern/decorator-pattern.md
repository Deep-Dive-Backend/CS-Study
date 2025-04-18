# 데코레이터 패턴(Decorator-pattern)

- 겍체에 추가 **요소를 동적으로 더할 수** 있습니다.
- 서브클래스를 만들 때보다 **훨씬 더 유연하게 기능을 확장**할 수 있습니다.


## 데코레이터의 작동 원리

![소금빵 예시](/design-pattern/img/decorator-pattern_bread.png)

- 소금빵
    - 그냥 먹어도 된다.
    - 소금빵이다.
- 이 외의 다른 소금빵들
    - 소금빵이라는 것은 변하지 않는다.
    - 데코에 따라 맛이 추가된 것이다.

중요한 것은 전부 소금빵이라는 것!

## 코드로 이해하기

![구조](/design-pattern/img/decorator-pattern_structure.png)

객체

- `Component`: 각 구성 요소를 의미합니다.
- `ConcreteComponent`: 실제 `Component`를 구현합니다.
- `Decorator`: `Component`를 꾸밀 데코레이터를 정의합니다.
- `ConcreteDecoratorA`, `ConcreteDecoratorB`: 실제 데코레이터를 구현합니다.

특징

- `Component`: interface나 abstract class로 정의합니다.
- `Decorator`: 인스턴스 변수로 `Component`를 포함하고 있습니다.

[관련 코드](https://github.com/sujeong-0/design-pattern/tree/2049242bc06a290445a0e478a2d4910dc5dd8f0b)

### 예시에 데코레이터 패턴 적용해보기

[예시 코드](https://github.com/sujeong-0/design-pattern/tree/770a6f67610de5a2a697422c0a861597cf1287c1)


### 예시: java io


### 참조

- [도서 - 헤드 퍼스트 디자인패턴(개정판)](https://www.hanbit.co.kr/store/books/look.php?p_code=B6113501223)