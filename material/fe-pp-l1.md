# Rendering a List  in React

## Part 1: Rendering a List of Todos in React

#### Objective:

In this part, you will render a list of todo items in React. This final part reinforces the same list-rendering pattern one last time.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part1 --template react
   cd rweek3-pp-part1
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part1` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

**Why this matters:**
Todo lists are a common real-world example. Each todo item is stored as an object inside an array.

1. In the `src` directory, create a file named `todosData.js`.
2. Add the following array of todo objects:

```js
const todosData = [
  {
    id: 1,
    task: "Learn React lists",
    completed: "No",
  },
  {
    id: 2,
    task: "Practice using map()",
    completed: "Yes",
  },
  {
    id: 3,
    task: "Build a small project",
    completed: "No",
  },
];

export default todosData;
```

### Step 2: Create a Todo Component

**Why this matters:**
Each todo item is rendered using the same component, making the list easy to maintain and update later.

1. Create a file named `Todo.jsx` in the `src` directory.
2. Add the following code:

```jsx
import React from 'react';

function Todo({ todo }) {
  return (
    <div className="todo">
      <h2 className="todo-task">{todo.task}</h2>
      <p><strong>Completed:</strong> {todo.completed}</p>
    </div>
  );
}

export default Todo;
```


### Step 3: Style the Todo Component

**Why this matters:**
Clear styling helps users quickly distinguish between different todo items.

1. Create a file named `Todo.css` in the `src` directory.
2. Add the following styles:

```css
.todo {
  background-color: #fff0f6;
  border: 1px solid #fcc2d7;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.todo-task {
  font-size: 1.2rem;
  margin: 0;
  color: #a61e4d;
}
```

### Step 4: Render Todos in App Component

**Why this matters:**
The same `map()` logic applies, even though the data represents tasks instead of books, jobs, or users.

1. Open `App.jsx` and remove all content.
2. Import the required files:

```jsx
import Todo from './Todo';
import todosData from './todosData';
import './Todo.css';
```

3. Render the todo list:

```jsx
function App() {
  return (
    <div className="App">
      <h1>Todo List</h1>
      <div className="todo-list">
        {todosData.map((todo) => (
          <Todo key={todo.id} todo={todo} />
        ))}
      </div>
    </div>
  );
}

export default App;
```


### Step 5: Test Your Application

* Visit `http://localhost:5173`.
* You should see **three todo items** rendered.
* Confirm there are no key warnings in the console.

----

## Part 2: Rendering a List of Jobs in React

#### Objective:

In this part, you will practice rendering lists in React by displaying a list of jobs using the `map()` function. This part follows the same pattern as Part 1 but uses different data.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part2 --template react
   cd rweek3-pp-part2
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part2` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

1. Inside the `src` directory, create a new file named `jobsData.js`.
2. Add an array of **three job objects** to the file:

```js
const jobsData = [
  {
    id: 1,
    title: "Frontend Developer",
    company: "Tech Corp",
    location: "Remote",
  },
  {
    id: 2,
    title: "Backend Developer",
    company: "Code Labs",
    location: "New York",
  },
  {
    id: 3,
    title: "UI/UX Designer",
    company: "Creative Studio",
    location: "London",
  },
];

export default jobsData;
```

### Step 2: Create a Job Component

1. Create a new file named `Job.jsx` in the `src` directory.
2. Add the following code to display a single job:

```jsx
import React from 'react';

function Job({ job }) {
  return (
    <div className="job">
      <h2 className="job-title">{job.title}</h2>
      <p><strong>Company:</strong> {job.company}</p>
      <p><strong>Location:</strong> {job.location}</p>
    </div>
  );
}

export default Job;
```

### Step 3: Style the Job Component

1. Create a new CSS file named `Job.css` in the `src` directory.
2. Add the following styles:

```css
.job {
  background-color: #eef6ff;
  border: 1px solid #b3d4fc;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.job-title {
  font-size: 1.2rem;
  margin: 0;
  color: #1a4fa3;
}
```

### Step 4: Render the Jobs in App Component

1. Open `App.jsx` and delete all existing content.
2. Import the required files at the top:

```jsx
import Job from './Job';
import jobsData from './jobsData';
import './Job.css';
```

3. Use the `map()` function to render the list of jobs:

```jsx
function App() {
  return (
    <div className="App">
      <h1>Job Listings</h1>
      <div className="job-list">
        {jobsData.map((job) => (
          <Job key={job.id} job={job} />
        ))}
      </div>
    </div>
  );
}

