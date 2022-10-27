---

title:  "코틀린 깊게 알아보기"

excerpt: "설명"

categories:

- Develop

tags:

- Kotlin

last_modified_at: 2022-10-24T02:01:20

toc: true
toc_sticky: true
---

---
## 머릿말

이 글은 '**Kotlin in action**'을 베이스로, 코틀린을 코틀린답게 써 보고자 코틀린을 심층 분석하기 위해 작성합니다.  

자바와의 차이점을 중점으로 설명하려고 계획중이며, 책 내용 중 쓸데없는 내용와 더 깊게 알아 볼 필요가 있는 내용을  
지극히 주관적인 판단 하에 추려서 정리 해보려고 합니다.  


## Kotlin이란 무엇인가 ?

코틀린이란, 익히 알고 있는 IDEA인 Intellij의 개발사 Jetbrains에서 만든 자바 플랫폼에서 돌아가는 새로운 프로그래밍 언어입니다.

코틀린은 간결하고 실용적이며 안전하도록 디자인 되었고, 자바와의 호환성에 중점을 두고 만들어 졌습니다. 다시말해 태생부터가 자바의 상위호환 포지션을 
노리고 만들어진 언어라 자바와 비슷하면서 자바에서의 불편을 최대한 해결하려 노력 한 모습이 많이 보입니다.

아래에서 코틀린의 특성인 실용성, 간결성, 안전성, 호환성 각각이 어떤 의미인지 조금 더 자세히 살펴보겠습니다.

### 실용성

코틀린은, 실력있는 개발자들에 의해 다년간의 IT업계 노하우를 바탕으로 설계 되었으며, 수많은 개발자들의 요구사항을 충족시킬 수 있도록 
주의 깊게 언어 특성을 선택했습니다. 언어의 탄생 이념 자체가 **자바의 생태계를 활용 할 수 있는 자바의 단점을 극복한 언어** 이기 떄문에 새로운 것을 
연구하기보단 이미 검증 된 해법과 기능들을 잘 어우러지게 하는 것에 집중했죠.

그 결과, 코틀린은 어떠한 스타일이나 패러다임을 강제하기보다 개발자의 취향에 맞게 스타일을 택할 수 있도록 열어두고 비즈니스 로직 작성 시 
불편할 수 있는 것들을 언어 혹은 기본 라이브러리 차원에서 지원해 주기 때문에 상당히 개발자 친화적인 언어라고 볼 수 있습니다.

<details>
<summary>간단 예제</summary>
<div markdown="1">

- in java
```java
public class Dummy {
    public static void main(String[] agrs) {
      List<String> numbers = List.of("1", "2", "3");
      List<Long> parseNumbers = numbers.stream()
        .map(Long::parseLong)
        .collect(Collectors.toList());
      System.out.println("번호목록 : " + parseNumbers.toString());        
    }
}
```

- in kotlin
```kotlin
fun main(args: Array<String>) { 
  val numbers = listOf("1", "2", "3")
  val parseNumbers = numbers.map { it.toLong() }
  println("번호목록 : $parseNumbers")
}
```
*별거 아닌 내용 인데도 힘의 차이가 느껴진다..* 

</div>
</details>

### 간결성

코드를 유지보수 하는 데에 가장 리소스가 많이 드는 부분이 어디일까요? 바로 기존 코드 파악입니다. 기존의 동작을 파악 해야 
어디를 고쳐도 되는지, 고친다면 이렇게 해도 되는지 안 되는지를 판단할 수가 있기 떄문입니다. 때문에 팀 단위로 협업을 하는 프로젝트에서 
**코드의 가독성**은 코드 품질을 결정하는 매우 중요한 요소로 작용하게 되는데요, 개발자의 의도와 상관 없이 언어의 한계 때문에 작성 되어야만 하는 
수많은 보일러플레이트 코드들은 가독성을 저해하는 주요 원인입니다.  

자바를 기준으로 보면, 클래스 하나를 생성하고 사용하는데 필요한 생성자, 게터, 세터 메서드들이 대표적인 예인데요. 코틀린은 이런 
불합리를 언어적 차원에서 완벽하게 배제하고, 주로 쓰이는 기능들 (위 예제에서도 언급 된 컬렉션을 다루는 일 같은) 을 사용하기 위한 
부수적인 준비 과정을 최대한 단축시켜 가독성의 비약적인 향상을 이뤄 냈습니다.

<details>
<summary>간단 예제</summary>
<div markdown="1">

- in java
```java
class Dummy {
    private String name;
    private int age;
    
    public Dummy() {}
    
    public Dummy(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public String getName() {
        return name;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public int getAge() {
        return age;
    }
}
```

- in kotlin
```kotlin
class Dummy(
  val name: String,
  val age: Int,
)
```

*자바도 Lombok을 쓰면 되지 않느냐 라는 의견이 나올 수 있는데, 공평하게 외부의 도움 없는 상황을 가정했습니다. ~~심지어 Lombok 써도 밀림~~* 
</div>
</details>

### 안전성

### 호환성(상호운용성)

## Kotlin 기초

## 함수 정의와 호출

## 클래스, 객체, 인터페이스

## 람다로 프로그래밍

## 코틀린 타입 시스템

## 연산자 오버로딩과 기타 관례

## 고차 함수 : 파라미터와 반환 값으로 람다 사용

## 제네릭스

## 어노테이션과 리플렉션

## 코루틴과 Async/Await