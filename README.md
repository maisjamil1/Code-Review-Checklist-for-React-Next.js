# Code Review Checklist for React/Next.js

## Component Structure & Size
- Code Formatting: Is the code properly formatted? (Consider using tools like Prettier.)

- Keep components small and focused.
🔸 If the file exceeds 200–300 lines, break it down into child components.
🔸 JSX Markup <= 50 Lines
- Large JSX blocks reduce readability. Split into smaller reusable components or extracted JSX elements.<br>✅


### Core Principles of Clean React Code
- Single Responsibility Principle (SRP)
Each component should do one thing well.
- Separation of Concerns
Separate logic from presentation: business logic → hooks/utils; JSX → components.
- DRY — Don’t Repeat Yourself
Extract reusable logic into custom hooks, helpers, or shared components.
- KISS — Keep It Simple, Stupid
Avoid premature abstractions or overly complex solutions.
- YAGNI — You Aren't Gonna Need It
Don’t add features or complexity until they are needed.
Avoid creating functions that are not essential. Focus on what is really necessary, keeping the code simple and direct.

- avoid  nested conditionals or deeply nested JSX.
- No unused props are passed to components.
- Use Consistent Naming Conventions
Naming conventions improve readability and help the team (and tools like linters) understand your code structure at a glance.

PascalCase: Use for React components, interfaces, and type aliases

```
const UserCard = () => { ... }

interface AdminUser { ... }

type TaskList = { ... }
```
camelCase: Use for variables, functions, arrays, and objects
```
const fetchData = () => { ... }
const userList = [ ... ]
```
Variables = nouns (user, formData)
Functions = verbs (fetchUsers, handleSubmit)

-  Avoid hardcoded values,Avoid magic strings/numbers. Define them once at the top of file or in a shared constants file..
❌ if (status === 1) → ✅ if (status === STATUS.ACTIVE)

 Group similar values under enums.
✅ enum Status { Active = 'active', Inactive = 'inactive' }

### Type Safety
 Use well-named interfaces and types.
✅ interface UserProfile { name: string; age: number; }

 Extend types/interfaces to avoid duplication.
✅ interface AdminUser extends UserProfile { role: string }

 Avoid "any" type .

 ### Best Practices
 Remove all console.log() before merging.
❌ console.log('Debug user')

 Use async/await or Promises, and handle errors.
✅ try { await fetchData() } catch (err) { handleError(err) }

 Use Promise.all when calling APIs in parallel.
✅ const [user, posts] = await Promise.all([getUser(), getPosts()])

 Add id or data-id for testability and automation.
✅ <button data-id="submit-btn">Submit</button>


###  React Specifics
 Fix React warnings in the console.
❌ Each child in a list should have a unique "key" prop.
✅ <li key={user.id}>{user.name}</li>

 Use custom hooks to abstract logic.
✅ useAuth(), usePagination()

 Extract common functions into reusable helpers.
✅ formatDate(), capitalizeFirstLetter()

 Prefer generic functions if logic is reusable.
✅ function paginate<T>(data: T[], page: number): T[] {}

 Avoid dangerouslySetInnerHTML unless sanitized.
✅ Use DOMPurify.sanitize(html) before injecting.

 If using timers (setInterval/setTimeout), clean them up.
✅

ts
Copy
Edit
useEffect(() => {
  const interval = setInterval(fetchData, 10000);
  return () => clearInterval(interval);
}, []);

- Use next/image for images and always provide alt attributes.
✅ <Image src="/logo.png" alt="Company logo" />

### Performance & Bundle Optimization
 - If a new library is added:

Check if a smaller alternative exists.

Review its bundle impact using bundlephobia.

-  Use lazy loading and dynamic imports for large or optional components.
✅ const Chart = dynamic(() => import('./Chart'), { ssr: false })

- Comment only where necessary ( Necessary comments are comments that describe the why.)

### Simplify State Management with useReducer
Avoid cluttering components with multiple useState calls. If you’re managing more than 3–4 related state variables or complex objects, switch to useReducer for better organization and readability.

Before:

```
const [isLoading, setIsLoading] = useState(false);
const [error, setError] = useState(null);
const [data, setData] = useState([]);
```

After:

```
const initialState = { isLoading: false, error: null, data: [] };

function reducer(state, action) {
  switch (action.type) {
    case 'SET_LOADING': return { ...state, isLoading: true };
    case 'SET_DATA': return { ...state, data: action.payload, isLoading: false };
    case 'SET_ERROR': return { ...state, error: action.payload, isLoading: false };
    default: return state;
  }
}
```
const [state, dispatch] = useReducer(reducer, initialState);
📌 Tip: Prefer useReducer for complex, interrelated state or when state transitions depend on previous state.

🔌 Boolean Props: Use Shorthand
Instead of:
```
<MyComponent isActive={true} />
```
Use:

```
<MyComponent isActive />
```
🧼 String Props: Avoid Unnecessary Curly Braces
Instead of:

```
<Title text={"Hello"} />
```
Use:

```
<Title text="Hello" />
```
🔄 Use Fragments Over Divs for Wrapping
When a wrapper element is needed but no actual HTML element is required, use fragments (<>...</>) to avoid unnecessary DOM nodes.

Good:
```
<>
  <h1>Welcome</h1>
  <p>Intro text</p>
</>
```
📭 Use Self-Closing Tags When There Are No Children
If a component or HTML tag has no children, write it as a self-closing tag:

Instead of:
```
<Avatar></Avatar>
```
Use:

```
<Avatar />
```
