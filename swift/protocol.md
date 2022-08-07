# protocol

## **Protocol** <a href="#protocol" id="protocol"></a>

Protocol'ler struct, class veya enum gibi yapıların içerisinde olması gereken fonksiyon, değişken vb nesneleri tanımladığımız arayüzlerdir. Farklı programlama dillerinde bulunan interface yapısına benzemektedir.

### **Protocol Neden Kullanılır?** <a href="#protocol-kullanmanin-amaci-nedir" id="protocol-kullanmanin-amaci-nedir"></a>

Swift'de aslında protocol'lerin kullanılma amacı swift'in **OOP**'da **** bulunan çoklu miras (**multiple inheritance**) özelliğini desteklememesidir. Swift 2.0 ile birlikte **POP** (Protocol Oriented Programing) yapısını tanıtarak OOP'nin eksiklerini gidermeye çalışmıştır. OOP struct ve enumlar ile tam anlamıyla çalışamadığından dolayı Protocol kullanımı swift içerisinde daha mantıklı hale gelmiştir. Çünkü protocol'ler struct, class veya enumlara birden fazla kez referans olabilir. Ayrıca birbirleri arasında da referans oluşturabilirler. Bu şekilde daha okunaklı bir kod inşa edebiliriz.

### **Protocol Yapısı** <a href="#protocol-yapisi" id="protocol-yapisi"></a>

Şimdi bir protocol oluşturalım.

```swift
protocol MovieProtocol {
    
}
```

Protocol içerisine fonksiyon ve değişken tanımlayalım.

```swift
protocol MovieProtocol {
    var title : String {get}
    
    var detail : String {get set}
    
    func getMovie()
    
    func getMovieCount() -> Int
}
```

Protocol içerisinde tanımladığımız değişkenlerin sonunda bulunan **{get set}** yapıları aslında bu değişkenin okunabilir ve yazılabilir olup olmayacağını belirtmemizi sağlamaktadır. **get** var ise bu değişkenimizin değeri görüntülenebilir. set mevcut ise bu değişkenimizin değeri güncellenebilir. Bunların her ikisini aynı anda kullanmak zorunda değiliz sadece birini de kullanabiliriz. Eğer herhangi bir **get** veya **set** tanımlaması belirtmezsek bu default olarak **{get set}** şeklinde algılanmaktadır. Bu protocol'den referans alan class veya sturct içerisinde tanımlanan property'i daha sonradan get only olarak kısıtlayamayız.

Protocol içerisine çeşitli tanımlamaları yaptık. Şimdi bu protocol'ümüzü kullanalım.

```swift
struct Movie : MovieProtocol {
    var title : String {
      get {
            return "Movie Title"
        }
    }
    var detail : String
    
    func getMovie() {
        
    }

    func getMovieCount() -> Int {
        return 0
    }
}
```

**Movie** adında bir sturct oluşturduk ve **MovieProtocol** sanki classlarda bulunan miras işlemini gerçekleştiriyor gibi struct ismimizden sonra : (iki nokta) koyarak yazdık. Swift'de bir struct veya class birden fazla protocol referans olarak alabilir. Fakat bir class'a protocol referans olarak tanımlanacaksa class'ın eğer varsa miras aldığı class isminden sonra , (virgül) koyarak tanımlanmalıdır. Yani class'larda öncelik miras alma işlemidir daha sonra protocol referansları yazılmalıdır.

### **Protocol Kullanımı Hakkında Bazı Bilgiler** <a href="#protocol-kullanimi-hakkinda-bazi-bilgiler" id="protocol-kullanimi-hakkinda-bazi-bilgiler"></a>

**1-** Bir protocol farklı birden fazla protocol'ü referans olarak alabilir. Aşağıdaki örneği inceleyerek durumu daha net anlayabiliriz.

```swift
protocol A {
    var name : String {get set}
}

protocol B: A {
    var age : Int {get set}
}

struct  Test : B {
    var name : String
    var age : Int
}
```

**Test** struct'ı **B** protocol'ünden referans alıyor ve içerisinde **name** ve **age** değişkenlerinin tanımlanması zorunlu hale geliyor. Çünkü **B** protocol'ümüzde **A** protocol'ümüzden referans almış durumdadır.

**2-** Bir protocol'ü sadece class'ların referans olarak kullanmasını istiyorsak bu protocol'e **AnyObject** referansını eklemeliyiz.

```swift
protocol DayProtocol: AnyObject {

}
```

**3-** Protocol içerisinde **init** fonksiyonunu tanımlayabiliriz. Eğer bu protocol'den bir class referans alırsa class içerisinde **init** fonksiyonunu tanımlarken başına **required** tagı eklenmelidir.

```swift
protocol DayProtocol {
   init()
}

class Day : DayProtocol {
     required init() {

     }
}
```

**NOT:** Yukarıdaki kodda bulunan Day class'ı eğer bir class'dan miras alıyor olsaydı init fonksiyonu _**`required override init`**_` ``` şeklinde yazılmalıydı.

**4-** Protocol içerisinde tanımladığımız bir property veya fonksiyonu optional hale getirebiliriz. Optional bir nesne üretmek için protocol tanımının başına **@objc** eklemeliyiz. Aşağıdaki örneği inceleyerek daha iyi anlayabiliriz.

```swift
@objc protocol DayProtocol {
   @objc optional var age: Int { get set }
   var name : String {get set}
}

class Day : DayProtocol {
    var name : String = "Bahri"

}
```

**NOT:** Optional bir değer içeren protocol sadece class ile birlikte kullanılabilir.
