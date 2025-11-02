<img src="image/woowacourseLogo.webp" alt="woowacourseLogo" style="width: 32%; display: block; margin: 0 auto;">

# 🪐 기본적인 Git 명령어

## 피드백 내용

> "git은 개발자 간의 협업을 위한 가장 기본적인 프로그램으로,
> 컴퓨터 파일의 변경 사항을 추적하고 여러 사용자 간의 해당 파일에 대한 작업을 조정한다.
> 지금은 add, commit, push 등의 간단한 명령어만 배워도 충분하지만,
> Git에 대해 미리 알아두어도 나쁠 것은 없다."

--- 

## 주요 Git 명령어 정리

실제 사용 시 작성된 순서를 따르므로, 순서대로 명령어를 사용하면 된다.

---

### 1. 브랜치 생성

```git
git checkout -b {branch-new} {branch-original}
```

`checkout`에 `-b`키워드를 사용하면 새 브랜치 생성과 브랜치 변경을 동시에 할 수 있다.

- **{branch-new} :** 새 브랜치명
- **{branch-original} :** 브랜치가 나올 브랜치
    - 생략 가능하다

```bash
git push origin  {branch-new}
```

원격 저장소에 새로운 브랜치 생성을 업데이트한다.

- **origin :** 로컬 저장소와 연결된 기본 원격 저장소를 이용
- **{branch-new} :** 원격 저장소에 업데이틀할 브랜치명

---

### 2. 커밋

```bash
git status
```

변경, 추가, 삭제된 목록을 보고 잘 못 수정된 파일이 없는지 확인해 준다.

```bash
git add .
```

수정된 파일을 스테이징한다.

```bash
git commit
```

스테이지에 올라와 있는 파일을 커밋한다.

```bash
git push origin {branch}
```

원격 저장소에 새로운 브랜치 생성을 업데이트한다.

- **{branch} :** 위에서 수정한 브랜치

---

### 3. 브랜치 병합

```bash
git checkout {brach}
```

병합할 대상 {branch}로 이동한다.::

- ex. `feature`를 `develop`으로 병합하고 싶을 경우, `{branch}`는 `develop`이 된다.

```bash
git merge --no-ff {branch}
```

브랜치를 병한다.

- **--no-ff :** Fast-Forward 방식으로 병합하지 않고, 병합 커밋이 만들어 진다.
- **{branch} :** 현재 브랜치로 {branch}를 병합

```bash
git push origin {branch}
```

원격 저장소에 새로운 브랜치 병합을 업데이트한다.

- **{branch} :** 병합한 브랜치명

---

### 브랜치 삭제

```bash
git branch -d {branch}
```

로컬 브랜치를 삭제한다.

```bash
git push origin --delete {branch}
```

원격 저장소의 브랜치를 삭제한다.

---

## 🪐 그 외 문서

- [우아한테크코스 프리코스 아카이브](https://github.com/rungeun/woowacourse-precourse-archive)