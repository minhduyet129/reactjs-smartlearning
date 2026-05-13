# TÀI LIỆU TOÀN DIỆN VỀ REACTJS

## Mục lục

1. [Giới thiệu về ReactJS](#1-giới-thiệu-về-reactjs)
2. [Core Concepts](#2-core-concepts)
3. [State Management](#3-state-management)
4. [Routing với React Router](#4-routing-với-react-router)
5. [Data Fetching](#5-data-fetching)
6. [Performance Optimization](#6-performance-optimization)
7. [Testing](#7-testing)
8. [Build Tools và Development Workflow](#8-build-tools-và-development-workflow)
9. [TypeScript Integration](#9-typescript-integration)
10. [Best Practices và Code Structure](#10-best-practices-và-code-structure)
11. [Security Considerations](#11-security-considerations)
12. [Accessibility (a11y)](#12-accessibility-a11y)
13. [Design Patterns](#13-design-patterns)
14. [Deployment Strategies](#14-deployment-strategies)
15. [Learning Roadmap](#15-learning-roadmap)
16. [Checklist đánh giá Code Quality](#16-checklist-đánh-giá-code-quality)

---

## 1. Giới thiệu về ReactJS

### 1.1 ReactJS là gì?

ReactJS là một thư viện JavaScript mã nguồn mở được phát triển bởi Facebook (Meta) để xây dựng giao diện người dùng (UI). React sử dụng mô hình **Component-Based Architecture** và **Declarative Programming**, giúp lập trình viên xây dựng các ứng dụng web phức tạp một cách dễ dàng và có tổ chức.

### 1.2 Tại sao nên học ReactJS?

| Ưu điểm | Mô tả |
|---------|-------|
| Virtual DOM | React sử dụng Virtual DOM để tối ưu hóa việc cập nhật giao diện, chỉ re-render những phần thực sự thay đổi |
| Component Reusability | Tái sử dụng component giúp giảm code trùng lặp và dễ bảo trì |
| Ecosystem phong phú | Hệ sinh thái lớn với nhiều thư viện hỗ trợ |
| Hỗ trợ TypeScript | React có hỗ trợ TypeScript tốt từ đầu |
| Cộng đồng lớn | Cộng đồng developer lớn, nhiều tài liệu và hỗ trợ |
| Job Market | Nhu cầu tuyển dụng cao trên thị trường lao động |

---

## 2. Core Concepts

### 2.1 Components

#### 2.1.1 Functional Components

```jsx
function Welcome({ name, age }) {
  return (
    <div className="welcome-container">
      <h1>Xin chào, {name}!</h1>
      <p>Tuổi: {age}</p>
    </div>
  );
}

const UserCard = ({ username, avatar, role }) => {
  return (
    <div className="user-card">
      <img src={avatar} alt={`${username}'s avatar`} />
      <h2>{username}</h2>
      <span className="role-badge">{role}</span>
    </div>
  );
};
```

#### 2.1.2 Class Components

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    this.handleIncrement = this.handleIncrement.bind(this);
  }

  handleIncrement() {
    this.setState(prevState => ({ count: prevState.count + 1 }));
  }

  render() {
    return (
      <div className="counter">
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleIncrement}>Increment</button>
      </div>
    );
  }
}
```

#### 2.1.3 Component Composition

```jsx
const Card = ({ title, children, footer }) => {
  return (
    <div className="card">
      <div className="card-header"><h3>{title}</h3></div>
      <div className="card-body">{children}</div>
      {footer && <div className="card-footer">{footer}</div>}
    </div>
  );
};

const Modal = ({ isOpen, onClose, children }) => {
  if (!isOpen) return null;
  return (
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={e => e.stopPropagation()}>
        <button onClick={onClose}>×</button>
        {children}
      </div>
    </div>
  );
};
```

#### 2.1.4 Pure Components

```jsx
const PureUserCard = React.memo(({ user, onSelect }) => {
  return (
    <div onClick={() => onSelect(user.id)}>
      <span>{user.name}</span>
    </div>
  );
});
```

### 2.2 Props

#### 2.2.1 Props cơ bản

```jsx
const UserProfile = ({ name, email, avatar, role }) => {
  return (
    <div className="user-profile">
      <img src={avatar} alt={name} />
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
};

const App = () => {
  return <UserProfile name="Nguyễn Văn A" email="email@example.com" />;
};
```

#### 2.2.2 PropTypes

```jsx
import PropTypes from 'prop-types';

const Button = ({ label, variant = 'primary', disabled = false }) => {
  return <button className={`btn-${variant}`} disabled={disabled}>{label}</button>;
};

Button.propTypes = {
  label: PropTypes.string.isRequired,
  variant: PropTypes.oneOf(['primary', 'secondary', 'danger']),
  disabled: PropTypes.bool
};
```

#### 2.2.3 Render Props

```jsx
const MouseTracker = ({ render }) => {
  const [position, setPosition] = useState({ x: 0, y: 0 });
  useEffect(() => {
    const handleMouseMove = (e) => setPosition({ x: e.clientX, y: e.clientY });
    window.addEventListener('mousemove', handleMouseMove);
    return () => window.removeEventListener('mousemove', handleMouseMove);
  }, []);
  return render(position);
};

const App = () => {
  return (
    <MouseTracker render={({ x, y }) => <div>Mouse: ({x}, {y})</div>} />
  );
};
```

### 2.3 State

#### 2.3.1 useState

```jsx
const Counter = () => {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(prev => prev + 1)}>+</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
};

const UserForm = () => {
  const [formData, setFormData] = useState({ username: '', email: '' });
  const handleChange = (e) => {
    setFormData(prev => ({ ...prev, [e.target.name]: e.target.value }));
  };
  return (
    <form>
      <input name="username" value={formData.username} onChange={handleChange} />
      <input name="email" value={formData.email} onChange={handleChange} />
    </form>
  );
};
```

#### 2.3.2 State vs Props

| Aspect | State | Props |
|--------|-------|-------|
| Mục đích | Lưu trữ dữ liệu nội bộ | Truyền dữ liệu cha → con |
| Thay đổi | Có thể thay đổi trong component | Read-only |
| Re-render | State thay đổi → Re-render | Props thay đổi → Re-render |

#### 2.3.3 Lifting State Up

```jsx
const TemperatureCalculator = () => {
  const [celsius, setCelsius] = useState('');
  const handleCelsiusChange = (value) => {
    setCelsius(value);
  };
  return (
    <div>
      <TemperatureInput label="Celsius" value={celsius} onChange={handleCelsiusChange} />
    </div>
  );
};

const TemperatureInput = ({ label, value, onChange }) => {
  return (
    <div>
      <label>{label}: </label>
      <input value={value} onChange={e => onChange(e.target.value)} />
    </div>
  );
};
```

### 2.4 Component Lifecycle

#### 2.4.1 Class Lifecycle

```
Mounting → constructor() → render() → componentDidMount()
Updating → render() → componentDidUpdate()
Unmounting → componentWillUnmount()
```

#### 2.4.2 Hooks Lifecycle (useEffect)

```jsx
useEffect(() => {
  // componentDidMount + componentDidUpdate
  return () => {
    // componentWillUnmount
  };
}, [dependency]);
```

### 2.5 Hooks Chi Tiết

#### 2.5.1 useState

```jsx
const [state, setState] = useState(initialValue);
const increment = () => setState(prev => prev + 1);
```

#### 2.5.2 useEffect

```jsx
const UserProfile = ({ userId }) => {
  const [user, setUser] = useState(null);

  useEffect(() => {
    let isMounted = true;
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => isMounted && setUser(data));
    return () => { isMounted = false; };
  }, [userId]);

  return user ? <div>{user.name}</div> : <div>Loading...</div>;
};
```

#### 2.5.3 useContext

```jsx
const ThemeContext = createContext({ theme: 'light', toggleTheme: () => {} });

const ThemedButton = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return <button className={`btn-${theme}`} onClick={toggleTheme}>Toggle</button>;
};
```

#### 2.5.4 useReducer

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT': return { count: state.count + 1 };
    case 'DECREMENT': return { count: state.count - 1 };
    default: return state;
  }
};

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  return (
    <div>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
    </div>
  );
};
```

#### 2.5.5 useCallback

```jsx
const handleClick = useCallback((id) => {
  console.log('Clicked:', id);
}, []);
```

#### 2.5.6 useMemo

```jsx
const filteredItems = useMemo(() => {
  return items.filter(item => item.completed);
}, [items]);
```

#### 2.5.7 useRef

```jsx
const AutoFocusInput = () => {
  const inputRef = useRef(null);
  useEffect(() => { inputRef.current?.focus(); }, []);
  return <input ref={inputRef} />;
};
```

#### 2.5.8 Custom Hooks

```jsx
const useLocalStorage = (key, initialValue) => {
  const [value, setValue] = useState(() => {
    try { return JSON.parse(localStorage.getItem(key)) || initialValue; }
    catch { return initialValue; }
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
};

const useFetch = (url) => {
  const [state, setState] = useState({ data: null, loading: true, error: null });

  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(data => setState({ data, loading: false, error: null }))
      .catch(error => setState({ data: null, loading: false, error }));
  }, [url]);

  return state;
};

const useDebounce = (value, delay) => {
  const [debouncedValue, setDebouncedValue] = useState(value);
  useEffect(() => {
    const timer = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);
  return debouncedValue;
};
```

---

## 3. State Management

### 3.1 Context API

```jsx
const AuthContext = createContext(null);

const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const login = (credentials) => {
    return authService.login(credentials).then(res => {
      setUser(res.user);
      return res;
    });
  };
  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

const useAuth = () => useContext(AuthContext);
```

### 3.2 Redux Toolkit

```jsx
import { configureStore, createSlice, createAsyncThunk } from '@reduxjs/toolkit';

const usersSlice = createSlice({
  name: 'users',
  initialState: { items: [], loading: false, error: null },
  reducers: {
    addUser: (state, action) => { state.items.push(action.payload); },
    removeUser: (state, action) => { state.items = state.items.filter(u => u.id !== action.payload); },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => { state.loading = true; })
      .addCase(fetchUsers.fulfilled, (state, action) => { state.items = action.payload; state.loading = false; })
      .addCase(fetchUsers.rejected, (state, action) => { state.error = action.error.message; state.loading = false; });
  }
});

export const fetchUsers = createAsyncThunk('users/fetch', async () => {
  const res = await fetch('/api/users');
  return res.json();
});

export const { addUser, removeUser } = usersSlice.actions;
export const selectUsers = (state) => state.users.items;

export const store = configureStore({
  reducer: { users: usersSlice.reducer }
});
```

### 3.3 Zustand

```jsx
import { create } from 'zustand';

const useStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
  user: null,
  setUser: (user) => set({ user }),
}));

const Counter = () => {
  const { count, increment } = useStore();
  return <button onClick={increment}>{count}</button>;
};
```

---

## 4. React Router

### 4.1 Setup và Routes

```jsx
import { BrowserRouter, Routes, Route, Link, NavLink } from 'react-router-dom';

const App = () => {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
        <NavLink to="/users" className={({ isActive }) => isActive ? 'active' : ''}>Users</NavLink>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users" element={<Users />} />
        <Route path="/users/:id" element={<UserDetail />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
};
```

### 4.2 Dynamic Routes

```jsx
const UserDetail = () => {
  const { id } = useParams();
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`/api/users/${id}`).then(res => res.json()).then(setUser);
  }, [id]);

  return user ? <div><h2>{user.name}</h2></div> : <div>Loading...</div>;
};
```

### 4.3 Nested Routes

```jsx
const App = () => {
  return (
    <Routes>
      <Route path="/dashboard" element={<Dashboard />}>
        <Route index element={<DashboardHome />} />
        <Route path="analytics" element={<Analytics />} />
        <Route path="reports" element={<Reports />} />
      </Route>
    </Routes>
  );
};

const Dashboard = () => {
  return (
    <div>
      <h1>Dashboard</h1>
      <Outlet />
    </div>
  );
};
```

### 4.4 Navigation

```jsx
const navigate = useNavigate();
navigate('/home');
navigate('/users', { replace: true });
navigate(-1);

const location = useLocation();
console.log(location.pathname);
```

### 4.5 Protected Routes

```jsx
const ProtectedRoute = ({ children, isAuthenticated }) => {
  if (!isAuthenticated) return <Navigate to="/login" replace />;
  return children;
};

const App = () => {
  return (
    <Routes>
      <Route path="/login" element={<Login />} />
      <Route path="/dashboard" element={
        <ProtectedRoute isAuthenticated={user !== null}>
          <Dashboard />
        </ProtectedRoute>
      } />
    </Routes>
  );
};
```

---

## 5. Data Fetching

### 5.1 Fetch API

```jsx
const fetchUsers = async () => {
  try {
    const response = await fetch('/api/users');
    if (!response.ok) throw new Error('Failed to fetch');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
};

const UsersComponent = () => {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetchUsers()
      .then(data => setUsers(data))
      .catch(err => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  return <ul>{users.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
};
```

### 5.2 Axios

```jsx
import axios from 'axios';

const api = axios.create({
  baseURL: '/api',
  timeout: 10000,
  headers: { 'Content-Type': 'application/json' }
});

api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

const fetchUsers = () => api.get('/users');
const createUser = (data) => api.post('/users', data);
const updateUser = (id, data) => api.put(`/users/${id}`, data);
const deleteUser = (id) => api.delete(`/users/${id}`);
```

### 5.3 React Query

```jsx
import { QueryClient, QueryClientProvider, useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 5 * 60 * 1000,
      retry: 3,
      refetchOnWindowFocus: false,
    },
  },
});

const Users = () => {
  const { data, isLoading, error } = useQuery({
    queryKey: ['users'],
    queryFn: () => fetch('/api/users').then(res => res.json()),
  });

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  return <ul>{data.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
};

const CreateUser = () => {
  const queryClient = useQueryClient();
  const mutation = useMutation({
    mutationFn: (newUser) => fetch('/api/users', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(newUser),
    }).then(res => res.json()),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['users'] });
    },
  });

  return (
    <button onClick={() => mutation.mutate({ name: 'New User' })}>
      Create User
    </button>
  );
};
```

### 5.4 SWR

```jsx
import useSWR from 'swr';

const fetcher = (url) => fetch(url).then(res => res.json());

const UserProfile = ({ userId }) => {
  const { data, error, isLoading } = useSWR(`/api/users/${userId}`, fetcher);

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error loading user</div>;
  return <div><h2>{data.name}</h2></div>;
};
```

---

## 6. Performance Optimization

### 6.1 React.memo

```jsx
const MemoizedComponent = React.memo(({ data, onClick }) => {
  return <div onClick={onClick}>{data.name}</div>;
});
```

### 6.2 useMemo

```jsx
const sortedData = useMemo(() => {
  return [...items].sort((a, b) => a.name.localeCompare(b.name));
}, [items]);
```

### 6.3 useCallback

```jsx
const handleClick = useCallback((id) => {
  console.log('Clicked:', id);
}, []);
```

### 6.4 Code Splitting

```jsx
import { lazy, Suspense } from 'react';

const LazyComponent = lazy(() => import('./HeavyComponent'));

const App = () => {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
};
```

### 6.5 useTransition

```jsx
import { useTransition } from 'react';

const TabComponent = () => {
  const [isPending, startTransition] = useTransition();
  const [tab, setTab] = useState('about');

  const handleTabChange = (newTab) => {
    startTransition(() => {
      setTab(newTab);
    });
  };

  return (
    <div>
      <button onClick={() => handleTabChange('about')}>About</button>
      <button onClick={() => handleTabChange('contact')}>Contact</button>
      {isPending ? <div>Loading...</div> : <TabContent tab={tab} />}
    </div>
  );
};
```

### 6.6 Lazy Loading Images

```jsx
const LazyImage = ({ src, alt }) => {
  const [isLoaded, setIsLoaded] = useState(false);
  return (
    <img
      src={src}
      alt={alt}
      loading="lazy"
      onLoad={() => setIsLoaded(true)}
      className={isLoaded ? 'loaded' : 'loading'}
    />
  );
};
```

---

## 7. Testing

### 7.1 Jest Basics

```jsx
test('adds 1 + 2 to equal 3', () => {
  expect(1 + 2).toBe(3);
});

test('object assignment', () => {
  const data = { one: 1 };
  data['two'] = 2;
  expect(data).toEqual({ one: 1, two: 2 });
});
```

### 7.2 React Testing Library

```jsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

test('renders counter with initial value', () => {
  render(<Counter initialCount={0} />);
  expect(screen.getByText('Count: 0')).toBeInTheDocument();
});

test('increments counter', async () => {
  render(<Counter initialCount={0} />);
  const button = screen.getByRole('button', { name: 'Increment' });
  fireEvent.click(button);
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});

test('form submission', async () => {
  render(<LoginForm />);
  await userEvent.type(screen.getByLabelText(/username/i), 'john');
  await userEvent.type(screen.getByLabelText(/password/i), 'password123');
  await userEvent.click(screen.getByRole('button', { name: /submit/i }));
});
```

### 7.3 Testing Async Code

```jsx
test('fetches and displays users', async () => {
  render(<Users />);
  expect(screen.getByText(/loading/i)).toBeInTheDocument();
  const users = await waitFor(() => screen.getAllByRole('listitem'));
  expect(users).toHaveLength(2);
});
```

### 7.4 Testing Custom Hooks

```jsx
import { renderHook, act } from '@testing-library/react';
import { useCounter } from './useCounter';

test('should increment', () => {
  const { result } = renderHook(() => useCounter());
  act(() => result.current.increment());
  expect(result.current.count).toBe(1);
});
```

---

## 8. Build Tools

### 8.1 Vite

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
npm run build
```

### 8.2 Webpack Configuration

```javascript
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.[contenthash].js',
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: { loader: 'babel-loader' },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
};
```

### 8.3 Babel Configuration

```json
{
  "presets": [
    "@babel/preset-env",
    ["@babel/preset-react", { "runtime": "automatic" }]
  ]
}
```

---

## 9. TypeScript Integration

### 9.1 Component Props

```tsx
interface ButtonProps {
  label: string;
  variant?: 'primary' | 'secondary';
  onClick?: () => void;
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ label, variant = 'primary', onClick, disabled }) => {
  return (
    <button className={`btn-${variant}`} onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
};
```

### 9.2 State Types

```tsx
interface User {
  id: string;
  name: string;
  email: string;
  role: 'admin' | 'user';
}

const [users, setUsers] = useState<User[]>([]);
const [selectedUser, setSelectedUser] = useState<User | null>(null);
```

### 9.3 Custom Hooks

```tsx
interface UseLocalStorageReturn<T> {
  value: T;
  setValue: (value: T | ((prev: T) => T)) => void;
}

function useLocalStorage<T>(key: string, initialValue: T): UseLocalStorageReturn<T> {
  const [value, setValue] = useState<T>(() => {
    const stored = localStorage.getItem(key);
    return stored ? JSON.parse(stored) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return { value, setValue };
}
```

---

## 10. Best Practices

### 10.1 Project Structure

```
src/
├── components/       # Reusable UI components
│   ├── Button/
│   ├── Modal/
│   └── Card/
├── pages/            # Route components
│   ├── Home/
│   ├── About/
│   └── Users/
├── hooks/            # Custom hooks
├── contexts/         # Context providers
├── services/         # API calls
├── utils/            # Helper functions
├── types/            # TypeScript types
└── styles/           # Global styles
```

### 10.2 Naming Conventions

```jsx
// Components: PascalCase
const UserProfile = () => {};

// Hooks: camelCase với prefix "use"
const useAuth = () => {};
const useFetch = (url) => {};

// Constants: SCREAMING_SNAKE_CASE
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = '/api';

// Files: kebab-case
// user-profile.tsx, use-auth.ts, api-service.ts
```

### 10.3 Error Handling

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <div>Something went wrong.</div>;
    }
    return this.props.children;
  }
}
```

### 10.4 Responsive Design

```jsx
const useMediaQuery = (query) => {
  const [matches, setMatches] = useState(window.matchMedia(query).matches);
  useEffect(() => {
    const mq = window.matchMedia(query);
    const handler = (e) => setMatches(e.matches);
    mq.addEventListener('change', handler);
    return () => mq.removeEventListener('change', handler);
  }, [query]);
  return matches;
};

