# Angular

### HOOKS

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

---

## Routing

in  app.routing.ts

```
export const myRoutes : Routes = [
    {path : '' , component : Accueil},
    {path : 'cv' , component : Cv},
    {path : 'cv/:id' , component : Infos},
    {path : 'accounts' , component : HomeAccounts},
    {path : 'servers' , component : ManageServers},
    {path : 'products' , component : HomeProducts},
]
```

in app.html

```
<router-outlet></router-outlet>
```

in app.config.ts

```

```

---

## navigate:

in component.html

**static routing**

```
<button (click)="goToCv()" class="btn btn-danger">Go To CV</button>
```

but requires in  component.ts

```typescript
export class Accueil {
private router = inject(Router)
goToCv() {
    this.router.navigateByUrl("cv")
}
```

OR

---

**dynamic routing**

```
<button routerLink="cv" class="btn btn-success">Go To CV</button>
```

---

 