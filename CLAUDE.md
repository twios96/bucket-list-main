# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

버킷 리스트(Bucket List) - 인생 목표를 기록하고 관리하는 웹 애플리케이션. Vanilla JavaScript로 구현된 정적 웹앱으로, 빌드 과정 없이 바로 실행 가능.

## Running the Application

```bash
# Option 1: Python simple server
python -m http.server 8000
# Open http://localhost:8000

# Option 2: VS Code Live Server extension
# Right-click index.html → "Open with Live Server"

# Option 3: Direct browser open
# Double-click index.html
```

## Architecture

### Module Structure

- **`js/storage.js`** - `BucketStorage` 객체: LocalStorage CRUD 및 데이터 관리
- **`js/app.js`** - `BucketListApp` 클래스: UI 제어, 이벤트 핸들링, 렌더링

### Data Flow

```
User Action → BucketListApp (Event Handler) → BucketStorage (LocalStorage) → render()
```

### Key Patterns

1. **Storage/UI 분리**: `BucketStorage`는 데이터 영속성만 담당, `BucketListApp`은 UI만 담당
2. **DOM 캐싱**: `cacheElements()`에서 모든 DOM 참조를 초기화 시점에 저장
3. **전역 인스턴스**: `app` 변수가 전역으로 노출되어 인라인 onclick에서 호출됨

### Data Structure

```javascript
{
  id: string,           // timestamp 기반 고유 ID
  title: string,        // 버킷 리스트 제목
  completed: boolean,   // 완료 여부
  createdAt: string,    // ISO date string
  completedAt: string | null
}
```

### LocalStorage Key

- `bucketList` - 전체 항목 배열 저장

## Tech Stack

- HTML5, CSS3, JavaScript (ES6+)
- Tailwind CSS (CDN)
- LocalStorage API

## Notes

- 프레임워크 없이 Vanilla JS로 구현
- 서버/데이터베이스 없이 브라우저 LocalStorage만 사용
- XSS 방지를 위해 `escapeHtml()` 함수 사용
