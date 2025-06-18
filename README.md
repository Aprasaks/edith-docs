# 📚 Edith Docs

A comprehensive documentation repository for development guides, tutorials, and best practices.

개발 가이드, 튜토리얼, 그리고 모범 사례를 위한 종합 문서 저장소입니다.

## 🚀 Overview / 개요

This repository contains markdown-based documentation that powers the Edith documentation website. All documents are written in Korean with code examples and can be dynamically fetched via GitHub API.

이 저장소는 Edith 문서 웹사이트를 지원하는 마크다운 기반 문서들을 포함하고 있습니다. 모든 문서는 한국어로 작성되며 코드 예제가 포함되어 있고, GitHub API를 통해 동적으로 가져올 수 있습니다.

## 📁 Repository Structure / 저장소 구조

```
edith-docs/
├── docs/
│   ├── react/              # React-related documentation
│   │   ├── react-hooks-guide.md
│   │   ├── react-optimization.md
│   │   └── react-best-practices.md
│   ├── nextjs/             # Next.js documentation
│   │   ├── nextjs-app-router.md
│   │   ├── nextjs-performance.md
│   │   └── nextjs-deployment.md
│   ├── javascript/         # JavaScript guides
│   │   ├── es6-features.md
│   │   ├── async-programming.md
│   │   └── modern-javascript.md
│   ├── typescript/         # TypeScript documentation
│   │   ├── typescript-basics.md
│   │   └── advanced-types.md
│   └── tools/              # Development tools
│       ├── git-workflow.md
│       └── vscode-setup.md
├── config/
│   └── categories.json     # Category configuration
└── README.md
```

## 📋 Document Categories / 문서 카테고리

### 🔵 React
- **React Hooks Guide** - Complete guide to React Hooks / React Hooks 완벽 가이드
- **React Optimization** - Performance optimization techniques / 성능 최적화 기법
- **React Best Practices** - Modern React development patterns / 모던 React 개발 패턴

### 🟢 Next.js
- **App Router Migration** - Migrating from Pages to App Router / Pages에서 App Router로 마이그레이션
- **Performance Optimization** - Next.js performance best practices / Next.js 성능 최적화
- **Deployment Guide** - Production deployment strategies / 프로덕션 배포 전략

### 🟡 JavaScript
- **ES6+ Features** - Modern JavaScript features and syntax / 모던 JavaScript 기능과 문법
- **Async Programming** - Promises, async/await, and more / Promise, async/await 등
- **Modern JavaScript** - Latest JavaScript patterns and practices / 최신 JavaScript 패턴과 관행

### 🔴 TypeScript
- **TypeScript Basics** - Getting started with TypeScript / TypeScript 시작하기
- **Advanced Types** - Complex type patterns and utilities / 복잡한 타입 패턴과 유틸리티

### 🟣 Development Tools
- **Git Workflow** - Effective Git strategies / 효과적인 Git 전략
- **VS Code Setup** - IDE configuration and extensions / IDE 설정과 확장 프로그램

## 🏷️ Document Format / 문서 형식

Each markdown file includes frontmatter metadata:

각 마크다운 파일은 다음과 같은 메타데이터를 포함합니다:

```yaml
---
title: "Document Title"
description: "Brief description of the document"
category: "React"
date: "2024-12-15"
readTime: "15min"
tags: ["React", "Hooks", "Frontend"]
status: "updated"  # new, updated, popular
author: "DemianDev"
slug: "react-hooks-guide"
---
```

## 🔧 Integration / 연동

This repository is designed to work with:

이 저장소는 다음과 함께 작동하도록 설계되었습니다:

- **GitHub API** - Dynamic content fetching / 동적 콘텐츠 가져오기
- **Next.js Application** - Documentation website / 문서 웹사이트
- **React Markdown** - Markdown rendering with syntax highlighting / 구문 강조가 포함된 마크다운 렌더링

## 🤝 Contributing / 기여하기

### Adding New Documents / 새 문서 추가하기

1. Create a new `.md` file in the appropriate category folder
   적절한 카테고리 폴더에 새 `.md` 파일 생성

2. Include proper frontmatter metadata
   적절한 frontmatter 메타데이터 포함

3. Write content in Korean with code examples
   코드 예제와 함께 한국어로 내용 작성

4. Submit a pull request
   풀 리퀘스트 제출

### Document Guidelines / 문서 가이드라인

- **Language**: Korean (한국어)
- **Code Examples**: Include practical, working examples / 실용적이고 작동하는 예제 포함
- **Structure**: Use clear headings and sections / 명확한 제목과 섹션 사용
- **Tags**: Add relevant tags for better categorization / 더 나은 분류를 위한 관련 태그 추가

## 📊 Status Indicators / 상태 표시기

- **🆕 NEW** - Recently added documents / 최근 추가된 문서
- **🔄 UPDATED** - Recently updated content / 최근 업데이트된 내용
- **🔥 POPULAR** - Frequently accessed documents / 자주 접근되는 문서

## 🔗 Related Projects / 관련 프로젝트

- **Documentation Website** - Main application that consumes these docs / 이 문서들을 사용하는 메인 애플리케이션
- **GitHub API Integration** - Fetches content dynamically / 동적으로 콘텐츠를 가져옴

## 📝 License / 라이선스

This project is open source and available under the MIT License.

이 프로젝트는 오픈 소스이며 MIT 라이선스 하에 제공됩니다.

---

**Last Updated**: JUNE 2025 / **마지막 업데이트**: 2025년 6월  
**Maintained by**: DemianDev / **관리자**: DemianDev
