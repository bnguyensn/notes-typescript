## Generics

### Basic

```typescript
// We don't know p's type
// We define generic type <T> for p
// Type declaration now works!
function f<T>(p: T): T { // a.k.a. the 'identity' function 
  return p
}

f<string>(''); // Explicitly set T
f(''); // Implicitly set T
```

### Classes

```typescript
class C<T> {
  p: T;
  m: () => T;
}

const c = new C();
c.p = '';
c.m();
```

### Generic constraints

```typescript
interface Character {
  name: string;
}

// Generic T is limited to follow interface Character
function sayCharacter<T extends Character>(char: T): string {
  return char.name
}
```

A type parameter can be constrained by another type parameter

```typescript
const d = {
  a: 1,
  b: 2,
};

function getProperty<O, K extends keyof O>(obj: O, key: K) {
  return obj[key]
}

getProperty(d, 'a'); // Works!
getProperty(d, 'c'); // Error: 'c' is not a key of d
```

Type for classes in class factories should be referred to using constructor functions.

```typescript
function createInstance<C>(c: { new (): C; }): C {
  return new c();
}
```
