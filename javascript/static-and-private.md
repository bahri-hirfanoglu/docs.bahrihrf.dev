# static & private

### **class field declarations**

ES2022 ile bir constructor ihtiyaç olmadan class genelinde özellik ataması yapabiliriz.

```javascript
//OLD
class Member {
    constructor() {
        this.name = 'Bahri'
    }
}

//NEW
class Member {
    name = 'Bahri';
}
```

### static

ES2022 ile class içerisinde static özellikler tanımlayabiliriz. Bu static özelliklere instance oluşturmadan erişim sağlayabiliriz.

```javascript
class Member {
  static name = "Bahri";

  static save() {
    console.log(`${this.name} has been recorded`)
  }
}

Member.save() //Bahri has been recorded
```

### private

ES2022 ile private özellik tanımlayabiliriz. Özelliklerin başına **#** ekleyerek private olarak tanımlama yapabiliriz. Bu özelliklere class dışarısından erişim sağlanamaz. Sadece getter ve setter tanımlamaları yapılarak erişim sağlayabiliriz.&#x20;

```javascript
class Member {
  #name = "Bahri";

  get name() {
    return this.#name
  }

  set name(name) {
    this.#name = name
  }
}

const member = new Member();
member.name = 'Kemal'

console.log(member.name) //Kemal
```

static private özellikler de tanımlanabiliriz. Bu özelliklere erişmek için getter ve setter tanımlamaları yapılmalıdır.&#x20;

```javascript
class Member {
  static #name = "Bahri";

  static get name() {
    return this.#name
  }
}

console.log(Member.name) //Bahri
```
