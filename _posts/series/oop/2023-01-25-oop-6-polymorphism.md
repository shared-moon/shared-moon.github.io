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

## 다형성(Polymorphism)

다형성이란, `다양한 형태를 가질 수 있는 성질`을 말합니다.

형태란, 무엇의 형태를 말하는 걸까요? 객체지향 언어에서는 크게 타입과 메서드의 형태로 구분합니다.

💡 타입(Type)은 Class와 같은 의미로 해석됩니다.
{: .notice--info }

## 타입의 다형성

객체지향 언어는 타입의 다양성을 보장합니다. 어떠한 변수의 타입이 정의 되었을 때, 이 변수에 대입될 수 있는 대상이
반드시 해당 타입은 아니어도 된다. **그 타입을 대체할 수 있으면 대입될 수 있다** 라는 규칙이 있는거죠.

### 업캐스팅

그럼, 타입은 어떻게 대체 할 수 있는걸까요?

사실 앞의 상속과 추상화에 대한 설명에서 이미 다루었던 내용입니다.

부모 클래스에 자식 클래스가 대입되거나, 인터페이스에 구현체가 대입되는 부분이 바로 업캐스팅이죠.

