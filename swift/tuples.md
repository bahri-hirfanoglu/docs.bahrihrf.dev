# tuples

**Tuples** diğer programlama dillerinde pek rastlamadığımız fakat swift içerisinde bulunan farklı veya aynı türdeki verileri bir grupta toplayan yapılardır. Örneklerle detaylarına inelim.&#x20;

Bir tuples tanımlayalım

```swift
let user = ("Bahri", "Hırfanoğlu", 23) 
```

Yukarıda görüldüğü gibi parantez içerisine Tuples içerisinde olmasını istediğimiz verileri aralarına virgül koyarak yazıyoruz.

Tuples içerisinde verilerimize erişelim.

```swift
let (name, surname, age) = user 
```

Tuples oluştururken içerisinde bulunan verileri sırasıyla sabitimize atayacaktır. Yani Tuples'ın 1. elemanı **name** sabitine, 2. elemanı **surname** sabitine, 3. elemanı **age** sabitine atanmış olacaktır.

Eğer tuples içerisinden sadece belirli verileri sabite aktarmak istiyorsak sabit oluştururken almak istemediğimiz veriler yerine **\_** işaretini koymamız yeterli olacaktır.&#x20;

```swift
let (name, _, age) = user
```

Tanımladığımız bir tuples içerisinde bulunan verilere index numaraları ilede erişebiliriz.

```swift
print("(index):",user.0, user.1, user.2) // (index): Bahri Hırfanoğlu 23 
```

Index numarası dizilerde olduğu gibi 0’dan başlamaktadır. Fakat **tuples** içerisindeki bir veriye index numarasından ulaşırken dizilerde olduğu gibi köşeli parantez kullanmayız. Tuples adını yazdıktan sonra nokta koyup direkt index numarasını yazmamız gerekmektedir.&#x20;

Ayrıca Tuples tanımlarkende aynı dictionary’lerde olduğu gibi her **tuples** verimize bir key tanımlayabiliriz. Böylece direkt olarak **tuples** ismimizden sonra nokta koyup key adımızı çağırarak veriye erişim sağlayabiliriz. &#x20;

```swift
let user = (name: "Ahmet", surname: "Nejdet", age: 33)
```

Tuples’lar genelde fonksiyonların toplu veri döndürme işlemlerinde kullanılmaktadır.&#x20;

```swift
func mathProc(val: Int)  -> (square: Int, times: Int) { 
    let square = val * val 
    let times = val * 2 
    return(square, times) 
} 
print(mathProc(val: 6)) 
```

**NOT**: Tuples’lar sadece basit türde karmaşık olmayan sabitleri depolamak için kullanılır. Karmaşık yapılar için struct vb. yapılar kullanılmalıdır. &#x20;
