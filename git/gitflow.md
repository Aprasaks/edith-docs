---
title: "Git 협업 가이드"
description: "협업시에 꼭 알아야 할 깃 정리표"
category: "Git"
date: "2025-06-27"
readTime: "3min"
tags: ["React", "Git", "Frontend"]
status: "new"
author: "DemianDev"
slug: "git-flow"
---

# Git 협업 중 발생한 오류 사례 및 해결방안

## 📋 개요
- **프로젝트**: QNA 작성 페이지 개발
- **상황**: 팀원이 공통 컴포넌트를 develop에 머지한 후 발생한 충돌
- **문제**: rebase 후 push 시 오류 발생

---

## 🔥 발생한 오류

### 1. Push Rejected Error
```bash
error: 업데이트를 'github.com:OZ-Coding-School/oz_externship_fe_01_team2.git'에 푸시하는데 실패했습니다
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
```

**원인**: rebase로 인한 히스토리 변경

---

## 🚨 문제 상황 분석

### 상황 흐름
1. **어제**: `feature/12--qna-form-ui` 브랜치에서 작업 완료 후 push
2. **오늘**: 다른 팀원이 Modal 공통 컴포넌트를 develop에 머지
3. **rebase 실행**: 최신 develop 내용을 가져오기 위해 rebase
4. **새 기능 추가**: QNA 폼 검증 기능 구현 후 커밋
5. **push 시도**: 오류 발생! 🔥

