---
title: "Markdown 에디터 가이드"
description: "마크다운에디터에 대한 모든 것"
category: "MarkdownEditor"
date: "2025-06-27"
readTime: "5min"
tags: ["React", "Markdown", "Editor", "Frontend"]
status: "new"
author: "DemianDev"
slug: "markdown-editor"
---

# 마크다운 에디터 완전 가이드: 개념부터 직접 구현까지

개발자라면 한 번쯤은 마크다운을 사용해봤을 것입니다. GitHub README, 기술 문서, 블로그 포스팅까지 마크다운은 이제 개발 생태계의 필수 도구가 되었죠. 하지만 마크다운을 '보기 좋게' 편집할 수 있는 에디터를 선택하거나 직접 만들어야 할 때는 어떨까요?

이 글에서는 마크다운 에디터의 기본 개념부터 주요 오픈소스 라이브러리 비교, 그리고 실제 개발 경험까지 모든 것을 다뤄보겠습니다.

## 마크다운 에디터란 무엇인가?

마크다운 에디터는 사용자가 마크다운 문법을 손쉽게 입력하고 편집할 수 있도록 도와주는 소프트웨어입니다. 단순히 텍스트를 입력하는 것을 넘어서 **실시간 미리보기**, **툴바 지원**, **다양한 포맷 변환** 등의 기능을 제공합니다.

### 마크다운의 탄생 배경

2004년 존 그루버(John Gruber)와 아론 스워츠(Aaron Swartz)가 개발한 마크다운의 핵심 철학은 간단합니다:

> "텍스트로 문서 작성은 쉽고, 렌더링하면 구조적으로 예쁜 문서가 나오게 하자"

몇 가지 간단한 문법만으로 제목, 리스트, 표, 코드, 링크, 이미지 등을 표현할 수 있어 개발자들에게 큰 사랑을 받게 되었습니다.

## 마크다운 에디터의 핵심 기능들

### 기본 기능

**마크다운 입력**
- 에디터 창에서 마크다운 문법을 직접 입력
- 구문 강조(Syntax Highlighting)로 가독성 향상

**실시간 미리보기**
- 입력과 동시에 렌더링된 결과를 확인
- 분할 화면 또는 토글 방식으로 제공

**툴바 지원**
- Bold, Italic, 헤더, 코드블럭, 리스트, 링크 등
- 클릭 한 번으로 마크다운 문법 자동 삽입

**단축키 지원**
- `Ctrl+B` (Bold), `Ctrl+I` (Italic) 등 직관적인 키 조합
- 개발자들이 익숙한 에디터 단축키와 유사

**포맷 변환**
- 마크다운 → HTML, PDF 등 다양한 형식으로 내보내기
- 역방향 변환(HTML → 마크다운)도 지원

### 고급 기능

**이미지 관리**
- 파일 업로드, 드래그&드롭, 클립보드 붙여넣기
- 이미지 크기 조절 및 정렬 옵션
- 이 부분에서 대부분의 라이브러리가 한계를 드러냅니다

**확장 문법 지원**
- 테이블, 수식(LaTeX), 다이어그램(Mermaid)
- 코드 하이라이팅, 체크리스트 등

**고급 UX 기능**
- 멀티컬럼 레이아웃
- 인라인 툴바
- 플러그인 시스템
- 버전 관리 및 협업 기능

## 주요 오픈소스 라이브러리 비교

### 1. Toast UI Editor

**특징**
- 네이버에서 개발한 한국 개발자 친화적 에디터
- 마크다운/위지윅(WYSIWYG) 모드 전환 가능
- 풍부한 한글 문서와 예제

**장점**
- 빠른 도입이 가능하고 학습 곡선이 완만함
- 플러그인, 테마, 이미지 업로드 등 기본 기능이 탄탄함
- 국내 커뮤니티 지원이 활발함

**한계**
- 마크다운으로 저장 시 이미지 크기/스타일 정보가 유실됨
- UI 커스터마이징에 제약이 있음
- 고급 기능 확장이 어려움

### 2. Tiptap

**특징**
- 현대적인 리치텍스트 에디터 기반의 하이브리드 방식
- 강력한 Extension 시스템으로 무한 확장 가능
- 유럽/미국 개발자들 사이에서 인기

