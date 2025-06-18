---
title: "React Hooks 완벽 가이드"
description: "useState, useEffect부터 커스텀 훅까지 React Hooks의 모든 것을 배워보세요"
category: "React"
date: "2025-06-19"
readTime: "15min"
tags: ["React", "Hooks", "Frontend", "JavaScript"]
status: "new"
author: "DemianDev"
slug: "react-hooks-guide"
---

# 🎣 React Hooks 완벽 가이드

React Hooks는 함수형 컴포넌트에서 상태와 생명주기 기능을 사용할 수 있게 해주는 강력한 기능입니다. React 16.8에서 도입된 이후 React 개발의 표준이 되었습니다.

## 📖 목차

1. [useState 훅](#-usestate-훅)
2. [useEffect 훅](#-useeffect-훅)
3. [useContext 훅](#-usecontext-훅)
4. [커스텀 훅 만들기](#-커스텀-훅-만들기)
5. [최적화 팁](#-최적화-팁)
6. [실전 예제](#-실전-예제)

## 🔄 useState 훅

`useState`는 가장 기본적인 훅으로, 함수형 컴포넌트에서 상태를 관리할 수 있게 해줍니다.

### 기본 사용법

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>현재 카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        증가
      </button>
      <button onClick={() => setCount(count - 1)}>
        감소
      </button>
      <button onClick={() => setCount(0)}>
        리셋
      </button>
    </div>
  );
}
```

### 객체 상태 관리

```jsx
function UserForm() {
  const [user, setUser] = useState({
    name: '',
    email: '',
    age: 0
  });

  const handleInputChange = (field, value) => {
    setUser(prevUser => ({
      ...prevUser,
      [field]: value
    }));
  };

  return (
    <form>
      <input
        type="text"
        placeholder="이름"
        value={user.name}
        onChange={(e) => handleInputChange('name', e.target.value)}
      />
      <input
        type="email"
        placeholder="이메일"
        value={user.email}
        onChange={(e) => handleInputChange('email', e.target.value)}
      />
      <input
        type="number"
        placeholder="나이"
        value={user.age}
        onChange={(e) => handleInputChange('age', parseInt(e.target.value))}
      />
    </form>
  );
}
```

### 주요 특징 및 주의사항

- **불변성 유지**: 상태를 직접 수정하지 말고 항상 새로운 값으로 설정
- **함수형 업데이트**: 이전 상태를 기반으로 업데이트할 때는 함수를 사용

```jsx
// ✅ 좋은 예 - 함수형 업데이트
setCount(prevCount => prevCount + 1);

// ❌ 나쁜 예 - 직접 참조 (비동기 업데이트 시 문제 발생 가능)
setCount(count + 1);
```

## ⚡ useEffect 훅

`useEffect`는 사이드 이펙트를 처리하는 훅입니다. 컴포넌트가 렌더링된 후에 실행됩니다.

### 기본 사용법

```jsx
import { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchUser() {
      try {
        setLoading(true);
        const response = await fetch(`/api/users/${userId}`);
        
        if (!response.ok) {
          throw new Error('사용자 정보를 가져올 수 없습니다');
        }
        
        const userData = await response.json();
        setUser(userData);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    }

    fetchUser();
  }, [userId]); // userId가 변경될 때마다 실행

  if (loading) return <div className="loading">로딩 중...</div>;
  if (error) return <div className="error">에러: {error}</div>;
  if (!user) return <div>사용자를 찾을 수 없습니다.</div>;

  return (
    <div className="user-profile">
      <img src={user.avatar} alt={user.name} />
      <h1>{user.name}</h1>
      <p>{user.email}</p>
      <p>가입일: {new Date(user.createdAt).toLocaleDateString()}</p>
    </div>
  );
}
```

### 의존성 배열 이해하기

```jsx
// 1. 빈 배열 [] - 컴포넌트 마운트 시에만 실행
useEffect(() => {
  console.log('컴포넌트가 마운트되었습니다');
}, []);

// 2. 배열 없음 - 매 렌더링마다 실행
useEffect(() => {
  console.log('매 렌더링마다 실행됩니다');
});

// 3. [value] - value가 변경될 때마다 실행
useEffect(() => {
  console.log('count가 변경되었습니다:', count);
}, [count]);
```

### 클린업 함수

```jsx
useEffect(() => {
  // 타이머 설정
  const timer = setInterval(() => {
    console.log('1초마다 실행');
  }, 1000);

  // 이벤트 리스너 추가
  const handleResize = () => {
    console.log('화면 크기가 변경되었습니다');
  };
  window.addEventListener('resize', handleResize);

  // 클린업 함수 - 컴포넌트 언마운트 또는 의존성 변경 시 실행
  return () => {
    clearInterval(timer);
    window.removeEventListener('resize', handleResize);
  };
}, []);
```

## 🌐 useContext 훅

`useContext`는 React Context를 함수형 컴포넌트에서 사용할 수 있게 해주는 훅입니다.

### Context 생성 및 사용

```jsx
import { createContext, useContext, useState } from 'react';

// 1. Context 생성
const ThemeContext = createContext();

// 2. Provider 컴포넌트
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(prevTheme => prevTheme === 'light' ? 'dark' : 'light');
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// 3. Context 사용하는 컴포넌트
function ThemedButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <button
      className={`btn btn-${theme}`}
      onClick={toggleTheme}
    >
      현재 테마: {theme}
    </button>
  );
}

// 4. 앱에서 사용
function App() {
  return (
    <ThemeProvider>
      <div className="app">
        <h1>테마 변경 예제</h1>
        <ThemedButton />
      </div>
    </ThemeProvider>
  );
}
```

## 🔧 커스텀 훅 만들기

반복되는 로직을 커스텀 훅으로 추출하여 재사용할 수 있습니다.

### useLocalStorage 훅

```jsx
import { useState, useEffect } from 'react';

function useLocalStorage(key, initialValue) {
  // localStorage에서 초기값 읽기
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error('localStorage에서 데이터를 읽는데 실패했습니다:', error);
      return initialValue;
    }
  });

  // 값 설정 함수
  const setValue = (value) => {
    try {
      // 함수인 경우 실행하여 값 얻기
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error('localStorage에 데이터를 저장하는데 실패했습니다:', error);
    }
  };

  return [storedValue, setValue];
}

