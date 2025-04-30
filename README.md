# Code Review Checklist for React/Next.js

## Component Structure & Size
 Keep components small and focused.
🔸 If the file exceeds 200–300 lines, break it down into child components.
🔸 JSX Markup <= 50 Lines
Large JSX blocks reduce readability. Split into smaller reusable components or extracted JSX elements.<br>✅


### Code Quality & Readability
- Follow the DRY (Don’t Repeat Yourself) principle.
🔸 Extract repeating logic or components.

- Follow YAGNI (You Aren’t Gonna Need It)
🔸Avoid creating functions that are not essential. Focus on what is really necessary, keeping the code simple and direct.

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

- Comment only where necessary
  
