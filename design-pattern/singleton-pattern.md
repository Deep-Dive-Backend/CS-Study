# 싱글톤 패턴 (Singleton Pattern)

실제 인스턴스가 1개만 존재하도록 하는 패턴을 의미합니다.

## 구현 코드

```java
public class Singleton {
 
 	private static Singleton instance;
 
 	private Singleton() {}
 
 	public static Singleton getInstance() {
 		if (instance == null) {
 			instance = new Singleton();
 		}
 		return instance;
 	}
 
 	// 이외의 메서드
 }
```

## 문제점

멀티스레딩 환경에서는 문제가 될 수 있습니다.
인스턴스를 생성하는 부분이 문제가 되어 실제 인스턴스가 여러 개가 될 수 있습니다.

## 해결하기 위한 방법

### 방법 1: synchronized

```java
public class Singleton {
 
 	private static Singleton instance;
 
 	private Singleton() {}
 
 	public static synchronized Singleton getInstance() {
 		if (instance == null) {
 			instance = new Singleton();
 		}
 		return instance;
 	}
 
 	// 이외의 메서드
 }
```

- 속도가 느릴 수 있습니다.

### 방법 2: 인스턴스를 클래스 로드 시점에 생성

```java
public class Singleton {

 	private static Singleton instance = new Singleton();
 
 	private Singleton() {}
 
 	public static Singleton getInstance() {
 		return instance;
 	}
 
 	// 이외의 메서드
}
```

- 실제 코드에서 사용되지 않더라도 인스턴스를 생성해야합니다.

### 방법 3: Double-Checked Locking, volatile

```java
public class Singleton {

 	private volatile static Singleton instance;
 
 	private Singleton() {}
 
 	public static Singleton getInstance() {
 	
        if (instance == null) { // 첫 번째 검사 (락 없음)
            synchronized (Singleton.class) {
                if (instance == null) { // 두 번째 검사 (락 있음)
                    instance = new Singleton();
                }
            }
        }
 	
 		return instance;
 	}
 
 	// 이외의 메서드
}
```

- `volatile`을 이용해  이용해 인스턴스 생성 시 명령어 재정렬(Instruction Reordering)을 방지하고, 여러 스레드 간의 **가시성 문제**도 해결할수 있습니다.

> volatile
> - 가시성 문제를 해결합니다.
> - 재정렬을 방지합니다.

### 방법 4: Holder 패턴

```java
public class Singleton {
    private Singleton() {}

    private static class Holder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return Holder.INSTANCE;
    }
}
```

- JVM 클래스 로딩 특성을 이용해서 lazy 한 방식입니다.

### 참조

- [도서 - 헤드 퍼스트 디자인패턴(개정판)](https://www.hanbit.co.kr/store/books/look.php?p_code=B6113501223)
- [volatile 변수](https://learn.microsoft.com/ko-kr/dotnet/csharp/language-reference/keywords/volatile)
