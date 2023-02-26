---

title:  "객체지향 이야기 - 3장"
excerpt: "객체지향 언어의 4가지 특징 - 캡슐화"
categories:
- 객체지향 이야기

tags:
- Java
- Kotlin
- OOP
- 캡슐화
- Encapsulation

related_key: OOP

header:
  teaser: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_image: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_filter: 0.5

last_modified_at: 2023-02-05T23:22:55

---

## 캡슐화(Encapsulation)

캡슐화란, [접근제어자](/shorts/access-modifier/)를 이용하여 `내부에서만 쓰이는 정보 / 외부에도 노출이 되는 정보`를 구분지어 **정보의 은닉과 정보의 보호**를 실현하는 것을 말합니다. 

**정보의 은닉과 보호**가 무엇을 뜻하는지, 아래에서 예시를 들어 설명 해 보겠습니다.

💡 *객체지향 언어의 4가지 특징은 [이곳](/객체지향%20이야기/oop-2-feature/)에서 한 눈에 확인하실 수 있습니다.*
{: .notice--info }

## 캡슐화가 되어있지 않은 경우

`잔돈이 필요했던 영희는 철수에게 5천원을 주며, 아무 음료수나 사 먹고 거스름돈은 다시 가져와라` 라는 심부름을 시켰다고 해보겠습니다.
먼저, 음료수를 사 먹고 거스름돈을 가져오는 Class를 정의 해 보겠습니다.

<details class="foldable">
<summary>예제</summary>
<div markdown="1">

```kotlin
class Employee(
  var money: Int,
  var drink: Drink? = null,
  var taste: String? = null,
) {
  fun buyDrink(drink: Drink) {
    this.drink = drink
    this.money -= drink.price
  }

  fun doDrink() {
    this.taste = "맛있다"
  }
  
  fun errand() {
      // ...
  }
}
```
<div class="code-caption">수상하기 짝이 없는 errand()</div>

</div>
</details>

지금부터 우리가 영희라고 가정 해 볼게요!

우리는 **아무 음료수나 사 먹고 거스름돈을 가져 올** 누군가가 필요합니다.
그 책임을 저는 Employee 라는 클래스에게 부여를 했습니다. Employee는 돈을 가지고 있고, 음료수를 사거나 마시는 기능을 가지고 있습니다.

이런 Employee의 책임을 가진, 지나가던 철수에게 5천원을 주고 일을 시키려 하는데 문제가 생겼습니다. 철수는 한번에 하나의 일 밖에 할 수가 없는 친구였던거죠!

```kotlin
fun 영희_심부름() {
  val 철수 = Employee(5_000)
  철수.buyDrink(Drink("콜라", 1_300))
  철수.doDrink()
  
  println("음료수 이름 : ${철수.drink.name} 음료수 가격 : ${철수.drink.price} 맛 : ${철수.taste} 거스름돈 : ${철수.money}")
}
```
<div class="code-caption">TMI 대방출..!</div>

그래서 우리는 5천원을 쥐여주고, 철수를 졸졸 따라 다니면서 콜라를 골라주고, 마시라고 알려주고, 결국 거스름 돈까지 얼마나 남았는지 직접 세어 봤습니다!
설상가상으로 철수는 물어보지도 않은 음료수 정보까지 줄줄이 나열하고 있군요!

이럴거면 심부름을 시킬 이유가 있었을까요? 우리가 원한 건 이게 아닙니다. 우린 철수가 뭘 사먹었는지, 먹긴 했는지, 맛은 어땠는지 등등 전혀 궁금하지 않습니다.
그렇게 자상한 사람이었다면 애초에 이런 심부름을 시키지 않았을 겁니다.

## 정보의 은닉

우리가 원하는 건 뭘까요? 뭘 어떻게 했는지는 중요치 않고, 거스름돈만 받으면 됩니다.

그런데 위에서 저희가 사용하지 않았지만, 뭔가 수상하게 숨어있는 메서드가 하나 있죠. 바로 `errand()`입니다.
모두가 생각하시는 대로 이 `...` 안에는 음료수를 사고 마시는 메서드가 들어있을 예정입니다.

**'그럼 그걸 사용했으면 되잖아?'** 라고 생각 하실텐데요, 우리는 철수가 음료수를 사기도 하고 마시기도 할 수 있다는 걸 알고 있었습니다.
왜냐하면, 철수가 알려주고 있었으니까요. 그래서 그냥 심부름을 시키면 되나? 아니면 음료수 사고 마시는걸 따로 시켜야 하나? 라는 고민을 하다가
그냥 **심부름은 뭘 하는지 모르겠으니 따로 시켜야겠다** 라고 결정을 하게 된 거죠.

