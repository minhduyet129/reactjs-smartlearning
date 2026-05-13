# TÀI LIỆU REACTJS TỪ CƠ BẢN ĐẾN PRODUCTION

## Mục lục

1. [Cách dùng tài liệu này](#1-cách-dùng-tài-liệu-này)
2. [React là gì](#2-react-là-gì)
3. [Bạn cần biết gì trước khi học React](#3-bạn-cần-biết-gì-trước-khi-học-react)
4. [Khởi động dự án React](#4-khởi-động-dự-án-react)
5. [Tư duy cốt lõi của React](#5-tư-duy-cốt-lõi-của-react)
6. [Core Concepts: JSX, Component, Props, State](#6-core-concepts-jsx-component-props-state)
7. [Hooks quan trọng](#7-hooks-quan-trọng)
8. [Forms và validation](#8-forms-và-validation)
9. [React Router](#9-react-router)
10. [Data Fetching và API](#10-data-fetching-và-api)
11. [State Management](#11-state-management)
12. [TypeScript với React](#12-typescript-với-react)
13. [Testing](#13-testing)
14. [Performance Optimization](#14-performance-optimization)
15. [Code Structure và Best Practices](#15-code-structure-và-best-practices)
16. [Accessibility, Security, Error Handling](#16-accessibility-security-error-handling)
17. [Build Tools và Deployment](#17-build-tools-và-deployment)
18. [Design Patterns thường gặp](#18-design-patterns-thường-gặp)
19. [Dự án thực hành theo lộ trình](#19-dự-án-thực-hành-theo-lộ-trình)
20. [Learning Roadmap để đi làm](#20-learning-roadmap-để-đi-làm)
21. [Checklist đánh giá code quality](#21-checklist-đánh-giá-code-quality)
22. [Tài liệu tham khảo](#22-tài-liệu-tham-khảo)

---

## 1. Cách dùng tài liệu này

Tài liệu này được viết cho người mới học React nhưng vẫn đủ rộng để bạn dùng tiếp khi bước vào môi trường làm việc thực tế.

### Cách học hiệu quả

1. Học theo đúng thứ tự từ phần `2` đến phần `10`.
2. Sau mỗi phần, tự viết lại ít nhất 1 ví dụ nhỏ.
3. Sau khi nắm core concepts, bắt đầu làm dự án CRUD nhỏ.
4. Chỉ học tối ưu, architecture, CI/CD sau khi đã xây được app hoàn chỉnh.

### Nguyên tắc quan trọng

- Không cần học thuộc code mẫu.
- Cần hiểu vì sao code hoạt động.
- Ưu tiên làm dự án nhỏ liên tục hơn là chỉ đọc tài liệu.

---

## 2. React là gì

React là một thư viện JavaScript dùng để xây dựng giao diện người dùng theo mô hình component.

### Hiểu ngắn gọn

- HTML mô tả cấu trúc giao diện.
- CSS mô tả cách giao diện hiển thị.
- JavaScript mô tả hành vi.
- React giúp bạn chia giao diện thành các khối nhỏ, tái sử dụng được và dễ bảo trì hơn.

### Vì sao React phổ biến

- Có tư duy component rất rõ ràng.
- Dễ quản lý state hơn so với thao tác DOM thủ công.
- Hệ sinh thái lớn: Router, form, state management, testing, deployment.
- Được dùng rộng rãi trong doanh nghiệp.

---

## 3. Bạn cần biết gì trước khi học React

Trước khi học React, bạn nên có nền tảng:

- HTML semantic
- CSS cơ bản, responsive
- JavaScript ES6+
- Array methods như `map`, `filter`, `find`
- `Promise`, `async/await`, `fetch`
- DOM và event cơ bản

### Dấu hiệu bạn đã sẵn sàng

- Hiểu vì sao `map()` dùng để render list.
- Hiểu spread operator `...`.
- Biết object và array nên được cập nhật theo kiểu immutable.

---

## 4. Khởi động dự án React

Người mới nên bắt đầu bằng `Vite`.

```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

### Cấu trúc cơ bản

```txt
src/
  App.jsx
  main.jsx
  assets/
```

### Vai trò của từng file

- `main.jsx`: mount ứng dụng React vào DOM.
- `App.jsx`: component gốc của ứng dụng.

---

## 5. Tư duy cốt lõi của React

Đây là phần quan trọng nhất. Nếu hiểu sai tư duy, bạn sẽ thấy React khó hơn thực tế.

### 5.1 UI là hàm của state

Có thể hiểu theo công thức:

```txt
UI = f(state)
```

Nghĩa là khi state thay đổi, React sẽ render lại UI tương ứng.

### 5.2 Component là đơn vị cơ bản

Mỗi phần giao diện nên được tách thành component:

- `Header`
- `Sidebar`
- `UserCard`
- `TodoItem`

### 5.3 Dữ liệu chảy từ trên xuống

Cha truyền dữ liệu xuống con qua `props`.

```txt
App -> ProductList -> ProductCard
```

### 5.4 Không ưu tiên thao tác DOM thủ công

Trong React, bạn không ưu tiên:

```js
document.getElementById("title").innerText = "Hello";
```

Bạn ưu tiên cập nhật state để React lo phần render giao diện.

---

## 6. Core Concepts: JSX, Component, Props, State

## 6.1 JSX là gì

JSX là cú pháp cho phép bạn viết UI trong JavaScript theo cách gần giống HTML.

```jsx
const element = <h1>Hello React</h1>;
```

### Lưu ý

- JSX không phải HTML thật.
- Dùng `className` thay vì `class`.
- Dùng `{}` để chèn JavaScript vào JSX.

```jsx
const name = "An";

export default function App() {
  return <h1>Xin chào {name}</h1>;
}
```

## 6.2 Component

Component là hàm trả về JSX.

```jsx
function Welcome() {
  return <h2>Welcome to React</h2>;
}
```

### Quy tắc đặt tên

- Component phải viết hoa chữ cái đầu.
- Một component nên có một trách nhiệm chính.

## 6.3 Props

Props là dữ liệu cha truyền xuống con.

```jsx
function UserCard({ name, role }) {
  return (
    <div>
      <h3>{name}</h3>
      <p>{role}</p>
    </div>
  );
}

export default function App() {
  return <UserCard name="Ngọc" role="Frontend Developer" />;
}
```

### Cần nhớ

- Props là read-only.
- Component con không nên sửa trực tiếp props.
- Nếu cần thay đổi dữ liệu, hãy dùng state ở component cha.

## 6.4 State

State là dữ liệu nội bộ của component, có thể thay đổi theo tương tác người dùng.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Số lần bấm: {count}</p>
      <button onClick={() => setCount(count + 1)}>Tăng</button>
    </div>
  );
}
```

### Khi nào dùng state

- Hiện hoặc ẩn modal
- Dữ liệu form
- Tab đang active
- Danh sách item sau khi gọi API

## 6.5 Props vs State

| Tiêu chí | Props | State |
|---|---|---|
| Đến từ đâu | Component cha | Component tự quản lý |
| Có thay đổi được không | Không | Có |
| Dùng khi nào | Truyền dữ liệu | Quản lý trạng thái thay đổi |

## 6.6 Render danh sách

```jsx
const todos = [
  { id: 1, text: "Học JSX" },
  { id: 2, text: "Học props" },
  { id: 3, text: "Học state" }
];

function TodoList() {
  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}
```

### Vì sao cần `key`

`key` giúp React biết item nào thay đổi, thêm mới hoặc bị xóa.

## 6.7 Conditional Rendering

```jsx
function UserStatus({ isLoggedIn }) {
  return isLoggedIn ? <p>Đã đăng nhập</p> : <p>Chưa đăng nhập</p>;
}
```

## 6.8 Event Handling

```jsx
function Button() {
  const handleClick = () => {
    alert("Bạn vừa bấm nút");
  };

  return <button onClick={handleClick}>Click me</button>;
}
```

## 6.9 Mini case study: Todo item

```jsx
function TodoItem({ todo, onToggle, onDelete }) {
  return (
    <li>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggle(todo.id)}
      />
      <span>{todo.text}</span>
      <button onClick={() => onDelete(todo.id)}>Xóa</button>
    </li>
  );
}
```

Qua ví dụ trên, bạn thấy được:

- `todo` là props
- `onToggle`, `onDelete` là callback props
- Component con phát sự kiện, component cha xử lý state

---

## 7. Hooks quan trọng

Hooks cho phép functional component có thêm khả năng quản lý state, side effect, context và tối ưu.

## 7.1 `useState`

```jsx
const [isOpen, setIsOpen] = useState(false);
```

### Lỗi thường gặp

```jsx
setCount(count + 1);
setCount(count + 1);
```

Khi cập nhật dựa trên state cũ, nên dùng:

```jsx
setCount((prev) => prev + 1);
setCount((prev) => prev + 1);
```

## 7.2 `useEffect`

Dùng cho side effects:

- Gọi API
- Gắn event listener
- Đồng bộ `localStorage`
- Đổi `document.title`

```jsx
import { useEffect, useState } from "react";

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    const controller = new AbortController();

    async function fetchUser() {
      try {
        setLoading(true);
        setError("");

        const response = await fetch(`/api/users/${userId}`, {
          signal: controller.signal
        });

        if (!response.ok) {
          throw new Error("Không thể tải dữ liệu user");
        }

        const data = await response.json();
        setUser(data);
      } catch (err) {
        if (err.name !== "AbortError") {
          setError(err.message);
        }
      } finally {
        setLoading(false);
      }
    }

    fetchUser();
    return () => controller.abort();
  }, [userId]);

  if (loading) return <p>Đang tải...</p>;
  if (error) return <p>{error}</p>;

  return <h2>{user?.name}</h2>;
}
```

### Cách hiểu dependency array

- `[]`: chạy 1 lần sau mount
- `[userId]`: chạy lại khi `userId` thay đổi
- Không truyền dependency: chạy sau mọi lần render

## 7.3 `useContext`

Dùng khi nhiều component cần cùng một dữ liệu mà nếu truyền qua props sẽ rất dài dòng.

```jsx
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext(null);

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme((prev) => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

function ThemeButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return <button onClick={toggleTheme}>Theme hiện tại: {theme}</button>;
}
```

### Khi nào nên dùng Context

- Auth user
- Theme
- Ngôn ngữ
- Global UI state nhỏ

## 7.4 `useReducer`

Dùng khi state phức tạp hơn `useState`.

```jsx
import { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return initialState;
    default:
      return state;
  }
}
```

### Dùng khi

- State có nhiều trường
- Logic update có nhiều case
- Muốn tách logic state ra khỏi JSX

## 7.5 `useRef`

```jsx
import { useEffect, useRef } from "react";

function SearchInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current?.focus();
  }, []);

  return <input ref={inputRef} placeholder="Nhập từ khóa..." />;
}
```

## 7.6 `useMemo` và `useCallback`

Người mới không nên lạm dụng hai hook này quá sớm.

- `useMemo`: nhớ lại giá trị đã tính toán
- `useCallback`: nhớ lại function

Chỉ dùng khi đã có dấu hiệu re-render không cần thiết hoặc tính toán nặng.

## 7.7 Custom Hooks

Custom hook là cách tách logic dùng lại được.

```jsx
import { useEffect, useState } from "react";

function useDebounce(value, delay = 500) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}
```

---

## 8. Forms và validation

Forms xuất hiện liên tục trong dự án thật.

## 8.1 Controlled form

```jsx
import { useState } from "react";

function LoginForm() {
  const [form, setForm] = useState({
    email: "",
    password: ""
  });

  const handleChange = (event) => {
    const { name, value } = event.target;
    setForm((prev) => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log(form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="email"
        type="email"
        value={form.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <input
        name="password"
        type="password"
        value={form.password}
        onChange={handleChange}
        placeholder="Password"
      />
      <button type="submit">Đăng nhập</button>
    </form>
  );
}
```

## 8.2 Validation

Bạn thường cần:

- Required
- Email format
- Password length
- Confirm password

### Nên học thư viện nào

- Để hiểu bản chất: học form thủ công trước
- Làm việc thực tế: học `React Hook Form`
- Validation schema: kết hợp `zod`

---

## 9. React Router

React Router cho phép SPA có nhiều trang theo URL.

## 9.1 Setup cơ bản

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/about" element={<AboutPage />} />
      </Routes>
    </BrowserRouter>
  );
}
```

## 9.2 Dynamic route

```jsx
import { useParams } from "react-router-dom";

function UserDetailPage() {
  const { id } = useParams();
  return <h2>User id: {id}</h2>;
}
```

## 9.3 Protected route

```jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ user, children }) {
  if (!user) return <Navigate to="/login" replace />;
  return children;
}
```

### Người mới cần học đến đâu

- Route cơ bản
- Route động
- Nested route
- Protected route
- `useNavigate`, `useParams`

---

## 10. Data Fetching và API

Phần lớn dự án thật đều phải giao tiếp với backend.

## 10.1 Mô hình cơ bản

Bạn gần như luôn cần:

- `loading`
- `error`
- `data`

```jsx
import { useEffect, useState } from "react";

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function fetchUsers() {
      try {
        setLoading(true);
        setError("");

        const response = await fetch("/api/users");
        if (!response.ok) {
          throw new Error("Tải dữ liệu thất bại");
        }

        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchUsers();
  }, []);

  if (loading) return <p>Đang tải dữ liệu...</p>;
  if (error) return <p>Lỗi: {error}</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

## 10.2 Fetch hay Axios

### Fetch

- Có sẵn trong trình duyệt
- Đơn giản
- Đủ cho học tập và dự án nhỏ

### Axios

- Có interceptors
- Tiện khi dự án có auth token, refresh token

## 10.3 React Query / TanStack Query

Dùng khi dự án lớn hơn để:

- Cache data
- Tự refetch
- Quản lý loading / error tốt hơn
- Xử lý mutation tiện hơn

### Gợi ý học

- Bắt đầu với `fetch`
- Sau đó học `axios`
- Khi đã có CRUD app, học `React Query`

## 10.4 RESTful APIs

- `GET /users`: lấy danh sách
- `GET /users/:id`: lấy chi tiết
- `POST /users`: tạo mới
- `PUT /users/:id`: cập nhật toàn bộ
- `PATCH /users/:id`: cập nhật một phần
- `DELETE /users/:id`: xóa

## 10.5 WebSocket

Dùng cho dữ liệu real-time:

- Chat
- Notification
- Dashboard cập nhật liên tục

---

## 11. State Management

## 11.1 Chọn công cụ nào

### Mức 1: Local state

Dùng `useState` hoặc `useReducer` nếu state chỉ nằm trong một vài component gần nhau.

### Mức 2: Context API

Dùng khi state cần chia sẻ rộng nhưng chưa quá phức tạp.

### Mức 3: Redux Toolkit hoặc Zustand

Dùng khi:

- Ứng dụng lớn
- Nhiều màn hình
- Nhiều state dùng chung
- Cần cấu trúc rõ và khả năng mở rộng tốt

## 11.2 Context API

Phù hợp với:

- Theme
- Auth cơ bản
- Language
- Settings

## 11.3 Redux Toolkit

Redux Toolkit là cách hiện đại để dùng Redux.

Bạn thường sẽ có:

- `store`
- `slice`
- `actions`
- `reducers`
- `asyncThunk`

## 11.4 Zustand

Zustand gọn và dễ bắt đầu hơn Redux Toolkit.

```jsx
import { create } from "zustand";

const useCounterStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 }))
}));
```

### Gợi ý thứ tự học

- Muốn dễ tiếp cận: Context -> Zustand -> Redux Toolkit
- Muốn theo hướng doanh nghiệp phổ biến: Context -> Redux Toolkit

---

## 12. TypeScript với React

Nếu muốn đi làm lâu dài, TypeScript rất nên học.

## 12.1 Props typing

```tsx
type ButtonProps = {
  label: string;
  onClick?: () => void;
  variant?: "primary" | "secondary";
};

function Button({ label, onClick, variant = "primary" }: ButtonProps) {
  return (
    <button className={`btn-${variant}`} onClick={onClick}>
      {label}
    </button>
  );
}
```

## 12.2 State typing

```tsx
type User = {
  id: number;
  name: string;
  email: string;
};

const [users, setUsers] = useState<User[]>([]);
const [selectedUser, setSelectedUser] = useState<User | null>(null);
```

### Lợi ích

- Gợi ý code tốt hơn
- Giảm bug do sai kiểu dữ liệu
- Refactor dễ hơn
- Dễ đọc code của team

### Gợi ý học

- Học React bằng JavaScript trước
- Chuyển sang TypeScript sau khi đã hiểu bản chất React

---

## 13. Testing

Testing giúp bạn tự tin hơn khi sửa code.

## 13.1 Nên test gì

- Utility functions
- Custom hooks
- Component có logic quan trọng
- User flow chính

## 13.2 Jest và React Testing Library

- Jest: test runner và assertion ecosystem
- React Testing Library: test theo góc nhìn người dùng

```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

test("increment counter", async () => {
  const user = userEvent.setup();
  render(<Counter />);

  await user.click(screen.getByRole("button", { name: /increment/i }));
  expect(screen.getByText("Count: 1")).toBeInTheDocument();
});
```

### Nguyên tắc quan trọng

- Test hành vi, không test implementation detail
- Ưu tiên `getByRole`, `getByLabelText`
- Test loading, error, empty state

---

## 14. Performance Optimization

Người mới thường học tối ưu quá sớm. Hãy nhớ:

> Code dễ đọc và đúng trước, tối ưu sau.

## Khi nào cần tối ưu

- Re-render nhiều và thấy chậm
- List lớn
- Tính toán nặng
- Bundle quá lớn

## Công cụ phổ biến

- `React.memo`
- `useMemo`
- `useCallback`
- Code splitting với `lazy` và `Suspense`

```jsx
import { lazy, Suspense } from "react";

const ReportPage = lazy(() => import("./ReportPage"));
```

### Sai lầm phổ biến

- Bọc `useMemo` khắp nơi
- Bọc `useCallback` cho mọi function
- Tối ưu khi chưa đo được vấn đề

---

## 15. Code Structure và Best Practices

## 15.1 Cấu trúc dễ dùng cho dự án vừa

```txt
src/
  app/
    router.jsx
    providers.jsx
  components/
    common/
    forms/
    layout/
  features/
    auth/
    users/
    todos/
  hooks/
  pages/
  services/
  utils/
  constants/
  types/
```

### Cách hiểu

- `components`: UI dùng lại được
- `features`: logic theo domain
- `pages`: màn hình gắn với router
- `services`: nơi gọi API

## 15.2 Naming convention

- Component: `PascalCase`
- Hook: `useSomething`
- Function, variable: `camelCase`
- Constant: `UPPER_SNAKE_CASE`

## 15.3 Best practices quan trọng

- Một component nên có một trách nhiệm rõ
- Logic phức tạp nên tách ra helper hoặc custom hook
- Không gọi API lung tung trong nhiều component nếu có thể tách service
- Không hard-code string lặp lại ở nhiều nơi
- Luôn có loading, error, empty state

---

## 16. Accessibility, Security, Error Handling

## 16.1 Accessibility

- Dùng semantic HTML
- Input phải có `label`
- Nút phải là `button`, không dùng `div` để click
- Modal cần quản lý focus
- Kiểm tra keyboard navigation

```jsx
<label htmlFor="email">Email</label>
<input id="email" type="email" />
```

## 16.2 Security

- Không tin user input
- Không render HTML raw nếu chưa sanitize
- Không hard-code secret trong frontend
- Xử lý token cẩn thận
- Validate cả client và server

## 16.3 Error handling

Bạn nên xử lý lỗi ở 3 tầng:

1. Tầng UI: hiện thông báo lỗi cho người dùng
2. Tầng API: bắt lỗi request
3. Tầng app: Error Boundary

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h2>Có lỗi xảy ra. Vui lòng thử lại.</h2>;
    }

    return this.props.children;
  }
}
```

---

## 17. Build Tools và Deployment

## 17.1 Vite

Nên dùng cho dự án mới và đa số SPA thông thường.

## 17.2 Webpack và Babel

- Webpack: đóng gói source code
- Babel: chuyển đổi cú pháp JavaScript / JSX

Người mới không cần đào ngay vào cấu hình Webpack.

## 17.3 Deployment

Đơn giản nhất:

- Vercel
- Netlify

```bash
npm run build
```

## 17.4 CI/CD

Đây là quy trình tự động:

- cài dependency
- chạy test
- build
- deploy

Người mới nên biết khái niệm trước, chưa cần master ngay.

---

## 18. Design Patterns thường gặp

Không cần học hết ngay. Hãy ghi nhớ để khi gặp trong dự án thì nhận ra.

## 18.1 Presentational và Container

- Presentational: tập trung vào UI
- Container: tập trung vào data và logic

## 18.2 Custom Hooks Pattern

Tách logic khỏi component UI.

## 18.3 Compound Components

Dùng cho UI phức tạp như:

- Tabs
- Accordion
- Modal

## 18.4 Provider Pattern

Dùng để bao quanh app bằng các context provider.

### Thứ tự ưu tiên học

1. Component composition
2. Custom hooks
3. Provider pattern
4. Compound components
5. HOC và render props để đọc code cũ

---

## 19. Dự án thực hành theo lộ trình

## 19.1 Dự án 1: Todo App

### Mục tiêu

- Component
- Props
- State
- Event handling
- Conditional rendering
- Form
- Local storage

### Tính năng

- Thêm, sửa, xóa todo
- Đánh dấu hoàn thành
- Lọc all / active / completed
- Lưu dữ liệu `localStorage`

## 19.2 Dự án 2: Blog CRUD App

### Mục tiêu

- Router
- Fetch API / Axios
- Loading / error state
- Form validation
- Deploy

### Tính năng

- Danh sách bài viết
- Trang chi tiết
- Tạo / sửa / xóa bài viết
- Search / pagination cơ bản

## 19.3 Dự án 3: Admin Dashboard

### Mục tiêu

- Auth
- State management
- React Query
- Role-based UI
- Testing
- TypeScript
- Production structure

### Tính năng

- Login
- Dashboard cards
- Quản lý user
- Quản lý permission
- Charts
- Responsive

---

## 20. Learning Roadmap để đi làm

## Giai đoạn 1: Nền tảng JavaScript

- ES6+
- Array methods
- async/await
- object và array immutability

## Giai đoạn 2: React core

- JSX
- component
- props
- state
- render list
- event
- form

## Giai đoạn 3: Hooks

- `useState`
- `useEffect`
- `useContext`
- `useReducer`
- `useRef`

## Giai đoạn 4: Làm 1 CRUD app

- Router
- API
- loading / error / empty state
- deploy lên Vercel / Netlify

## Giai đoạn 5: State management và testing

- Context
- Redux Toolkit hoặc Zustand
- React Query
- Jest + React Testing Library

## Giai đoạn 6: Production mindset

- TypeScript
- performance
- accessibility
- security
- CI/CD

### Mục tiêu cuối cùng

Bạn có thể:

- đọc hiểu code React của người khác
- tự xây dựng một app hoàn chỉnh
- biết cách tổ chức dự án
- biết debug, test và deploy

---

## 21. Checklist đánh giá code quality

## 21.1 React fundamentals

- [ ] Component có tên rõ ràng
- [ ] Props và state được tách rõ
- [ ] Không mutate state trực tiếp
- [ ] Dùng `key` đúng trong list
- [ ] Không đặt quá nhiều logic vào một component

## 21.2 UX và UI

- [ ] Có loading state
- [ ] Có error state
- [ ] Có empty state
- [ ] Form có validate
- [ ] Responsive trên mobile

## 21.3 Code maintainability

- [ ] Cấu trúc thư mục dễ tìm
- [ ] Tên file, hook, component thống nhất
- [ ] Logic lặp lại đã được tách ra
- [ ] Gọi API đã được tách thành service nếu cần

## 21.4 Production readiness

- [ ] Có test cho logic quan trọng
- [ ] Có Error Boundary
- [ ] Có xử lý auth cơ bản
- [ ] Không hard-code secret
- [ ] Đã tối ưu những nơi thực sự cần

## 21.5 Accessibility và security

- [ ] Input có label
- [ ] Button dùng semantic đúng
- [ ] Không dùng `dangerouslySetInnerHTML` bừa bãi
- [ ] Validate input người dùng
- [ ] Có thể thao tác bằng bàn phím

---

## 22. Tài liệu tham khảo

1. [React Official Documentation](https://react.dev)
2. [React Router Documentation](https://reactrouter.com)
3. [Redux Toolkit Documentation](https://redux-toolkit.js.org)
4. [TanStack Query Documentation](https://tanstack.com/query)
5. [React Hook Form Documentation](https://react-hook-form.com)
6. [Testing Library Documentation](https://testing-library.com)
7. [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook)

---

## Tổng kết

Nếu bạn là người mới, đừng cố học hết React trong một lần đọc.

Hãy nhớ thứ tự:

1. Hiểu `component`, `props`, `state`
2. Hiểu `useEffect` và API
3. Làm 1 CRUD app
4. Học router, global state, testing
5. Sau cùng mới đào sâu tối ưu, architecture, deployment và patterns

> React không khó vì cú pháp. React khó ở chỗ bạn phải hiểu cách dữ liệu chảy, state thay đổi và giao diện được tổ chức.

Nếu bạn đi đúng thứ tự, React sẽ dễ hơn rất nhiều.

---

*Document created: 2026-05-13*  
*Last updated: 2026-05-13*  
*Version: 2.1*
