# class & access modifiers

## **Class** <a href="#class" id="class"></a>

Class yani sınıf genel anlamıyla içerisinde nesneleri barındıran ve nesnelerin başlangıç değerlerini tanımlayıp nesnelere özel aksiyonları belirleyebildiğimiz şablonlardır diyebiliriz. Örneklerle hızlı bir giriş yapalım.&#x20;

Sınıf oluşturalım ve içerisinde bir kaç değişken tanımlayalım.

```swift
class Message {
    var title : String
    var detail: String
    
    init(title: String, detail: String) {
        self.title = title
        self.detail = detail
    }
}
```

Sınıf oluşturmak için class tagını yazıp daha sonra sınıfımıza vermek istediğimiz adı yazdık. Süslü parantez açarak sınıfımızı oluşturmuş olduk. Sınıfımız içerisine **title** ve **detail** adında iki adet değişken oluşturduk ve bunların **string** tipinde olacağını belirttik. Fakat başlangıç değeri atamadık. Eğer bir değişkene başlangıç değeri ataması yapmadıysak class yapısının içerisinde bulunan **init (initialization)** metodu ile bu değişkenleri sınıfımızın bir nesnesini üretirken almamız gerekmektedir. init metodu class'ların kurucu fonksiyonlarıdır ve class'lar oluşturulurken çalıştırılırlar. **NOT**: Eğer bir fonksiyon içerisinde oluşturulan parametre ismi sınıfımızın genelinde var olan bir parametre ile aynı ise bunların çakışmaması için sınıfımızın genelinde oluşturduğumuz değişkenin başına **self** yazarak erişim sağlayabiliriz.

Sınıfımızın bir nesnesini oluşturalım.

```swift
let message = Message(title: "Yeni Mesaj", detail: "Sınıf nesnesi oluşturuldu.")

print(message.title, message.detail)
//output Yeni Mesaj Sınıf nesnesi oluşturuldu.
```

Sınıfımızdan nesne oluşturmak için message adında bir sabit oluşturduk ve daha sonra sınıfımızın adını yazıp parantez açarak init metoduna gönderilecek parametreleri girdik. Artık message değişkeni sınıfımızın bir nesnesidir. Yani sınıfımız içerisinde bulunan öğelere erişebilen bir **Message** şablonu kopyasıdır.

Sınıfımızın içine fonksiyon tanımlayalım.

```swift
class Message {
    var title : String
    var detail: String
    
    init(title: String, detail: String) {
        self.title = title
        self.detail = detail
    }
    
    func writeMessage() {
        print("Başlık: \(title) Detay: \(detail)")
    }
}

let message = Message(title: "Yeni Mesaj", detail: "Sınıf nesnesi oluşturuldu.")

message.writeMessage()

//output Başlık: Yeni Mesaj Detay: Sınıf nesnesi oluşturuldu.
```

Yukarıda Message sınıfımız içerisinde writeMessage adında bir fonksiyon tanımladık ve bu fonksiyonu oluşturduğumuz sınıf nesnemiz aracılığı ile çağırdık.

**Birden fazla init metodu tanımlama**

```swift
class Message {
    var title : String
    var detail: String
    
    init(title: String, detail: String) {
        self.title = title
        self.detail = detail
    }
    
    init(title: String){
        self.title = title
        self.detail = "Detay boş bırakıldı."
        writeMessage()
    }
    
    func writeMessage() {
        print("Başlık: \(title) Detay: \(detail)")
    }
}

let message = Message(title: "Yeni Bilgiler")

//output Başlık: Yeni Bilgiler Detay: Detay boş bırakıldı.
```

Sınıflar içerisine birden fazla init metodu oluşturulabilir. Fakat oluşturulan init metodları birbirlerinden farklı olmalıdır. Bir init metodumuz title ve detail parametrelerini beklerken diğer init metodumuz sadece title parametresini beklemekte ve değer atamalarını yaptıktan sonra writeMessage fonksiyonunu çağırmaktadır. Kodumuzun en alt satırında görüldüğü gibi Message sınıfından bir nesne oluşturduk fakat init metodu olarak sadece title parametresini isteyeni kullandık.

### **Miras (Inheritance)** <a href="#miras-inheritance" id="miras-inheritance"></a>

Miras bir sınıfın başka bir sınıftan kalıtım alması olayına denir. Miras alınan sınıf superclass miras alan sınıf subclass olarak adlandırılır.

