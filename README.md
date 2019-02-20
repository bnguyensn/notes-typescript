# TypeScript Notes

A more condensed version of the TypeScript handbook.

### Table of Contents

[Basic Types](#basic-types)

[Variable Declarations](#variable-declarations)

[Interfaces](#interfaces)

## Basic Types

WIP

## Variable Declarations

WIP

## Interfaces

### Basic interface

```
interface I {
  propA: number;
  propOptional?: string;
  readonly propReadOnly: number[];
}
```

### Excess property checks

#### Background

Consider this code:

```
interface J {
  propA?: string;
  propB?: string;
}

function f(param: J) {
  // ...
}
```

And the errors below:

```
// error: 'propC' not expected in type 'J'
f({
  propA: "",
  propC: "",
});

// error: 'propC' not expected in type 'J'
const C: J = { propA: "", propC: "" };
```

The errors occurred because the object literal `{ propA: "", propC: "" }` undergoes *excess property checking* when it was:
* passed as an argument to function `f`
* assigned to variable `C`

Since the property `propC` was not defined in interface `J`, the errors occurred.

#### Get around

Method 1: use type assertion on the object literal:

```
// works!
f({
  propA: "",
  propC: "",
} as J);

// works!
const C: J = ({ propA: "", propC: "" } as J);
```

Method 2: add a string index signature to the interface:

```
// Note the newly added property [propX: string]: any
interface J {
  propA?: string;
  propB?: string;
  [propX: string]: any;
}

// works!
f({
  propA: "",
  propC: "",
});

// works!
const C: J = { propA: "", propC: "" };
```

Method 3: assign the object literal to a variable:

```
const O = { propA: "", propC: "" };

// works!
f(O);

// works!
const C: J = O;
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