// 사용 예시
function Settings() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  const [language, setLanguage] = useLocalStorage('language', 'ko');

  return (
    <div>
      <h2>설정</h2>
      <div>
        <label>테마: </label>
        <select value={theme} onChange={(e) => setTheme(e.target.value)}>
          <option value="light">라이트</option>
          <option value="dark">다크</option>
        </select>
      </div>
      
      <div>
        <label>언어: </label>
        <select value={language} onChange={(e) => setLanguage(e.target.value)}>
          <option value="ko">한국어</option>
          <option value="en">English</option>
        </select>
      </div>
    </div>
  );
}
```

### useFetch 훅

```jsx
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        setError(null);
        
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error.message);
      } finally {
        setLoading(false);
      }
    };

    if (url) {
      fetchData();
    }
  }, [url]);

  return { data, loading, error };
}

// 사용 예시
function PostList() {
  const { data: posts, loading, error } = useFetch('/api/posts');

  if (loading) return <div>로딩 중...</div>;
  if (error) return <div>에러: {error}</div>;

  return (
    <div>
      {posts?.map(post => (
        <article key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.content}</p>
        </article>
      ))}
    </div>
  );
}
```

## 🚀 최적화 팁

### 1. 불필요한 리렌더링 방지

```jsx
import { memo, useCallback, useMemo } from 'react';

