## Classes

All class members are `public` by default.
`super()` in sub-classes' constructors must be called before accessing `this`.

```typescript
class Character {
  name: string;
  hp: number;
  
  constructor(firstName: string, lastName: string, hp: number) {
    this.name = `${firstName} ${lastName}`;
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name}.`);
  }
}

class Warrior extends Character {
  constructor(firstName: string, lastName: string) {
    super(firstName, lastName, 100);
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name} and I'm a strong warrior.`);
  }
}

class Mage extends Character {
  constructor(firstName: string, lastName: string) {
    super(firstName, lastName, 50);
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name} and I'm a wise mage.`);
  }
}

class MageWithSecret extends Mage {
  private secret: string;
  
  constructor(firstName: string, lastName: string, secret: string) {
    super(firstName, lastName);
    this.secret = secret;   
  }
}

const MS = new MageWithSecret('Kael', 'Sunstrider', 'demonic dealings');
MS.secret; // error: 'secret' is private
```

