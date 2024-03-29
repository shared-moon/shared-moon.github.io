---

title:  "객체지향 이야기 - 2장"
excerpt: "객체지향 언어의 4가지 특징"
categories:
- 객체지향 이야기

tags:
- Java
- Kotlin
- OOP
- 캡슐화
- 상속
- 추상화
- 다형성

related_key: OOP

header:
  teaser: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_image: https://drive.google.com/uc?id=1G_jevpqrq8QXZTyW3fuzw2-wTxa7YWGx
  overlay_filter: 0.5

last_modified_at: 2023-02-04T00:28:46

---

## 객체지향 언어

객체지향 언어에는 **캡슐화, 상속, 추상화, 다형성** 이라는 네 가지 특징이 있습니다. 이를 언어 레벨에서 지원을 해 주는 프로그래밍 언어를
우리는 객체지향 언어라고 부릅니다.

## 객체지향 언어의 장점

객체지향 프로그래밍은 근본적으로 **유지보수를 용이하게 하기 위해** 탄생했습니다. 이를 위해 개발자들은 코드의 **재사용성을 높여 반복을 최소화** 하고,
**보다 사람이 이해하기 쉬운 구조**를 만들어 내고자 했으며 이것이 곧 객체지향 언어의 장점이 되었습니다.

💡 *객체지향 프로그래밍에 대한 자세한 내용은 [이전 포스팅](/develop/oop-1-intro)에서 다루고 있습니다.*
{: .notice--info }

아래에서, 재사용성을 높이고 인간 친화적인 구조를 만들기 위해 만들어진 객체지향 언어의 네 가지 특징을 각각 살펴보겠습니다.

## 캡슐화 (Encapsulation)

Class는 필드와 메서드를 가지고 있습니다.

필드와 메서드는 그 쓰임새에 따라 Class 자신만 알고 있어야 되는 정보, 바깥에서도 알아야 되는 정보로 나뉘는데요.
이를 구분하기 위해 [접근제어자](/shorts/access-modifier/)를 제공합니다.

[접근제어자](/shorts/access-modifier/)를 활용하여 내부에서 쓰이는 정보와 외부에서도 참조가 가능한 정보를 나누면
[정보의 은닉](/객체지향%20이야기/oop-3-encapsulation/#정보의-은닉)과
[정보의 보호](/객체지향%20이야기/oop-3-encapsulation/#정보의-보호)라는 이점을 얻을 수 있습니다.

요약하자면, 캡슐화란 [접근제어자](/shorts/access-modifier/)를 활용하여 외부에 공개되는 정보를 제어하는 것으로
[정보의 은닉](/객체지향%20이야기/oop-3-encapsulation/#정보의-은닉)과
[정보의 보호](/객체지향%20이야기/oop-3-encapsulation/#정보의-보호)를 실현하는 것이라고 할 수 있습니다.

[캡슐화 더 자세히 알아보기](/객체지향%20이야기/oop-3-encapsulation/)
{: .notice }

## 상속 (Inheritance)

클래스는 다른 클래스의 필드와 메서드를 이어 받아 **기능을 확장**시킬 수 있습니다. 이를 상속이라고 합니다.

상속 대상이 되는 클래스는 **부모 클래스**, 상속을 받은 클래스는 **자식 클래스**라고 부릅니다. 자식 클래스는 부모 클래스의
`private`한 필드나 메서드를 제외하면 전부 접근이 가능합니다.

자식 클래스는 부모 클래스의 필드나 메서드를 그대로 사용 가능하기에 **재사용성**을 크게 향상시킬 수 있는데요.
강력한 기능이지만 그만큼 [사용에 주의](/객체지향%20이야기/oop-4-inheritance/#상속의-장단점)를 요합니다.

상속은 기본적으로 부모 클래스의 정보를 그대로 사용하기 때문에 클래스가 굉장히 강하게 결합됩니다. 때문에 변경에서 자유롭지 못하며, 
상속을 잘못 사용 할 경우 어마어마한 사이드이펙트가 발생할 수 있습니다.

또한, 자식 클래스에게 접근 권한을 열어주기 때문에 **캡슐화**가 깨지게 됩니다. 

💡 *상속은 정말 확실한 상황이 아니면 사용을 지양하는 것이 좋으며, 요즘은 [상속보다는 조합](/shorts/inheritance-vs-composition/)을 사용하도록 권장하고 있습니다.*
{: .notice--warning }

[상속 더 자세히 알아보기](/객체지향%20이야기/oop-4-inheritance/)
{: .notice }

## 추상화 (Abstration)

**추상적**이다 라는 것은 **구체적이지 않다**라는 뜻입니다. 따라서 추상화란 구체적인 것을 구체적이지 않게 만드는 일을 말합니다.

추상화를 하는 방법은 추상 클래스(Abstract Class)나 인터페이스(Interface)를 이용하는 방법이 있습니다.
둘 다 추상 메서드를 정의할 수 있으며, 스스로는 객체를 만들 수 없다는 특징이 있습니다.

💡 익명 클래스(Anonymous Class)로는 생성이 가능합니다.
{: .notice--info }

추상 클래스는 추상 메서드라는 개념을 제공하지만 근본적으로는 클래스이기 때문에 그 용도가 **기능의 확장**에 있고
인터페이스는 모든 메서드가 추상 메서드이기 때문에 **구현을 강제**하는것을 목적으로 합니다.

일반적으로 추상화를 한다고 하면 인터페이스를 사용하는 것을 말합니다.

추상화를 이용하면 클래스 간 결합도를 낮추고 확장성이 높은 코드를 만들 수 있지만, 코드의 직관성이 떨어지는 단점이 있기 때문에
[주의해서 사용](/객체지향%20이야기/oop-5-abstration/#추상화-주의사항)해야 합니다.

[추상화 더 자세히 알아보기](/객체지향%20이야기/oop-5-abstration/)
{: .notice }

## 다형성 (Polymorphism)

다형성이란, 타입이나 메서드가 **다양한 현태를 가질 수 있는 성질**을 뜻합니다.

타입의 다형성으로는 [업캐스팅](/객체지향%20이야기/oop-6-polymorphism/#업캐스팅),
메서드의 다형성으로는 [오버라이딩](/객체지향%20이야기/oop-6-polymorphism/#오버라이딩)과
[오버로딩](/객체지향%20이야기/oop-6-polymorphism/#오버로딩)이 있습니다.

객체지향 언어에서 타입의 다형성을 지원하기 때문에 상속이나 추상화를 이용 해 코드의 재사용성과 유지보수의 용이성을
높일 수 있는 것이기에 상속, 추상화와 깊은 관계를 맺고 있는 특징입니다.

[다형성 더 자세히 알아보기](/객체지향%20이야기/oop-6-polymorphism/)
{: .notice }

## 마무리

객체지향 언어의 특징들은 `객체지향적인 프로그래밍을 하도록 도와주는 방안`일 뿐입니다. 객체지향 언어를 사용한다고
객체지향적인 프로그래밍을 하는 것이라고 볼 수는 없습니다.

객체지향적인 프로그래밍을 하기 위해서는 [몇가지 원칙들](/객체지향%20이야기/oop-7-solid/)을 이해하고
상황에 맞게 이 특징들을 활용 할 수 있어야 합니다.