### 왜 오류가 발생했나?
```
Before rebase:  A---B---C (feature/12--qna-form-ui)
                   /
              D---E---F---G (develop)

After rebase:   D---E---F---G---A'---B'---C'---H (feature/12--qna-form-ui)
```
- 커밋 해시가 변경됨 (A→A', B→B', C→C')
- 원격 브랜치는 여전히 A-B-C를 가리키고 있음
- Git이 "뒤처진 브랜치"로 인식

---

## 💡 해결 방법

### 올바른 해결책
```bash
git push --force-with-lease origin feature/12--qna-form-ui
```

### 다른 해결 방법들
```bash
# 1. 위험한 방법 (사용 금지)
git push --force origin feature/12--qna-form-ui

# 2. merge 사용 (히스토리 복잡해짐)
git pull origin feature/12--qna-form-ui
git push origin feature/12--qna-form-ui
```

---

## 🛡️ 예방 방법

### 1. 브랜치 전략 명확화
- **merge vs rebase 규칙** 정하기
- **force push 가이드라인** 수립

### 2. 커뮤니케이션
- 공통 컴포넌트 변경 시 팀에 공지
- rebase 전 팀원들과 상의

### 3. 안전한 명령어 사용
```bash
# 안전한 force push
git push --force-with-lease origin branch-name

# rebase 전 백업
git branch backup-branch-name
```

---

## 🎯 배운 점

### 1. Git 협업의 복잡성
- 단순해 보이는 작업도 팀 환경에서는 복잡해질 수 있음
- 여러 사람이 동시에 작업할 때의 충돌 상황

### 2. 명령어의 중요성
- `--force`와 `--force-with-lease`의 차이점
- rebase가 히스토리에 미치는 영향

### 3. 문제 해결 능력
- 오류 메시지 읽고 분석하는 능력
- 다양한 해결책 중 최적의 방법 선택

---

## 🔮 앞으로의 개선 방안

### 1. 팀 규칙 정립
- Git workflow 문서화
- 코드 리뷰 프로세스 강화

### 2. 도구 활용
- Git GUI 도구 활용
- VS Code Git extension 적극 활용

### 3. 지속적 학습
- Git 고급 기능 학습
- 팀 단위 Git 워크숍 진행

---

## 💬 질문 & 토론

- **Q**: 여러분은 비슷한 상황을 경험해본 적이 있나요?
- **Q**: rebase vs merge, 어떤 전략을 선호하시나요?
- **Q**: 팀 프로젝트에서 Git 관련 규칙이 있다면 공유해주세요!

---

*"오류는 성장의 기회다. 중요한 건 같은 실수를 반복하지 않는 것!"* 🚀

---

# Git Rebase vs Merge: 팀 협업에서의 올바른 선택

팀 프로젝트를 진행하다 보면 필연적으로 마주치게 되는 상황이 있습니다. 바로 **브랜치 충돌**이죠. 이때 개발자는 두 가지 선택지 앞에 서게 됩니다: `git merge`와 `git rebase`. 어떤 것을 선택해야 할까요?

## 🤔 Merge vs Rebase: 근본적인 차이점

### Merge: "기록 보존주의자"
```
Before:
main:    A---B---C
              \
feature:       D---E

After Merge:
main:    A---B---C-------M
              \         /
feature:       D---E---/
```

Merge는 **히스토리를 보존**합니다. 언제 어떤 브랜치가 합쳐졌는지, 누가 어떤 작업을 했는지 모든 기록이 남아있죠.

### Rebase: "히스토리 재구성주의자"
```
Before:
main:    A---B---C
              \
feature:       D---E

After Rebase:
main:    A---B---C---D'---E'
```

Rebase는 **히스토리를 재작성**합니다. 마치 처음부터 순서대로 개발한 것처럼 깔끔한 일직선을 만들어냅니다.

## 📊 실제 팀 협업 시나리오

### 상황: 3명의 개발자가 동시에 작업

```
팀 구성:
👨‍💻 강혁: 백엔드 API 개발
👩‍💻 상희: 프론트엔드 UI 개발  
👨‍💻 민수: 데이터베이스 스키마 작업
```

#### Merge 방식의 히스토리
```bash
git log --oneline --graph

*   f8a2c1d Merge branch 'feature/ui'
|\  
| * d4c2a1b 상희: UI 수정
|/  
*   a7f9e3c Merge branch 'feature/api'
|\  
| * b8e1f4d 강혁: API 연결
* | c5d7a2e 민수: DB 스키마 수정
|/  
*   e9f2b5c Merge branch 'feature/database'
|\  
| * f1c8d7a 민수: 테이블 생성
|/  
* 2a4b6c8 프로젝트 초기 설정
```

**😵 문제점:**
- 누가 언제 뭘 했는지 파악하기 어려움
- 커밋이 시간순으로 뒤섞여 있음
- 기능별 연관성을 찾기 어려움

#### Rebase 방식의 히스토리
```bash
git log --oneline

f1c8d7a 민수: 테이블 생성
c5d7a2e 민수: DB 스키마 수정
b8e1f4d 강혁: API 연결  
d4c2a1b 상희: UI 수정
2a4b6c8 프로젝트 초기 설정
```

**✨ 장점:**
- 논리적 개발 순서: DB → API → UI
- 각 개발자의 작업 흐름이 명확
- 디버깅 시 코드 추적이 용이

## 🔥 멘토의 조언: "Merge의 한계"

> **"Merge는 강혁님의 커밋과 상희님의 커밋의 우선순위를 판단하지 않습니다. 그리고 변경사항을 제대로 줄 세우지도 않습니다."**

### 실제 사례로 이해하기

**시나리오:** API 에러가 발생했을 때

**Merge 히스토리로 디버깅:**
```bash
# 시간순으로 뒤죽박죽
git log --oneline
d4c2a1b 상희: UI 버튼 스타일 수정
b8e1f4d 강혁: API 엔드포인트 추가
a3f5c2e 상희: 모달 컴포넌트 생성
f7b9d1c 강혁: 인증 로직 구현

# 🤷‍♂️ API 관련 커밋이 어디 있지?
# 🤷‍♂️ 인증이 먼저인가, 엔드포인트가 먼저인가?
```

**Rebase 히스토리로 디버깅:**
```bash
# 논리적 순서로 정렬
git log --oneline
f7b9d1c 강혁: 인증 로직 구현
b8e1f4d 강혁: API 엔드포인트 추가
a3f5c2e 상희: 모달 컴포넌트 생성
d4c2a1b 상희: UI 버튼 스타일 수정

# ✅ 인증 → 엔드포인트 순서구나!
# ✅ 문제는 인증 로직에 있을 것 같은데?
```

## 🚀 실무에서의 Rebase 워크플로우

### Step 1: 브랜치 생성 및 개발
```bash
# 1) dev에서 내 작업 브랜치 뽑기
git checkout dev
git pull origin dev
git checkout -b feature/my-awesome-feature

# 2) 열심히 개발하고 푸시
git add .
git commit -m "기능 구현 완료"
git push origin feature/my-awesome-feature
```

### Step 2: PR 생성 및 충돌 확인
```bash
# 3) GitHub에서 PR 생성
# "Conflicts detected! 😱"
```

### Step 3: 충돌 해결 (핵심!)

#### 상황 분석
```
내가 작업 시작할 때:
dev: A---B---C (버전 a)
      \
내 브랜치: D---E

다른 팀원이 먼저 머지 후:
dev: A---B---C---F---G (버전 a-2)
      \
내 브랜치: D---E (충돌 발생!)
```

#### Rebase로 해결
```bash
# 4) 최신 dev 기준으로 rebase
git checkout feature/my-awesome-feature
git fetch origin dev
git rebase origin/dev

# 충돌 발생 시 해결
# Auto-merging conflict detected...
# 파일 수정 후
git add .
git rebase --continue

# 5) Force push (중요!)
git push --force origin feature/my-awesome-feature
```

#### 결과
```
# Rebase 후 깔끔한 히스토리
dev: A---B---C---F---G---D'---E'
                         ↑
                    내 작업이 최신 dev 위에!
```

## 🎨 시각적 비교

### Merge 방식
```
🔀 복잡한 분기 구조
main: ●---●---●---◆
       \         /|\ 
feat1:  ●---●---/ | \
feat2:   \        |  ●---●
          ●---●---/

❌ 히스토리가 복잡함
❌ 개발 순서 파악 어려움
❌ 디버깅 시 추적 복잡
```

### Rebase 방식
```
🔄 깔끔한 일직선 구조
main: ●---●---●---●---●---●---●

✅ 논리적 개발 순서
✅ 각 기능별 그룹핑
✅ 디버깅 추적 용이
```

## ⚖️ 상황별 선택 가이드

### 🟢 Rebase를 사용해야 할 때

**개인 브랜치 정리**
```bash
# ✅ 아직 공유되지 않은 내 브랜치
git checkout feature/my-work
git rebase main
```

**깔끔한 히스토리가 중요한 프로젝트**
```bash
# ✅ 오픈소스, 포트폴리오 프로젝트
# 누구나 이해하기 쉬운 커밋 히스토리 필요
```

**코드 리뷰의 효율성**
```bash
# ✅ PR 리뷰 시 논리적 순서로 코드 확인 가능
# 커밋 하나하나가 스토리를 가짐
```

### 🔴 Rebase를 피해야 할 때

**공유된 브랜치**
```bash
# ❌ 절대 금지!
git checkout main
git rebase anything  # 팀 전체 혼란 초래
```

**복잡한 충돌이 예상되는 경우**
```bash
# ❌ 너무 많은 충돌 → merge가 더 안전
git merge origin/main
```

## 🎯 실무 팀 규칙 예시

### Rule 1: 브랜치별 전략
```bash
# 개인 브랜치: rebase OK
feature/user-login → rebase main

# 공유 브랜치: merge ONLY  
main, develop → merge 만 사용
```

### Rule 2: 워크플로우
```bash
1. feature 브랜치에서 개발
2. 개발 완료 후 main 기준으로 rebase
3. PR 생성 및 팀 리뷰
4. main에 merge (squash merge 권장)
```

### Rule 3: 절대 금지사항
```bash
# 🚫 공유 브랜치 rebase
git checkout main
git rebase feature/anything

# 🚫 이미 push된 커밋 rebase (팀원과 상의 없이)
git rebase -i HEAD~5  # 다른 팀원이 이미 pull했다면 위험
```

## 📈 성능과 협업 효율성

### Rebase의 장점
| 측면 | Merge | Rebase |
|------|-------|--------|
| **히스토리 가독성** | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **디버깅 효율성** | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **코드 리뷰** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **신입 개발자 학습** | ⭐⭐ | ⭐⭐⭐⭐ |
| **안전성** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

### 실제 개발 시간 단축 효과
```bash
# 버그 발생 시 원인 파악 시간
Merge 히스토리: 30분 (여러 브랜치 추적)
Rebase 히스토리: 5분 (일직선 추적)

# 코드 리뷰 시간  
Merge PR: 20분 (컨텍스트 파악 어려움)
Rebase PR: 10분 (논리적 순서로 리뷰)
```

## 🛠️ 고급 Rebase 테크닉

### Interactive Rebase로 커밋 정리
```bash
# 여러 커밋을 하나로 합치기
git rebase -i HEAD~3

# 에디터에서:
pick a1b2c3d 기능 구현
squash d4e5f6g 오타 수정  
squash g7h8i9j 코드 리팩토링

# 결과: 3개 커밋이 1개로 합쳐짐
```

### 특정 커밋만 가져오기
```bash
# Cherry-pick과 rebase 조합
git checkout feature/new-work
git rebase --onto main feature/old-work~3 feature/old-work
```

## 💡 실무 꿀팁

### 1. Rebase 전 백업
```bash
# 혹시 모르니 백업 브랜치 생성
git checkout -b feature/my-work-backup
git checkout feature/my-work
git rebase main
```

### 2. 충돌 해결 시 도구 활용
```bash
# VS Code, IntelliJ 등의 merge tool 사용
git config --global merge.tool vscode
git mergetool
```

### 3. Force Push 대신 Force-with-lease
```bash
# 더 안전한 force push
git push --force-with-lease origin feature/my-work
```

## 🎓 결론: 현명한 선택을 위한 가이드

### 🎯 핵심 원칙
> **"개인 브랜치에서는 rebase로 정리하고, 공유 브랜치에서는 merge로 안전하게"**

### 🚀 권장 워크플로우
1. **개발 시작**: `main`에서 `feature` 브랜치 생성
2. **개발 중**: 수시로 커밋, 필요시 interactive rebase로 정리
3. **PR 전**: `main` 기준으로 rebase하여 충돌 해결
4. **리뷰 후**: `main`에 merge (squash merge 권장)


---

### 참고 자료
- [Git 공식 문서 - Rebase](https://git-scm.com/docs/git-rebase)
- [Atlassian Git 튜토리얼](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)
- [GitHub - About merge methods](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges)

### 태그
#Git #Rebase #Merge #협업 #버전관리 #개발워크플로우 #팀프로젝트
