## Type Inference

### Best common type

When no common type is found, a union is chosen.

```typescript
// TypeScript considers the types of all x's elements: number, string, and null
// A best common type is chosen as the x's type
const x = [0, '', null];
```

### Contextual type

An expression's type can be implied by its location.