const ExpensiveComponent = memo(({ data, onUpdate }) => {
  // 비용이 많이 드는 계산을 메모이제이션
  const processedData = useMemo(() => {
    console.log('데이터 처리 중...');
    return data.map(item => ({
      ...item,
      processed: true,
      timestamp: Date.now()
    }));
  }, [data]);

  // 콜백 함수 메모이제이션
  const handleClick = useCallback((id) => {
    onUpdate(id);
  }, [onUpdate]);

  return (
    <div>
      {processedData.map(item => (
        <div key={item.id} onClick={() => handleClick(item.id)}>
          {item.name} - {item.processed ? '처리됨' : '처리 안됨'}
        </div>
      ))}
    </div>
  );
});
```

### 2. 조건부 Effect 실행

```jsx
function UserDashboard({ userId, shouldFetch }) {
  const [userData, setUserData] = useState(null);

  useEffect(() => {
    // 조건에 따라 실행
    if (!shouldFetch || !userId) return;
    
    fetchUserData(userId)
      .then(setUserData)
      .catch(console.error);
  }, [userId, shouldFetch]);

  return <div>{/* 컴포넌트 내용 */}</div>;
}
```

### 3. 디바운싱과 함께 사용

```jsx
function SearchInput() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);

  useEffect(() => {
    if (!query.trim()) {
      setResults([]);
      return;
    }

    // 디바운싱을 위한 타이머
    const timer = setTimeout(async () => {
      try {
        const response = await fetch(`/api/search?q=${encodeURIComponent(query)}`);
        const data = await response.json();
        setResults(data.results);
      } catch (error) {
        console.error('검색 중 오류:', error);
      }
    }, 300);

    return () => clearTimeout(timer);
  }, [query]);

  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="검색어를 입력하세요..."
      />
      <ul>
        {results.map(result => (
          <li key={result.id}>{result.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

## 💡 실전 예제

### Todo 앱 만들기

```jsx
import { useState, useEffect } from 'react';

function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState('');
  const [filter, setFilter] = useState('all'); // all, active, completed

  // localStorage에서 todo 불러오기
  useEffect(() => {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      setTodos(JSON.parse(savedTodos));
    }
  }, []);

  // todos 변경시 localStorage에 저장
  useEffect(() => {
    localStorage.setItem('todos', JSON.stringify(todos));
  }, [todos]);

  const addTodo = () => {
    if (inputValue.trim()) {
      const newTodo = {
        id: Date.now(),
        text: inputValue.trim(),
        completed: false,
        createdAt: new Date().toISOString()
      };
      setTodos(prev => [...prev, newTodo]);
      setInputValue('');
    }
  };

  const toggleTodo = (id) => {
    setTodos(prev =>
      prev.map(todo =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  const deleteTodo = (id) => {
    setTodos(prev => prev.filter(todo => todo.id !== id));
  };

  const filteredTodos = todos.filter(todo => {
    if (filter === 'active') return !todo.completed;
    if (filter === 'completed') return todo.completed;
    return true;
  });

  return (
    <div className="todo-app">
      <h1>할 일 목록</h1>
      
      <div className="input-section">
        <input
          type="text"
          value={inputValue}
          onChange={(e) => setInputValue(e.target.value)}
          onKeyPress={(e) => e.key === 'Enter' && addTodo()}
          placeholder="새 할 일을 입력하세요..."
        />
        <button onClick={addTodo}>추가</button>
      </div>

      <div className="filter-section">
        <button
          className={filter === 'all' ? 'active' : ''}
          onClick={() => setFilter('all')}
        >
          전체
        </button>
        <button
          className={filter === 'active' ? 'active' : ''}
          onClick={() => setFilter('active')}
        >
          진행 중
        </button>
        <button
          className={filter === 'completed' ? 'active' : ''}
          onClick={() => setFilter('completed')}
        >
          완료됨
        </button>
      </div>

      <ul className="todo-list">
        {filteredTodos.map(todo => (
          <li key={todo.id} className={todo.completed ? 'completed' : ''}>
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => toggleTodo(todo.id)}
            />
            <span>{todo.text}</span>
            <button onClick={() => deleteTodo(todo.id)}>삭제</button>
          </li>
        ))}
      </ul>

      <div className="stats">
        <p>
          전체: {todos.length}, 
          완료: {todos.filter(t => t.completed).length}, 
          남은 일: {todos.filter(t => !t.completed).length}
        </p>
      </div>
    </div>
  );
}
```

## 📚 마무리

React Hooks는 함수형 컴포넌트의 가능성을 크게 확장시켜주는 강력한 도구입니다. 

### 핵심 포인트

1. **useState**: 상태 관리의 기본
2. **useEffect**: 사이드 이펙트 처리와 생명주기
3. **useContext**: 전역 상태 관리
4. **커스텀 훅**: 로직 재사용과 코드 구조화
5. **최적화**: 성능을 위한 메모이제이션

### 다음 단계

- **useReducer**: 복잡한 상태 로직 관리
- **useRef**: DOM 접근과 값 저장
- **useMemo & useCallback**: 성능 최적화
- **React Query/SWR**: 서버 상태 관리
- **Zustand/Redux Toolkit**: 전역 상태 관리

올바른 사용법을 익히고 최적화 기법을 적용하면 더욱 효율적이고 유지보수하기 좋은 React 애플리케이션을 만들 수 있습니다! 🚀
