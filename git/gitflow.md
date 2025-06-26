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
