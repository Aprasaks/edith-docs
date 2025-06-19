# 📚 edith-docs 기여 가이드

edith-docs에 기여해주셔서 감사합니다! 이 가이드를 따라 문서를 작성하고 기여할 수 있습니다.

## 🚀 빠른 시작

### 방법 1: GitHub 웹에서 직접 편집 (간단함)
1. **파일 추가**: `Add file` → `Create new file`
2. **파일 경로**: `카테고리명/파일명.md` (예: `react/새로운-가이드.md`)
3. **내용 작성** 후 **Commit** 클릭

### 방법 2: Fork & Pull Request (권장)
1. **우상단 Fork 버튼** 클릭
2. **본인 레포에서 작업**
3. **Pull Request 생성**

## 📁 문서 구조

```
edith-docs/
├── react/          # React 관련 문서
├── nextjs/         # Next.js 관련 문서
├── javascript/     # JavaScript 관련 문서
├── typescript/     # TypeScript 관련 문서
├── css/           # CSS 관련 문서
└── tools/         # 개발 도구 관련 문서
```

## 📝 문서 작성 가이드

### 1. 파일명 규칙
- **소문자 사용**: `react-hooks-guide.md`
- **하이픈 연결**: `nextjs-app-router.md`
- **의미있는 이름**: 내용을 잘 표현하는 이름

### 2. 필수 Frontmatter
모든 문서 상단에 다음 정보를 포함해주세요:

```yaml
---
title: "문서 제목"
description: "문서 설명 (1-2줄)"
category: "React"
date: "2024-12-19"
readTime: "10min"
tags: ["React", "Hooks", "Frontend"]
status: "new"  # new, updated, popular
author: "작성자명"
slug: "파일명-without-extension"
---
```

### 3. 문서 구조 예시

```markdown
---
title: "React useState 완벽 가이드"
description: "useState Hook의 기본부터 고급 사용법까지"
category: "React"
date: "2024-12-19"
readTime: "15min"
tags: ["React", "Hooks", "State"]
status: "new"
author: "홍길동"
slug: "react-usestate-guide"
---

# 🎯 React useState 완벽 가이드

useState는 React에서 가장 기본적이고 중요한 Hook입니다.

## 📖 목차
1. [기본 사용법](#기본-사용법)
2. [고급 패턴](#고급-패턴)
3. [실전 예제](#실전-예제)

## 🚀 기본 사용법

useState Hook을 사용하면 함수형 컴포넌트에서 상태를 관리할 수 있습니다.

### 예제 코드
\`\`\`jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        증가
      </button>
    </div>
  );
}
\`\`\`

### 주요 포인트
- **불변성 유지**: 상태를 직접 수정하지 말고 setter 함수 사용
- **함수형 업데이트**: 이전 상태를 기반으로 업데이트할 때 활용

## 💡 고급 패턴

### 객체 상태 관리
\`\`\`jsx
const [user, setUser] = useState({
  name: '',
  email: '',
  age: 0
});

const updateUser = (field, value) => {
  setUser(prev => ({
    ...prev,
    [field]: value
  }));
};
\`\`\`

## 🔥 실전 예제

실제 프로젝트에서 활용할 수 있는 예제들을 소개합니다.

## 📚 참고 자료
- [React 공식 문서](https://react.dev)
- [다른 관련 문서](링크)

## 💬 마무리

useState를 잘 활용하면 더 나은 React 애플리케이션을 만들 수 있습니다.
```

## 🎨 작성 스타일 가이드

### ✅ 좋은 예시
- **이모지 활용**: 제목에 관련 이모지 사용
- **코드 예제**: 실제 작동하는 코드 제공
- **단계별 설명**: 초보자도 이해할 수 있게
- **실전 예제**: 바로 적용 가능한 내용

### ❌ 피해야 할 것
- 너무 이론적인 내용만
- 코드 예제 없는 설명
- 오타나 문법 오류
- 너무 짧거나 너무 긴 문서

## 📋 체크리스트

문서 작성 완료 전에 확인해주세요:

- [ ] Frontmatter 정보가 정확한가?
- [ ] 코드 예제가 작동하는가?
- [ ] 오타나 문법 오류는 없는가?
- [ ] 목차와 내용이 일치하는가?
- [ ] 초보자도 이해할 수 있는가?

## 🔄 리뷰 프로세스

### Pull Request 생성 시:
1. **명확한 제목**: "Add React useState guide" 
2. **설명 작성**: 어떤 내용을 추가했는지
3. **체크리스트 확인**: 위 체크리스트 완료

### 리뷰어 가이드:
- **내용 정확성**: 기술적 내용이 정확한가?
- **가독성**: 이해하기 쉬운가?
- **완성도**: 예제와 설명이 충분한가?
- **일관성**: 다른 문서와 스타일이 일치하는가?

## 🏷️ 카테고리별 가이드

### React
- Hook 사용법, 컴포넌트 패턴, 상태 관리 등
- 실제 프로젝트에서 사용할 수 있는 예제 중심

### Next.js
- 라우팅, 데이터 페칭, 배포, 최적화 등
- 버전별 차이점과 마이그레이션 가이드

### JavaScript
- ES6+ 문법, 비동기 처리, 함수형 프로그래밍 등
- 최신 JavaScript 기능과 실용적 패턴

### CSS
- 레이아웃, 애니메이션, 반응형 디자인 등
- 모던 CSS 기법과 최적화 방법

## 🤝 커뮤니티 가이드라인

- **존중**: 서로 다른 의견을 존중해주세요
- **건설적 피드백**: 구체적이고 도움이 되는 리뷰
- **협력**: 함께 더 나은 문서를 만들어가요
- **배움**: 실수는 배움의 기회입니다

## 📞 도움이 필요하시면

- **GitHub Issues**: 질문이나 제안사항
- **GitHub Discussions**: 일반적인 토론
- **Pull Request**: 직접적인 기여

## 🎉 기여해주셔서 감사합니다!

여러분의 기여로 더 많은 개발자들이 도움을 받을 수 있습니다. 

**함께 멋진 문서 아카이브를 만들어가요!** 🚀
