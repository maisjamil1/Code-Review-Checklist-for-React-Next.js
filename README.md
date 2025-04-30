# Code Review Checklist for React/Next.js

## Component Structure & Size
 Keep components small and focused.
🔸 If the file exceeds 200–300 lines, break it down into child components.

### Code Quality & Readability
- Follow the DRY (Don’t Repeat Yourself) principle.
🔸 Extract repeating logic or components.

- Follow YAGNI (You Aren’t Gonna Need It)
🔸Avoid creating functions that are not essential. Focus on what is really necessary, keeping the code simple and direct.

- No unused props are passed to components.
- Meaningful variable and function names:

Variables = nouns (user, formData)

Functions = verbs (fetchUsers, handleSubmit)
-  Avoid hardcoded values, use named constants.
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