const ResponsiveComponent = () => {
  const isMobile = useMediaQuery('(max-width: 768px)');
  const isTablet = useMediaQuery('(min-width: 769px) and (max-width: 1024px)');

  return (
    <div>
      {isMobile && <MobileLayout />}
      {isTablet && <TabletLayout />}
      {!isMobile && !isTablet && <DesktopLayout />}
    </div>
  );
};
```

---

## 11. Security Considerations

### 11.1 XSS Prevention

```jsx
// ❌ Dangerous - raw HTML
const DangerousComponent = ({ content }) => {
  return <div dangerouslySetInnerHTML={{ __html: content }} />;
};

// ✅ Safe - sanitize HTML hoặc escape
const SafeComponent = ({ content }) => {
  return <div>{content}</div>;
};
```

### 11.2 CSRF Protection

```jsx
const api = axios.create({ baseURL: '/api' });
api.interceptors.request.use((config) => {
  const token = document.querySelector('meta[name="csrf-token"]')?.content;
  if (token) config.headers['X-CSRF-Token'] = token;
  return config;
});
```

### 11.3 Authentication

```jsx
const ProtectedRoute = ({ children }) => {
  const { user, loading } = useAuth();

  if (loading) return <div>Loading...</div>;
  if (!user) return <Navigate to="/login" />;
  return children;
};
```

### 11.4 Input Validation

```jsx
import { z } from 'zod';

