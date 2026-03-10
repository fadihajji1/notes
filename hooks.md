# hooks

**React vs. Angular** :

- `useState` **vs.** `signal()`: 
  - React’s `useState` re-renders the entire component on state change. 
  - Angular’s `signal()` enables fine-grained updates without unnecessary re-renders.
- `useMemo` **vs.** `computed()`: 
  - React’s `useMemo` requires explicit dependency arrays, risking bugs from incorrect or missing dependencies. 
  - Angular’s `computed()` automatically tracks dependencies, making it more intuitive and less error-prone.
- `useEffect` **vs.** `effect()`: Both handle side effects, but :
  - React’s `useEffect` relies on dependency arrays. 
  - Angular’s `effect()` automatically detects dependencies, reducing boilerplate and potential errors.

 