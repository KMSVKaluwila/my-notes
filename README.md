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