const userSchema = z.object({
  email: z.string().email('Invalid email format'),
  password: z.string().min(8, 'Password must be at least 8 characters'),
  age: z.number().min(18, 'Must be at least 18'),
});

const validateUser = (data) => {
  const result = userSchema.safeParse(data);
  if (!result.success) {
    return { valid: false, errors: result.error.flatten() };
  }
  return { valid: true, data: result.data };
};
```

---

## 12. Accessibility (a11y)

### 12.1 Semantic HTML

```jsx
// ❌ Bad
<div onClick={onClick}>Click me</div>

// ✅ Good
<button onClick={onClick}>Click me</button>
```

### 12.2 ARIA Labels

```jsx
<button aria-label="Close modal" onClick={onClose}>
  <span aria-hidden="true">×</span>
</button>

<input
  type="text"
  aria-label="Search"
  aria-describedby="search-hint"
/>
<p id="search-hint">Type to search for items</p>
```

### 12.3 Keyboard Navigation

```jsx
const KeyboardNav = () => {
  const [focusIndex, setFocusIndex] = useState(0);

  useEffect(() => {
    const handleKeyDown = (e) => {
      if (e.key === 'ArrowDown') setFocusIndex(prev => (prev + 1) % items.length);
      if (e.key === 'ArrowUp') setFocusIndex(prev => (prev - 1 + items.length) % items.length);
    };
    window.addEventListener('keydown', handleKeyDown);
    return () => window.removeEventListener('keydown', handleKeyDown);
  }, []);

  return (
    <div role="listbox" tabIndex={0}>
      {items.map((item, index) => (
        <div
          key={item.id}
          role="option"
          aria-selected={index === focusIndex}
          tabIndex={index === focusIndex ? 0 : -1}
        >
          {item.name}
        </div>
      ))}
    </div>
  );
};
```

### 12.4 Focus Management

```jsx
const Modal = ({ isOpen, onClose }) => {
  const modalRef = useRef(null);

  useEffect(() => {
    if (isOpen) {
      modalRef.current?.focus();
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = 'auto';
    }
  }, [isOpen]);

  return isOpen ? (
    <div ref={modalRef} tabIndex={-1} role="dialog" aria-modal="true">
      <button onClick={onClose}>Close</button>
    </div>
  ) : null;
};
```

---

## 13. Design Patterns

### 13.1 Container/Presentational

```jsx
const UserListContainer = () => {
  const [users, setUsers] = useState([]);
  useEffect(() => { fetchUsers().then(setUsers); }, []);
  return <UserListPresenter users={users} />;
};

