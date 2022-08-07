# subscript

Subscript yapısı Herhangi bir method tanımlamadan class, struct veya enum içerisinde tanımladığımız diziler, kümeler, **collectionlar** vb yapılarının değerlerini döndürmemize veya güncellenmemize olanak sağlamaktadır.

```swift
subscript(index: Int) -> String { 

        get { 

        return String() } 

        set (newValue) { 

        } 

} 
```

Subscriptlerde **set** zorunlu değildir fakat **get** zorunludur.&#x20;

Swift içerisinde bulunan **array** ve **dictionary**'lerde subscript yapısını kullanmaktadır. Örneğin bir dizinin belirli bir indisindeki veriyi getirmek istediğimizde arka planda aşağıdakine benzer bir subscript yapısı çalışmaktadır. Aynı şekilde dictionary’ler içinde bu yapı geçerlidir sadece orada index yerine **key** (anahtar kelime) ile get veya set yapılır.&#x20;

```swift
struct Array<Element> { 

    subscript(index: Int) -> Element{ 

       get{ 
          return array[index] 
       } 

       set(newValue){ 
         array[index] = newValue 
       } 
    } 
} 
```

Kendi oluşturduğumuz bir class veya sturct içerisinde birden fazla subscript yapısı oluşturabiliriz.

```swift
struct Event { 

    var eventsArray: [String] = ["1. etkinlik","2. etkinlik","3. etkinlik","4. etkinlik","5. etkinlik"] 

    subscript(eventIndex: Int) -> String{ 

        get{ 
            return eventsArray[eventIndex] 
        } 

        set(newValue){ 
            eventsArray[eventIndex] = newValue 
        } 
    } 

        subscript(event: String) -> Int{ 
        return eventsArray.firstIndex(of: event)! 
    } 
} 

var instance = Event() 

print(instance[2]) 

instance[2] = “Test” 
```

Yukarıda görüldüğü gibi **Event** adında bir struct bulunmaktadır ve içerisinde **eventsArray** adında bir dizi tanımlanmıştır. **Event** structından bir instance oluşturarak direkt olarak köşeli parantezler içerisinde 2 rakamını yazarsak **eventsArray** dizisinin 2. indisinde bulunan veriyi bize döndürür. Aynı şekilde kodumuzun son satırında olduğu gibi 2. indisinde bulunan veriyi güncelleyebiliriz. 2. olarak tanımlanan subscript yapısını kullanmak için yapmamız gereken tek şey köşeli parantezler içerisinde string bir değer girmektedir. String bir değer girdiğimizde eğer girilen değer dizimiz içerisinde varsa görüldüğü ilk indis numarasını verecektir.
