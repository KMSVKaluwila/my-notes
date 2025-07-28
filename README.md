# Complete React JS Learning Guide

## Table of Contents
1. [Environment Setup](#environment-setup)
2. [React Fundamentals](#react-fundamentals)
3. [Components](#components)
4. [JSX](#jsx)
5. [Props](#props)
6. [State Management](#state-management)
7. [Event Handling](#event-handling)
8. [Conditional Rendering](#conditional-rendering)
9. [Lists and Keys](#lists-and-keys)
10. [Forms](#forms)
11. [Lifecycle Methods](#lifecycle-methods)
12. [Hooks](#hooks)
13. [Context API](#context-api)
14. [Error Boundaries](#error-boundaries)
15. [Performance Optimization](#performance-optimization)
16. [Testing](#testing)
17. [Best Practices](#best-practices)
18. [Practice Projects](#practice-projects)

---

## Environment Setup

### Prerequisites
- Node.js (version 14 or higher)
- npm or yarn package manager
- Code editor (VS Code recommended)

### Method 1: Create React App (Recommended for beginners)
```bash
# Install Create React App globally
npm install -g create-react-app

# Create a new React project
npx create-react-app my-react-app
cd my-react-app
npm start
```

### Method 2: Vite (Faster alternative)
```bash
# Create project with Vite
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

### Essential VS Code Extensions
- ES7+ React/Redux/React-Native snippets
- Bracket Pair Colorizer
- Auto Rename Tag
- Prettier - Code formatter
- ESLint

### Project Structure
```
my-react-app/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── components/
│   ├── hooks/
│   ├── context/
│   ├── utils/
│   ├── App.js
│   ├── App.css
│   └── index.js
├── package.json
└── README.md
```

---

## React Fundamentals

### What is React?
React is a JavaScript library for building user interfaces, particularly web applications. It focuses on creating reusable UI components and managing application state efficiently.

### Key Concepts
- **Virtual DOM**: React creates a virtual representation of the DOM for efficient updates
- **Component-based**: Build encapsulated components that manage their own state
- **Declarative**: Describe what the UI should look like for any given state
- **Learn Once, Write Anywhere**: Can be used for web, mobile, and desktop applications

---

## Components

Components are the building blocks of React applications. They can be defined as functions or classes.

### Functional Components (Recommended)
```jsx
// Simple functional component
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Arrow function component
const Welcome = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

// Component with destructured props
const Welcome = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```

### Class Components (Legacy but still important to understand)
```jsx
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

### Component Composition
```jsx
function App() {
  return (
    <div>
      <Welcome name="Alice" />
      <Welcome name="Bob" />
      <Welcome name="Charlie" />
    </div>
  );
}
```

**Practice Exercise**: Create a `UserCard` component that displays user information (name, email, avatar).

---

## JSX

JSX is a syntax extension for JavaScript that allows you to write HTML-like code in your JavaScript files.

### Basic JSX Rules
```jsx
// 1. Must return a single parent element
function MyComponent() {
  return (
    <div>
      <h1>Title</h1>
      <p>Description</p>
    </div>
  );
}

// 2. Use React Fragment for multiple elements without wrapper
function MyComponent() {
  return (
    <>
      <h1>Title</h1>
      <p>Description</p>
    </>
  );
}

// 3. JavaScript expressions in curly braces
function MyComponent() {
  const name = 'John';
  const age = 25;
  
  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>You are {age} years old</p>
      <p>Next year you'll be {age + 1}</p>
    </div>
  );
}
```

### JSX Attributes
```jsx
function MyComponent() {
  const imageUrl = 'https://example.com/image.jpg';
  const altText = 'Description';
  
  return (
    <div>
      {/* className instead of class */}
      <div className="container">
        {/* htmlFor instead of for */}
        <label htmlFor="email">Email:</label>
        <input id="email" type="email" />
        
        {/* Dynamic attributes */}
        <img src={imageUrl} alt={altText} />
        
        {/* Style as object */}
        <div style={{ color: 'red', fontSize: '16px' }}>
          Styled text
        </div>
      </div>
    </div>
  );
}
```

**Practice Exercise**: Create a `ProductCard` component using JSX that displays product information with proper styling.

---

## Props

Props (properties) are used to pass data from parent components to child components.

### Basic Props Usage
```jsx
// Child component
function Greeting({ name, age, isStudent }) {
  return (
    <div>
      <h2>Hello, {name}!</h2>
      <p>Age: {age}</p>
      {isStudent && <p>Status: Student</p>}
    </div>
  );
}

// Parent component
function App() {
  return (
    <div>
      <Greeting name="Alice" age={20} isStudent={true} />
      <Greeting name="Bob" age={25} isStudent={false} />
    </div>
  );
}
```

### Props with Objects and Arrays
```jsx
function UserProfile({ user, hobbies }) {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>Email: {user.email}</p>
      <h3>Hobbies:</h3>
      <ul>
        {hobbies.map((hobby, index) => (
          <li key={index}>{hobby}</li>
        ))}
      </ul>
    </div>
  );
}

// Usage
const userData = { name: 'John', email: 'john@example.com' };
const userHobbies = ['Reading', 'Swimming', 'Coding'];

<UserProfile user={userData} hobbies={userHobbies} />
```

### Default Props
```jsx
function Button({ text, color = 'blue', size = 'medium' }) {
  return (
    <button 
      className={`btn btn-${color} btn-${size}`}
    >
      {text}
    </button>
  );
}

// Alternative syntax for default props
Button.defaultProps = {
  color: 'blue',
  size: 'medium'
};
```

### Props Validation with PropTypes
```jsx
import PropTypes from 'prop-types';

function UserProfile({ name, age, email, isActive }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Email: {email}</p>
      <p>Status: {isActive ? 'Active' : 'Inactive'}</p>
    </div>
  );
}

UserProfile.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
  email: PropTypes.string,
  isActive: PropTypes.bool
};
```

**Practice Exercise**: Create a `MovieCard` component that receives movie data as props and displays it with proper validation.

---

## State Management

State represents data that can change over time in your component.

### useState Hook
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(0);
  
  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

### Multiple State Variables
```jsx
function UserForm() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [age, setAge] = useState(0);
  
  return (
    <form>
      <input 
        type="text" 
        placeholder="Name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <input 
        type="email" 
        placeholder="Email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input 
        type="number" 
        placeholder="Age"
        value={age}
        onChange={(e) => setAge(parseInt(e.target.value))}
      />
    </form>
  );
}
```

### Object State
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
        placeholder="Name"
        value={user.name}
        onChange={(e) => handleInputChange('name', e.target.value)}
      />
      <input 
        type="email" 
        placeholder="Email"
        value={user.email}
        onChange={(e) => handleInputChange('email', e.target.value)}
      />
    </form>
  );
}
```

### Array State
```jsx
function TodoList() {
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState('');
  
  const addTodo = () => {
    if (inputValue.trim()) {
      setTodos([...todos, { id: Date.now(), text: inputValue, completed: false }]);
      setInputValue('');
    }
  };
  
  const toggleTodo = (id) => {
    setTodos(todos.map(todo => 
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    ));
  };
  
  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };
  
  return (
    <div>
      <input 
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        placeholder="Add a todo"
      />
      <button onClick={addTodo}>Add</button>
      
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            <span 
              style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}
              onClick={() => toggleTodo(todo.id)}
            >
              {todo.text}
            </span>
            <button onClick={() => deleteTodo(todo.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

**Practice Exercise**: Build a shopping cart component that manages items, quantities, and total price.

---

## Event Handling

React events are synthetic events that wrap native events to provide consistent behavior across browsers.

### Basic Event Handling
```jsx
function Button() {
  const handleClick = (e) => {
    e.preventDefault();
    console.log('Button clicked!');
    console.log('Event:', e);
  };
  
  const handleMouseOver = () => {
    console.log('Mouse over!');
  };
  
  return (
    <button 
      onClick={handleClick}
      onMouseOver={handleMouseOver}
    >
      Click me!
    </button>
  );
}
```

### Form Events
```jsx
function ContactForm() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: ''
  });
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form submitted:', formData);
    // Process form data
  };
  
  const handleReset = () => {
    setFormData({ name: '', email: '', message: '' });
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text"
        name="name"
        value={formData.name}
        onChange={handleChange}
        placeholder="Name"
      />
      <input 
        type="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <textarea 
        name="message"
        value={formData.message}
        onChange={handleChange}
        placeholder="Message"
      />
      <button type="submit">Submit</button>
      <button type="button" onClick={handleReset}>Reset</button>
    </form>
  );
}
```

### Keyboard Events
```jsx
function SearchBox() {
  const [query, setQuery] = useState('');
  
  const handleKeyDown = (e) => {
    if (e.key === 'Enter') {
      console.log('Searching for:', query);
    } else if (e.key === 'Escape') {
      setQuery('');
    }
  };
  
  return (
    <input 
      type="text"
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      onKeyDown={handleKeyDown}
      placeholder="Search... (Press Enter to search, Esc to clear)"
    />
  );
}
```

**Practice Exercise**: Create a calculator component that handles button clicks and keyboard input.

---

## Conditional Rendering

Display different content based on certain conditions.

### If-Else with Ternary Operator
```jsx
function UserGreeting({ isLoggedIn, username }) {
  return (
    <div>
      {isLoggedIn ? (
        <h1>Welcome back, {username}!</h1>
      ) : (
        <h1>Please sign in.</h1>
      )}
    </div>
  );
}
```

### Logical AND Operator
```jsx
function Notifications({ messages }) {
  return (
    <div>
      <h1>Inbox</h1>
      {messages.length > 0 && (
        <p>You have {messages.length} unread messages.</p>
      )}
      
      {messages.length === 0 && (
        <p>No new messages.</p>
      )}
    </div>
  );
}
```

### Switch Statement Alternative
```jsx
function StatusMessage({ status }) {
  const renderStatusMessage = () => {
    switch (status) {
      case 'loading':
        return <div>Loading...</div>;
      case 'success':
        return <div>Data loaded successfully!</div>;
      case 'error':
        return <div>Error loading data.</div>;
      default:
        return <div>Unknown status.</div>;
    }
  };
  
  return (
    <div>
      <h2>Status:</h2>
      {renderStatusMessage()}
    </div>
  );
}
```

### Complex Conditional Rendering
```jsx
function UserDashboard({ user, isLoading, error }) {
  if (isLoading) {
    return <div>Loading user data...</div>;
  }
  
  if (error) {
    return <div>Error: {error.message}</div>;
  }
  
  if (!user) {
    return <div>No user data available.</div>;
  }
  
  return (
    <div>
      <h1>Welcome, {user.name}!</h1>
      {user.isPremium && (
        <div className="premium-badge">Premium Member</div>
      )}
      
      {user.notifications && user.notifications.length > 0 && (
        <div>
          <h3>Notifications ({user.notifications.length})</h3>
          <ul>
            {user.notifications.map((notification, index) => (
              <li key={index}>{notification}</li>
            ))}
          </ul>
        </div>
      )}
    </div>
  );
}
```

**Practice Exercise**: Create a weather app component that shows different content based on weather conditions.

---

## Lists and Keys

Rendering lists of data is a common pattern in React applications.

### Basic List Rendering
```jsx
function NumberList({ numbers }) {
  return (
    <ul>
      {numbers.map((number, index) => (
        <li key={index}>{number}</li>
      ))}
    </ul>
  );
}

// Usage
const numbers = [1, 2, 3, 4, 5];
<NumberList numbers={numbers} />
```

### List with Objects
```jsx
function UserList({ users }) {
  return (
    <div>
      {users.map(user => (
        <div key={user.id} className="user-card">
          <h3>{user.name}</h3>
          <p>Email: {user.email}</p>
          <p>Age: {user.age}</p>
        </div>
      ))}
    </div>
  );
}
```

### List with Components
```jsx
function ProductCard({ product }) {
  return (
    <div className="product-card">
      <img src={product.image} alt={product.name} />
      <h3>{product.name}</h3>
      <p>${product.price}</p>
      <button>Add to Cart</button>
    </div>
  );
}

function ProductList({ products }) {
  return (
    <div className="product-grid">
      {products.map(product => (
        <ProductCard key={product.id} product={product} />
      ))}
    </div>
  );
}
```

### Filtering and Sorting Lists
```jsx
function MovieList({ movies, searchTerm, sortBy }) {
  const filteredAndSortedMovies = movies
    .filter(movie => 
      movie.title.toLowerCase().includes(searchTerm.toLowerCase())
    )
    .sort((a, b) => {
      if (sortBy === 'title') return a.title.localeCompare(b.title);
      if (sortBy === 'year') return b.year - a.year;
      if (sortBy === 'rating') return b.rating - a.rating;
      return 0;
    });
  
  return (
    <div>
      {filteredAndSortedMovies.length === 0 ? (
        <p>No movies found.</p>
      ) : (
        filteredAndSortedMovies.map(movie => (
          <div key={movie.id} className="movie-card">
            <h3>{movie.title}</h3>
            <p>Year: {movie.year}</p>
            <p>Rating: {movie.rating}/10</p>
          </div>
        ))
      )}
    </div>
  );
}
```

### Dynamic List Management
```jsx
function ManageableList() {
  const [items, setItems] = useState([
    { id: 1, text: 'Item 1', completed: false },
    { id: 2, text: 'Item 2', completed: true },
  ]);
  const [newItemText, setNewItemText] = useState('');
  
  const addItem = () => {
    if (newItemText.trim()) {
      const newItem = {
        id: Date.now(),
        text: newItemText,
        completed: false
      };
      setItems([...items, newItem]);
      setNewItemText('');
    }
  };
  
  const deleteItem = (id) => {
    setItems(items.filter(item => item.id !== id));
  };
  
  const toggleItem = (id) => {
    setItems(items.map(item =>
      item.id === id ? { ...item, completed: !item.completed } : item
    ));
  };
  
  return (
    <div>
      <div>
        <input 
          value={newItemText}
          onChange={(e) => setNewItemText(e.target.value)}
          placeholder="Add new item"
        />
        <button onClick={addItem}>Add</button>
      </div>
      
      <ul>
        {items.map(item => (
          <li key={item.id}>
            <span 
              style={{ 
                textDecoration: item.completed ? 'line-through' : 'none' 
              }}
              onClick={() => toggleItem(item.id)}
            >
              {item.text}
            </span>
            <button onClick={() => deleteItem(item.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

**Practice Exercise**: Build a contact list with search, filter, and sort functionality.

---

## Forms

Forms are essential for user input in web applications.

### Basic Form Handling
```jsx
function BasicForm() {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: ''
  });
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form submitted:', formData);
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>Username:</label>
        <input 
          type="text"
          name="username"
          value={formData.username}
          onChange={handleChange}
          required
        />
      </div>
      
      <div>
        <label>Email:</label>
        <input 
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
          required
        />
      </div>
      
      <div>
        <label>Password:</label>
        <input 
          type="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
          required
        />
      </div>
      
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Form with Validation
```jsx
function ValidatedForm() {
  const [formData, setFormData] = useState({
    email: '',
    password: '',
    confirmPassword: ''
  });
  const [errors, setErrors] = useState({});
  
  const validateForm = () => {
    const newErrors = {};
    
    // Email validation
    if (!formData.email) {
      newErrors.email = 'Email is required';
    } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
      newErrors.email = 'Email is invalid';
    }
    
    // Password validation
    if (!formData.password) {
      newErrors.password = 'Password is required';
    } else if (formData.password.length < 6) {
      newErrors.password = 'Password must be at least 6 characters';
    }
    
    // Confirm password validation
    if (formData.password !== formData.confirmPassword) {
      newErrors.confirmPassword = 'Passwords do not match';
    }
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
    
    // Clear error when user starts typing
    if (errors[name]) {
      setErrors(prev => ({
        ...prev,
        [name]: ''
      }));
    }
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    if (validateForm()) {
      console.log('Form is valid:', formData);
    }
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>Email:</label>
        <input 
          type="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
        {errors.email && <span className="error">{errors.email}</span>}
      </div>
      
      <div>
        <label>Password:</label>
        <input 
          type="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
        />
        {errors.password && <span className="error">{errors.password}</span>}
      </div>
      
      <div>
        <label>Confirm Password:</label>
        <input 
          type="password"
          name="confirmPassword"
          value={formData.confirmPassword}
          onChange={handleChange}
        />
        {errors.confirmPassword && <span className="error">{errors.confirmPassword}</span>}
      </div>
      
      <button type="submit">Submit</button>
    </form>
  );
}
```

### Different Input Types
```jsx
function ComprehensiveForm() {
  const [formData, setFormData] = useState({
    text: '',
    email: '',
    password: '',
    number: 0,
    date: '',
    select: '',
    radio: '',
    checkboxes: [],
    textarea: '',
    file: null
  });
  
  const handleChange = (e) => {
    const { name, value, type, checked, files } = e.target;
    
    if (type === 'checkbox') {
      if (checked) {
        setFormData(prev => ({
          ...prev,
          [name]: [...prev[name], value]
        }));
      } else {
        setFormData(prev => ({
          ...prev,
          [name]: prev[name].filter(item => item !== value)
        }));
      }
    } else if (type === 'file') {
      setFormData(prev => ({
        ...prev,
        [name]: files[0]
      }));
    } else {
      setFormData(prev => ({
        ...prev,
        [name]: value
      }));
    }
  };
  
  return (
    <form>
      {/* Text Input */}
      <div>
        <label>Text:</label>
        <input 
          type="text"
          name="text"
          value={formData.text}
          onChange={handleChange}
        />
      </div>
      
      {/* Number Input */}
      <div>
        <label>Number:</label>
        <input 
          type="number"
          name="number"
          value={formData.number}
          onChange={handleChange}
        />
      </div>
      
      {/* Date Input */}
      <div>
        <label>Date:</label>
        <input 
          type="date"
          name="date"
          value={formData.date}
          onChange={handleChange}
        />
      </div>
      
      {/* Select Dropdown */}
      <div>
        <label>Select:</label>
        <select name="select" value={formData.select} onChange={handleChange}>
          <option value="">Choose...</option>
          <option value="option1">Option 1</option>
          <option value="option2">Option 2</option>
          <option value="option3">Option 3</option>
        </select>
      </div>
      
      {/* Radio Buttons */}
      <div>
        <label>Radio:</label>
        <label>
          <input 
            type="radio"
            name="radio"
            value="option1"
            checked={formData.radio === 'option1'}
            onChange={handleChange}
          />
          Option 1
        </label>
        <label>
          <input 
            type="radio"
            name="radio"
            value="option2"
            checked={formData.radio === 'option2'}
            onChange={handleChange}
          />
          Option 2
        </label>
      </div>
      
      {/* Checkboxes */}
      <div>
        <label>Checkboxes:</label>
        <label>
          <input 
            type="checkbox"
            name="checkboxes"
            value="checkbox1"
            checked={formData.checkboxes.includes('checkbox1')}
            onChange={handleChange}
          />
          Checkbox 1
        </label>
        <label>
          <input 
            type="checkbox"
            name="checkboxes"
            value="checkbox2"
            checked={formData.checkboxes.includes('checkbox2')}
            onChange={handleChange}
          />
          Checkbox 2
        </label>
      </div>
      
      {/* Textarea */}
      <div>
        <label>Textarea:</label>
        <textarea 
          name="textarea"
          value={formData.textarea}
          onChange={handleChange}
          rows="4"
          cols="50"
        />
      </div>
      
      {/* File Input */}
      <div>
        <label>File:</label>
        <input 
          type="file"
          name="file"
          onChange={handleChange}
        />
      </div>
    </form>
  );
}
```

**Practice Exercise**: Create a user registration form with comprehensive validation and different input types.

---

## Lifecycle Methods

Lifecycle methods allow you to hook into different phases of a component's lifecycle.

### Class Component Lifecycle
```jsx
import React, { Component } from 'react';

class LifecycleExample extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
      data: null
    };
    console.log('Constructor: Component is being created');
  }
  
  // Mounting phase
  componentDidMount() {
    console.log('ComponentDidMount: Component has been mounted');
    // Perfect place for API calls, subscriptions
    this.fetchData();
  }
  
  // Updating phase
  componentDidUpdate(prevProps, prevState) {
    console.log('ComponentDidUpdate: Component has been updated');
    
    // Example: Fetch new data when props change
    if (prevProps.userId !== this.props.userId) {
      this.fetchData();
    }
  }
  
  // Unmounting phase
  componentWillUnmount() {
    console.log('ComponentWillUnmount: Component is about to be unmounted');
    // Cleanup: Remove event listeners, cancel API calls, clear timers
    if (this.timer) {
      clearInterval(this.timer);
    }
  }
  
  fetchData = () => {
    // Simulate API call
    setTimeout(() => {
      this.setState({ data: 'Fetched data' });
    }, 1000);
  }
  
  handleIncrement = () => {
    this.setState({ count: this.state.count + 1 });
  }
  
  render() {
    console.log('Render: Component is rendering');
    return (
      <div>
        <h2>Count: {this.state.count}</h2>
        <button onClick={this.handleIncrement}>Increment</button>
        <p>Data: {this.state.data || 'Loading...'}</p>
      </div>
    );
  }
}
```

**Practice Exercise**: Create a timer component that starts when mounted and cleans up when unmounted.

---

## Hooks

Hooks allow you to use state and other React features in functional components.

### useState Hook
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
      
      <input 
        type="text" 
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Enter your name"
      />
      <p>Hello, {name}!</p>
    </div>
  );
}
```

### useEffect Hook
```jsx
import React, { useState, useEffect } from 'react';

// Basic useEffect
function BasicEffect() {
  const [count, setCount] = useState(0);
  
  // Runs after every render
  useEffect(() => {
    document.title = `Count: ${count}`;
  });
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// useEffect with dependency array
function EffectWithDependencies() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');
  
  // Only runs when count changes
  useEffect(() => {
    console.log('Count changed:', count);
  }, [count]);
  
  // Only runs once (on mount)
  useEffect(() => {
    console.log('Component mounted');
    return () => {
      console.log('Component will unmount');
    };
  }, []);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      
      <input 
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Name"
      />
    </div>
  );
}

// Data fetching with useEffect
function DataFetcher({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    const fetchUser = async () => {
      try {
        setLoading(true);
        setError(null);
        const response = await fetch(`/api/users/${userId}`);
        const userData = await response.json();
        setUser(userData);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    
    if (userId) {
      fetchUser();
    }
  }, [userId]);
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!user) return <div>No user found</div>;
  
  return (
    <div>
      <h2>{user.name}</h2>
      <p>Email: {user.email}</p>
    </div>
  );
}
```

### useContext Hook
```jsx
import React, { createContext, useContext, useState } from 'react';

// Create context
const ThemeContext = createContext();

// Theme provider component
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  
  const toggleTheme = () => {
    setTheme(prev => prev === 'light' ? 'dark' : 'light');
  };
  
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Component using context
function ThemedButton() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  
  return (
    <button 
      onClick={toggleTheme}
      style={{
        backgroundColor: theme === 'light' ? '#fff' : '#333',
        color: theme === 'light' ? '#333' : '#fff'
      }}
    >
      Toggle Theme (Current: {theme})
    </button>
  );
}

// App component
function App() {
  return (
    <ThemeProvider>
      <div>
        <h1>Themed App</h1>
        <ThemedButton />
      </div>
    </ThemeProvider>
  );
}
```

### useReducer Hook
```jsx
import React, { useReducer } from 'react';

// Reducer function
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: 0 };
    case 'set':
      return { count: action.payload };
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });
  
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
      <button onClick={() => dispatch({ type: 'set', payload: 10 })}>Set to 10</button>
    </div>
  );
}

// Complex state management with useReducer
const todoReducer = (state, action) => {
  switch (action.type) {
    case 'add':
      return [...state, { id: Date.now(), text: action.payload, completed: false }];
    case 'toggle':
      return state.map(todo =>
        todo.id === action.payload ? { ...todo, completed: !todo.completed } : todo
      );
    case 'delete':
      return state.filter(todo => todo.id !== action.payload);
    case 'clear_completed':
      return state.filter(todo => !todo.completed);
    default:
      return state;
  }
};

function TodoApp() {
  const [todos, dispatch] = useReducer(todoReducer, []);
  const [inputValue, setInputValue] = useState('');
  
  const addTodo = () => {
    if (inputValue.trim()) {
      dispatch({ type: 'add', payload: inputValue });
      setInputValue('');
    }
  };
  
  return (
    <div>
      <input 
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        placeholder="Add todo"
      />
      <button onClick={addTodo}>Add</button>
      <button onClick={() => dispatch({ type: 'clear_completed' })}>
        Clear Completed
      </button>
      
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            <span 
              style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}
              onClick={() => dispatch({ type: 'toggle', payload: todo.id })}
            >
              {todo.text}
            </span>
            <button onClick={() => dispatch({ type: 'delete', payload: todo.id })}>
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### Custom Hooks
```jsx
// Custom hook for local storage
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error('Error reading from localStorage:', error);
      return initialValue;
    }
  });
  
  const setValue = (value) => {
    try {
      setStoredValue(value);
      window.localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error('Error writing to localStorage:', error);
    }
  };
  
  return [storedValue, setValue];
}

// Custom hook for API calls
function useApi(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        setError(null);
        const response = await fetch(url);
        const result = await response.json();
        setData(result);
      } catch (err) {
        setError(err.message);
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

// Using custom hooks
function UserProfile({ userId }) {
  const [preferences, setPreferences] = useLocalStorage('userPrefs', {});
  const { data: user, loading, error } = useApi(`/api/users/${userId}`);
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  
  return (
    <div>
      <h2>{user?.name}</h2>
      <p>Theme: {preferences.theme || 'default'}</p>
      <button onClick={() => setPreferences({ ...preferences, theme: 'dark' })}>
        Set Dark Theme
      </button>
    </div>
  );
}
```

### Other Important Hooks
```jsx
import React, { useRef, useMemo, useCallback, useState } from 'react';

// useRef Hook
function RefExample() {
  const inputRef = useRef(null);
  const countRef = useRef(0);
  
  const focusInput = () => {
    inputRef.current.focus();
  };
  
  const incrementCount = () => {
    countRef.current += 1;
    console.log('Count:', countRef.current);
  };
  
  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
      <button onClick={incrementCount}>Increment Ref Count</button>
    </div>
  );
}

// useMemo Hook
function ExpensiveComponent({ items, filter }) {
  const expensiveValue = useMemo(() => {
    console.log('Computing expensive value...');
    return items
      .filter(item => item.includes(filter))
      .map(item => item.toUpperCase())
      .sort();
  }, [items, filter]);
  
  return (
    <ul>
      {expensiveValue.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

// useCallback Hook
function CallbackExample() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState([]);
  
  const addTodo = useCallback((text) => {
    setTodos(prev => [...prev, { id: Date.now(), text }]);
  }, []);
  
  const increment = useCallback(() => {
    setCount(prev => prev + 1);
  }, []);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
      <TodoList todos={todos} onAddTodo={addTodo} />
    </div>
  );
}
```

**Practice Exercise**: Create a custom hook for handling form state and validation.

---

## Context API

Context provides a way to pass data through the component tree without having to pass props down manually at every level.

### Basic Context Setup
```jsx
import React, { createContext, useContext, useState } from 'react';

// 1. Create Context
const UserContext = createContext();

// 2. Create Provider Component
export function UserProvider({ children }) {
  const [user, setUser] = useState(null);
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  
  const login = (userData) => {
    setUser(userData);
    setIsAuthenticated(true);
  };
  
  const logout = () => {
    setUser(null);
    setIsAuthenticated(false);
  };
  
  const value = {
    user,
    isAuthenticated,
    login,
    logout
  };
  
  return (
    <UserContext.Provider value={value}>
      {children}
    </UserContext.Provider>
  );
}

// 3. Custom hook to use context
export function useUser() {
  const context = useContext(UserContext);
  if (!context) {
    throw new Error('useUser must be used within a UserProvider');
  }
  return context;
}

// 4. Components using context
function LoginForm() {
  const { login } = useUser();
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    // Simulate login
    login({ email, name: 'John Doe' });
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
      <input 
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        placeholder="Password"
      />
      <button type="submit">Login</button>
    </form>
  );
}

function UserProfile() {
  const { user, logout, isAuthenticated } = useUser();
  
  if (!isAuthenticated) {
    return <LoginForm />;
  }
  
  return (
    <div>
      <h2>Welcome, {user.name}!</h2>
      <p>Email: {user.email}</p>
      <button onClick={logout}>Logout</button>
    </div>
  );
}

function App() {
  return (
    <UserProvider>
      <div>
        <h1>My App</h1>
        <UserProfile />
      </div>
    </UserProvider>
  );
}
```

### Advanced Context with useReducer
```jsx
import React, { createContext, useContext, useReducer } from 'react';

// Actions
const ACTIONS = {
  ADD_ITEM: 'ADD_ITEM',
  REMOVE_ITEM: 'REMOVE_ITEM',
  UPDATE_QUANTITY: 'UPDATE_QUANTITY',
  CLEAR_CART: 'CLEAR_CART'
};

// Reducer
function cartReducer(state, action) {
  switch (action.type) {
    case ACTIONS.ADD_ITEM:
      const existingItem = state.items.find(item => item.id === action.payload.id);
      if (existingItem) {
        return {
          ...state,
          items: state.items.map(item =>
            item.id === action.payload.id
              ? { ...item, quantity: item.quantity + 1 }
              : item
          )
        };
      }
      return {
        ...state,
        items: [...state.items, { ...action.payload, quantity: 1 }]
      };
      
    case ACTIONS.REMOVE_ITEM:
      return {
        ...state,
        items: state.items.filter(item => item.id !== action.payload)
      };
      
    case ACTIONS.UPDATE_QUANTITY:
      return {
        ...state,
        items: state.items.map(item =>
          item.id === action.payload.id
            ? { ...item, quantity: action.payload.quantity }
            : item
        )
      };
      
    case ACTIONS.CLEAR_CART:
      return {
        ...state,
        items: []
      };
      
    default:
      return state;
  }
}

// Context
const CartContext = createContext();

// Provider
export function CartProvider({ children }) {
  const [state, dispatch] = useReducer(cartReducer, {
    items: [],
    total: 0
  });
  
  // Computed values
  const total = state.items.reduce((sum, item) => sum + (item.price * item.quantity), 0);
  const itemCount = state.items.reduce((sum, item) => sum + item.quantity, 0);
  
  // Actions
  const addItem = (item) => {
    dispatch({ type: ACTIONS.ADD_ITEM, payload: item });
  };
  
  const removeItem = (id) => {
    dispatch({ type: ACTIONS.REMOVE_ITEM, payload: id });
  };
  
  const updateQuantity = (id, quantity) => {
    if (quantity <= 0) {
      removeItem(id);
    } else {
      dispatch({ type: ACTIONS.UPDATE_QUANTITY, payload: { id, quantity } });
    }
  };
  
  const clearCart = () => {
    dispatch({ type: ACTIONS.CLEAR_CART });
  };
  
  const value = {
    items: state.items,
    total,
    itemCount,
    addItem,
    removeItem,
    updateQuantity,
    clearCart
  };
  
  return (
    <CartContext.Provider value={value}>
      {children}
    </CartContext.Provider>
  );
}

// Custom hook
export function useCart() {
  const context = useContext(CartContext);
  if (!context) {
    throw new Error('useCart must be used within a CartProvider');
  }
  return context;
}

// Components
function ProductCard({ product }) {
  const { addItem } = useCart();
  
  return (
    <div className="product-card">
      <h3>{product.name}</h3>
      <p>${product.price}</p>
      <button onClick={() => addItem(product)}>
        Add to Cart
      </button>
    </div>
  );
}

function Cart() {
  const { items, total, itemCount, updateQuantity, removeItem, clearCart } = useCart();
  
  if (items.length === 0) {
    return <div>Your cart is empty</div>;
  }
  
  return (
    <div>
      <h2>Cart ({itemCount} items)</h2>
      {items.map(item => (
        <div key={item.id} className="cart-item">
          <span>{item.name}</span>
          <span>${item.price}</span>
          <input 
            type="number"
            value={item.quantity}
            onChange={(e) => updateQuantity(item.id, parseInt(e.target.value))}
            min="0"
          />
          <button onClick={() => removeItem(item.id)}>Remove</button>
        </div>
      ))}
      <div>Total: ${total.toFixed(2)}</div>
      <button onClick={clearCart}>Clear Cart</button>
    </div>
  );
}
```

### Multiple Contexts
```jsx
// Theme Context
const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  
  const toggleTheme = () => {
    setTheme(prev => prev === 'light' ? 'dark' : 'light');
  };
  
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Language Context
const LanguageContext = createContext();

export function LanguageProvider({ children }) {
  const [language, setLanguage] = useState('en');
  
  const translations = {
    en: { welcome: 'Welcome', goodbye: 'Goodbye' },
    es: { welcome: 'Bienvenido', goodbye: 'Adiós' },
    fr: { welcome: 'Bienvenue', goodbye: 'Au revoir' }
  };
  
  const translate = (key) => translations[language][key] || key;
  
  return (
    <LanguageContext.Provider value={{ language, setLanguage, translate }}>
      {children}
    </LanguageContext.Provider>
  );
}

// Combined Provider
function AppProviders({ children }) {
  return (
    <ThemeProvider>
      <LanguageProvider>
        <UserProvider>
          <CartProvider>
            {children}
          </CartProvider>
        </UserProvider>
      </LanguageProvider>
    </ThemeProvider>
  );
}

// Using multiple contexts
function Header() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  const { language, setLanguage, translate } = useContext(LanguageContext);
  const { user, logout } = useUser();
  const { itemCount } = useCart();
  
  return (
    <header style={{ backgroundColor: theme === 'light' ? '#fff' : '#333' }}>
      <h1>{translate('welcome')}</h1>
      
      <select value={language} onChange={(e) => setLanguage(e.target.value)}>
        <option value="en">English</option>
        <option value="es">Español</option>
        <option value="fr">Français</option>
      </select>
      
      <button onClick={toggleTheme}>
        {theme === 'light' ? '🌙' : '☀️'}
      </button>
      
      <div>Cart: {itemCount} items</div>
      
      {user && (
        <div>
          {user.name} | <button onClick={logout}>Logout</button>
        </div>
      )}
    </header>
  );
}
```

**Practice Exercise**: Create a settings context that manages user preferences like theme, language, and notifications.

---

## Error Boundaries

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree and display a fallback UI.

### Basic Error Boundary
```jsx
import React from 'react';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null, errorInfo: null };
  }
  
  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    // Log error details
    console.error('Error caught by boundary:', error);
    console.error('Error info:', errorInfo);
    
    // You can also log the error to an error reporting service here
    this.setState({
      error: error,
      errorInfo: errorInfo
    });
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div style={{ padding: '20px', border: '1px solid red', margin: '20px' }}>
          <h2>Something went wrong!</h2>
          <p>We're sorry, but something unexpected happened.</p>
          
          {process.env.NODE_ENV === 'development' && (
            <details style={{ marginTop: '20px' }}>
              <summary>Error Details (Development Only)</summary>
              <pre style={{ color: 'red', marginTop: '10px' }}>
                {this.state.error && this.state.error.toString()}
              </pre>
              <pre style={{ color: 'red', marginTop: '10px' }}>
                {this.state.errorInfo.componentStack}
              </pre>
            </details>
          )}
          
          <button 
            onClick={() => this.setState({ hasError: false, error: null, errorInfo: null })}
            style={{ marginTop: '20px', padding: '10px' }}
          >
            Try Again
          </button>
        </div>
      );
    }
    
    return this.props.children;
  }
}
```

### Advanced Error Boundary with Logging
```jsx
class AdvancedErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      hasError: false,
      error: null,
      errorInfo: null,
      eventId: null
    };
  }
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    const errorDetails = {
      error: error.toString(),
      errorInfo: errorInfo.componentStack,
      userAgent: navigator.userAgent,
      timestamp: new Date().toISOString(),
      url: window.location.href,
      userId: this.props.userId || 'anonymous'
    };
    
    // Log to external service (e.g., Sentry, LogRocket, etc.)
    this.logErrorToService(errorDetails);
    
    this.setState({
      error,
      errorInfo,
      eventId: this.generateEventId()
    });
  }
  
  logErrorToService = (errorDetails) => {
    // Example: Send to your error tracking service
    fetch('/api/errors', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(errorDetails)
    }).catch(err => console.error('Failed to log error:', err));
  };
  
  generateEventId = () => {
    return Math.random().toString(36).substr(2, 9);
  };
  
  render() {
    if (this.state.hasError) {
      return (
        <div className="error-boundary">
          <div className="error-content">
            <h1>Oops! Something went wrong</h1>
            <p>
              We've encountered an unexpected error. Our team has been notified 
              and is working on a fix.
            </p>
            
            {this.state.eventId && (
              <p>
                <strong>Error ID:</strong> {this.state.eventId}
                <br />
                <small>Please include this ID when contacting support.</small>
              </p>
            )}
            
            <div className="error-actions">
              <button 
                onClick={() => window.location.reload()}
                className="btn btn-primary"
              >
                Reload Page
              </button>
              
              <button 
                onClick={() => window.history.back()}
                className="btn btn-secondary"
              >
                Go Back
              </button>
              
              <button 
                onClick={() => this.setState({ 
                  hasError: false, 
                  error: null, 
                  errorInfo: null 
                })}
                className="btn btn-tertiary"
              >
                Try Again
              </button>
            </div>
            
            {this.props.showDetails && process.env.NODE_ENV === 'development' && (
              <details className="error-details">
                <summary>Technical Details</summary>
                <pre>{this.state.error?.toString()}</pre>
                <pre>{this.state.errorInfo?.componentStack}</pre>
              </details>
            )}
          </div>
        </div>
      );
    }
    
    return this.props.children;
  }
}
```

### Error Boundary Hook (React 18+)
```jsx
import { useState, useEffect } from 'react';

function useErrorHandler() {
  const [error, setError] = useState(null);
  
  const resetError = () => setError(null);
  
  const captureError = (error, errorInfo) => {
    setError({ error, errorInfo });
  };
  
  useEffect(() => {
    if (error) {
      console.error('Error captured:', error);
      // Log error to service
    }
  }, [error]);
  
  return { error, resetError, captureError };
}

// HOC for error handling
function withErrorBoundary(Component, errorComponent) {
  return function WithErrorBoundaryComponent(props) {
    return (
      <ErrorBoundary fallback={errorComponent}>
        <Component {...props} />
      </ErrorBoundary>
    );
  };
}

// Usage
const SafeComponent = withErrorBoundary(
  MyComponent,
  <div>Something went wrong with this component</div>
);
```

### Component-Specific Error Boundaries
```jsx
// Specific error boundary for async operations
class AsyncErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    if (error.name === 'ChunkLoadError') {
      // Handle code splitting errors
      window.location.reload();
      return;
    }
    
    console.error('Async operation failed:', error);
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div className="async-error">
          <h3>Loading Error</h3>
          <p>Failed to load this section. Please try refreshing the page.</p>
          <button onClick={() => window.location.reload()}>
            Refresh Page
          </button>
        </div>
      );
    }
    
    return this.props.children;
  }
}

// Route-level error boundary
class RouteErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    console.error('Route error:', error);
  }
  
  render() {
    if (this.state.hasError) {
      return (
        <div className="route-error">
          <h1>Page Not Found</h1>
          <p>The page you're looking for encountered an error.</p>
          <button onClick={() => window.location.href = '/'}>
            Go Home
          </button>
        </div>
      );
    }
    
    return this.props.children;
  }
}
```

### Using Error Boundaries in App Structure
```jsx
function App() {
  return (
    <ErrorBoundary>
      <div className="app">
        <RouteErrorBoundary>
          <Header />
        </RouteErrorBoundary>
        
        <main>
          <AsyncErrorBoundary>
            <Routes>
              <Route path="/" element={<Home />} />
              <Route path="/profile" element={<Profile />} />
              <Route path="/settings" element={<Settings />} />
            </Routes>
          </AsyncErrorBoundary>
        </main>
        
        <RouteErrorBoundary>
          <Footer />
        </RouteErrorBoundary>
      </div>
    </ErrorBoundary>
  );
}
```

**Practice Exercise**: Create an error boundary that handles different types of errors (network, rendering, chunk loading) with appropriate fallback UIs.

---

## Performance Optimization

React provides several techniques to optimize application performance.

### React.memo
```jsx
import React, { memo, useState } from 'react';

// Without memo - re-renders on every parent update
function ExpensiveComponent({ name, count }) {
  console.log('ExpensiveComponent rendered');
  
  // Simulate expensive computation
  const expensiveValue = useMemo(() => {
    let result = 0;
    for (let i = 0; i < 1000000; i++) {
      result += i;
    }
    return result;
  }, []);
  
  return (
    <div>
      <h3>Hello {name}</h3>
      <p>Count: {count}</p>
      <p>Expensive Value: {expensiveValue}</p>
    </div>
  );
}

// With memo - only re-renders when props change
const OptimizedComponent = memo(ExpensiveComponent);

// Custom comparison function
const OptimizedComponentWithCustomComparison = memo(ExpensiveComponent, (prevProps, nextProps) => {
  // Return true if props are equal (skip re-render)
  return prevProps.name === nextProps.name && prevProps.count === nextProps.count;
});

function Parent() {
  const [count, setCount] = useState(0);
  const [otherState, setOtherState] = useState(0);
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        Update Count: {count}
      </button>
      <button onClick={() => setOtherState(otherState + 1)}>
        Update Other State: {otherState}
      </button>
      
      {/* This will re-render unnecessarily */}
      <ExpensiveComponent name="John" count={count} />
      
      {/* This will only re-render when name or count changes */}
      <OptimizedComponent name="Jane" count={count} />
    </div>
  );
}
```

### useMemo Hook
```jsx
import React, { useMemo, useState } from 'react';

function ExpensiveList({ items, filter, sortBy }) {
  // Expensive computation - only runs when dependencies change
  const processedItems = useMemo(() => {
    console.log('Processing items...');
    
    return items
      .filter(item => item.name.toLowerCase().includes(filter.toLowerCase()))
      .sort((a, b) => {
        if (sortBy === 'name') return a.name.localeCompare(b.name);
        if (sortBy === 'price') return a.price - b.price;
        return 0;
      })
      .map(item => ({
        ...item,
        formattedPrice: `${item.price.toFixed(2)}`
      }));
  }, [items, filter, sortBy]);
  
  return (
    <div>
      <h3>Processed Items ({processedItems.length})</h3>
      {processedItems.map(item => (
        <div key={item.id}>
          <span>{item.name}</span> - <span>{item.formattedPrice}</span>
        </div>
      ))}
    </div>
  );
}

function App() {
  const [items] = useState([
    { id: 1, name: 'Apple', price: 1.50 },
    { id: 2, name: 'Banana', price: 0.75 },
    { id: 3, name: 'Orange', price: 2.00 }
  ]);
  const [filter, setFilter] = useState('');
  const [sortBy, setSortBy] = useState('name');
  const [unrelatedState, setUnrelatedState] = useState(0);
  
  return (
    <div>
      <input 
        value={filter}
        onChange={(e) => setFilter(e.target.value)}
        placeholder="Filter items..."
      />
      
      <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
        <option value="name">Sort by Name</option>
        <option value="price">Sort by Price</option>
      </select>
      
      <button onClick={() => setUnrelatedState(unrelatedState + 1)}>
        Unrelated Update: {unrelatedState}
      </button>
      
      <ExpensiveList items={items} filter={filter} sortBy={sortBy} />
    </div>
  );
}
```

### useCallback Hook
```jsx
import React, { useCallback, useState, memo } from 'react';

// Child component that receives callback as prop
const ChildComponent = memo(({ onButtonClick, title }) => {
  console.log(`ChildComponent (${title}) rendered`);
  
  return (
    <div>
      <h4>{title}</h4>
      <button onClick={onButtonClick}>Click me</button>
    </div>
  );
});

function Parent() {
  const [count, setCount] = useState(0);
  const [otherCount, setOtherCount] = useState(0);
  
  // Without useCallback - creates new function on every render
  const handleClick1 = () => {
    setCount(count + 1);
  };
  
  // With useCallback - memoizes function, only changes when dependencies change
  const handleClick2 = useCallback(() => {
    setOtherCount(prev => prev + 1);
  }, []); // Empty dependency array - function never changes
  
  const handleClick3 = useCallback(() => {
    setCount(prev => prev + count); // Depends on count
  }, [count]);
  
  return (
    <div>
      <p>Count: {count}</p>
      <p>Other Count: {otherCount}</p>
      
      {/* These will re-render unnecessarily due to new function reference */}
      <ChildComponent title="Child 1" onButtonClick={handleClick1} />
      
      {/* These will only re-render when necessary */}
      <ChildComponent title="Child 2" onButtonClick={handleClick2} />
      <ChildComponent title="Child 3" onButtonClick={handleClick3} />
      
      <button onClick={() => setCount(count + 1)}>Update Count</button>
    </div>
  );
}
```

### Code Splitting with React.lazy
```jsx
import React, { Suspense, lazy, useState } from 'react';

// Lazy load components
const HeavyComponent = lazy(() => import('./HeavyComponent'));
const AnotherComponent = lazy(() => import('./AnotherComponent'));

// Loading component
function LoadingSpinner() {
  return (
    <div style={{ display: 'flex', justifyContent: 'center', padding: '20px' }}>
      <div>Loading...</div>
    </div>
  );
}

// Error boundary for lazy components
function LazyErrorBoundary({ children }) {
  return (
    <ErrorBoundary
      fallback={
        <div>
          <h3>Failed to load component</h3>
          <button onClick={() => window.location.reload()}>
            Retry
          </button>
        </div>
      }
    >
      {children}
    </ErrorBoundary>
  );
}

function App() {
  const [currentView, setCurrentView] = useState('home');
  
  const renderView = () => {
    switch (currentView) {
      case 'heavy':
        return (
          <LazyErrorBoundary>
            <Suspense fallback={<LoadingSpinner />}>
              <HeavyComponent />
            </Suspense>
          </LazyErrorBoundary>
        );
      case 'another':
        return (
          <LazyErrorBoundary>
            <Suspense fallback={<LoadingSpinner />}>
              <AnotherComponent />
            </Suspense>
          </LazyErrorBoundary>
        );
      default:
        return <div>Home View</div>;
    }
  };
  
  return (
    <div>
      <nav>
        <button onClick={() => setCurrentView('home')}>Home</button>
        <button onClick={() => setCurrentView('heavy')}>Heavy Component</button>
        <button onClick={() => setCurrentView('another')}>Another Component</button>
      </nav>
      
      <main>
        {renderView()}
      </main>
    </div>
  );
}
```

### Virtual Scrolling
```jsx
import React, { useState, useMemo, useRef, useEffect } from 'react';

function VirtualizedList({ items, itemHeight = 50, containerHeight = 400 }) {
  const [scrollTop, setScrollTop] = useState(0);
  const containerRef = useRef();
  
  const visibleItems = useMemo(() => {
    const startIndex = Math.floor(scrollTop / itemHeight);
    const endIndex = Math.min(
      startIndex + Math.ceil(containerHeight / itemHeight) + 1,
      items.length
    );
    
    return items.slice(startIndex, endIndex).map((item, index) => ({
      ...item,
      index: startIndex + index
    }));
  }, [items, scrollTop, itemHeight, containerHeight]);
  
  const handleScroll = (e) => {
    setScrollTop(e.target.scrollTop);
  };
  
  const totalHeight = items.length * itemHeight;
  const offsetY = Math.floor(scrollTop / itemHeight) * itemHeight;
  
  return (
    <div
      ref={containerRef}
      style={{
        height: containerHeight,
        overflow: 'auto',
        border: '1px solid #ccc'
      }}
      onScroll={handleScroll}
    >
      <div style={{ height: totalHeight, position: 'relative' }}>
        <div style={{ transform: `translateY(${offsetY}px)` }}>
          {visibleItems.map(item => (
            <div
              key={item.id}
              style={{
                height: itemHeight,
                display: 'flex',
                alignItems: 'center',
                padding: '0 10px',
                borderBottom: '1px solid #eee'
              }}
            >
              #{item.index}: {item.name}
            </div>
          ))}
        </div>
      </div>
    </div>
  );
}

// Usage
function App() {
  const items = useMemo(() => 
    Array.from({ length: 10000 }, (_, i) => ({
      id: i,
      name: `Item ${i}`
    }))
  , []);
  
  return (
    <div>
      <h2>Virtualized List (10,000 items)</h2>
      <VirtualizedList items={items} />
    </div>
  );
}
```

### Performance Monitoring
```jsx
import React, { Profiler, useState } from 'react';

function onRenderCallback(id, phase, actualDuration, baseDuration, startTime, commitTime) {
  console.log('Profiler:', {
    id,
    phase, // 'mount' or 'update'
    actualDuration, // Time spent rendering the committed update
    baseDuration, // Estimated time to render the entire subtree without memoization
    startTime, // When React began rendering this update
    commitTime // When React committed this update
  });
  
  // Log to analytics service
  if (actualDuration > 16) { // More than one frame (60fps)
    console.warn(`Slow render detected in ${id}: ${actualDuration}ms`);
  }
}

function PerformanceMonitoredApp() {
  const [count, setCount] = useState(0);
  
  return (
    <Profiler id="App" onRender={onRenderCallback}>
      <div>
        <h1>Performance Monitored App</h1>
        <button onClick={() => setCount(count + 1)}>
          Count: {count}
        </button>
        
        <Profiler id="ExpensiveComponent" onRender={onRenderCallback}>
          <ExpensiveComponent count={count} />
        </Profiler>
      </div>
    </Profiler>
  );
}
```

### Bundle Analysis and Optimization
```jsx
// webpack-bundle-analyzer configuration
// package.json scripts:
// "analyze": "npm run build && npx webpack-bundle-analyzer build/static/js/*.js"

// Tree shaking - Import only what you need
// ❌ Bad - imports entire library
import _ from 'lodash';
import * as lodash from 'lodash';

// ✅ Good - imports only specific functions
import { debounce, throttle } from 'lodash';

// Dynamic imports for code splitting
const LazyChart = lazy(() => 
  import('chart.js').then(module => ({ default: module.Chart }))
);

// Preloading critical resources
function CriticalResourceLoader() {
  useEffect(() => {
    // Preload critical images
    const img = new Image();
    img.src = '/critical-image.jpg';
    
    // Preload critical data
    fetch('/api/critical-data').then(response => response.json());
  }, []);
  
  return null;
}
```

**Practice Exercise**: Optimize a large list component with virtualization, memoization, and code splitting.

---

## Testing

Testing ensures your React components work correctly and prevents regressions.

### Jest and React Testing Library Setup
```bash
# Install testing dependencies
npm install --save-dev @testing-library/react @testing-library/jest-dom @testing-library/user-event jest-environment-jsdom
```

### Basic Component Testing
```jsx
// Button.js
import React from 'react';

function Button({ children, onClick, disabled = false, variant = 'primary' }) {
  return (
    <button
      onClick={onClick}
      disabled={disabled}
      className={`btn btn-${variant}`}
      data-testid="button"
    >
      {children}
    </button>
  );
}

export default Button;

// Button.test.js
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import '@testing-library/jest-dom';
import Button from './Button';

describe('Button Component', () => {
  test('renders button with text', () => {
    render(<Button>Click me</Button>);
    
    const button = screen.getByRole('button', { name: /click me/i });
    expect(button).toBeInTheDocument();
  });
  
  test('calls onClick when clicked', async () => {
    const handleClick = jest.fn();
    const user = userEvent.setup();
    
    render(<Button onClick={handleClick}>Click me</Button>);
    
    const button = screen.getByRole('button');
    await user.click(button);
    
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
  
  test('is disabled when disabled prop is true', () => {
    render(<Button disabled>Click me</Button>);
    
    const button = screen.getByRole('button');
    expect(button).toBeDisabled();
  });
  
  test('applies correct CSS class for variant', () => {
    render(<Button variant="secondary">Click me</Button>);
    
    const button = screen.getByRole('button');
    expect(button).toHaveClass('btn btn-secondary');
  });
});
```

### Testing Components with State
```jsx
// Counter.js
import React, { useState } from 'react';

function Counter({ initialValue = 0, step = 1 }) {
  const [count, setCount] = useState(initialValue);
  
  const increment = () => setCount(count + step);
  const decrement = () => setCount(count - step);
  const reset = () => setCount(initialValue);
  
  return (
    <div>
      <h2 data-testid="count">Count: {count}</h2>
      <button onClick={increment} data-testid="increment">
        +{step}
      </button>
      <button onClick={decrement} data-testid="decrement">
        -{step}
      </button>
      <button onClick={reset} data-testid="reset">
        Reset
      </button>
    </div>
  );
}

export default Counter;

// Counter.test.js
import React from 'react';
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Counter from './Counter';

describe('Counter Component', () => {
  test('displays initial count', () => {
    render(<Counter initialValue={5} />);
    
    expect(screen.getByTestId('count')).toHaveTextContent('Count: 5');
  });
  
  test('increments count when increment button is clicked', async () => {
    const user = userEvent.setup();
    render(<Counter initialValue={0} step={2} />);
    
    const incrementButton = screen.getByTestId('increment');
    await user.click(incrementButton);
    
    expect(screen.getByTestId('count')).toHaveTextContent('Count: 2');
  });
  
  test('decrements count when decrement button is clicked', async () => {
    const user = userEvent.setup();
    render(<Counter initialValue={10} step={3} />);
    
    const decrementButton = screen.getByTestId('decrement');
    await user.click(decrementButton);
    
    expect(screen.getByTestId('count')).toHaveTextContent('Count: 7');
  });
  
  test('resets count when reset button is clicked', async () => {
    const user = userEvent.setup();
    render(<Counter initialValue={5} />);
    
    // Change the count first
    await user.click(screen.getByTestId('increment'));
    expect(screen.getByTestId('count')).toHaveTextContent('Count: 6');
    
    // Then reset
    await user.click(screen.getByTestId('reset'));
    expect(screen.getByTestId('count')).toHaveTextContent('Count: 5');
  });
});
```

### Testing Forms
```jsx
// LoginForm.js
import React, { useState } from 'react';

function LoginForm({ onSubmit, loading = false }) {
  const [formData, setFormData] = useState({
    email: '',
    password: ''
  });
  const [errors, setErrors] = useState({});
  
  const validateForm = () => {
    const newErrors = {};
    
    if (!formData.email) {
      newErrors.email = 'Email is required';
    } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
      newErrors.email = 'Email is invalid';
    }
    
    if (!formData.password) {
      newErrors.password = 'Password is required';
    } else if (formData.password.length < 6) {
      newErrors.password = 'Password must be at least 6 characters';
    }
    
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };
  
  const handleSubmit = (e) => {
    e.preventDefault();
    if (validateForm()) {
      onSubmit(formData);
    }
  };
  
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
    
    // Clear error when user starts typing
    if (errors[name]) {
      setErrors(prev => ({ ...prev, [name]: '' }));
    }
  };
  
  return (
    <form onSubmit={handleSubmit} data-testid="login-form">
      <div>
        <label htmlFor="email">Email:</label>
        <input
          id="email"
          name="email"
          type="email"
          value={formData.email}
          onChange={handleChange}
          data-testid="email-input"
        />
        {errors.email && (
          <div data-testid="email-error" role="alert">
            {errors.email}
          </div>
        )}
      </div>
      
      <div>
        <label htmlFor="password">Password:</label>
        <input
          id="password"
          name="password"
          type="password"
          value={formData.password}
          onChange={handleChange}
          data-testid="password-input"
        />
        {errors.password && (
          <div data-testid="password-error" role="alert">
            {errors.password}
          </div>
        )}
      </div>
      
      <button 
        type="submit" 
        disabled={loading}
        data-testid="submit-button"
      >
        {loading ? 'Logging in...' : 'Login'}
      </button>
    </form>
  );
}

export default LoginForm;

// LoginForm.test.js
import React from 'react';
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import LoginForm from './LoginForm';

describe('LoginForm Component', () => {
  const mockOnSubmit = jest.fn();
  
  beforeEach(() => {
    mockOnSubmit.mockClear();
  });
  
  test('renders form fields', () => {
    render(<LoginForm onSubmit={mockOnSubmit} />);
    
    expect(screen.getByLabelText(/email/i)).toBeInTheDocument();
    expect(screen.getByLabelText(/password/i)).toBeInTheDocument();
    expect(screen.getByRole('button', { name: /login/i })).toBeInTheDocument();
  });
  
  test('shows validation errors for empty fields', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);
    
    const submitButton = screen.getByRole('button', { name: /login/i });
    await user.click(submitButton);
    
    expect(screen.getByTestId('email-error')).toHaveTextContent('Email is required');
    expect(screen.getByTestId('password-error')).toHaveTextContent('Password is required');
    expect(mockOnSubmit).not.toHaveBeenCalled();
  });
  
  test('shows validation error for invalid email', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);
    
    await user.type(screen.getByTestId('email-input'), 'invalid-email');
    await user.click(screen.getByRole('button', { name: /login/i }));
    
    expect(screen.getByTestId('email-error')).toHaveTextContent('Email is invalid');
  });
  
  test('shows validation error for short password', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);
    
    await user.type(screen.getByTestId('password-input'), '123');
    await user.click(screen.getByRole('button', { name: /login/i }));
    
    expect(screen.getByTestId('password-error')).toHaveTextContent('Password must be at least 6 characters');
  });
  
  test('submits form with valid data', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);
    
    await user.type(screen.getByTestId('email-input'), 'test@example.com');
    await user.type(screen.getByTestId('password-input'), 'password123');
    await user.click(screen.getByRole('button', { name: /login/i }));
    
    expect(mockOnSubmit).toHaveBeenCalledWith({
      email: 'test@example.com',
      password: 'password123'
    });
  });
  
  test('clears errors when user starts typing', async () => {
    const user = userEvent.setup();
    render(<LoginForm onSubmit={mockOnSubmit} />);
    
    // Trigger validation errors
    await user.click(screen.getByRole('button', { name: /login/i }));
    expect(screen.getByTestId('email-error')).toBeInTheDocument();
    
    // Start typing to clear error
    await user.type(screen.getByTestId('email-input'), 'test');
    expect(screen.queryByTestId('email-error')).not.toBeInTheDocument();
  });
  
  test('shows loading state', () => {
    render(<LoginForm onSubmit={mockOnSubmit} loading={true} />);
    
    const submitButton = screen.getByRole('button');
    expect(submitButton).toHaveTextContent('Logging in...');
    expect(submitButton).toBeDisabled();
  });
});
```

### Testing API Calls and Async Operations
```jsx
// UserProfile.js
import React, { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    const fetchUser = async () => {
      try {
        setLoading(true);
        setError(null);
        
        const response = await fetch(`/api/users/${userId}`);
        if (!response.ok) {
          throw new Error('Failed to fetch user');
        }
        
        const userData = await response.json();
        setUser(userData);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    
    if (userId) {
      fetchUser();
    }
  }, [userId]);
  
  if (loading) {
    return <div data-testid="loading">Loading...</div>;
  }
  
  if (error) {
    return <div data-testid="error">Error: {error}</div>;
  }
  
  if (!user) {
    return <div data-testid="no-user">No user found</div>;
  }
  
  return (
    <div data-testid="user-profile">
      <h2>{user.name}</h2>
      <p>Email: {user.email}</p>
      <p>Role: {user.role}</p>
    </div>
  );
}

export default UserProfile;

// UserProfile.test.js
import React from 'react';
import { render, screen, waitFor } from '@testing-library/react';
import UserProfile from './UserProfile';

// Mock fetch
global.fetch = jest.fn();

describe('UserProfile Component', () => {
  beforeEach(() => {
    fetch.mockClear();
  });
  
  test('shows loading state initially', () => {
    fetch.mockResolvedValueOnce({
      ok: true,
      json: async () => ({ id: 1, name: 'John', email: 'john@example.com', role: 'user' })
    });
    
    render(<UserProfile userId={1} />);
    
    expect(screen.getByTestId('loading')).toBeInTheDocument();
  });
  
  test('displays user data after successful fetch', async () => {
    const mockUser = {
      id: 1,
      name: 'John Doe',
      email: 'john@example.com',
      role: 'admin'
    };
    
    fetch.mockResolvedValueOnce({
      ok: true,
      json: async () => mockUser
    });
    
    render(<UserProfile userId={1} />);
    
    await waitFor(() => {
      expect(screen.getByTestId('user-profile')).toBeInTheDocument();
    });
    
    expect(screen.getByText('John Doe')).toBeInTheDocument();
    expect(screen.getByText('Email: john@example.com')).toBeInTheDocument();
    expect(screen.getByText('Role: admin')).toBeInTheDocument();
  });
  
  test('displays error message when fetch fails', async () => {
    fetch.mockRejectedValueOnce(new Error('Network error'));
    
    render(<UserProfile userId={1} />);
    
    await waitFor(() => {
      expect(screen.getByTestId('error')).toBeInTheDocument();
    });
    
    expect(screen.getByText('Error: Network error')).toBeInTheDocument();
  });
  
  test('displays error when API returns error status', async () => {
    fetch.mockResolvedValueOnce({
      ok: false,
      status: 404
    });
    
    render(<UserProfile userId={1} />);
    
    await waitFor(() => {
      expect(screen.getByTestId('error')).toBeInTheDocument();
    });
    
    expect(screen.getByText('Error: Failed to fetch user')).toBeInTheDocument();
  });
  
  test('does not fetch when userId is not provided', () => {
    render(<UserProfile />);
    
    expect(fetch).not.toHaveBeenCalled();
    expect(screen.getByTestId('loading')).toBeInTheDocument();
  });
  
  test('refetches when userId changes', async () => {
    const mockUser1 = { id: 1, name: 'John', email: 'john@example.com', role: 'user' };
    const mockUser2 = { id: 2, name: 'Jane', email: 'jane@example.com', role: 'admin' };
    
    fetch
      .mockResolvedValueOnce({
        ok: true,
        json: async () => mockUser1
      })
      .mockResolvedValueOnce({
        ok: true,
        json: async () => mockUser2
      });
    
    const { rerender } = render(<UserProfile userId={1} />);
    
    await waitFor(() => {
      expect(screen.getByText('John')).toBeInTheDocument();
    });
    
    rerender(<UserProfile userId={2} />);
    
    await waitFor(() => {
      expect(screen.getByText('Jane')).toBeInTheDocument();
    });
    
    expect(fetch).toHaveBeenCalledTimes(2);
    expect(fetch).toHaveBeenCalledWith('/api/users/1');
    expect(fetch).toHaveBeenCalledWith('/api/users/2');
  });
});
```

### Testing Context and Custom Hooks
```jsx
// useAuth.js - Custom hook
import { useState, useContext, createContext } from 'react';

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  
  const login = async (credentials) => {
    const response = await fetch('/api/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(credentials)
    });
    
    if (response.ok) {
      const userData = await response.json();
      setUser(userData);
      setIsAuthenticated(true);
      return { success: true };
    } else {
      return { success: false, error: 'Invalid credentials' };
    }
  };
  
  const logout = () => {
    setUser(null);
    setIsAuthenticated(false);
  };
  
  return (
    <AuthContext.Provider value={{ user, isAuthenticated, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within AuthProvider');
  }
  return context;
}

// useAuth.test.js
import React from 'react';
import { render, screen, act } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { AuthProvider, useAuth } from './useAuth';

// Test component that uses the hook
function TestComponent() {
  const { user, isAuthenticated, login, logout } = useAuth();
  
  return (
    <div>
      <div data-testid="auth-status">
        {isAuthenticated ? `Logged in as ${user?.name}` : 'Not logged in'}
      </div>
      <button
        onClick={() => login({ email: 'test@example.com', password: 'password' })}
        data-testid="login-button"
      >
        Login
      </button>
      <button onClick={logout} data-testid="logout-button">
        Logout
      </button>
    </div>
  );
}

// Mock fetch
global.fetch = jest.fn();

describe('useAuth Hook', () => {
  beforeEach(() => {
    fetch.mockClear();
  });
  
  const renderWithProvider = (component) => {
    return render(
      <AuthProvider>
        {component}
      </AuthProvider>
    );
  };
  
  test('initial state is not authenticated', () => {
    renderWithProvider(<TestComponent />);
    
    expect(screen.getByTestId('auth-status')).toHaveTextContent('Not logged in');
  });
  
  test('login sets user and authentication status', async () => {
    const user = userEvent.setup();
    const mockUser = { id: 1, name: 'John Doe', email: 'test@example.com' };
    
    fetch.mockResolvedValueOnce({
      ok: true,
      json: async () => mockUser
    });
    
    renderWithProvider(<TestComponent />);
    
    await user.click(screen.getByTestId('login-button'));
    
    expect(screen.getByTestId('auth-status')).toHaveTextContent('Logged in as John Doe');
  });
  
  test('logout clears user and authentication status', async () => {
    const user = userEvent.setup();
    const mockUser = { id: 1, name: 'John Doe', email: 'test@example.com' };
    
    fetch.mockResolvedValueOnce({
      ok: true,
      json: async () => mockUser
    });
    
    renderWithProvider(<TestComponent />);
    
    // Login first
    await user.click(screen.getByTestId('login-button'));
    expect(screen.getByTestId('auth-status')).toHaveTextContent('Logged in as John Doe');
    
    // Then logout
    await user.click(screen.getByTestId('logout-button'));
    expect(screen.getByTestId('auth-status')).toHaveTextContent('Not logged in');
  });
  
  test('throws error when used outside provider', () => {
    // Suppress console.error for this test
    const consoleSpy = jest.spyOn(console, 'error').mockImplementation(() => {});
    
    expect(() => {
      render(<TestComponent />);
    }).toThrow('useAuth must be used within AuthProvider');
    
    consoleSpy.mockRestore();
  });
});
```

### Testing with Mock Service Worker (MSW)
```jsx
// setupTests.js
import { setupServer } from 'msw/node';
import { rest } from 'msw';

// Setup MSW server
export const server = setupServer(
  rest.get('/api/users/:id', (req, res, ctx) => {
    const { id } = req.params;
    
    const users = {
      '1': { id: 1, name: 'John Doe', email: 'john@example.com', role: 'admin' },
      '2': { id: 2, name: 'Jane Smith', email: 'jane@example.com', role: 'user' }
    };
    
    const user = users[id];
    
    if (user) {
      return res(ctx.json(user));
    } else {
      return res(ctx.status(404), ctx.json({ error: 'User not found' }));
    }
  }),
  
  rest.post('/api/login', (req, res, ctx) => {
    const { email, password } = req.body;
    
    if (email === 'test@example.com' && password === 'password') {
      return res(ctx.json({ 
        id: 1, 
        name: 'Test User', 
        email: 'test@example.com' 
      }));
    } else {
      return res(ctx.status(401), ctx.json({ error: 'Invalid credentials' }));
    }
  })
);

// Start server before all tests
beforeAll(() => server.listen());

// Reset handlers after each test
afterEach(() => server.resetHandlers());

// Close server after all tests
afterAll(() => server.close());

// UserProfile.msw.test.js
import React from 'react';
import { render, screen, waitFor } from '@testing-library/react';
import { server } from './setupTests';
import { rest } from 'msw';
import UserProfile from './UserProfile';

describe('UserProfile with MSW', () => {
  test('displays user data', async () => {
    render(<UserProfile userId={1} />);
    
    await waitFor(() => {
      expect(screen.getByTestId('user-profile')).toBeInTheDocument();
    });
    
    expect(screen.getByText('John Doe')).toBeInTheDocument();
    expect(screen.getByText('Email: john@example.com')).toBeInTheDocument();
  });
  
  test('handles API error', async () => {
    // Override the default handler for this test
    server.use(
      rest.get('/api/users/:id', (req, res, ctx) => {
        return res(ctx.status(500), ctx.json({ error: 'Server error' }));
      })
    );
    
    render(<UserProfile userId={1} />);
    
    await waitFor(() => {
      expect(screen.getByTestId('error')).toBeInTheDocument();
    });
  });
});
```

### Integration Testing
```jsx
// App.integration.test.js
import React from 'react';
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { BrowserRouter } from 'react-router-dom';
import App from './App';
import { AuthProvider } from './contexts/AuthContext';

// Wrapper component for providers
function AppWrapper({ children }) {
  return (
    <BrowserRouter>
      <AuthProvider>
        {children}
      </AuthProvider>
    </BrowserRouter>
  );
}

describe('App Integration Tests', () => {
  test('complete user login flow', async () => {
    const user = userEvent.setup();
    
    render(<App />, { wrapper: AppWrapper });
    
    // Initially not logged in
    expect(screen.getByText(/login/i)).toBeInTheDocument();
    
    // Fill in login form
    await user.type(screen.getByLabelText(/email/i), 'test@example.com');
    await user.type(screen.getByLabelText(/password/i), 'password');
    await user.click(screen.getByRole('button', { name: /login/i }));
    
    // Should be logged in and see dashboard
    await waitFor(() => {
      expect(screen.getByText(/welcome/i)).toBeInTheDocument();
    });
    
    // Should be able to logout
    await user.click(screen.getByRole('button', { name: /logout/i }));
    
    await waitFor(() => {
      expect(screen.getByText(/login/i)).toBeInTheDocument();
    });
  });
  
  test('navigation between routes', async () => {
    const user = userEvent.setup();
    
    render(<App />, { wrapper: AppWrapper });
    
    // Navigate to different routes
    await user.click(screen.getByRole('link', { name: /about/i }));
    expect(screen.getByText(/about page/i)).toBeInTheDocument();
    
    await user.click(screen.getByRole('link', { name: /contact/i }));
    expect(screen.getByText(/contact page/i)).toBeInTheDocument();
  });
});
```

**Practice Exercise**: Write comprehensive tests for a todo app including components, hooks, context, and API interactions.

---

## Best Practices

Following best practices ensures maintainable, performant, and scalable React applications.

### Component Organization
```jsx
// ✅ Good - Single Responsibility Principle
function UserCard({ user }) {
  return (
    <div className="user-card">
      <UserAvatar src={user.avatar} alt={user.name} />
      <UserInfo name={user.name} email={user.email} />
      <UserActions userId={user.id} />
    </div>
  );
}

// ❌ Bad - Too many responsibilities
function UserCard({ user, onEdit, onDelete, onMessage, showActions, theme }) {
  const [isEditing, setIsEditing] = useState(false);
  const [message, setMessage] = useState('');
  
  // Too much logic in one component
  return (
    <div className={`user-card ${theme}`}>
      {/* Complex nested JSX */}
    </div>
  );
}
```

### Prop Types and TypeScript
```jsx
// With PropTypes
import PropTypes from 'prop-types';

function Button({ children, onClick, variant, size, disabled }) {
  return (
    <button
      className={`btn btn-${variant} btn-${size}`}
      onClick={onClick}
      disabled={disabled}
    >
      {children}
    </button>
  );
}

Button.propTypes = {
  children: PropTypes.node.isRequired,
  onClick: PropTypes.func,
  variant: PropTypes.oneOf(['primary', 'secondary', 'danger']),
  size: PropTypes.oneOf(['small', 'medium', 'large']),
  disabled: PropTypes.bool
};

Button.defaultProps = {
  variant: 'primary',
  size: 'medium',
  disabled: false
};

// With TypeScript (preferred)
interface ButtonProps {
  children: React.ReactNode;
  onClick?: () => void;
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'small' | 'medium' | 'large';
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ 
  children, 
  onClick, 
  variant = 'primary', 
  size = 'medium', 
  disabled = false 
}) => {
  return (
    <button
      className={`btn btn-${variant} btn-${size}`}
      onClick={onClick}
      disabled={disabled}
    >
      {children}
    </button>
  );
};
```

### Custom Hooks Best Practices
```jsx
// ✅ Good - Reusable and focused
function useApi(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  
  const fetchData = useCallback(async () => {
    try {
      setLoading(true);
      setError(null);
      const response = await fetch(url);
      const result = await response.json();
      setData(result);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  }, [url]);
  
  useEffect(() => {
    if (url) {
      fetchData();
    }
  }, [url, fetchData]);
  
  return { data, loading, error, refetch: fetchData };
}

// ✅ Good - Input handling hook
function useFormInput(initialValue) {
  const [value, setValue] = useState(initialValue);
  
  const handleChange = useCallback((e) => {
    setValue(e.target.value);
  }, []);
  
  const reset = useCallback(() => {
    setValue(initialValue);
  }, [initialValue]);
  
  return {
    value,
    onChange: handleChange,
    reset
  };
}

// Usage
function ContactForm() {
  const name = useFormInput('');
  const email = useFormInput('');
  const message = useFormInput('');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log({
      name: name.value,
      email: email.value,
      message: message.value
    });
    
    // Reset form
    name.reset();
    email.reset();
    message.reset();
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="Name" {...name} />
      <input type="email" placeholder="Email" {...email} />
      <textarea placeholder="Message" {...message} />
      <button type="submit">Send</button>
    </form>
  );
}
```

### State Management Patterns
```jsx
// ✅ Good - Lift state up when needed
function App() {
  const [user, setUser] = useState(null);
  const [cart, setCart] = useState([]);
  
  return (
    <div>
      <Header user={user} cartCount={cart.length} />
      <ProductList onAddToCart={(product) => setCart([...cart, product])} />
      <Cart items={cart} onUpdateCart={setCart} />
    </div>
  );
}

// ✅ Good - Use useReducer for complex state
const cartReducer = (state, action) => {
  switch (action.type) {
    case 'ADD_ITEM':
      const existingItem = state.find(item => item.id === action.payload.id);
      if (existingItem) {
        return state.map(item =>
          item.id === action.payload.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      }
      return [...state, { ...action.payload, quantity: 1 }];
      
    case 'REMOVE_ITEM':
      return state.filter(item => item.id !== action.payload);
      
    case 'UPDATE_QUANTITY':
      return state.map(item =>
        item.id === action.payload.id
          ? { ...item, quantity: action.payload.quantity }
          : item
      );
      
    default:
      return state;
  }
};

function ShoppingCart() {
  const [cart, dispatch] = useReducer(cartReducer, []);
  
  return (
    <div>
      {cart.map(item => (
        <div key={item.id}>
          <span>{item.name}</span>
          <button onClick={() => dispatch({ type: 'REMOVE_ITEM', payload: item.id })}>
            Remove
          </button>
        </div>
      ))}
    </div>
  );
}
```

### Performance Best Practices
```jsx
// ✅ Good - Memoize expensive calculations
function ExpensiveComponent({ items, filter }) {
  const filteredItems = useMemo(() => {
    return items.filter(item => 
      item.name.toLowerCase().includes(filter.toLowerCase())
    );
  }, [items, filter]);
  
  return (
    <div>
      {filteredItems.map(item => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
}

// ✅ Good - Memoize callbacks
function TodoList({ todos, onToggle, onDelete }) {
  const handleToggle = useCallback((id) => {
    onToggle(id);
  }, [onToggle]);
  
  const handleDelete = useCallback((id) => {
    onDelete(id);
  }, [onDelete]);
  
  return (
    <div>
      {todos.map(todo => (
        <TodoItem
          key={todo.id}
          todo={todo}
          onToggle={handleToggle}
          onDelete={handleDelete}
        />
      ))}
    </div>
  );
}

// ✅ Good - Use React.memo for pure components
const TodoItem = memo(({ todo, onToggle, onDelete }) => {
  return (
    <div>
      <span
        style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}
        onClick={() => onToggle(todo.id)}
      >
        {todo.text}
      </span>
      <button onClick={() => onDelete(todo.id)}>Delete</button>
    </div>
  );
});
```

### Error Handling Best Practices
```jsx
// ✅ Good - Comprehensive error handling
function DataFetcher({ url }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    const abortController = new AbortController();
    
    const fetchData = async () => {
      try {
        setLoading(true);
        setError(null);
        
        const response = await fetch(url, {
          signal: abortController.signal
        });
        
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const result = await response.json();
        setData(result);
      } catch (err) {
        if (err.name !== 'AbortError') {
          setError(err.message);
        }
      } finally {
        setLoading(false);
      }
    };
    
    fetchData();
    
    return () => {
      abortController.abort();
    };
  }, [url]);
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!data) return <div>No data</div>;
  
  return <div>{JSON.stringify(data)}</div>;
}

// ✅ Good - Error boundary usage
function App() {
  return (
    <ErrorBoundary>
      <Router>
        <Routes>
          <Route path="/" element={
            <ErrorBoundary>
              <Home />
            </ErrorBoundary>
          } />
          <Route path="/profile" element={
            <ErrorBoundary>
              <Profile />
            </ErrorBoundary>
          } />
        </Routes>
      </Router>
    </ErrorBoundary>
  );
}
```

### Accessibility Best Practices
```jsx
// ✅ Good - Accessible form
function AccessibleForm() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: ''
  });
  const [errors, setErrors] = useState({});
  
  return (
    <form role="form" aria-label="Contact form">
      <div>
        <label htmlFor="name">
          Name *
        </label>
        <input
          id="name"
          type="text"
          value={formData.name}
          onChange={(e) => setFormData({...formData, name: e.target.value})}
          aria-required="true"
          aria-invalid={!!errors.name}
          aria-describedby={errors.name ? "name-error" : undefined}
        />
        {errors.name && (
          <div id="name-error" role="alert" aria-live="polite">
            {errors.name}
          </div>
        )}
      </div>
      
      <div>
        <label htmlFor="email">
          Email *
        </label>
        <input
          id="email"
          type="email"
          value={formData.email}
          onChange={(e) => setFormData({...formData, email: e.target.value})}
          aria-required="true"
          aria-invalid={!!errors.email}
          aria-describedby={errors.email ? "email-error" : undefined}
        />
        {errors.email && (
          <div id="email-error" role="alert" aria-live="polite">
            {errors.email}
          </div>
        )}
      </div>
      
      <button type="submit" aria-describedby="submit-help">
        Send Message
      </button>
      <div id="submit-help">
        All fields marked with * are required
      </div>
    </form>
  );
}

// ✅ Good - Accessible modal
function Modal({ isOpen, onClose, children, title }) {
  const modalRef = useRef();
  
  useEffect(() => {
    if (isOpen) {
      modalRef.current?.focus();
    }
  }, [isOpen]);
  
  useEffect(() => {
    const handleEscape = (e) => {
      if (e.key === 'Escape') {
        onClose();
      }
    };
    
    if (isOpen) {
      document.addEventListener('keydown', handleEscape);
      document.body.style.overflow = 'hidden';
    }
    
    return () => {
      document.removeEventListener('keydown', handleEscape);
      document.body.style.overflow = 'unset';
    };
  }, [isOpen, onClose]);
  
  if (!isOpen) return null;
  
  return (
    <div
      className="modal-overlay"
      onClick={onClose}
      role="dialog"
      aria-modal="true"
      aria-labelledby="modal-title"
    >
      <div
        ref={modalRef}
        className="modal-content"
        onClick={(e) => e.stopPropagation()}
        tabIndex={-1}
      >
        <div className="modal-header">
          <h2 id="modal-title">{title}</h2>
          <button
            onClick={onClose}
            aria-label="Close modal"
            className="modal-close"
          >
            ×
          </button>
        </div>
        <div className="modal-body">
          {children}
        </div>
      </div>
    </div>
  );
}
```

### Code Organization and Structure
```
src/
├── components/           # Reusable UI components
│   ├── common/          # Generic components (Button, Modal, etc.)
│   ├── forms/           # Form-related components
│   └── layout/          # Layout components (Header, Footer, etc.)
├── pages/               # Page components
├── hooks/               # Custom hooks
├── contexts/            # React contexts
├── services/            # API calls and external services
├── utils/               # Utility functions
├── constants/           # Application constants
├── types/               # TypeScript type definitions
├── __tests__/           # Test files
└── assets/              # Images, fonts, etc.
```

### Folder Structure Example
```jsx
// components/common/Button/index.js
export { default } from './Button';

// components/common/Button/Button.js
import React from 'react';
import PropTypes from 'prop-types';
import './Button.css';

const Button = ({ children, variant, size, ...props }) => {
  return (
    <button
      className={`btn btn--${variant} btn--${size}`}
      {...props}
    >
      {children}
    </button>
  );
};

Button.propTypes = {
  children: PropTypes.node.isRequired,
  variant: PropTypes.oneOf(['primary', 'secondary']),
  size: PropTypes.oneOf(['small', 'medium', 'large'])
};

Button.defaultProps = {
  variant: 'primary',
  size: 'medium'
};

export default Button;

// Usage
import Button from 'components/common/Button';

function App() {
  return (
    <Button variant="secondary" size="large">
      Click me
    </Button>
  );
}
```

**Practice Exercise**: Refactor an existing React app to follow these best practices, including proper component organization, accessibility, and performance optimizations.

---

## Practice Projects

Here are progressive projects to practice React concepts:

### Project 1: Todo App (Beginner)
**Skills Practiced**: Components, State, Event Handling, Lists, Forms

**Features to Implement**:
- Add new todos
- Mark todos as complete/incomplete
- Delete todos
- Filter todos (All, Active, Completed)
- Edit existing todos
- Local storage persistence

**Component Structure**:
```jsx
App
├── TodoHeader
├── TodoForm
├── TodoFilters
├── TodoList
│   └── TodoItem
└── TodoFooter
```

### Project 2: Weather App (Beginner-Intermediate)
**Skills Practiced**: API calls, useEffect, Error handling, Conditional rendering

**Features to Implement**:
- Current weather display
- 5-day forecast
- Search by city
- Geolocation support
- Loading states
- Error handling
- Weather icons

### Project 3: E-commerce Product Catalog (Intermediate)
**Skills Practiced**: Complex state, useReducer, Context API, Performance optimization

**Features to Implement**:
- Product listing with pagination
- Search and filtering
- Shopping cart functionality
- Product details modal
- Category navigation
- Sort options
- Wishlist functionality

**State Management**:
```jsx
// CartContext.js
const cartReducer = (state, action) => {
  switch (action.type) {
    case 'ADD_TO_CART':
      // Implementation
    case 'REMOVE_FROM_CART':
      // Implementation
    case 'UPDATE_QUANTITY':
      // Implementation
    default:
      return state;
  }
};
```

### Project 4: Social Media Dashboard (Intermediate-Advanced)
**Skills Practiced**: Complex routing, Authentication, Real-time updates, Advanced state management

**Features to Implement**:
- User authentication
- Post creation and editing
- Comments and likes
- User profiles
- Follow/unfollow functionality
- Real-time notifications
- Image upload
- Responsive design

### Project 5: Project Management Tool (Advanced)
**Skills Practiced**: Drag and drop, Complex forms, Data visualization, Testing

**Features to Implement**:
- Kanban board with drag & drop
- Project and task management
- Team collaboration
- Time tracking
- Charts and analytics
- File attachments
- Real-time collaboration

**Advanced Components**:
```jsx
// DragDropBoard.js
import { DragDropContext, Droppable, Draggable } from 'react-beautiful-dnd';

function KanbanBoard({ columns, onTaskMove }) {
  const handleDragEnd = (result) => {
    // Handle drag and drop logic
  };
  
  return (
    <DragDropContext onDragEnd={handleDragEnd}>
      {columns.map(column => (
        <Droppable key={column.id} droppableId={column.id}>
          {(provided) => (
            <div ref={provided.innerRef} {...provided.droppableProps}>
              {column.tasks.map((task, index) => (
                <Draggable key={task.id} draggableId={task.id} index={index}>
                  {(provided) => (
                    <div
                      ref={provided.innerRef}
                      {...provided.draggableProps}
                      {...provided.dragHandleProps}
                    >
                      <TaskCard task={task} />
                    </div>
                  )}
                </Draggable>
              ))}
              {provided.placeholder}
            </div>
          )}
        </Droppable>
      ))}
    </DragDropContext>
  );
}
```

### Project Implementation Tips

1. **Start Small**: Begin with basic functionality and gradually add features
2. **Plan Your State**: Design your state structure before coding
3. **Component Design**: Think about reusability and single responsibility
4. **Testing**: Write tests as you develop, not after
5. **Performance**: Use React DevTools Profiler to identify bottlenecks
6. **Accessibility**: Test with screen readers and keyboard navigation
7. **Mobile First**: Design for mobile devices first, then scale up

### Learning Path Recommendation

1. **Week 1-2**: Complete Todo App and Weather App
2. **Week 3-4**: Build E-commerce Product Catalog
3. **Week 5-6**: Create Social Media Dashboard
4. **Week 7-8**: Develop Project Management Tool
5. **Week 9-10**: Add advanced features and optimizations

### Additional Learning Resources

- **React Documentation**: https://react.dev/
- **React DevTools**: Browser extension for debugging
- **Storybook**: Tool for building UI components in isolation
- **React Hook Form**: Library for efficient form handling
- **React Query**: Data fetching and state management
- **React Router**: Client-side routing
- **Styled Components**: CSS-in-JS styling solution

### Next Steps After Mastering React

1. **Next.js**: Full-stack React framework
2. **React Native**: Mobile app development
3. **State Management Libraries**: Redux, Zustand, Jotai
4. **Testing Libraries**: Cypress, Playwright
5. **Build Tools**: Webpack, Vite, Parcel
6. **TypeScript**: Add type safety to your React apps

Remember: The key to mastering React is consistent practice and building real projects. Start with simple projects and gradually increase complexity as you become more comfortable with the concepts.

---

## Conclusion

This comprehensive guide covers all essential React concepts from basic components to advanced patterns. Remember that React is a powerful library, but mastering it requires hands-on practice. Start with the fundamentals, build projects, write tests, and gradually explore advanced topics.

The most important advice: **Build, build, build!** There's no substitute for practical experience when learning React. Each project will teach you something new and help solidify your understanding of React concepts.

Good luck on your React journey!