```swift
class Fruit {
    var name : String
    var color: String
    
    init(name: String, color: String) {
        print("super class init")
        self.name = name
        self.color = color
    }
}

class Apple : Fruit {
    
    override init(name: String, color: String) {
        print("sub class init")
        super.init(name: name, color: color)
    }
}


let apple = Apple(name: "Elma", color: "red")
print(apple.name)

/* output
sub class init
super class init
Elma
*/
```

Fruit ve Apple adında iki sınıf oluşturduk. Apple sınıfımızın Fruit sınıfından miras almasını istedik. Bunun için sınıf adımızdan sonra **:** (iki nokta) koyarak miras alınacak sınıf adını girdik. Artık Apple sınıfımız Fruit sınıfı içerisinde nesnelere erişebilecek ve kendi nesneleriymiş gibi hareket edebilecek. Aslında miras mantığı burada ortaya çıkmaktadır. Miras alınan sınıf miras alan sınıftan daha geniş bir yapıya hitap etmelidir. Yani fruit sınıfı apple sınıfını kapsamalıdır. (Bu durum zorunlu değildir ama OOP yapısına göre böyle olmalıdır.) Fruit sınıfı içerisinde tüm meyvelerde olacak ortak özellikler tanımlanabilir. Biz name ve color adında iki değişken tanımladık. Artık birden fazla meyve sınıfı oluşturduğumuzda bu fruit sınıfından miras alarak sabit değerleri sürekli yeniden üretmek zorunda kalmayacağız. Yani Banana adında bir sınıf üretip miras alınacak sınıfı fruit olarak belirlediğimizde artık Banana sınıfının da name ve color adında iki değişkeni olacak.

### **Çok Biçimlilik (Polymorphism)** <a href="#cok-bicimlilik-polymorphism" id="cok-bicimlilik-polymorphism"></a>

Yukarıda miras yapısını anlatırken verdiğimiz örnekte Apple sınıfımız içerisinde init metodunu tanımlarken başına **override** tagını ekledik. Aslında bu çok biçimlilik yapısına örnektir. Fakat aşağıdaki örneği inceleyerek olayı daha iyi anlayabiliriz.

```swift
class Car {
    func changeColor() {
        print("color changed")
    }
}

class Mercedes : Car {
    override func changeColor() {
    print("mercedes change color")
    }
}


let mercedes = Mercedes()
mercedes.changeColor()

//output mercedes change color
```

Car bizim miras alınan sınıfımız (super class). Mercedes ise miras alan sınıf (sub class). Eğer biz Car sınıfı içerisinde bulunan **changeColor** fonksiyonunu Mercedes sınıfı içerisinde kullanmak istersek fonksiyonun adı aynı olacak şekilde Mercedes sınıfı içerisine yazabiliriz ve başına **override** tagını ekleyerek Car sınıfındaki changeColor fonksiyonunu geçersiz kılabiliriz. Bu yapının kullanılma amacı olası spesifik durumlarda sub class'a özel metod ve property tanımlamaktır. Yani super class'daki property veya metodları geçersiz kılmaktır.

Yapının neden kullanıldığını anlamak için şöyle bir kod oluşturalım.

```swift
class Car {
    
    var km: Int = 0
    var year: Int = 0
    
    func changeColor() {
        print("color changed")
    }
}

class Mercedes : Car {
    override func changeColor() {
    print("mercedes changeColor not supported!")
    }
}


class Audi : Car {

}

class BMW : Car {

}


let mercedes = Mercedes()
mercedes.km = 100000
mercedes.year = 2020
mercedes.changeColor()

let audi = Audi()
audi.km = 10000
audi.year = 2022
audi.changeColor()

let bmw = BMW()
bmw.km = 234000
bmw.year = 2019
bmw.changeColor()

/* output
mercedes changeColor not supported!
color changed
color changed
*/
```

Oluşturduğumuz senaryoda Audi, BMW ve Mercedes sınıfları Car sınıfından miras almakta. Audi ve BMW sınıflarında renk değiştirme özelliği var. Fakat Mercedes marka araçlar bunu desteklemediği için o sınıfta override yapısını kullanarak Mercedes içinde ona özel bir changeColor tasarladık ve içerisine desteklemediğine dair mesajımızı ekledik. Şimdi biz miras almadan da bu işlemi yapabilirdik fakat o zaman her marka araçta olan km ve year değişkenlerini de mercedese özel tekrar oluşturmamız gerekirdi. Fakat biz sadece bir adet fonksiyonu geçersiz kılmak istedik. İşte bu gibi spesifik durumlarda override yapısını kullanarak sub class'a özel property veya fonksiyon tanımlayabiliriz.