export default App;
```


### Step 5: Test Your Application

1. Ensure your development server is running.
2. Open your browser at `http://localhost:5173`.
3. You should see **three job listings** rendered on the page.
4. Open the browser console and confirm there are **no key warnings**.


### Key Takeaway

* The process of rendering lists in React remains the same:

  * Store data in an array
  * Create a reusable component
  * Use `map()` to render each item
  * Always provide a **unique `key` prop**

----

## Part 3: Rendering a List of Users in React

#### Objective:

In this part, you will render a list of users in React using the `map()` function. The steps are the same as in the previous parts; only the data and component names change.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part3 --template react
   cd rweek3-pp-part3
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part3` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

1. In the `src` directory, create a new file named `usersData.js`.
2. Add the following array of user objects:

```js
const usersData = [
  {
    id: 1,
    name: "Alice Johnson",
    email: "alice@example.com",
    role: "Admin",
  },
  {
    id: 2,
    name: "Bob Smith",
    email: "bob@example.com",
    role: "Editor",
  },
  {
    id: 3,
    name: "Charlie Brown",
    email: "charlie@example.com",
    role: "Viewer",
  },
];

export default usersData;
```

### Step 2: Create a User Component

1. Create a new file named `User.jsx` in the `src` directory.
2. Add the following code:

```jsx
import React from 'react';

function User({ user }) {
  return (
    <div className="user">
      <h2 className="user-name">{user.name}</h2>
      <p><strong>Email:</strong> {user.email}</p>
      <p><strong>Role:</strong> {user.role}</p>
    </div>
  );
}

export default User;
```


### Step 3: Style the User Component

1. Create a file named `User.css` in the `src` directory.
2. Add the following styles:

```css
.user {
  background-color: #f4fdf7;
  border: 1px solid #b7e4c7;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.user-name {
  font-size: 1.2rem;
  margin: 0;
  color: #2d6a4f;
}
```

### Step 4: Render Users in App Component

1. Open `App.jsx` and clear its content.
2. Import the required files:

```jsx
import User from './User';
import usersData from './usersData';
import './User.css';
```

3. Render the list of users using `map()`:

```jsx
function App() {
  return (
    <div className="App">
      <h1>User List</h1>
      <div className="user-list">
        {usersData.map((user) => (
          <User key={user.id} user={user} />
        ))}
      </div>
    </div>
  );
}

export default App;
```

### Step 5: Test Your Application

* Open the browser at `http://localhost:5173`.
* You should see **three users** displayed on the page.
* Confirm there are no key warnings in the console.


----

## Part 4: Rendering a List of Movies in React

#### Objective:

In this part, you will render a list of movies in React using the `map()` function. The structure and steps remain the same as the previous parts.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part4 --template react
   cd rweek3-pp-part4
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part4` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

1. In the `src` directory, create a new file named `moviesData.js`.
2. Add the following array of movie objects:

```js
const moviesData = [
  {
    id: 1,
    title: "Inception",
    director: "Christopher Nolan",
    year: 2010,
  },
  {
    id: 2,
    title: "The Matrix",
    director: "The Wachowskis",
    year: 1999,
  },
  {
    id: 3,
    title: "Interstellar",
    director: "Christopher Nolan",
    year: 2014,
  },
];

export default moviesData;
```


### Step 2: Create a Movie Component

1. Create a new file named `Movie.jsx` in the `src` directory.
2. Add the following code:

```jsx
import React from 'react';

function Movie({ movie }) {
  return (
    <div className="movie">
      <h2 className="movie-title">{movie.title}</h2>
      <p><strong>Director:</strong> {movie.director}</p>
      <p><strong>Year:</strong> {movie.year}</p>
    </div>
  );
}

export default Movie;
```

### Step 3: Style the Movie Component

1. Create a file named `Movie.css` in the `src` directory.
2. Add the following styles:

```css
.movie {
  background-color: #fff4e6;
  border: 1px solid #ffd8a8;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.movie-title {
  font-size: 1.2rem;
  margin: 0;
  color: #d9480f;
}
```

### Step 4: Render Movies in App Component

1. Open `App.jsx` and remove all existing content.
2. Import the required files:

```jsx
import Movie from './Movie';
import moviesData from './moviesData';
import './Movie.css';
```

3. Use `map()` to render the movies:

```jsx
function App() {
  return (
    <div className="App">
      <h1>Movie List</h1>
      <div className="movie-list">
        {moviesData.map((movie) => (
          <Movie key={movie.id} movie={movie} />
        ))}
      </div>
    </div>
  );
}

