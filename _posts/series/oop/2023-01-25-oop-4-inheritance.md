---

title:  "객체지향 이야기 - 4장"
excerpt: "객체지향 언어의 4가지 특징 - 상속"
categories:
- 객체지향 이야기

tags:
- Java
- Kotlin
- OOP
- 상속
- Inheritance

related_key: OOP

header:
  teaser: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_image: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_filter: 0.5

last_modified_at: 2023-02-05T23:22:55

---

💡본문의 모든 예제는 [이곳](https://github.com/shared-moon/blog-example/tree/main/src/main/kotlin/com/example/moonyoo/oop/inheritance)에서 확인하실 수 있습니다.
{: .notice--info }

## 상속(Inheritance)

상속이란, 다른 클래스의 필드 및 메서드를 그대로 이어받아 사용하는 것을 말합니다. `private` 한 멤버를 제외 한 나머지는
모두 접근을 할 수 있고, 그 외에 자신의 기능을 따로 가질 수 있어 일반적으로 상속을 **기능을 확장한다**라고 표현을 합니다.

상속이라는 말과 어울리게, 상속을 받는 클래스는 **자식 클래스** 상속의 대상이 되는 클래스는 **부모 클래스**라고 표현합니다.

그럼, 이 상속이라는 건 어떻게 받을 수 있을까요?

💡 *객체지향 언어의 4가지 특징은 [이곳](/객체지향%20이야기/oop-2-feature/)에서 한 눈에 확인하실 수 있습니다.*
{: .notice--info }

## 상속을 받는 방법

간단합니다. 객체지향 언어는 객체지향의 특징을 언어 차원에서 지원을 해 준다고 했습니다. 언어마다 상속을 받는 방법이 있으니 그대로 이용 하시면 됩니다. 

아래와 같이 부모 클래스를 만들어 보겠습니다.

```kotlin
open class Phone(
  private val phoneNumber: String,
) {
  fun call() {
    println("call $phoneNumber")
  }
}
```
<div class="code-caption">[1-1] 전화밖에 안되는 유물</div>

이제 이 Phone을 상속받는 자식 클래스, SmartPhone을 만들어 보겠습니다.

```kotlin
class SmartPhone(
  phoneNumber: String,
  private val gameTitle: String,
) : Phone(phoneNumber = phoneNumber) {
  fun game() {
    println("play $gameTitle")
  }
}
```
<div class="code-caption">[1-2] 전화기인가 게임기인가</div>

위의 `: Phone(..)` 부분이 바로 상속을 받는 부분입니다. 아까 상속은 기능의 확장 이라고 말씀 드렸습니다. SmartPhone은
부모 클래스인 Phone의 `call()`을 그대로 사용 할 수 있죠. 하지만 phoneNumber에는 직접 접근할 수 없습니다. 바로 private으로 선언 되었기 때문이죠.
아무리 자식이라도 허락해 줄 수 없는 것이 있는 법입니다.

아무튼 두 클래스는 아래와 같이 사용 할 수 있습니다.

<details class="foldable">
<summary>예제</summary>
<div markdown="1">

```kotlin
fun main() {
    val phone = Phone("010-1234-5678")

    phone.call()
//    phone.game()

    val smartPhone = SmartPhone("010-1234-5678", "game")

    smartPhone.call()
    smartPhone.game()
}
```
<div class="code-caption">[1-3] phone은 게임을 할 수 없다..</div>
</div>
</details>

## this와 super

여기서 잠깐 하나 짚고 넘어갈 것이 있는데요, 위의 SmartPhone의 `: Phone(..)` 부분을 보시면 SmartPhone이 마치 Phone을
생성하고 있는 것 처럼 보입니다. **'상속 받은건 알겠는데.. 부모는 왜 굳이 따로 만들어 줘야 하지? 이미 받아온 거 아닌가?'**
하는 생각이 들지 않나요? 왜 그럴까요 ?

상속을 받은 클래스는 자신의 멤버와 부모 클래스의 멤버 모두에 접근할 수 있는데요, 객체지향 언어는 [다형성](/객체지향%20이야기/oop-6-polymorphism/)이라는 특징을 갖고 있기 때문에 
자신의 멤버와 부모의 멤버를 구분을 할 수 있어야 하기 때문이죠.

구분하는 방법은 간단합니다. 자식 클래스에서 자신의 멤버를 사용할 때는 `this` 부모의 멤버를 사용할 때는 `super` 예약어를 사용하면 됩니다.

두 클래스를 변경 해 보겠습니다.

```kotlin
    open class Phone(
        protected val phoneNumber: String,
    ) {
        open fun call() {
            println("super call $phoneNumber")
        }
    }

    class SmartPhone(
        phoneNumber: String,
        private val gameTitle: String,
    ) : Phone(phoneNumber = phoneNumber) {
        override fun call() {
            println("child call $phoneNumber")
        }
        
        fun allCall() {
            this.call()
            super.call()
        }
      // ...
    }
```
<div class="code-caption">[2-1]</div>

SmartPhone은 자신만의 `call()` 메서드를 가지게 되었습니다! 그리고 자신과 부모의 메서드를 각각 호출하는 `allCall()` 메서드도 새로 생겼네요.

이제 SmartPhone의 `allCall()`을 호출하면, SmartPhone의 `call()`과 Phone의 `call()`이 차례로 수행되는 걸 확인하실 수 있습니다.

💡 자식은 부모의 `private`에는 접근 못하지 않나요? 라는 질문을 하실 수 있는데, 내부 메서드는 본인 외에는 존재 여부조차 알 수가 없어
`기능`으로 보지 않습니다.
{: .notice--primary }

## 자식 클래스와 부모 클래스의 관계

우리는 SmartPhone이 Phone이 가진 모든 기능을 사용할 수 있다는 것을 확인했습니다. 그 말은 SmartPhone은
Phone을 완벽히 대체 할 수 있다는 얘기죠. 즉, **자식 클래스는 부모 클래스의 충분 조건** 이라고 할 수 있습니다.

<div markdown="1" style="max-width: 400px; margin-left: auto; margin-right: auto" >

![이미지](https://drive.google.com/uc?id=1gsfnyIOVfDV0n4yoA9xo2jVRKsqJaoQ2)
*완벽한 상하관계에 있다*
</div>

이렇게 되면, 우리는 SmartPhone을 Phone 처럼 쓸 수 있지 않을까요? Phone의 모든 기능을 사용할 수 있다고 보장을 받았으니까요!
예제를 통해 한번 확인 해 보겠습니다.

<details class="foldable">
<summary>예제</summary>
<div markdown="1">

```kotlin
    fun main() {
      val smartPhone = SmartPhone("010-1111-2222", "game")
      val phone: Phone = smartPhone
      phone.call()
      // phone.game()
    }
```
<div class="code-caption">[3-1]</div>
</div>
</details>


분명 SmartPhone을 만들었는데, Phone이라는 타입으로 감싸도 여전히 `call()` 메서드를 사용 할 수 있습니다. 이는 상속의 개념이
부모의 기능을 전부 가지고 있음을 보장하기 때문에 가능하며, 이렇게 부모 타입으로 캐스팅 하는 것을 `업캐스팅(Upcasting)` 이라고 합니다.

💡 업캐스팅은 다형성의 한 종류입니다. 다형성에 대한 자세한 설명은 [이곳](/객체지향%20이야기/oop-6-polymorphism/)에서 확인하실 수 있습니다.
{: .notice--info }

## 상속의 장단점

상속에 대해 살펴 보니, 상속은 부모 클래스의 기능을 그대로 사용할 수 있게 해 주어, 코드의 중복을 줄여주고 손쉽게 기능을 확장할 수 있게 함으로
편의성을 증대해 주는 아주 좋은 녀석인 것 같습니다.

그럼, 상속은 단점이 없을까요?

아이러니 하게도, 상속은 **부모 클래스의 멤버를 그대로 사용** 한다는 장점이 그대로 최대 단점이 됩니다.

### 부모 클래스의 캡슐화 깨짐

자식 클래스는 private한 멤버를 제외 한 부모 클래스의 기능을 그대로 사용 할 수 있다고 했습니다. 그러면 상속을 이용한다는 건, 결국 
부모 클래스의 멤버를 private하지 않게 바꾸겠다는 의미입니다. 캡슐화가 깨지면, 정보의 은닉과 보호를 하기 어려워 집니다.

💡캡슐화에 대한 자세한 설명은 [이곳](/객체지향%20이야기/oop-3-encapsulation)에서 확인하실 수 있습니다.
{: .notice--info }

### 강한 결합도

자식 클래스는 부모 클래스의 기능을 그대로 사용 할 수 있다는 말은 다시 말하면, **자식 클래스는 부모 클래스에 의존적이다** 라고 해석 할 수 있습니다.
심지어 상속은 부모 클래스의 변경이 그대로 반영이 되기 때문에 굉장히 강하게 결합되어 있을 수 밖에 없습니다.

때문에 부모 클래스의 변경이 자식 클래스 전체에, 나아가 **자식 클래스를 사용하는 모든 코드**에 영향이 미칠 것이고, 이는 유지보수를 어렵게 만드는 원인이 됩니다.

```kotlin
open class Phone(
  protected val phoneNumber: String,
) {
  open fun call() {
    println("super send sms $phoneNumber")
  }
}

class SmartPhone(
  phoneNumber: String,
  private val gameTitle: String,
) : Phone(phoneNumber = phoneNumber) {
  // ...
}

class User {
  fun call(phone: SmartPhone) {
    phone.call()
  }
}
```
<div class="code-caption">[4-1] SmartPhone의 call은 부모의 기능을 그대로 쓰고 있다</div>

이런 상황에서, SmartPhone은 아무것도 변경되지 않지만, Phone의 `call()`이 시그니처가 변경 된다면 어떻게 될까요 ?

```kotlin
open class Phone(
  protected val phoneNumber: String,
) {
  open fun call(otherPhoneNumber: String) {
    println("super send sms $otherPhoneNumber")
  }
}

class User {
  fun call(phone: SmartPhone) {
//    phone.call() 컴파일 에러
  }
}
```
<div class="code-caption">[4-2] 아무것도 안했는데 갑자기 컴파일 에러가 난다..</div>

이렇게, 부모가 아닌 하위 클래스를 직접 쓰고 있던 부분 전체에 영향을 미치게 됩니다. 지금이야 한군데였지만, 하위 클래스가 다수가 되고
해당 메서드를 사용하는곳이 수십 수백개가 있다면, 부모 클래스를 변경하고 싶어도 변경 할 수가 없겠죠.

**'근데, 메서드 시그니처가 바뀌면 원래 다 바꿔야 하는 거 아닌가요?'** 라는 의문이 생길 수 있을 것 같네요.

맞습니다. 메서드 시그니처가 바뀌면 해당 메서드를 사용하는 곳은 당연히 변경을 해야 하는데요.
여기서는, **내가 사용하지 않는 클래스의 변경**이 나한테까지 영향을 준다는 게 핵심입니다.

예시는 메서드 시그니처를 변경해서 보여드렸지만, 사실 이런 경우는 컴파일이 실패하기 때문에 고생을 많이 할 수는 있어도 그리 큰 일은 아닌데요.

문제는 내부 구현이 바뀌는 경우가 더 큽니다.

외부에서 어떻게 쓰이고 있는지를 모두 파악해야 하고, 컴파일 시점에 잡아낼 수가 없기 때문에 더 큰 장애로 이어질 수 있기 때문이죠.

💡 이런 단점 때문에 단순 재사용만을 위해 상속을 사용하는 건 지양하고 있으며, 재사용을 위해서는 [상속보단 조합](/shorts/inheritance-vs-composition/)을 이용하는 걸 권장합니다. 
{: .notice--info }

### 리스코프 치환 법칙 위배 가능성

자식 클래스는 부모 클래스를 완벽히 대체한다고 했습니다. 구조적으론 그렇지만 과연 실제 기능도 무조건 그럴까요? 

자식 클래스가 부모 클래스의 기능을 마냥 그대로 사용하면 그럴 수도 있겠지만, 애석하게도 자식 클래스는 자기 주장이 강합니다.
스스로의 기능을 가질 수도 있고, 메서드 오버라이딩을 통해 기능을 재정의 할 수도 있습니다.

이번엔 예제를 이렇게 바꿔 보겠습니다.

```kotlin
    open class Phone(
        protected val phoneNumber: String,
        private var prevPhoneNumber: String = "",
    ) {
        open fun call(otherPhoneNumber: String) {
            println("super send sms $otherPhoneNumber")
            prevPhoneNumber = otherPhoneNumber
        }

        open fun quickCall() {
            call(prevPhoneNumber)
        }
    }

    class User {
        fun call(phone: Phone) {
            phone.call("010-1111-2222")
            phone.quickCall()
        }
    }
```
<div class="code-caption">[5-1] 고마운 기능이 생겼다</div>

Phone 클래스에 `빠른 전화걸기` 기능이 생겼습니다! 이 기능을 사용하면 가장 최근에 걸었던 번호로 다시 걸 수가 있죠.
하지만, Phone을 상속받는 SmartPhone이 아래와 같이 구현된다면 어떻게 될까요?

```kotlin
    class SmartPhone(
        phoneNumber: String,
        private val fallbackPhoneNumber: String
    ) : Phone(phoneNumber = phoneNumber) {
        override fun quickCall() {
            call(fallbackPhoneNumber)
        }
    }
```
<div class="code-caption">[5-2] 정해진 번호로만 전화를 건다</div>

User는 가만히 있는데, 매개변수로 어떤 클래스가 넘어오느냐에 따라 결과가 달라집니다. 이를 리스코프 치환 법칙을 어겼다고 얘기합니다.

<details class="foldable">
<summary>접기</summary>
<div markdown="1">

```kotlin
    fun main() {
        val phone = Phone("010-1234-5678", "game")
        val smartPhone = SmartPhone("010-1234-5678", "010-0000-0000")
        val user = User()

        user.call(phone)
        user.call(smartPhone)
    }
```
<div class="code-caption">[5-3] call(..)에 넘겨지는 객체에 따라 결과가 다르다</div>
</div>
</details>

💡 사실 리스코프 치환 법칙 위배 가능성은 상속보다는 다형성에 의한 문제로 보는 것이 맞습니다. 하지만 상속을 하기 적합한 상황인지를 판단하는 잣대가 될 수 있어
상속에서 함께 다뤄 봤습니다.
{: .notice--info }

## 마무리

정리하면 **상속**이란, 근본적으로 **기능의 확장**을 의미하며 부모 클래스의 기능을 확장한 **자식 클래스는 부모 클래스를 완벽히 대체** 할 수 있기 때문에
부모 클래스의 타입으로 캐스팅 하여 사용 할 수 있습니다. 다만, 상속의 구조적 특성으로 인해 부모 클래스와 자식은 반드시 강하게 결합 될 수 밖에 없으며
상속을 사용 할 때는 정말로 상속이 필요한 상황인지 꼼꼼히 따져보는 것이 좋습니다.