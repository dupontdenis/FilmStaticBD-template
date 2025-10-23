# Film Collection - Static Database Template

A simple web application template for displaying a film collection using vanilla JavaScript ES6 modules and Bootstrap styling.

## 📋 Project Overview

This project demonstrates how to create a static film database application with multiple viewing options. It uses ES6 modules to manage data and dynamically renders film information in different formats using JavaScript templates.

## 🚀 Features

- **Static Data Management**: Film data stored in a reusable ES6 module
- **Multiple View Options**: 
  - Table view with film titles and directors
  - List view with formatted film information
- **Responsive Design**: Bootstrap 4.5.2 for mobile-friendly layouts
- **ES6 Modules**: Modern JavaScript module system for clean code organization
- **Template Literals**: Dynamic HTML generation using JavaScript template literals

## 📁 Project Structure

```
FilmStaticBD-template/
│
├── index.html              # Landing page with navigation
├── filmListArray.html      # Table view of films
├── filmListUl.html         # List view of films
├── dataFilms.mjs          # Film data module (ES6)
└── README.md              # Project documentation
```

## 🎬 Data Structure

The project includes two main data structures in `dataFilms.mjs`:

### Films Array
Contains film objects with the following properties:
- `title`: Film title
- `year`: Release year
- `director`: Director name
- `actors`: Array of actor names

### Actor Salaries Map
A JavaScript Map containing actor salaries (in USD) for the films in the collection.

### Sample Films
- Inception (2010)
- The Dark Knight (2008)
- Titanic (1997)
- Avatar (2009)
- Mad Max: Fury Road (2015)

## 🛠️ Technologies Used

- **HTML5**: Semantic markup
- **CSS**: Bootstrap 4.5.2 via CDN
- **JavaScript**: ES6+ features including:
  - ES6 Modules (`import`/`export`)
  - Template literals
  - Arrow functions
  - Array methods (`forEach`)
  - `insertAdjacentHTML` for DOM manipulation

## 💻 Getting Started

### Prerequisites

- A modern web browser with ES6 module support (Chrome, Firefox, Safari, Edge)
- A local web server (required for ES6 modules to work)

### Installation

1. Clone or download this repository
2. Navigate to the project directory

### Running the Application

Since this project uses ES6 modules, you need to serve it through a web server. Here are several options:

#### Option 1: Using Python
```bash
# Python 3
python -m http.server 8000

```

#### Option 2: Using Node.js (http-server)
```bash
npx http-server -p 8000
```

#### Option 3: Using VS Code Live Server Extension
- Install the "Live Server" extension
- Right-click on `index.html`
- Select "Open with Live Server"

### Accessing the Application

Open your browser and navigate to:
```
http://localhost:8000
```

## 📖 Usage

1. **Home Page**: Navigate between different views using the provided buttons
2. **Table View** (`filmListArray.html`): View films in a structured table format
3. **List View** (`filmListUl.html`): View films in a list format with director information

## 🎨 Two Display Methods Explained

This project demonstrates two different approaches to displaying the film collection, each using the same underlying data but presenting it differently:

### 1. Table View (`filmListArray.html`)

**Display Format**: Bootstrap table with rows and columns

**Visual Structure**:
```
┌─────────────────────┬──────────────────────┐
│ Title               │ Director             │
├─────────────────────┼──────────────────────┤
│ Inception           │ Christopher Nolan    │
│ The Dark Knight     │ Christopher Nolan    │
│ ...                 │ ...                  │
└─────────────────────┴──────────────────────┘
```

**Use Case**: 
- Best for comparing multiple properties side-by-side
- Ideal for data that needs to be scanned quickly
- Professional, spreadsheet-like appearance
- Easy to sort and filter (with additional JavaScript)

**Template Structure**:
```javascript
const filmTemplate = (film) => `
    <tr>
        <td>${film.title}</td>
        <td>${film.director}</td>
    </tr>
`;
```

### 2. List View (`filmListUl.html`)

**Display Format**: Bootstrap list group with formatted items

**Visual Structure**:
```
┌──────────────────────────────────────────┐
│ Inception - Directed by Christopher Nolan │
├──────────────────────────────────────────┤
│ The Dark Knight - Directed by Christopher │
│ Nolan                                     │
├──────────────────────────────────────────┤
│ ...                                       │
└──────────────────────────────────────────┘
```

**Use Case**:
- Better for narrative or descriptive content
- More readable for mobile devices
- Natural reading flow
- Easier to add icons, badges, or action buttons