export default App;
```


### Step 5: Test Your Application

* Visit `http://localhost:5173`.
* You should see **three movies** rendered on the page.
* Check the console for any missing key warnings.

-----


## Part 5: Rendering a List of Products in React

#### Objective:

In this part, you will render a list of products in React. You will also learn **why** each step is needed when working with lists in React.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part5 --template react
   cd rweek3-pp-part5
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part5` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

**Why this matters:**
React components should focus on displaying data, not storing large datasets. Keeping data in a separate file makes your code cleaner and easier to manage.

1. In the `src` directory, create a file named `productsData.js`.
2. Add the following array of product objects:

```js
const productsData = [
  {
    id: 1,
    name: "Laptop",
    price: 1200,
    category: "Electronics",
  },
  {
    id: 2,
    name: "Headphones",
    price: 150,
    category: "Electronics",
  },
  {
    id: 3,
    name: "Office Chair",
    price: 300,
    category: "Furniture",
  },
];

export default productsData;
```


### Step 2: Create a Product Component

**Why this matters:**
Breaking UI into small components makes your app reusable and easier to understand. Each `Product` component is responsible for displaying **one product**.

1. Create a file named `Product.jsx` in the `src` directory.
2. Add the following code:

```jsx
import React from 'react';

function Product({ product }) {
  return (
    <div className="product">
      <h2 className="product-name">{product.name}</h2>
      <p><strong>Price:</strong> ${product.price}</p>
      <p><strong>Category:</strong> {product.category}</p>
    </div>
  );
}

export default Product;
```


### Step 3: Style the Product Component

**Why this matters:**
CSS helps visually separate list items so users can clearly see where one item starts and another ends.

1. Create a file named `Product.css` in the `src` directory.
2. Add the following styles:

```css
.product {
  background-color: #f8f9fa;
  border: 1px solid #dee2e6;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.product-name {
  font-size: 1.2rem;
  margin: 0;
  color: #343a40;
}
```


### Step 4: Render Products in App Component

**Why this matters:**
The `map()` function allows React to loop over data and return a component for each item in the array.

1. Open `App.jsx` and clear its content.
2. Import the necessary files:

```jsx
import Product from './Product';
import productsData from './productsData';
import './Product.css';
```

3. Render the products:

```jsx
function App() {
  return (
    <div className="App">
      <h1>Product List</h1>
      <div className="product-list">
        {productsData.map((product) => (
          <Product key={product.id} product={product} />
        ))}
      </div>
    </div>
  );
}

export default App;
```

**Key Concept – `key` Prop:**
React uses the `key` prop to keep track of list items efficiently. Each key must be **unique**.


### Step 5: Test Your Application

* Open `http://localhost:5173`.
* You should see **three products** rendered on the page.


-------

## Part 6: Rendering a List of Students in React

#### Objective:

In this part, you will render a list of students and reinforce how React handles lists using the same approach as previous parts.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part6 --template react
   cd rweek3-pp-part6
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part6` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

**Why this matters:**
Storing student data in an array allows React to easily loop through and display each student.

1. Create a file named `studentsData.js` in the `src` directory.
2. Add the following array:

```js
const studentsData = [
  {
    id: 1,
    name: "John Doe",
    major: "Computer Science",
    year: "Sophomore",
  },
  {
    id: 2,
    name: "Jane Smith",
    major: "Biology",
    year: "Junior",
  },
  {
    id: 3,
    name: "Mike Johnson",
    major: "Mathematics",
    year: "Senior",
  },
];

export default studentsData;
```

### Step 2: Create a Student Component

**Why this matters:**
Each student is rendered using the same component structure, making the UI consistent.

1. Create a file named `Student.jsx` in the `src` directory.
2. Add the following code:

```jsx
import React from 'react';

function Student({ student }) {
  return (
    <div className="student">
      <h2 className="student-name">{student.name}</h2>
      <p><strong>Major:</strong> {student.major}</p>
      <p><strong>Year:</strong> {student.year}</p>
    </div>
  );
}