const UserListPresenter = ({ users }) => {
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
};
```

### 13.2 Higher Order Components

```jsx
const withLoading = (Component) => {
  return ({ isLoading, ...props }) => {
    if (isLoading) return <div>Loading...</div>;
    return <Component {...props} />;
  };
};

const UserListWithLoading = withLoading(UserList);
```

### 13.3 Compound Components

```jsx
const Tabs = ({ children }) => {
  const [activeTab, setActiveTab] = useState(0);
  return (
    <TabsContext.Provider value={{ activeTab, setActiveTab }}>
      {children}
    </TabsContext.Provider>
  );
};

Tabs.TabList = ({ children }) => <div role="tablist">{children}</div>;
Tabs.Tab = ({ label, index }) => {
  const { activeTab, setActiveTab } = useContext(TabsContext);
  return (
    <button
      role="tab"
      aria-selected={activeTab === index}
      onClick={() => setActiveTab(index)}
    >
      {label}
    </button>
  );
};
Tabs.TabPanel = ({ index, children }) => {
  const { activeTab } = useContext(TabsContext);
  return activeTab === index ? <div>{children}</div> : null;
};
```

### 13.4 Provider Pattern

```jsx
const AppProvider = ({ children }) => {
  return (
    <AuthProvider>
      <ThemeProvider>
        <ToastProvider>
          {children}
        </ToastProvider>
      </ThemeProvider>
    </AuthProvider>
  );
};
```

---

## 14. Deployment Strategies

### 14.1 Vercel

```bash
npm install -g vercel
vercel --prod
```

### 14.2 Netlify

```bash
npm install -g netlify-cli
netlify deploy --prod
```

### 14.3 Docker

```dockerfile
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### 14.4 CI/CD Pipeline

