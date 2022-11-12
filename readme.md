# React Router Private Routes

**What is a Private Route?**

A private route is a route that is only accessible to authenticated users. If a user is not authenticated, they will be redirected to a login page.

**Why do we need Private Routes?**

We need private routes to protect our application from unauthorized users. If we don't have private routes, anyone can access our application and see our data.

**How do we implement Private Routes?**

We can implement private routes by using the `Navigate` component from `react-router-dom`. The `Navigate` component will redirect the user to a specified route if a condition is met.

## scenario

In this lesson, we will implement a private route for the `Dashboard` component. If a user is not authenticated, they will be redirected to the `Login` component when they try to access the `Dashboard` component via the `/dashboard` route in the browser.

**Note:** this is a simplified example. In a real application, you would want to store the authentication state in a global state management library like `Redux` or `MobX` and check the authentication state in the `PrivateRoute` component.

## how to create a private route

Let's create a private route for our `Dashboard` component. We will use the `Navigate` component to redirect the user to the `Login` component if they are not authenticated.

```jsx
import { Navigate, Outlet } from 'react-router-dom';

export default function PrivateRoute() {
    const isAuthenticated = false; // check if the user is authenticated.
  /*  In a real application, you would want to store the authentication state in a global state management library like Redux or MobX and check the authentication state here. */

  return isAuthenticated ? <Outlet /> : <Navigate to="/login" />;
}
```

In the code above, we are using the `Navigate` component to redirect the user to the `/login` route if they are not authenticated. We are also using the `Outlet` component to render the child routes of the `PrivateRoute` component.

## how to use a private route

Let's use the `PrivateRoute` component in our `App` component.

```jsx
import { Routes, Route } from 'react-router-dom';
import PrivateRoute from './PrivateRoute';
import Dashboard from './Dashboard';
import Login from './Login';

export default function App() {
  return (
    <Routes>
      <Route path="/" element={<PrivateRoute />}>
        <Route path="dashboard" element={<Dashboard />} />
      </Route>
      <Route path="/login" element={<Login />} />
    </Routes>
  );
}
```

In the code above, we are using the `PrivateRoute` component as the parent route of the `Dashboard` component. This means that the `Dashboard` component will only be rendered if the user is authenticated and will be redirected to the `Login` component if they are not authenticated.

## how to redirect a user to a specific route after login

Let's redirect the user to the `Dashboard` component after they login. We will use the `useNavigate` hook to redirect the user to the `Dashboard` component after they login.

```jsx
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';

export default function Login() {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const navigate = useNavigate();

  const handleSubmit = (event) => {
    event.preventDefault();

    // if the user is authenticated
    if (username === 'admin' && password === 'admin') {
      navigate('/dashboard'); // redirect to the dashboard after login
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Username
        <input
          type="text"
          value={username}
          onChange={(event) => setUsername(event.target.value)}
        />
      </label>
      <label>
        Password
        <input
          type="password"
          value={password}
          onChange={(event) => setPassword(event.target.value)}
        />
      </label>
      <button type="submit">Login</button>
    </form>
  );
}
```

In the code above, we are using the `useNavigate` hook to redirect the user to the `/dashboard` route after they login. We are also using the `Navigate` component in the `PrivateRoute` component to redirect the user to the `Login` component if they are not authenticated.

## how to redirect a user to the previous route after login

Let's redirect the user to the previous route after they login. We will use the `useLocation` hook to get the previous route and the `useNavigate` hook to redirect the user to the previous route after they login.

```jsx
import { useState } from 'react';
import { useLocation, useNavigate } from 'react-router-dom';

export default function Login() {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const location = useLocation();
  const navigate = useNavigate();

  const handleSubmit = (event) => {
    event.preventDefault();

    // if the user is authenticated
    if (username === 'admin' && password === 'admin') {
      navigate(location.state?.from || '/dashboard'); // redirect to the previous route after login
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Username
        <input
          type="text"
          value={username}
          onChange={(event) => setUsername(event.target.value)}
        />
      </label>
      <label>
        Password
        <input
          type="password"
          value={password}
          onChange={(event) => setPassword(event.target.value)}
        />
      </label>
      <button type="submit">Login</button>
    </form>
  );
}
```

In the code above, we are using the `useLocation` hook to get the previous route and the `useNavigate` hook to redirect the user to the previous route after they login. We are also using the `Navigate` component in the `PrivateRoute` component to redirect the user to the `Login` component if they are not authenticated.

## conclusion

we have learned how to implement private routes in our application. We have also learned how to redirect a user to a specific route after login and how to redirect a user to the previous route after login.

---

Thanks for reading.

if you liked the tutorial please give it a star 🌟

also follow me.

**Yahya EL Ganayni**

- GitHub: [github](https://github.com/yahyaelganyni1)
- Twitter: [@YElganayni](https://twitter.com/YElganayni)
- LinkedIn: [LinkedIn](https://www.linkedin.com/in/yahya-el-ganayni-a456115b/)
