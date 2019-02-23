## Classes

### Classes and sub-classes

####Class

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

####Sub-class

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

### Public, private, and protected

#### Public

All class members are `public` by default.

#### Private

Accessing private members from outside their class is not allowed.

Different classes with "similar" private members are not compatible. The private members must come from the same place.
 
 `protected` members follow the same rules.

```typescript
class WarriorWithSecret extends Warrior {
  private secret: string;
  
  constructor(name: string, secret: string) {
    super(name);
    this.secret = secret;   
  }
}

class MageWithSecret extends Mage {
  private secret: string;
  
  constructor(name: string, secret: string) {
    super(name);
    this.secret = secret;   
  }
}

let secretWarrior = new WarriorWithSecret('Varian Wrynn', 'royal bloodline');
let secretMage = new MageWithSecret('Kael Sunstrider', 'demonic dealings');

 // error: 'secret' is private
console.log(secretWarrior.secret);

// error: 'WarriorWithSecret' and 'MageWithSecret' are not compatible
secretWarrior = secretMage;
```