맨 앞에서 얘기 했던 것 처럼, 접근제어자를 이용해 우리는 내부에서 필요한 정보와 외부에서 필요한 정보를 구분 할 수 있습니다.
이렇게, 외부에는 외부에서 필요한 정보만 노출시킬 수 있도록 하는 것을 우리는 **정보의 은닉** 이라고 얘기합니다.

<details class="foldable">
<summary>예제</summary>
<div markdown="1">

```kotlin
class Employee(
  var money: Int,
  private var drink: Drink? = null,
  private var taste: String? = null,
) {
  fun errand() {
      buyDrink(Drink("콜라", 1_300))
      doDrink()
  }
  
  private fun buyDrink(drink: Drink) {
    this.drink = drink
    this.money -= drink.price
  }

  private fun doDrink() {
    this.taste = "맛있다"
  }
}
```
<div class="code-caption">외부에서는 무슨 음료를 사는지, 맛이 어땠는지 알 수가 없다</div>

</div>
</details>

우리는 이제 철수가 무엇을 사먹는지, 맛이 어땠는지는 알 수가 없습니다! 거스름돈만 잘 가져오면 그만이지요!

```kotlin
fun 영희_심부름() {
  val 철수 = Employee(5_000)
  철수.errand()
  
  println("거스름돈 : ${철수.money}")
}
```
<div class="code-caption">철수에게 눈치가 생겼다</div>

이제 우리는 필요한 정보만 볼 수 있어서 다른건 고민 할 필요가 없습니다. 그냥 쓸 수 있는 기능을 쓰면 되는거지요.

## 정보의 보호

이렇게 해피엔딩인 줄 알았는데.. 아직 하나가 더 남았습니다. 철수같이 심부름을 하는 Employee들만 보면 돈을 뺏어가는 Robber 효민이가 있습니다.

<details class="foldable">
<summary>예제</summary>
<div markdown="1">

```kotlin
class Robber() {
    fun robbery(employee: Employee) {
        employee.money -= 5_000
    }
}
```
<div class="code-caption">5천원 넘게는 안뺐는 강도</div>

</div>
</details>

영희에게 5천원을 받고 심부름을 가는 도중 효민이를 만난 철수는 무력하게 돈을 뺏기고 음료수를 살 수 없게 되었습니다.

```kotlin
fun 영희_심부름() {
  val 효민 = Robber()
  val 철수 = Employee(5_000)
  
  효민.robbery(철수)
  철수.errand()
  
  println("거스름돈 : ${철수.money}")
}
```
<div class="code-caption">음수가 나온다..</div>

철수는 결국 울면서 영희에게 돌아왔다고 합니다..

철수는 왜 효민이에게 돈을 뺏길 수 밖에 없었을까요? 그건 바로 철수의 돈을 가져가도 아무도 뭐라고 할 사람이 없기 때문입니다!

철수 곁에 보디가드라도 붙어있어 돈에 접근하는 것을 막았다면 뺏기지 않았겠지요. 이처럼 중요한 정보를 외부에서 함부로 접근하지 못하도록 하는 것을
**정보의 보호** 라고 합니다. 이 역시 접근제어자를 이용 해 해결 할 수 있지요.

<details class="foldable">
<summary>예제</summary>
<div markdown="1">

```kotlin
class Employee(
  private var money: Int,
  private var drink: Drink? = null,
  private var taste: String? = null,
) {
  fun errand() {
      buyDrink(Drink("콜라", 1_300))
      doDrink()
  }
  
  fun remainMoney() = money
  
  private fun buyDrink(drink: Drink) {
    this.drink = drink
    this.money -= drink.price
  }

  private fun doDrink() {
    this.taste = "맛있다"
  }
}
```
<div class="code-caption">드디어 안전해졌다</div>

</div>
</details>

이제 철수는 돈을 뺏기지 않아도 됩니다. 효민이는 철수의 돈에 접근 할 권리가 없거든요. 우리의 언어로 표현하자면, 효민이가 철수의 돈에 접근하는 걸
법적으로 금지 시킨 것과 같습니다. 실제로 private한 필드에 외부에서 접근하려 하면 컴파일 에러가 나지요.

## 마무리

필요한 정보만 보여주어 해당 클래스의 기능을 효율적으로 사용하게 하고, 중요한 필드에의 접근을 막아 아예 위험한 일이 발생 할 방법을 없애는 것으로
보안성을 향상시키는 것이죠.

간단한 예제라 와닿지 않았을 수도 있었겠지만, **내부에서만 사용되는 정보와 외부에서 참조되어도 되는 정보를 잘 구분해서 제공하는 것**. 이것이 캡슐화의 핵심입니다.

💡 remainMoney() 때문에 '필드에 접근 가능한 것 아닌가?' 라는 의문이 드실 수 있습니다. 정보의 보호란 결국 setter를 제한하는 것으로
read 기능과는 결이 다릅니다.
{: .notice--warning }