**장점**
- 커스터마이징 자유도가 최고 수준
- 플러그인 생태계가 풍부함
- 최신 웹 기술 스택 활용

**한계**
- 순수 마크다운 저장 구조가 아님
- 복잡한 커스터마이징 시 러닝 커브가 가파름
- HTML/JSON/마크다운 간 변환 로직을 직접 설계해야 함

### 3. uiw/react-md-editor

**특징**
- React 환경에서 빠르게 적용 가능한 경량 에디터
- 실시간 미리보기와 기본 툴바 제공

**장점**
- 매우 가벼우며 설치/설정이 간단함
- React 프로젝트에 즉시 적용 가능
- 학습 비용이 거의 없음

**한계**
- 이미지 업로드, 크기 조절 등 고급 기능 미지원
- 확장성이 제한적임
- 대규모 프로젝트보다는 프로토타입에 적합

### 4. 기타 솔루션들

**Typora**
- 데스크톱 앱으로 "입력 = 미리보기" 통합 UX 제공
- 로컬 파일 관리와 플러그인 지원이 우수

**StackEdit, HackMD**
- 웹 기반 협업 도구로 실시간 공유 및 버전 관리 지원
- 클라우드 저장소 연동 가능

## 마크다운 에디터의 근본적 한계: 이미지 문제

마크다운 에디터를 선택하거나 개발할 때 가장 큰 걸림돌은 **이미지 처리**입니다.

### 마크다운 표준의 한계

기본 마크다운 문법에는 `![alt](url)` 형태의 이미지 삽입만 지원됩니다. 여기에는 다음과 같은 정보가 포함되지 않습니다:

- 이미지 크기 (width, height)
- 정렬 방식 (left, center, right)
- 스타일 속성 (border, shadow 등)

### 확장 문법의 한계

일부 에디터에서는 다음과 같은 확장 문법을 지원하기도 합니다:

```markdown
![image](url =100x200)
<img src="url" width="200" height="150">
```

하지만 이런 확장 문법들은:
- 마크다운 표준이 아니어서 호환성 문제가 발생
- 다른 마크다운 파서에서 제대로 렌더링되지 않을 수 있음
- 파서마다 지원하는 문법이 달라 일관성 부족

### 라이브러리별 대응 방식

대부분의 마크다운 에디터는 다음과 같은 방식으로 이 문제를 우회합니다:

1. **WYSIWYG 모드에서만 이미지 조작 허용**
   - 사용자는 위지윅 모드에서 이미지 크기를 조절할 수 있음
   - 하지만 마크다운으로 저장할 때는 부가 정보가 사라짐

2. **HTML/JSON 형태로 별도 저장**
   - 마크다운과 별도로 스타일 정보를 저장
   - 복원 시 두 정보를 결합하여 렌더링

3. **커스텀 파서 사용**
   - 자체적인 마크다운 확장 문법 정의
   - 다른 환경과의 호환성 포기

## 직접 구현의 필요성과 장점

### 왜 직접 만들어야 할까?

기존 오픈소스 라이브러리들의 한계점들을 정리하면:

**기능적 한계**
- 이미지 크기/스타일 정보 손실 문제
- 제한적인 플러그인 시스템
- 고정된 UI/UX로 인한 브랜딩 제약

**기술적 한계**
- 마크다운 ↔ HTML/JSON 변환 로직의 불완전성
- 특정 프레임워크/라이브러리 의존성
- 성능 최적화의 어려움

**서비스 요구사항**
- 복잡한 비즈니스 로직 통합 필요
- 특별한 워크플로우 지원
- 고도로 커스터마이징된 사용자 경험

### 직접 구현한 에디터의 구조 (실제 사례)

다음은 실제로 구현한 마크다운 에디터의 핵심 구조입니다:

**기술 스택**
- React + TypeScript
- 커스텀 마크다운 파서 (remark/rehype 기반)
- 상태 관리를 위한 Context API

**주요 기능**
- 양분할 화면 (마크다운 입력 + 실시간 미리보기)
- 이미지 드래그&드롭 업로드
- 이미지 선택 후 크기 조정 UI
- 커스텀 툴바 (Bold, Italic, Underline, Code 등)
- 미리보기 영역의 커스텀 렌더링

