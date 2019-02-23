## Interfaces

### Basic interface

```
interface Character {
  name: string;
  age?: number;
  bloodType?: string;
  readonly createDate: Date;
}
```

### Excess property checks

#### Background

Consider this code:

```
interface Character {
  age?: string;
  bloodType?: string;
}

function createNewCharacter(character: Character) {
  // ...
}
```

And the errors below:

```
// error: 'rightHanded' not expected in type 'Character'
createNewCharacter({
  age: 30,
  rightHanded: true,
});

// error: 'rightHanded' not expected in type 'Character'
const character: Character = { age: 30, rightHanded: true };
```

The errors occurred because the object literal `{ age: 30, rightHanded: true }` undergoes *excess property checking* when it was:
* passed as an argument to function `createNewCharacter()`
* assigned to variable `character`

Since the property `rightHanded` was not defined in interface `Character`, the errors occurred.

#### Get around

Method 1: use type assertion on the object literal:

```
// works!
createNewCharacter({ age: 30, rightHanded: true } as J);

// works!
const character: Character = ({ age: 30, rightHanded: true } as J);
```

Method 2: add a string index signature to the interface:

```
// Note the newly added property [property: string]: any
interface Character {
  age?: number;
  bloodType?: string;
  [property: string]: any;
}

// works!
createNewCharacter({
  age: 30,
  rightHanded: true,
});

// works!
const character: Character = { age: 30, rightHanded: true };
```

Method 3: assign the object literal to a variable:

```
const C = { age: 30, rightHanded: true };

// works!
createNewCharacter(C);

// works!
const character: Character = C;
```

#### Conclusion

A majority of excess property errors are bugs. Keep in mind the above get around techniques, but revise your type declarations as well.

### Function types

```
interface I {
  (paramA: number, paramB: string): boolean;
}

// Assign the interface to a function variable
const F: I = function(paramA: number, paramB: string) {
  return true;
}

// Parameter names do not need to match
// Return type can be implied
const G: I = function(a: number, b: string) {
  return true;
}
```

### Indexable types

Only `string` and `number` types are supported for index signatures.

```
interface I {
  [index: number]: string; // when an I is indexed with a number, it will return a string
}

interface ReadOnlyI {
  readonly [index: number]: string; // disallow assigment to indices
}

const a: ReadOnlyI = ["", ""];
a[2] = ""; // error
```

The type returned from a numeric indexer must be a subtype of the type returned from the string indexer. This is because JavaScript converts `number` indices to `string` indices before indexing. For example: `a[1]` will be converted to `a["1"]`.

```
class A {
  // ...
}

class B extends A {
  // ...
}

// works!
interface J {
  [index: string]: A;
  [index: number]: B;
}

// error: A is not a subtype of B
interface J {
  [index: number]: A;
  [index: string]: B;
}
```

`string` index signatures enforce that all properties match their return type.

```
interface I {
  [index: string]: number;
  propA: number; // works!
  propB: string; // error: propB's type is not a subtype of the indexer
}
```

### Class types

Interfaces describe the public side of class.

```
// Constructor type is defined separately
interface IConstructor {
  new (paramB: number);
}

interface I {
  propA: number;
  methodM(paramA: string);
}

class C implements I {
  propA: 0;
  methodM(paramA: string) {
    // ..,
  }
  constructor(paramB: number) { }
}
```

### Extending interfaces

```
interface Shape {
  paramA: string;
}

interface PenStroke {
  paramB: boolean;
}

interface Square extends Shape, PenStroke {
  paramC: number;
}

const Square = <Square>{
  paramA: "",
  paramB: true,
  paramC: 0,
};
```

### Hybrid types

```
interface I {
  (paramA: number): void;
  paramB: number;
  functionA(): void;
}

const a = <I>(paramA: number): void => { };
a.paramB = 0;
a.functionA = (): void => { }
```

### Interfaces extending Classes

When an interface extends a class type, it inherits all members (private and protected as well) of the class, but not its implementations.

Thus when an interface extends a class type with private or protected members, that interface can only be implemented by that class or its sub-class.

```
class Control {
  private state: any;
}

interface SelectableControl extends Control {
  select(): void;
}

class Button extends Control implements SelectableControl {
  select() { }
}

class TextBox extends Control {
  select() { }
}

// error: property 'state' is missing in type 'Image'.
class Image implements SelectableControl {
  select() { }
}
```