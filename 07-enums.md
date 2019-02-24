## Enums

Enums are sets of named constants.

Order:
1. Enum initialized with constants
2. Enum without initializer
3. Enum with initializer

#### Numeric enums

Numeric enums automatically increment.

```typescript
enum LettersToNumbers {
  A = 1, // Default is 0
  B, // Automatically becomes 2
  // ...
}

console.log(LettersToNumbers.A); // 1
```

Numeric enums have *reverse mapping*.

```typescript
enum Stuff {
  A, B,
}

console.log(Stuff.A); // 0
console.log(Stuff[Stuff.A]); // 'A'
```

#### String enums

String enums are clearer than numeric enums when debugging.

```typescript
enum Directions {
  N = 'North',
  E = 'East',
  S = 'South',
  W = 'West',
}
```

String enums do not have *reverse mapping*.

#### Heterogeneous (diverse) enums

You can mix numeric and string enums, but this is not common in practice.

```typescript
enum Mixedbag {
  A = 1,
  B = 'Two',
}
```

#### Constant enums

Constant enums are removed during compilation.

```typescript
const enum LettersToNumbers {
  A, B,
}

console.log(LettersToNumbers.A); // In generated code, will be inlined to console.log(0); 
```

#### Ambient enums

Ambient enums are used to describe the shape of existing enums.

```typescript
declare enum Stuff {
  A,
  B = 2,
  C,
}
```