```yaml
# GitHub Actions
name: CI/CD
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
      - name: Build
        run: npm run build
      - name: Deploy
        run: npm run deploy
```

---

## 15. Learning Roadmap

```
Giai đoạn 1: Cơ bản (2-3 tuần)
├── HTML/CSS nâng cao
├── JavaScript ES6+
├── DOM Manipulation
└── Async JavaScript (Promises, async/await)

Giai đoạn 2: React Fundamentals (3-4 tuần)
├── Components (Functional & Class)
├── JSX
├── Props và State
├── Event Handling
├── Conditional Rendering
├── Lists và Keys
└── Forms cơ bản

Giai đoạn 3: React Hooks (2-3 tuần)
├── useState, useEffect
├── useContext
├── useReducer
├── useCallback, useMemo
├── useRef
└── Custom Hooks

Giai đoạn 4: React Router (1-2 tuần)
├── Basic Routing
├── Dynamic Routes
├── Nested Routes
├── Protected Routes
└── Navigation

Giai đoạn 5: State Management (2-3 tuần)
├── Context API
├── Redux Toolkit
├── Zustand
└── React Query/SWR

Giai đoạn 6: Advanced Topics (3-4 tuần)
├── Performance Optimization
├── Testing (Jest, RTL)
├── TypeScript
├── Security Best Practices
├── Accessibility
└── Design Patterns

Giai đoạn 7: Build & Deploy (1-2 tuần)
├── Vite/Webpack
├── Docker
├── Vercel/Netlify
├── CI/CD
└── Monitoring
```

