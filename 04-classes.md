## Classes

### Classes and sub-classes

#### Class

```typescript
class Character {
  name: string;
  spec: string;
  
  constructor(name: string, spec: string) {
    this.name = name;
    this.spec = spec;
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name}.`);
  }
  
  saySpec() {
    console.log(`I'm a ${this.spec}`);
  }
}
```

#### Sub-class

`super()` in sub-classes' constructors must be called before accessing `this`.

```typescript
class Warrior extends Character {
  constructor(name: string) {
    super(name, 'warrior');
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name} and I'm a strong warrior.`);
  }
}

class Mage extends Character {
  constructor(name: string) {
    super(name, 'mage');
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name} and I'm a wise mage.`);
  }
}
```

### Modifiers

There are accessibility (`public`, `private`, and `protected`) and `readonly` modifiers.

Modifiers can be combined e.g. `private readonly x`.

#### Public

All class members are `public` by default.

#### Private

Accessing private members from outside their class is not allowed.

Different classes with "similar" private members are not compatible. The private members must come from the same place.
 
 `protected` members follow the same rules.

```typescript
class WarriorWithPrivateSecret extends Warrior {
  private secret: string;
  
  constructor(name: string, secret: string) {
    super(name);
    this.secret = secret;   
  }
}

class MageWithPrivateSecret extends Mage {
  private secret: string;
  
  constructor(name: string, secret: string) {
    super(name);
    this.secret = secret;   
  }
}

let secretWarrior = new WarriorWithPrivateSecret('Varian Wrynn', 'royal bloodline');
let secretMage = new MageWithPrivateSecret('Kael Sunstrider', 'demonic dealings');

 // Error: 'secret' is private
console.log(secretWarrior.secret);

// Error: 'WarriorWithPrivateSecret' and 'MageWithPrivateSecret' are not compatible
// WarriorWithPrivateSecret's and MageWithPrivateSecret's secret member do not come from the same place
secretWarrior = secretMage;
```

#### Protected

`protected` members are identical to `private` ones, but can be accessed by sub-classes.

```typescript
class WarriorWithProtectedSecret extends Warrior {
  protected secret: string;
  
  constructor(name: string, secret: string) {
    super(name);
    this.secret = secret;
  }
}

class DummyWarriorWithProtectedSecret extends WarriorWithProtectedSecret {
  constructor(secret: string) {
    super('John Smith', secret);
  }
  
  saySecret() {
    console.log(`My secret is ${this.secret}`); // Works!
  }
}

const dummySecretWarrior = new DummyWarriorWithProtectedSecret('cheater');

// Error: 'secret' is protected
console.log(dummySecretWarrior.secret);
```

A `protected` constructor restricts its instantiation via sub-classes only.

```typescript
class CharacterWithProtectedConstructor {
  name: string;
  spec: string;
  
  protected constructor(name: string, spec: string) {
    this.name = name;
    this.spec = spec;
  }
}

class Warrior extends CharacterWithProtectedConstructor {
  constructor(name: string) {
    super(name, 'warrior');
  }
}

// Error: 'CharacterWithProtectedConstructor' has a protected constructor
const varian = new CharacterWithProtectedConstructor('Varian Wrynn', 'warrior');

// Works!
const grom = new Warrior('Grom HellScream');
```

#### Read-only

Read-only properties must be initialized and can't be re-assigned.

#### Parameter properties

Parameters with modifiers don't need to be assigned in the constructor. This is called *parameter properties*.

```typescript
class HumanWarrior extends Warrior {
  readonly race: string = 'human'; // No need to do anything else to use this.race
  
  constructor(name: string, private readonly bloodType: string) {
    super(name);
    // No need to do this.bloodType = bloodType
    // readonly bloodType is not declared above the constructor either
  }
  
  sayRace() {
    console.log(`My race is ${this.race}.`);
  }
  
  sayBloodType() {
    console.log(`My blood type is ${this.bloodType}.`);
  }
}
```