**핵심 구현 방식**
```typescript
// 에디터 상태 구조
interface EditorState {
  markdown: string;
  metadata: {
    images: {
      [url: string]: {
        width?: number;
        height?: number;
        align?: 'left' | 'center' | 'right';
        caption?: string;
      }
    };
    // 기타 메타데이터
  };
}
```

**정보 보존 로직**
1. 마크다운 텍스트와 별도로 메타데이터 저장
2. 렌더링 시 두 정보를 결합
3. 마크다운 파싱 시 메타데이터 참조하여 확장 렌더링


## 에디터 커스터마이징 실전 팁

### 1. 이미지 메타데이터 관리

이미지 크기 등 부가 정보는 마크다운 표준으로는 저장이 불가능합니다. 다음과 같은 방식을 추천합니다:

```javascript
// 방법 1: JSON 메타데이터 별도 저장
const editorData = {
  content: "![image](url)", // 순수 마크다운
  metadata: {
    images: {
      "url": { width: 300, height: 200, align: "center" }
    }
  }
};

// 방법 2: 커스텀 HTML 속성 활용
const htmlContent = `<img src="url" width="300" height="200" data-align="center">`;
```

### 2. 커스텀 파서/렌더러 구축

`remark`, `rehype`, `markdown-it` 등의 라이브러리를 활용하여 커스텀 파서를 구축할 수 있습니다:

```javascript
import { remark } from 'remark';
import remarkHtml from 'remark-html';

const processor = remark()
  .use(remarkHtml)
  .use(customImagePlugin); // 커스텀 이미지 처리 플러그인

function customImagePlugin() {
  return (tree) => {
    // 이미지 노드를 찾아서 메타데이터 적용
    visit(tree, 'image', (node) => {
      const metadata = getImageMetadata(node.url);
      if (metadata) {
        node.data = { ...node.data, ...metadata };
      }
    });
  };
}
```

### 3. 경험 

**드래그&드롭 구현**
```javascript
const handleDrop = (e) => {
  e.preventDefault();
  const files = Array.from(e.dataTransfer.files);
  files.forEach(file => {
    if (file.type.startsWith('image/')) {
      uploadImage(file).then(url => {
        insertImageToEditor(url);
      });
    }
  });
};
```

**단축키 처리**
```javascript
const handleKeyDown = (e) => {
  if (e.ctrlKey || e.metaKey) {
    switch (e.key) {
      case 'b':
        e.preventDefault();
        insertMarkdown('**', '**');
        break;
      case 'i':
        e.preventDefault();
        insertMarkdown('*', '*');
        break;
    }
  }
};
```

## 선택 가이드: 언제 무엇을 써야 할까?

### 빠른 프로토타이핑이 필요한 경우
- **추천**: uiw/react-md-editor, Toast UI Editor
- **이유**: 설정이 간단하고 기본 기능이 충분함
- **적합한 프로젝트**: MVP, 사내 도구, 개인 프로젝트

### 브랜딩과 UX 커스터마이징이 중요한 경우
- **추천**: Tiptap, 직접 구현
- **이유**: 높은 자유도와 확장성
- **적합한 프로젝트**: 상용 서비스, 차별화된 에디터가 필요한 경우

### 이미지 크기 조절이 필수인 경우
- **추천**: 직접 구현
- **이유**: 현재로서는 이 요구사항을 완벽하게 만족하는 오픈소스가 없음
- **주의사항**: JSON/HTML 기반 상태 관리와 커스텀 파서 필요

### 협업 기능이 핵심인 경우
- **추천**: StackEdit, HackMD 등 기존 솔루션 활용
- **이유**: 실시간 협업 기능 구현의 복잡성
- **대안**: Firebase, Socket.io 등을 활용한 직접 구현


### 참고 자료

- [Markdown 공식 문서](https://daringfireball.net/projects/markdown/)
- [Toast UI Editor GitHub](https://github.com/nhn/tui.editor)
- [Tiptap 공식 문서](https://tiptap.dev/)
- [uiw/react-md-editor](https://github.com/uiwjs/react-md-editor)
- [remark 생태계](https://remark.js.org/)

### 태그
#마크다운 #에디터 #React #웹개발 #오픈소스 #UX #프론트엔드