export default Student;
```

### Step 3: Style the Student Component

**Why this matters:**
Consistent styling improves readability and reinforces that each student is a separate list item.

1. Create a file named `Student.css` in the `src` directory.
2. Add the following styles:

```css
.student {
  background-color: #f0f4ff;
  border: 1px solid #c7d2fe;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.student-name {
  font-size: 1.2rem;
  margin: 0;
  color: #3730a3;
}
```

### Step 4: Render Students in App Component

**Why this matters:**
This step brings everything together: data, components, and list rendering.

1. Open `App.jsx` and remove all existing content.
2. Import the required files:

```jsx
import Student from './Student';
import studentsData from './studentsData';
import './Student.css';
```

3. Render the list of students:

```jsx
function App() {
  return (
    <div className="App">
      <h1>Student List</h1>
      <div className="student-list">
        {studentsData.map((student) => (
          <Student key={student.id} student={student} />
        ))}
      </div>
    </div>
  );
}

export default App;
```

### Step 5: Test Your Application

* Visit `http://localhost:5173`.
* You should see **three students** displayed.
* Confirm there are no key warnings in the console.


--------

## Part 7: Rendering a List of Countries in React

#### Objective:

In this part, you will render a list of countries in React and further reinforce how lists are displayed using the `map()` function.

### Step 0: Set Up Your Project

1. Open your `VS Code` editor in the `week3` directory.
2. Create a new React project and start the development server. For full steps on creating a React project with `Vite`, refer to [these instructions](./vite.md). In brief, run:

   ```bash
   npx create-vite@latest week3-pp-part7 --template react
   cd rweek3-pp-part7
   npm install
   npm run dev
   ```

   - This will create a new React project named `week3-pp-part7` and start it.
   - **Note**: By default, Vite runs on port `5173`.  
   - When using Vite with React, it’s recommended to use the `.jsx` extension for files containing JSX syntax. If a file contains only standard JavaScript, the `.js` extension is fine.

### Step 1: Create a Data File

**Why this matters:**
Storing country data in an array allows React to loop through the data and render one component per country.

1. In the `src` directory, create a new file named `countriesData.js`.
2. Add the following array of country objects:

```js
const countriesData = [
  {
    id: 1,
    name: "Canada",
    capital: "Ottawa",
    population: "38 million",
  },
  {
    id: 2,
    name: "Germany",
    capital: "Berlin",
    population: "83 million",
  },
  {
    id: 3,
    name: "Japan",
    capital: "Tokyo",
    population: "125 million",
  },
];

export default countriesData;
```


### Step 2: Create a Country Component

**Why this matters:**
Each country is displayed using the same component structure, which keeps the UI consistent and reusable.

1. Create a file named `Country.jsx` in the `src` directory.
2. Add the following code:

```jsx
import React from 'react';

function Country({ country }) {
  return (
    <div className="country">
      <h2 className="country-name">{country.name}</h2>
      <p><strong>Capital:</strong> {country.capital}</p>
      <p><strong>Population:</strong> {country.population}</p>
    </div>
  );
}

export default Country;
```

### Step 3: Style the Country Component

**Why this matters:**
Styling helps visually separate each country in the list, making the information easier to read.

1. Create a file named `Country.css` in the `src` directory.
2. Add the following styles:

```css
.country {
  background-color: #e6fcf5;
  border: 1px solid #96f2d7;
  padding: 15px;
  margin: 10px;
  border-radius: 5px;
}

.country-name {
  font-size: 1.2rem;
  margin: 0;
  color: #087f5b;
}
```

### Step 4: Render Countries in App Component

**Why this matters:**
This is where the array is turned into visible UI using the `map()` function.

1. Open `App.jsx` and clear its content.
2. Import the required files:

```jsx
import Country from './Country';
import countriesData from './countriesData';
import './Country.css';
```

3. Render the countries list:

```jsx
function App() {
  return (
    <div className="App">
      <h1>Country List</h1>
      <div className="country-list">
        {countriesData.map((country) => (
          <Country key={country.id} country={country} />
        ))}
      </div>
    </div>
  );
}

export default App;
```

### Step 5: Test Your Application

* Open `http://localhost:5173`.
* You should see **three countries** displayed.
* Check the console for key-related warnings.



