---

title:  "객체지향 이야기 - 5장"
excerpt: "객체지향 언어의 4가지 특징 - 추상화"
categories:
- 객체지향 이야기

tags:
- Java
- Kotlin
- OOP
- 추상화
- Abstration

related_key: OOP

header:
  teaser: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_image: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_filter: 0.5

last_modified_at: 2023-02-05T23:22:55

---

💡본문의 모든 예제는 [이곳](https://github.com/shared-moon/github-blog-example/tree/main/src/main/kotlin/com/example/moonyoo/oop/abstration)에서 확인하실 수 있습니다.
{: .notice--info }

## 추상화(Abstration)

추상화란, **말그대로 추상적으로 바꾸는 일**을 말합니다. 추상적이라는 건 무슨 뜻일까요? 우리는 현실세계에서 종종 추상적이다 라는 말을 씁니다.

마음, 사랑, 우정과 같이 관측할 수 없는, **구체적으로 정의할 수 없는 막연한 어떤 것**을 우리는 추상적이다 라고 표현을 하죠.
다시 말해, 추상적이라는 것은 **구체적이지 않은 것**이라고 해석할 수 있습니다.

객체지향 언어에서의 추상적이라는 표현도 의미는 크게 다르지 않습니다. 다만 그 대상이 관념이나 형상 같은 것이 아니라 **객체의 특성**이라는 데서 차이가 있습니다.

## 객체의 특성

앞선 내용을 정리하면 추상화란, **구체적인 어떤 것을 구체적이지 않게 표현하는 일**입니다.
객체지향에서 추상화가 필요한 이유를 생각해서 다시 정리 해 보면 **구체적이고 일반적인 어떤 것을 구체적이지 않은 하나의 특성으로 표현하는 일**을 말합니다.

그럼, 특성이란 무엇을 말하는 걸까요? 사전적 정의로는 `특수한 성질`, 좀 더 프로그램적으로 표현 하면 `특정 클래스가 가지는 성질`을 말합니다.

간단하게 예를 들어 보겠습니다.

`새와 비행기`의 공통점 하면 무엇이 떠오르시나요? 바로 `날 수 있다`는 것입니다.
각각 어떤 방식으로 날 수가 있나요?

새는 `날개짓을 해서` 날 것이고, 비행기는 `연료를 태워` 날게 될 겁니다.
이렇게 `어떻게`가 명시되어 있는 것을 구체적이라고 표현하고 추상화를 한다는 건 이 어떻게를 배제하는 겁니다.

`난다`라는 특성을 추출하면 아래와 같은 모양이 나옵니다.

```kotlin
interface Flyable {
  fun fly()
}

class Bird : Flyable {
  override fun fly() {
    // 날개짓을 한다
  }
}

class AirPlane : Flyable {
  override fun fly() {
    // 연료를 태운다
  }
}
```

Bird와 AirPlane은 날수 있는 특성을 가지게 되었습니다. 이제 사람들은 이 특성만 보고도 어떻게 하는지는 모르겠지만
아무튼 얘네는 `날 수 있다`는 것을 알 수 있습니다.

이 특성을 정의 할 때 잊지 말아야 할 것은, **추상화의 방향은 아래에서 위로 향한다**는 점입니다.

추상화는 **구체적이고 일반적인** 것을 대상으로 한다고 했습니다. 이 일반적이다 라는 말은
**같은 목적으로 만들어진 기능이 두 개 이상 있다** 라는 뜻이죠.

즉, 추상화를 미리 하고 그것에 맞춰 기능을 구현하는 게 아니라, `추상화를 할 만한 기능들이 존재 할 때` 고려하는 게 맞습니다.

💡 물론, 개발자의 경험과 역량에 따라 설계 당시에 추상화가 필요한 부분을 고려 할 수도 있습니다.
{: .notice--warning }

이제 클래스가 가지는 특성을 정의하는 과정을 한번 살펴 보겠습니다.

## 추상화의 과정

예시로 신용카드를 살펴보겠습니다. 신용카드는 어떤 기능이 있나요?

기본적으로 값을 `지불` 할 수 있죠. 그런데 이 지불한 금액은 실제로 갖고 다니지는 않습니다. 계좌에 있는 돈을 카드사가`청구`해서 가져가죠
이렇게 크게 `지불과 청구` 두 가지 기능이 있다고 하고 생각 해 보겠습니다.

```kotlin
class CreditCard {
    fun pay() {
        println("신용카드로 비용을 지불했습니다.")
    }

    fun billing() {
        println("매월 26일 카드값이 청구됩니다.")
    }
}
```
<div class="code-caption">[1-1] 신용카드는 결제일이 정해져 있다</div>

이 카드를 사용하려면, 카드를 인식해 비용을 결제하고 결제 된 금액을 청구 할 수 있는 포스기가 필요 할 것 같네요

```kotlin
class Pos {
    fun sell(creditCard: CreditCard) {
        creditCard.pay()
        creditCard.billing()
    }
}
```
<div class="code-caption">[1-2] 신용카드만 받을 수 있는 포스기</div>

이렇게 우리는 신용카드를 통해 제품을 구매할 수 있는 기능을 만들 수 있었습니다. 여기까지는 아무런 문제가 없는데요,
프로그램의 세계에서 사건은 항상 기능이 커지면서 일어납니다.

### 요구사항의 변경

이 포스기를 사용하던 점주에게서 요구사항이 들어 왔습니다. `체크카드도 결제가 되게 해 주세요`

그래서 우리는 아래와 같이 체크카드를 정의했습니다.

```kotlin
class CheckCard {
    fun pay() {
        println("체크카드로 비용을 지불했습니다.")
    }

    fun billing() {
        println("계좌로 카드값이 청구됩니다.")
    }
}
```
<div class="code-caption">[2-1] 체크카드는 돈이 바로 빠져나간다</div>

그리고 포스기가 체크카드도 이용 할 수 있도록 만들었습니다.

```kotlin
class Pos {
    fun sell(creditCard: CreditCard) {
        creditCard.pay()
        creditCard.billing()
    }

    fun sell(checkCard: CheckCard) {
        checkCard.pay()
        checkCard.billing()
    }
}
```
<div class="code-caption">[2-2] Ctrl + C + V</div>

우리는 메서드의 다형성을 이용해서 신용카드와 체크카드를 둘 다 사용할 수 있는 포스기를 만들어냈습니다!
이제 요구사항도 만족 시켰으니 개발은 끝난걸까요?

평생 이대로 사용하기만 한다면 좋겠지만, 고객의 요구사항은 늘 변화합니다.
지금은 두개밖에 없지만 각 카드사별로 무수히 많은 카드들을 사용 가능하게 바꾼다면 어떻게 될까요?

`Pos` 클래스는 카드의 종류 별로 `sell(..)`메서드를 추가해야 할겁니다.

이런 구조가 바로 개방폐쇄 원칙에서 말하는 **확장에 열려있지 않은** 구조입니다. 새로운 기능이 추가가 될 때마다 Pos 클래스가 변경이 되어야 하니까요.

### 일반적인 특성 정의

결국 우리가 바라는 건 이런겁니다. **새로운 카드가 추가 되더라도 Pos 클래스는 변경이 없었으면 좋겠다**

어떻게 바꿀 수 있을지 두 개의 sell 메서드를 한 번 살펴 보겠습니다.

자세히 보니, 두개의 sell 메서드는 관심사가 같습니다. 비용을 `지불` 하고 대금을 `청구` 하는 절차를 가지고 있죠.

그렇다면, Pos의 입장에서는 넘겨받는 파라미터를 **어떻게 하는지는 내 알바 아니고, 지불이랑 청구를 할 수 있는 거 아무거나** 라고 정의할 수 있지 않을까요?

이것을 조금 문장을 다듬어보면 **구체적이지 않은 지불과 청구를 할 수 있는 특성** 이라고 표현 할 수 있고, 이 과정을 `추상화` 라고 얘기합니다.

### 인터페이스

이제 추상화를 했으니, 이 추상적인 개념을 어떻게 정의 할 수 있는지 알아보겠습니다.

위에서 추상화를 얘기하면서 **어떻게 하는지는 알 바 아니**라는 표현을 썼는데요, 이처럼 어떻게(How)가 배제되면서 정확한 동작을 명시하지 않는
바디가 비어있는 메서드를 `추상 메서드(Abstract Method)` 라고 부릅니다.

우리는 `지불`과 `청구`를 추상메서드로 정의해야 하는데요, 이 추상 메서드를 정의할 수 있는 방법은 `추상 클래스(Abstract Class)`와 `인터페이스(Interface)`
가 있습니다.

둘 다 추상 메서드 선언이 가능하지만, 사용하기 위해선 추상 클래스는 **상속**을 받아야 하고, 인터페이스는 **구현**을 해야 합니다.
둘은 용도가 완전히 다르기 때문에 이번 설명에서는 인터페이스를 대상으로 하겠습니다.

💡 상속이란 **기능의 확장**을 위한 것이기 때문에 추상 클래스는 기능의 확장을 좀 더 유연하게 하기 위해 추상 메서드를 지원하는 것이지
근본적으로 추상화를 위해 만들어진 개념이 아닙니다.
{: .notice--info }

인터페이스는 만드는 방식이 클래스와 유사합니다. `지불`과 `청구`가 정의 된 Card라는 인터페이스를 만들어 보겠습니다.

```kotlin
interface Card {
    fun pay()
    fun billing()
}
```
<div class="code-caption">[3-1]메서드에 내용이 없다</div>

드디어 말로만 설명하던 추상화가 모습을 드러냈습니다. 이제 앞서 설명한 내용들이 무슨 말인지 확 와 닿으셨을거라고 생각합니다.

Card라는 특성은 지불과 청구를 할 수 있지만 그 구체적인 내용은 잘 모르는 상태입니다. 그럼 이 특성을 부여받은 클래스는 어떤 모습이 될까요?

```kotlin
class CreditCard: Card {
    override fun pay() {
        println("신용카드로 비용을 지불했습니다.")
    }

    override fun billing() {
        println("매월 26일 카드값이 청구됩니다.")
    }
}

class CheckCard: Card {
    override fun pay() {
        println("체크카드로 비용을 지불했습니다.")
    }

    override fun billing() {
        println("계좌로 카드값이 청구됩니다.")
    }
}
```
<div class="code-caption">[3-2] 구체적인 내용이 정의 되어 있다</div>

이제 CreditCard와 CheckCard는 Card라는 특성을 가지고 있습니다.

Card는 `지불`과 `청구`를 할 수 있었죠. 즉, CreditCard와 CheckCard는 `지불`과 `청구`를 할 수 있다고 보증이 된 클래스가 된 거죠.

💡 추상 메서드는 내용이 없는 껍데기이기 때문에 이를 상속받거나 구현하게 되면 반드시 오버라이딩을 해 주도록 언어 레벨에서 강제하고 있습니다.
{: .notice--info }

그럼 `Pos` 클래스에서는 어떤 변화가 생겼는지 살펴 보겠습니다.

```kotlin
class Pos {
    fun sell(card: Card) {
        card.pay()
        card.billing()
    }
}
```
<div class="code-caption">[3-3] 파라미터로 인터페이스를 받는다</div>

파라미터의 타입으로 각각의 구체적인 클래스가 아닌 인터페이스를 명시하고 있습니다.

이로써 Pos가 원했던 **어떻게 하는지는 잘 모르겠고, 지불과 결제를 할 수 있는 것**을 받아서 처리 할 수 있게 되었고,
`sell()` 메서드는 이제 Card라는 인터페이스가 구현이 되어있기만 하면 어떤 타입이라도 다 처리 할 수가 있죠.

이렇게 여러개의 비슷한 기능에서 특성을 뽑아내고, 그 특성에 맞게 인터페이스를 만들어 각각 구현 할 수 있도록 하는 것을 `추상화를 한다` 라고 합니다.

💡 추상화를 통해 구현체가 아닌 인터페이스에 의존는 구조를 만들도록 권장하는 원칙을 `개방폐쇄의 원칙` 이라고 합니다.
{: .notice--info }

## 추상화 주의사항

추상화에도 명백한 단점이 존재합니다. 바로 **가독성이 저하**된다는 것이죠.

앞에서 여러번 말씀드린 추상화의 **구체적이지 않다**는 특징 때문에, 인터페이스를 의존하는 기능은 어떤 구현체가 오느냐에 따라
동작이 달라집니다. 필연적으로 코드가 현재 컨텍스트를 이탈하므로 직관적이지가 않죠.

추상화를 멀리 해야 한다는 얘기는 아닙니다. 다만, 그만큼 신중하게 잘 써야 한다는 이야기입니다.

### 추상화의 대상

추상화는 특성을 정의하는 작업이라고 했습니다. 그렇기 때문에 무엇을 추상화 할 지를 결정하는 건 아주 중요한 일입니다.

만약, 위의 예제에서 Card가 아닌 Pos에 집중하여 `sell()` 을 추상화 했다면 어떻게 됐을까요?

최종적으로 Pos를 사용하는 입장에선 마찬가지로 변경이 적어질 수 있으나, 사용할 카드가 늘어 날 수록 Pos의 구현체가
늘어나는 주객전도의 현상을 보게 될 겁니다.

이번 예제는 워낙 간단한 내용이라 당연히 그런 판단을 할 리는 없겠지만, 실무에서는 워낙 복잡한 비즈니스가 얽혀 있기 때문에
추상화를 할 대상을 잘 못 선정하는 경우도 생깁니다.

문제는 이런 일이 발생했을 때 상황을 인식 하는 건 다음 요구사항이 들어왔을 때라는 거죠.
클래스 디자인은 방법이 정말 무궁무진해서 그 당시에는 정답처럼 보여 놓칠 수가 있습니다.

### 추상화의 레벨과 범위

추상화를 한다는 것은, 결과적으론 외부에 `이러한 기능들을 쓸 수 있도록 보장`하는 것을 말합니다. 그리고 하나의 인터페이스에 명시 된
기능들은 묶어서 사용 할 가능성이 높기 때문에 구현체의 플로우에 제약이 생길 확률이 높아집니다.

때문에 인터페이스에는 보다 고차원적인 특성에 집중하고 세부적인 내용은 구현체에 일임하는 것이 좋습니다.

위의 카드 예제를 다시 한 번 보겠습니다. 지금은 결제수단이 카드만 있어서 큰 문제가 없었습니다.

하지만, 현금을 받을 수 있게 해 달라는 요구사항이 추가된다면 어떻게 될까요?
현금은 카드와 달리 청구 과정이 필요치 않습니다. 지불하는 즉시 결제가 끝난 것이기 때문이죠.

현금은 원래의 메서드를 사용하기 위해 필요 없는 `billing()`을 구현해야 할까요? 아니면 현금을 위한 별도의 메서드를 만들어야 할까요?

상황에 따라 취할 수 있는 방법이 있는데요, 먼저 굳이 `billing()`을 강제 할 필요가 없을 경우 추상화의 레벨을 한 단계 올려 볼 수 있습니다.

`지불`과 `청구`를 각각 추상화 하는게 아니라 `결제`라는 하나의 특성으로 묶어보면, 아래와 같은 인터페이스가 만들어집니다.

```kotlin
interface Payment {
    fun pay()
}
```
<div class="code-caption">[4-1] 결제를 추상화했다</div>

그리고 이를 구현하는 구현체들은 이렇게 만들어지겠죠?

```kotlin
class CreditCard: Payment {
    override fun pay() {
        println("신용카드로 비용을 지불했습니다.")
        billing()
    }

    private fun billing() {
        println("매월 26일 카드값이 청구됩니다.")
    }
}

class CheckCard: Payment {
    override fun pay() {
        println("체크카드로 비용을 지불했습니다.")
        billing()
    }

    private fun billing() {
        println("계좌로 카드값이 청구됩니다.")
    }
}

class Cash: Payment {
    override fun pay() {
        println("현금으로 결제했습니다.")
    }

}
```
<div class="code-caption">[4-2] 구현체들의 권한이 강해졌다.</div>

각 구현체들은 `pay()`만 구현하게 되었습니다. 그리고 `지불과 청구`를 할지, `지불`만 할지는 각 구현체가 알아서 결정하게 되었죠.
이렇게 하면 카드를 받든, 현금을 받든 Pos는 변경 없이 사용 할 수가 있게 됩니다.

하지만 이렇게 추상화의 레벨을 올리면 한 가지 단점이 있는데요, 바로 플로우를 강제하지 못한다는겁니다. 위에서 한 번
저차원의 추상화가 플로우를 강제하기 때문에 단점이라고 언급을 했었는데, 그럼 이건 모순 아닌가요? 라고 생각하실 수 있습니다.

보통의 경우에는 그렇습니다만, 추상화 레벨이 적정 수준을 넘어가게 되면 오히려 안하느니만 못하는 경우가 생깁니다. 메서드의 
확장을 용이하게 한다고 파라미터 타입으로 `Object나 Any`를 받는것과 같은 문제죠.

만약, 요구사항이 `카드는 결제 시 지불과 청구를 진행해야 한다`라고 되어 있다면, 우리는 어떻게 추상화를 해 볼 수 있을까요?

카드와 현금은 `지불`이라는 공통된 특성이 있습니다. `청구`는 카드 종류에서만 다시 구현이 되면 되겠지요. 그러면 우리는 원래 정의했던
Card 라는 인터페이스를 이렇게 재정의 해 볼 수 있을 것 같습니다.

```kotlin
interface Payment {
    fun pay()
}

interface Billable {
    fun billing()
}

interface Card: Payment, Billable
```
<div class="code-caption">[5-1] 인터페이스를 잘게 쪼갰다</div>

`지불`과 `청구`는 별도의 인터페이스를 정의하고, 이 두 가지의 특성이 다 필요한 Card 인터페이스를 재정의 했습니다.
이제 우리는 지불 방식에 따라 다른 인터페이스를 구현할 수 있는 선택권을 얻었습니다.

```kotlin
class CreditCard: Card {
    override fun pay() {
        println("신용카드로 비용을 지불했습니다.")
    }

    override fun billing() {
        println("매월 26일 카드값이 청구됩니다.")
    }
}

class CheckCard: Card {
    override fun pay() {
        println("체크카드로 비용을 지불했습니다.")
    }

    override fun billing() {
        println("계좌로 카드값이 청구됩니다.")
    }
}

class Cash: Payment {
    override fun pay() {
        println("현금으로 결제했습니다.")
    }
}
```
<div class="code-caption">[5-2] 결제 유형에 따라 다른 인터페이스를 구현한다</div>

추상화의 레벨을 높이는 것과는 모양이 조금 다르지만, 두 방법의 목적은 결국 `인터페이스는 분리가 가능 한 가장 작은 단위로 쪼갠다`
라는 것입니다. 이에 대해서는 인터페이스 분리 원칙에서 자세히 다뤄보겠습니다.

## 마무리

추상화의 목적은 `유지보수의 용이성` 이며 그를 위해 재사용성 증대와 변경 최소화를 하기 위한 방안을 제시합니다. 다만, 코드의
직관성이 떨어질 수 있기 때문에 적절한 범위에 적당히 사용 할 수 있는 스킬을 익혀야 하고 이건 많이 해 보는 수 밖에 없습니다.

특히 추상화는 가독성에 영향을 미치는 터라 반드시 제3자의 의견을 많이 들어 볼 것을 추천합니다.

추상화를 진행 한 뒤의 코드는 머릿속에 그림이 그려졌을 때와 아닐 때 가독성이 확연히 차이가 나기 때문에
만든 사람이 보면 그럴듯 해 보이지만 다른 사람이 보면 제 3외국어 같은 느낌을 받을 수도 있습니다.