---

## 16. Checklist Đánh Giá Code Quality

### 16.1 Functionality
- [ ] Component hoạt động đúng như mong đợi
- [ ] Xử lý tất cả edge cases
- [ ] Error handling đầy đủ
- [ ] Loading states được hiển thị
- [ ] Empty states được xử lý

### 16.2 Code Structure
- [ ] Component có một responsibility duy nhất
- [ ] KHÔNG có code trùng lặp (DRY)
- [ ] Tên biến và hàm có ý nghĩa (meaningful names)
- [ ] KHÔNG có commented-out code
- [ ] Import statements có tổ chức

### 16.3 Performance
- [ ] KHÔNG có unnecessary re-renders
- [ ] useMemo/useCallback được sử dụng khi cần thiết
- [ ] Images được lazy load
- [ ] Heavy computations được memoized
- [ ] Code splitting được áp dụng

### 16.4 React Best Practices
- [ ] Functional components thay vì Class components
- [ ] Props là read-only
- [ ] State updates là immutable
- [ ] Side effects trong useEffect
- [ ] Cleanup functions trong useEffect

### 16.5 TypeScript
- [ ] Props được type correctly
- [ ] State có kiểu rõ ràng
- [ ] KHÔNG có any types không cần thiết
- [ ] Interfaces/types được tái sử dụng

