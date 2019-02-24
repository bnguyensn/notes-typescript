## Functions

### Basic

```typescript
function add(x: number, y: number): number {
  return x + y
}

const subtract = (x: number, y: number): number => x - y;

// TypeScript can infer the return type if it's omitted
function multiply (x: number, y: number) {
  return x * y
}

// Implementations' parameter names do not matter
// Implementations do not have to declare types (contextual typing)
const divide: (number1: number, number2: number) => number = 
  (x, y) => x / y;

// Optional parameters must follow non-optional ones
// No need to use optional '?' if there is a default value
// Parameters with default values do not have to follow non-optional ones 
function sayHello(firstName: string = 'stranger', lastName?: string) {
  console.log(`Hello ${firstName} ${lastName}!`);
}

sayHello(); // Hello stranger !

// Rest parameters
function sayMultipleHellos(...names: string[]) {
  console.log(`Hello ${names.join(', ')}!`);
}

sayMultipleHellos('Adam', 'Becky', 'Caroline'); // Hello Adam, Becky, Caroline!
```

### *this*

The type of `this` defaults to `any` (implicit `this`).

Important for:
* Function factories: functions that create functions
* Callbacks: functions that are called at a later time in different context

You should:
* Use arrow functions (no `this` of itself, use parent's)
* Declare type for `this`: `function f(this: void): void;`

### Overloads

```typescript
function sayN(n: number): string; // Overload #1
function sayN(n: string): number; // Overload #2

function sayN(n) {
  if (typeof n === 'number') {
    return ''
  } else if (typeof n === 'string') {
    return 0
  }
}
```
