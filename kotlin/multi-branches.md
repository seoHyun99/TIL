# if-else & when

## 1. if-else

Java와 Kotlin의 if-else문을 사용하는데 있어서 큰 차이는 없다.  
자바와 달리 코틀린은 if-else 문은 값을 직접 반환할 수 있고 삼항 연산자를 대체할 수 있다.

#### 자바, 코틀린 if-else문 비교

```java
//java
int version = 0
String versionText;

if (version == 0) {
  versionText = "0";
} else if (version == 1) {
  versionText= "1";
} else {
  versionText = "알 수 없음";
}
```

```kotiln
// 직접 반환
val version: Int = 0
val versionText: String = if (version == 0) {
  "0"
} else if (version == 1) {
  "1"
} else {
  "알 수 없음"
}
```

#### 자바, 코틀린 삼항 연산자 (:) 비교

```java
int age = 17;
boolean isStudent = age < 20 ? true : false;

```

```kotlin
val age: Int = 17;
val isStudent: Boolean = if (age < 20) true else false
```