**Template Structure**:
```javascript
const filmTemplate = (film) => `
    <li class="list-group-item">
        ${film.title} - Directed by ${film.director}
    </li>
`;
```

### Comparison

| Feature | Table View | List View |
|---------|-----------|-----------|
| **Layout** | Grid/Columns | Stacked Items |
| **Bootstrap Class** | `.table` | `.list-group` |
| **Best For** | Structured data | Reading content |
| **Mobile** | Requires horizontal scroll | Fully responsive |
| **Extensibility** | Add columns | Add content blocks |

## 🔄 Common JavaScript Pattern

Both display methods share the **same reusable pattern**, demonstrating good code design principles:

### The Pattern: Import → Select → Template → Render

This pattern is consistently applied in both `filmListArray.html` and `filmListUl.html`:

```javascript
// 1. IMPORT: Get data from external module
import { films } from './dataFilms.mjs';

// 2. SELECT: Get the DOM element where data will be inserted
const container = document.getElementById('target-element');

// 3. TEMPLATE: Define how each item should be rendered
const filmTemplate = (film) => `
    <element>
        ${film.property}
    </element>
`;

// 4. RENDER: Loop through data and insert HTML
films.forEach(film => {
    container.insertAdjacentHTML('beforeend', filmTemplate(film));
});
```

### Pattern Breakdown

#### Step 1: Import Data
```javascript
import { films } from './dataFilms.mjs';
```
- Uses ES6 module syntax
- Separates data from presentation logic
- Makes data reusable across multiple pages
- Enables easy data updates in one place

#### Step 2: Select Target Container
```javascript
// Table view
const filmsTableBody = document.getElementById('films-table-body');

// List view
const filmsList = document.getElementById('films-list');
```
- Identifies where rendered content will go
- Uses semantic HTML IDs
- Keeps original HTML clean (no hardcoded data)

#### Step 3: Create Template Function
```javascript
const filmTemplate = (film) => `
    <tr>
        <td>${film.title}</td>
        <td>${film.director}</td>
    </tr>
`;
```
- **Arrow function** for concise syntax
- **Template literals** (backticks) for multi-line HTML
- **String interpolation** (`${...}`) for dynamic data
- Returns HTML string for each film
- Easy to modify presentation without changing logic

#### Step 4: Render with forEach
```javascript
films.forEach(film => {
    container.insertAdjacentHTML('beforeend', filmTemplate(film));
});
```
- **`forEach`**: Iterates over each film in the array
- **`insertAdjacentHTML`**: Efficiently adds HTML without parsing entire DOM
- **`'beforeend'`**: Inserts inside container, after last child
- Each iteration adds one film to the display

### Why This Pattern?

**Advantages**:
✅ **Separation of Concerns**: Data, logic, and presentation are separate
✅ **DRY Principle**: Template function defined once, used multiple times
✅ **Maintainability**: Change template in one place affects all items
✅ **Scalability**: Easy to add more films—just update the data file
✅ **Readability**: Clear, step-by-step process that's easy to understand
✅ **Flexibility**: Swap display methods by changing only the template function

**Real-World Applications**:
- E-commerce product listings
- Blog post displays
- User comment sections
- Social media feeds
- Dashboard widgets
- Search results

### Alternative Approaches (Not Used Here)

This project uses **vanilla JavaScript**, but the pattern scales to frameworks:

- **React**: Components with `.map()` instead of `.forEach()`
- **Vue**: `v-for` directive in templates
- **Angular**: `*ngFor` structural directive

Understanding this vanilla pattern helps you learn any framework faster!

## 🔧 Customization

### Adding New Films

Edit `dataFilms.mjs` and add new film objects to the `films` array:

```javascript
{
    title: "Your Film Title",
    year: 2024,
    director: "Director Name",
    actors: ["Actor 1", "Actor 2"]
}
```

### Modifying Views

Each HTML file (`filmListArray.html`, `filmListUl.html`) contains:
- A template function that defines how each film is displayed
- A rendering loop that processes the film data

Modify the `filmTemplate` function in each file to change how films are displayed.

## 🌐 Browser Compatibility

This project requires a browser that supports:
- ES6 Modules
- Template literals
- Arrow functions
- `insertAdjacentHTML`

## 📝 Learning Objectives

This template is ideal for learning:
- ES6 module system
- DOM manipulation with vanilla JavaScript
- Template literals for dynamic HTML generation
- Bootstrap integration
- Static data management
- Modern JavaScript best practices

---
## Adding Actor Salaries in dataFilms.mjs

Add new entries to the `actorSalaries` Map:

```javascript
["Actor Name", 50000]
```