### 16.6 Security
- [ ] User input được validate
- [ ] KHÔNG có sensitive data hardcoded
- [ ] XSS prevention
- [ ] Authentication/Authorization checks

### 16.7 Accessibility
- [ ] Semantic HTML được sử dụng
- [ ] ARIA labels khi cần thiết
- [ ] Keyboard navigation hoạt động
- [ ] Color contrast đủ
- [ ] Screen reader compatible

### 16.8 Testing
- [ ] Unit tests cho custom hooks
- [ ] Component tests cho UI logic
- [ ] Integration tests cho user flows
- [ ] Coverage đạt >80%

### 16.9 Documentation
- [ ] Components có JSDoc comments
- [ ] Complex logic có giải thích
- [ ] README với setup instructions
- [ ] API documentation

---

## Tài Liệu Tham Khảo

1. [React Official Documentation](https://react.dev)
2. [React Hooks API Reference](https://react.dev/reference/react)
3. [React Router Documentation](https://reactrouter.com)
4. [Redux Toolkit Documentation](https://redux-toolkit.js.org)
5. [TanStack Query Documentation](https://tanstack.com/query)
6. [Testing Library Documentation](https://testing-library.com)
7. [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook)
8. [Airbnb JavaScript Style Guide](https://airbnb.io/javascript/react)
9. [WAI-ARIA Practices](https://www.w3.org/WAI/ARIA/apg)

---

*Document created: 2026-05-13*
*Last updated: 2026-05-13*
*Version: 1.0*
