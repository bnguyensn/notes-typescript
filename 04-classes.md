## Classes

### Classes and sub-classes

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

All class members are `public` by default.

Accessing a private member is not allowed

```typescript
class MageWithSecret extends Mage {
  private secret: string;
  
  constructor(firstName: string, lastName: string, secret: string) {
    super(firstName, lastName);
    this.secret = secret;   
  }
}

const MS = new MageWithSecret('Kael', 'Sunstrider', 'demonic dealings');

 // error: 'secret' is private
console.log(MS.secret);
```