### **Sınıf (Class) Erişim Denetleyicileri (**access modifiers**)** <a href="#sinif-class-erisim-denetleyicileri" id="sinif-class-erisim-denetleyicileri"></a>

Erişim denetleyicileri sınıf veya sınıfımızın içerisinde bulunan fonksiyon, metod ve propertylere erişimi denetleyen anahtar sözcüklerdir.&#x20;

Eğer bir sınıfı veya sınıf içerisindeki değişkenlerin erişim denetleyicisini belirtmediysek bu varsayılan olarak **internal'dir**. internal sınıflara veya nesnelere sadece aynı modül içinden erişilebilir. Şimdi diğer erişim denetleyicilerine göz atalım.

**1- Final**

Bir sınıfımız var ve bu sınıftan miras alınmasını istemiyoruz. O zaman yapmamız gereken tek şey sınıfımızı oluştururken final tagı ile işaretlemektir.

```swift
final class Car {
}
```

**2- Open - Public**

Public ile işaretlediğimiz sınıflarımıza farklı modüller dahil her yerden erişim sağlanarak miras alınabilir fakat fonksiyonları override edilemez. Eğer farklı modüllerden erişilip fonksiyonlarımızın override edilmesini istiyorsak o zaman open ile işaretlemeliyiz. Ayrıca override edilmesini istediğimiz fonksiyonlarıda open olarak işaretlemeliyiz.

```swift
open class Car {
}

wwpublic class Car {
}
```

**3- Fileprivate - Private**

Private sınıf veya nesnelere herhangi bir yerden erişim sağlanamaz. Fakat fileprivate olarak işaretlenmiş sınıf veya nesnelerimize sadece aynı dosya içerisinde erişim sağlanabilir.

Biraz örnek yaparak erişim denetleyicilerini pekiştirelim.

```swift
public class City {
    private var population : Double
    
    init(population: Double) {
    self.population = population    
    }
    
    private func getPopulatin(){
        print(population)
    }
}

class Ankara : City { 
   override init(population: Double) {
       super.init(population: population)
   }
}

let ankara = Ankara(population: 5.6)
ankara.getPopulatin()
```

Bu örnekte City ve Ankara adında iki sınıf oluşturduk. Daha sonra Ankara sınıfının City sınıfından miras almasını istedik ve gerekli initialization işlemlerini yaptık. Daha sonra kodumuzun en alt kısmında Ankara sınıfından bir nesne oluşturarak getPopulation fonksiyonunu çağırdık. Fakat bu işlem sonucunda derleyicimiz bize hata mesajı verecektir. Çünkü City sınıfımız public olabilir fakat getPopulation fonksiyonu private yani alt sınıflar (sub sınıflar) erişemez. İşte bu şekilde miras veren sınıfımız içindeki çeşitli property veya fonksiyonları miras alan sınıflarla paylaşmak istemiyorsak private olarak işaretleyebiliriz.

### **Super & Self** <a href="#super-self" id="super-self"></a>

Yukarıda bir çok örnek yaptık. Örneklerde super ve self terimlerini kullandık. Kısaca bu terimlerinde ne işe yaradığını öğrenip class yazımı sonlandıracağım.

**self** bulunduğumuz sınıf içerisinde var olan tüm nesnelere aynı sınıf içerisinde erişmek için kullanılan ön ektir. Yani name adında bir değişkenimiz mevcutsa bu değişkene sınıfımızın içerisinde bulunan herhangi bir yapının içinde **self.name** şeklinde erişebiliriz.

**super** miras alan sınıfın miras veren sınıftaki tüm nesnelere kendi içerisinde erişmesini sağlayan ön ektir. Daha detaylı anlamak için aşağıdaki örneğini inceleyebilirsiniz. (NOT: super ile private nesnelere erişim sağlanamaz.)

```swift
class User {
    var name: String = "Bahri"
}

class Bahri : User {
    func getUserName() -> String {
        return super.name
    }
}

let bahri = Bahri()
print(bahri.getUserName())
```
