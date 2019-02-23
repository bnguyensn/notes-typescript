## Classes

```typescript
class Character {
  name: string;
  
  constructor(firstName: string, lastName: string) {
    this.name = `${firstName} ${lastName}`;
  }
  
  sayHello() {
    console.log(`Hi, I'm ${this.name}`);
  }
}
```


