# Husky 설정 가이드

## 개요
Husky는 Git hooks를 쉽게 관리할 수 있게 해주는 도구입니다. 코드 품질을 유지하고 팀 협업을 원활하게 하기 위해 커밋 전후에 자동으로 스크립트를 실행할 수 있습니다.

## 설치 및 기본 설정

### 1. Husky 설치
```bash
npm install --save-dev husky
```

### 2. Git hooks 초기화
```bash
npx husky install
```

### 3. package.json에 prepare 스크립트 추가
```json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```

이 스크립트는 `npm install` 실행 시 자동으로 Husky를 초기화합니다.

## 주요 Git Hooks 설정

### Pre-commit Hook (커밋 전 실행)
코드 품질 검사를 위해 가장 많이 사용되는 훅입니다.

```bash
# ESLint 검사
npx husky add .husky/pre-commit "npm run lint"

# Prettier 포맷팅
npx husky add .husky/pre-commit "npm run format"

# 여러 명령어 실행
npx husky add .husky/pre-commit "npm run lint && npm run format && npm test"
```

### Commit-msg Hook (커밋 메시지 검사)
커밋 메시지 규칙을 강제하기 위해 사용합니다.

```bash
npx husky add .husky/commit-msg "npx commitlint --edit \$1"
```

### Pre-push Hook (푸시 전 실행)
원격 저장소에 푸시하기 전 최종 검사를 실행합니다.

```bash
npx husky add .husky/pre-push "npm run build && npm test"
```

## 커밋 메시지 규칙 설정 (Commitlint)

### 1. Commitlint 설치
```bash
npm install --save-dev @commitlint/cli @commitlint/config-conventional
```

### 2. commitlint.config.js 파일 생성
```javascript
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'feat',     // 새로운 기능
        'fix',      // 버그 수정
        'docs',     // 문서 수정
        'style',    // 코드 스타일 변경
        'refactor', // 코드 리팩토링
        'test',     // 테스트 추가/수정
        'chore',    // 기타 작업
        'perf',     // 성능 개선
        'ci',       // CI 관련
        'build',    // 빌드 관련
        'revert'    // 되돌리기
      ]
    ],
    'subject-max-length': [2, 'always', 50],
    'subject-min-length': [2, 'always', 10]
  }
}
```

### 3. 커밋 메시지 형식
```
type: subject

body (선택사항)

footer (선택사항)
```

**예시:**
```
feat: 사용자 로그인 기능 추가

OAuth 2.0을 사용한 소셜 로그인 기능을 구현했습니다.
- Google 로그인 지원
- 자동 로그인 상태 유지

Closes #123
```

## 실전 설정 예시

### package.json 스크립트 설정
```json
{
  "scripts": {
    "prepare": "husky install",
    "lint": "eslint . --ext .js,.jsx,.ts,.tsx",
    "lint:fix": "eslint . --ext .js,.jsx,.ts,.tsx --fix",
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "test": "jest",
    "build": "npm run build:prod"
  }
}
```

### 추천 Pre-commit 설정
```bash
# .husky/pre-commit 파일 내용
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npm run lint:fix
npm run format
npm run test
```

### 추천 Commit-msg 설정
```bash
# .husky/commit-msg 파일 내용
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx commitlint --edit $1
```

## 팀 협업을 위한 권장사항

### 1. 점진적 도입
- 처음에는 pre-commit hook만 설정
- 팀이 적응한 후 commit-msg hook 추가
- 마지막에 pre-push hook 도입

### 2. 성능 최적화
```bash
# 변경된 파일만 검사 (lint-staged 사용)
npm install --save-dev lint-staged

# package.json에 추가
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{json,css,md}": ["prettier --write"]
  }
}

# .husky/pre-commit 수정
npx lint-staged
```

### 3. 긴급 상황 대응
```bash
# 임시로 hook 우회 (권장하지 않음)
git commit -m "hotfix: 긴급 수정" --no-verify
```

## 문제 해결

### 권한 오류 해결
```bash
chmod +x .husky/*
```

### Hook 재설정
```bash
rm -rf .husky
npx husky install
# 모든 hook 다시 추가
```

### 팀원 초기 설정
```bash
# 프로젝트 클론 후
npm install
npm run prepare
```

## 마무리

Husky를 통해 코드 품질을 자동으로 관리하면:
- 일관된 코드 스타일 유지
- 버그 조기 발견
- 팀 협업 효율성 향상
- 코드 리뷰 품질 개선

점진적으로 도입하여 팀의 개발 프로세스를 개선해보세요!
