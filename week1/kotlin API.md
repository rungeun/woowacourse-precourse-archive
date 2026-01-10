<img src="../image/woowacourseLogo.webp" alt="woowacourseLogo" style="width: 32%">

# 🪐 kotlin API

>  Kotlin에서 제공하는 API를 적극 활용한다
>
> 함수(메서드)를 직접 구현하기 전에 **API에서 해당 함수를 제공하는지 확인**한다.
> 예를 들어 사용자를 출력할 때 사용자가 둘 이상인 경우
> 쉼표(,) 기반 문자열을 출력하도록 다음과 같이 구현할 수 있다.
>
> ```kotlin
> val members = listOf("pobi", "jason")
> val result = members.joinToString(",") // "pobi,jason"
> ```
> _※ 프리코수 1주차 피드백에서 발췌_

---

## 1. listOf
