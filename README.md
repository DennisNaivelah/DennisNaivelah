**Initialize Project (Vite + React):**
   ```bash
   npm create vite@latest my-app -- --template react   cd my-app
   npm install
   ```

   ```bash
   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init -p
   npm install react-router-dom
   ```

---

## tailwind.config.js
```js
module.exports = {
  content: [
    './index.html',
    './src/**/*.{js,jsx,ts,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## postcss.config.js
```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

## package.json (scripts excerpt)
```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

## src/index.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## src/main.jsx
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import { BrowserRouter } from 'react-router-dom';
import App from './App';
import './index.css';

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

## src/App.jsx
```jsx
import { Routes, Route, Link } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Login from './pages/Login';
import Signup from './pages/Signup';

export default function App() {
  return (
    <div className="min-h-screen bg-gray-50">
      <nav className="bg-white shadow p-4">
        <ul className="flex space-x-6">
          <li><Link to="/" className="hover:text-indigo-600">Home</Link></li>
          <li><Link to="/about" className="hover:text-indigo-600">About</Link></li>
          <li><Link to="/login" className="hover:text-indigo-600">Login</Link></li>
          <li><Link to="/signup" className="hover:text-indigo-600">Sign Up</Link></li>
        </ul>
      </nav>
      <main className="p-6">
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/login" element={<Login />} />
          <Route path="/signup" element={<Signup />} />
        </Routes>
      </main>
    </div>
  );
}
```

## src/pages/Home.jsx
```jsx
export default function Home() {
  return (
    <section className="flex flex-col items-center justify-center h-[70vh] bg-indigo-50 rounded-lg p-8">
      <h1 className="text-5xl font-extrabold mb-4">Welcome to MyApp</h1>
      <p className="text-xl text-gray-700">A forward-thinking React + Tailwind project.</p>
    </section>
  );
}
```

## src/pages/About.jsx
```jsx
export default function About() {
  return (
    <div className="max-w-2xl mx-auto bg-white shadow-md rounded-lg p-8">
      <h2 className="text-3xl font-semibold mb-4">About Us</h2>
      <p className="text-gray-600">
        We specialize in crafting modern web interfaces with React and Tailwind CSS,
        focusing on responsive design and great UX.
      </p>
    </div>
  );
}
```

## src/pages/Login.jsx
```jsx
import { useState } from 'react';
export default function Login() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const handleSubmit = e => {
    e.preventDefault();
    // TODO: authentication logic
    console.log({ email, password });
  };

  return (
    <div className="flex items-center justify-center h-[70vh]">
      <form onSubmit={handleSubmit} className="w-full max-w-sm bg-white p-6 rounded-lg shadow-md">
        <h3 className="text-2xl font-bold mb-6">Login</h3>
        <label className="block mb-4">
          <span className="text-gray-700">Email</span>
          <input
            type="email"
            required
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring focus:ring-indigo-200"
            value={email}
            onChange={e => setEmail(e.target.value)}
          />
        </label>
        <label className="block mb-6">
          <span className="text-gray-700">Password</span>
          <input
            type="password"
            required
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring focus:ring-indigo-200"
            value={password}
            onChange={e => setPassword(e.target.value)}
          />
        </label>
        <button
          type="submit"
          className="w-full bg-indigo-600 text-white py-2 rounded-lg hover:bg-indigo-700 transition"
        >
          Sign In
        </button>
      </form>
    </div>
  );
}
```

## src/pages/Signup.jsx
```jsx
import { useState } from 'react';
export default function Signup() {
  const [form, setForm] = useState({ name: '', email: '', password: '' });

  const handleChange = e => setForm({ ...form, [e.target.name]: e.target.value });
  const handleSubmit = e => {
    e.preventDefault();
    // TODO: registration logic
    console.log(form);
  };

  return (
    <div className="flex items-center justify-center h-[70vh]">
      <form onSubmit={handleSubmit} className="w-full max-w-sm bg-white p-6 rounded-lg shadow-md">
        <h3 className="text-2xl font-bold mb-6">Sign Up</h3>
        <label className="block mb-4">
          <span className="text-gray-700">Name</span>
          <input
            name="name"
            type="text"
            required
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring focus:ring-green-200"
            value={form.name}
            onChange={handleChange}
          />
        </label>
        <label className="block mb-4">
          <span className="text-gray-700">Email</span>
          <input
            name="email"
            type="email"
            required
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring focus:ring-green-200"
            value={form.email}
            onChange={handleChange}
          />
        </label>
        <label className="block mb-6">
          <span className="text-gray-700">Password</span>
          <input
            name="password"
            type="password"
            required
            className="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:ring focus:ring-green-200"
            value={form.password}
            onChange={handleChange}
          />
        </label>
        <button
          type="submit"
          className="w-full bg-green-600 text-white py-2 rounded-lg hover:bg-green-700 transition"
        >
          Create Account
        </button>
      </form>
    </div>
  );
}
```
