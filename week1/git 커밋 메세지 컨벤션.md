<img src="image/woowacourseLogo.webp" alt="woowacourseLogo" style="width: 32%; display: block; margin: 0 auto;">

# 🪐 git 커밋 메세지 컨벤션

> "해당 커밋에서 수행된 작업을 이해할 수 있도록 커밋 메시지를 작성한다. 또한 팀의 좋은 코드 리뷰 문화는 작은 커밋을 작성하는 것에서 비롯된다."
> - [좋은 git 커밋 메시지를 작성하기 위한 7가지 약속](https://meetup.nhncloud.com/posts/106)
>
> _※ 1주차 피드백에서 발췌_

커밋 메시지를 제각각 작성하면 내용 파악에만 불필요한 시간이 소모됩니다. 커밋 컨벤션을 통해 팀 내부는 물론 오픈소스 커뮤니티에서도 일관된 형식으로 소통할 수 있습니다.

이를 통해 얻을 수 있는 이점은 다음과 같습니다:

- 더 좋은 커밋 **로그** 가독성
- 더 나은 **협업**과 **리뷰** 프로세스
- 더 쉬운 코드 **유지보수**

## 0. 커밋 메세지 형식

```shell
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

---

## 1. 커밋 종류 - `<Type>`

커밋의 종류를 나타냅니다.

| Type         | 설명                            |
|--------------|-------------------------------|
| **feat**     | 새로운 기능 추가                     |
| **fix**      | 버그 수정                         |
| **docs**     | 문서화 작업                        |
| **style**    | 코드 포맷팅, 세미콜론 누락 등 (동작에 영향 없음) |
| **refactor** | 코드 리팩토링                       |
| **test**     | 누락된 테스트 추가                    |
| **chore**    | 코드 기능과 무관한 잡일                 |

### - Chore 상황 예시

- `.gitignore` 업데이트
- 폴더 구조 정리
- Gradle 의존성 버전 업데이트

**예시:** `feat`

---

## 2. 변경 범위 - `<Scope>`

변경 사항의 범위를 나타냅니다 (도메인/엔티티별).

**예시:** `input`, `profile`, `data`, `user`, `order` 등

---

## 3. 커밋 제목 - `<Subject>`

변경 사항을 간단하게 나타내는 커밋의 제목입니다.

- **명령조**로
- **소문자**로 시작
- **마침표 없음**
- 제목 첫글자를 **대문자**로
- 영문 기준 **50자** 이내로

**예시:** `입력 값 검증`

---

## 4. 구분 공백 - `<BLANK LINE>`

본문을 구분하기 위한 공백으로, 컨벤션에 따라 반드시 지켜야 합니다.

## 5. 메세지 본문 - `<Body>` (선택사항)

변경 사항에 대한 상세 설명을 작성합니다.

**예시:** `- 자동차 이름 입력 값 검증 `

---

## 6. 이슈 연동 - `<Footer>` (선택사항)

> **!주의:** "일부 프로젝트에서는 작업을 이슈 또는 풀 리퀘스트와 연결하기 위해 커밋 메시지에 이슈 또는 풀 리퀘스트 번호를 포함하기도 한다. 그러나 이 접근 방식은 원본 저장소의 관련 없는 이슈 또는 풀
> 리퀘스트에 영향을 미칠 수 있다. 따라서 이 과정에서는 커밋 메시지에 이슈 또는 풀 리퀘스트 번호를 포함하지 않는다."

이슈 트래커와 연동할 때 사용합니다.

### 키워드

| 키워드                 | 용도           |
|---------------------|--------------|
| `Closes #123`       | 이슈 닫기        |
| `Fixes #123`        | 버그 수정 시      |
| `Resolves #123`     | 문제 해결 시      |
| `Closes #123, #456` | 여러 이슈 한번에 처리 |

### 동작 방식

- `{키워드 #이슈번호}` 작성 시 자동으로 해당 이슈와 연결
- PR이 merge되면 이슈가 자동으로 닫힘

**예시:** `Closes #1`

---

## 예시

### Commit Message 1

```
feat(auth): 소셜 로그인 기능 추가

로그인 화면에 소셜 로그인 옵션 추가:
- Google 로그인 Firebase Auth 연동
- Kakao 로그인 SDK 연동
- 자동 로그인 기능 추가

Closes #123
```

### Commit Message 2

```
fix(profile): 프로필 이미지 로딩 실패 오류 수정

Glide를 사용한 이미지 로딩 시 네트워크 오류 처리 추가
placeholder와 error 이미지 설정으로 사용자 경험 개선

Closes #456
```

### Commit Message 3

```
docs(readme): 프로젝트 설치 가이드 업데이트

빌드 환경 정보 추가:
- 필수 Gradle 플러그인 목록
- local.properties 설정 방법
```

### Commit Message 4

```
style(home): 홈 화면 코드 포맷팅 수정
```

### Commit Message 5

```
refactor(payment): 결제 서비스 전략 패턴 적용

결제 방식별 처리 로직을 전략 패턴으로 리팩토링:
- PaymentStrategy 인터페이스 추가
- CreditCardPayment, KakaoPayment 구현체 분리
- 코드 가독성 및 유지보수성 향상
```

### Commit Message 6

```
test(product): 상품 서비스 단위 테스트 추가
```

### Commit Message 7

```
chore(gradle): Kotlin 1.9.0 및 의존성 버전 업데이트

주요 업데이트:
- Kotlin 1.8.22 -> 1.9.0
- Coroutines 1.7.0 -> 1.7.3
```

## References

- [좋은 git 커밋 메시지를 작성하기 위한 7가지 약속](http://meetup.nhncloud.com/posts/106)
- [AngularJS Git Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)

## 🪐 그 외 문서

- [우아한테크코스 프리코스 아카이브](https://github.com/rungeun/woowacourse-precourse-archive)