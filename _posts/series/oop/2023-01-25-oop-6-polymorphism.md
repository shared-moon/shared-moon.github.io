---

title:  "객체지향 이야기 - 6장"
excerpt: "객체지향 언어의 4가지 특징 - 다형성"
categories:
- 객체지향 이야기

tags:
- Java
- Kotlin
- OOP
- 다형성
- Polymorphism

related_key: OOP

header:
  teaser: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_image: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_filter: 0.5

last_modified_at: 2023-02-05T23:22:55

---

💡본문의 모든 예제는 [이곳](https://github.com/shared-moon/github-blog-example/tree/main/src/main/kotlin/com/example/moonyoo/oop/polymorphism)에서 확인하실 수 있습니다.
{: .notice--info }

## 다형성(Polymorphism)

다형성이란, `다양한 형태를 가질 수 있는 성질`을 말합니다.

형태란, 무엇의 형태를 말하는 걸까요? 객체지향 언어에서는 크게 타입과 메서드의 형태로 구분합니다.

동일한 타입 혹은 동일한 구조의 메서드를 수행해도 다른 동작을 할 수 있도록 지원 해 주는 것이 바로 다형성이죠.

즉, 형태라는 건 `타입이나 메서드의 세부 구현`을 의미한다고 볼 수 있습니다.

💡 타입(Type)은 Class와 같은 의미로 해석됩니다.
{: .notice--info }

## 타입의 다형성

객체지향 언어는 타입의 다양성을 보장합니다. 어떠한 변수의 타입이 정의 되었을 때, 이 변수에 대입될 수 있는 대상이
반드시 해당 타입은 아니어도 된다. **그 타입을 대체할 수 있는 다른 타입이 대입될 수 있다** 라는 규칙이 있는거죠.

### 업캐스팅

그럼, 타입은 어떻게 대체 할 수 있을까요?

사실 앞의 상속과 추상화에 대한 설명에서 이미 다루었던 내용입니다.

부모 클래스에 자식 클래스가 대입되거나, 인터페이스에 구현체가 대입되는 행위를 `하위 개념이 상위 개념으로 변환된다`하여
업캐스팅(Up-Casting)이라고 부릅니다.

업캐스팅이 되면, 하위 클래스는 상위 클래스의 껍데기를 쓰게 되기 때문에 상위 클래스에 정의 된 메서드만 사용 가능합니다.

다시 말해 변수의 타입이 상위 클래스로 선언 되었으면 그 변수에는 여러 형태의 하위 클래스가 대입 될 수 있고, 해당 변수의 기능은
어떤 클래스가 대입 되었느냐에 따라 다양한 형태로 동작할 수 있기 때문에 업캐스팅은 타입의 다형성을 지원하는 방법이라고 볼 수 있습니다.

아래에서, 업캐스팅의 예제를 살펴 보겠습니다.

```kotlin
open class A {
  fun print() {
    println("I'm A!!")
  }
}

class B : A()
```
<div class="code-caption">[1-1] B는 A의 하위타입이다</div>

이렇게 A,B 가 선언되어 있으면, B는 A타입의 변수에 대입이 될 수 있습니다.

```kotlin
fun main() {
    val a: A = B()
    a.print()
}
```
<div class="code-caption">[1-2] A타입 변수에 하위 객체가 대입됐다</div>

변수 a는 A타입으로 선언 되었지만 B타입의 객체가 대입이 되었습니다. 물론 B에는 A를 상속받은 것 외에 따로 정의된 게 없으니
A와 같은 동작을 하게 됩니다.

위에서 언급한 타입이 달라지면 다른 동작을 한다라는 설명에 비해 예시가 조금 빈양 해 보일 수 있는데요, 다른 동작을 하기 위해서는
타입 뿐만이 아니라 메서드의 다향성을 위한 `메서드 오버라이딩`이 필요하기 때문에 조금 뒤에서 다뤄보겠습니다.

### 다운캐스팅(X)

다운캐스팅은 업캐스팅의 반대되는 개념으로, `상위 개념을 하위 개념으로 변환`하는 것을 뜻합니다.

사실, 다운캐스팅은 엄밀히 말하면 다형성의 종류로 보기는 어렵습니다. 하지만 타입의 다형성을 얘기 할 때 종종 같이 설명되기에 언급을 해 보겠습니다.

다운캐스팅은 왜 다형성의 종류로 보기가 어렵다는걸까요? `부모 클래스가 자식 클래스로도 될 수 있다는 거니까 다양한 형태를 가지는 거 아닌가?`
라는 의문을 가질 수 있습니다.

하지만 다형성에서 말하는 다양향 형태는 기본적으로 `동일한 생김새`를 가지는 것을 전제로 하고 있습니다.

위에 설명 된 업캐스팅이나 아래에 나올 메서드 오버라이딩, 오버로딩이 모두 그런 조건을 만족하고 있죠.

하지만 다운캐스팅은 다릅니다. 다운캐스팅은 대전제로 `캐스팅하려는 부모 클래스가 해당 자식 클래스로 만들 수 있어야한다`가 깔려있습니다.
다시 말하면, `캐스팅이 안 될 수도 있다`라는 뜻이죠.

이게 무슨 문제가 있는지 아래 예제를 통해 한 번 살펴 보겠습니다.

```kotlin
interface A {
    fun print()
}

class B : A {
    override fun print() {
        println("I'm B!!")
    }
}

class C : A {
    override fun print() {
        printC()
    }

    fun printC() {
        println("I'm C!!")
    }
}
```
<div class="code-caption">[2-1] C는 자신만의 메서드가 있다</div>

이렇게 A, B, C가 정의되었을 때 A타입의 변수를 받았지만 C의 `printC()`를 별도로 호출하고 싶은 경우가 있을 수 있습니다.

```kotlin
fun print(a: A) {
    val c: C = a as C
    c.printC()
}
```
<div class="code-caption">[2-2] C만 가지고 있는 기능을 쓰려면 강제로 변환해야 한다</div>

여기서 주목해야 할 것은 `a as C` 부분입니다. 상위 타입으로는 하위 타입에만 명시된 기능을 사용하지 못합니다.
그래서 하위 타입의 기능을 쓰기 위해서는 `강제로` 형변환을 해줘야 하죠.

그러다 보니, 다운캐스팅은 실패하는 경우가 생깁니다. `파라미터 a`에 넘겨진 객체가 C타입 이라면 문제가 없습니다.
하지만 위에 같이 선언 된 A를 구현한 B라면, 파라미터로는 넘어갈 수 있지만 c로 변환이 될 수가 없죠.

이럴 때 `ClassCastException`이 발생합니다. 이 ClassCastException은 RuntimeException의 하위 클래스죠.
즉, 컴파일 시점에 문제가 있는지 발견 할 수 없다는 뜻입니다.

```kotlin
fun main() {
    print(C())
    print(B())
}
```
<div class="code-caption">[2-3] 실행을 해 봐야 문제를 확인할 수 있다</div>

이런 문제를 방지하려면 어떻게 해야 할까요? 형변환을 하기 전에 변환이 가능한지 확인을 해야 합니다. 

자바에서는 `instanceOf` 코틀린에서는 `is`로 확인을 하게 되죠.

```kotlin
fun print(a: A) {
    if (a is C) {
        a.printC()
        return
    }
    a.print()
}
```
<div class="code-caption">[3-1] C 타입일때만 printC()가 호출된다</div>

이렇게 되면 C 타입의 기능을 큰 문제 없이 활용 할 수 있습니다.

💡 a를 C로 명시적 형변환을 하지 않아도 printC()를 호출 할 수 있는 것은 코틀린이 스마트 캐스팅을 지원해주기 때문입니다.
간단히 얘기하면 `a is C`로 검증이 된 이후 a는 자동으로 C타입으로 캐스팅이 되었다고 볼 수 있습니다.
{: .notice--info }

위의 업캐스팅의 경우와 비교해보면 차이를 느끼실텐데요, C타입의 특정한 기능을 사용하기 위해 `분기문`을 이용했습니다.
이는 `동일한 절차`로 수행될 수 없는 기능이라는 얘기이고, C타입으로 캐스팅을 하는 순간 개념의 범위가 축소됩니다.

이런 이유로, 다운캐스팅은 마치 업캐스팅과 짝인 것 같은 이름을 가지고 있지만, 다형성과는 거리가 먼 개념입니다.

💡 다운캐스팅도 경우에 따라 유용하게 쓰이는 기능입니다. 다형성이 아니니 나쁘다 라는 얘기가 아니라 다형성이라는 카테고리로
묶기에는 어려움이 있다 라는 얘기를 하고 싶었습니다.
{: .notice--warning }

## 메서드의 다형성

객체지향 언어는 메서드 레벨의 다형성도 보장합니다. 타입의 다형성과 크게 다른 개념도 아니고, 사실 이 메서드의 다형성을
지원하기 때문에 타입의 다형성이 의미를 가질 수 있기에 분리해서 다룰 개념은 아니라고 생각하긴 합니다.

메서드의 다형성은 크게 `오버라이딩(Overriding)`과 `오버로딩(Overloading)`이 있습니다.

### 오버라이딩

메서드 오버라이딩은 상위 타입에 정의 된 메서드를 하위 타입에서 `재정의` 하는 것을 말합니다.

메서드 오버라이딩은 선언 시 다음과 같은 규칙을 가지고 있습니다.

- 메서드 시그니처는 상위 타입과 같아야 한다 (단, 반환 타입은 상위 타입에서 정의 된 반환 타입의 하위을 허용함)
- 상위 타입의 접근 지정자보다 좁은 범위의 접근 지정자를 선언할 수 없다
- 상위 타입의 메서드보다 큰 범위의 예외를 선언 할 수 없다

정도인데 그냥 쉽게 `상위 타입과 메서드 시그니처는 같아야 한다`고 이해하셔도 무방합니다.

몇가지 예외를 허용하긴 하지만 굳이 상위 타입과 다르게 설정 할 이유가 없고 만약 실수를 하더라도 이 부분은 컴파일 시점에
감지가 되기 때문에 크게 문제를 일으킬 수 있는 여지가 없기 때문입니다.

💡 오버라이딩에 대해선 상속, 추상화에 이어 업캐스팅에서도 계속 언급을 했기에 예제는 굳이 다루지 않겠습니다.
{: .notice--primary }

### 오버로딩

메서드 오버로딩은 같은 이름을 가진 메서드를 `중복 선언` 하는 것을 말합니다.

메서드 오버로딩은 다음과 같은 규칙을 가지고 있습니다.

- 메서드의 이름은 같아야 한다
- 메서드의 매개변수가 달라야 한다
- 메서드의 리턴타입이 같아야 한다

💡 메서드 오버로딩은 사실 리턴타입은 상관이 없습니다. 하지만 매개변수와 리턴타입이 다르면 그건 다른 메서드로 취급되기 때문에
오버로딩이라고 할 수 없어 규칙에 포함시켰습니다.
{: .notice--warning }

메서드 오버로딩을 쓰면 어떤 이점이 있을까요?

바로 `같은 이름을 사용할 수 있다`는 것입니다. `같은 이름이 왜..?` 라고 생각하실 수도 있으니 
같은 이름이 허용되지 않았을 경우의 예를 들어 보겠습니다.

```kotlin
class User(
    private val name: String,
    private val age: Int,
)

fun createUser(name: String, age: Int) = User(name, age)
fun createUserWithoutName(age: Int) = User("", age)
fun createUserWithoutAge(name: String) = User(name, 0)
```
<div class="code-caption">[4-1] 결국 다 같은 동작을 한다</div>

세 개의 메서드는 같은 일을 하고 있습니다. `User`를 생성해 주는 일이죠.
같은 이름을 허용해주지 않는다면 동일한 작업을 하는데도 이렇게 적절한 이름을 따로 지어줘야 합니다.

아무리 작명이 개발자의 숙명이라고 해도 이건 너무 가혹하지 않나요?

개발자의 고통 말고, 가독성 측면에서도 이점이 있습니다. 바로 예제로 살펴 보겠습니다.

```kotlin
fun createUser(name: String, age: Int) = User(name, age)
fun createUser(age: Int) = createUser("", age)
fun createUser(name: String) = createUser(name, 0)
```
<div class="code-caption">[5-1] 평행세계의 createUser</div>

메서드의 이름에는 힘이 있습니다. 이름이 같아진 것으로, 이 녀석은 외부에서 보기에 `아, 같은 일을 하는 메서드구나`
라는 것을 암시적으로 알려줄 수 있습니다.

위의 예제에서도 가능하긴 했지만, 이름이 같기 때문에 내부에서 다른 파라미터를 가지는 또다른 '자신'을 호출하는 것도
위화감이 없습니다.

## 마무리

다형성은 `다양한 형태를 가질 수 있는 성질` 이라고 축약하기에는 그 종류가 참 많습니다.

이 모든 기능들이 결국은 `유지보수를 용이하게 하기 위한` 배려입니다. 각각 무엇인지 외우기 보다는 유지보수에 유리한
높은 품질의 코드를 작성하도록 늘 신경쓰다 보면 자연스레 체득하게 될 겁니다.

지금까지 `객체지향 언어의 특징`에 대해 알아 보았는데요, 다음 장 부터는 어떻게 해야 이 특징들을 잘 활용 할수 있는지에
대해 알아보도록 하겠습니다.