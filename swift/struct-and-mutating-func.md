# struct & mutating func

## Struct

Sturct içerisinde değişken, fonksiyon vb şeyleri tanımlayabildiğimiz class'a benzer yapılardır. Fakat bazı özellikleri ile class'dan ayrılmaktadır. Struct yapısını anlamak class ile farklarını inceleyelim.

### **Struct - Class Farkları** <a href="#struct-class-farklari" id="struct-class-farklari"></a>

**1-)** Class'larda init fonksiyonunu bizim oluşturmamız gerekirken structlarda bu otomatik olarak yapılmaktadır.

```swift
struct StructProduct {
    var title: String
    var detail: String
}

class ClassProduct {
    var title: String
    var detail: String
    
    init(title: String, detail: String) {
        self.title = title
        self.detail = detail
    }
}
```

**2-)** Class'larda bulunan miras (**Inheritance**) özelliği structlarda bulunmamaktadır.

**3-)** Class'lar ile oluşturduğumuz nesnelerin eşit olup olmadığını kontrol edebiliyorken structlar ile oluşturduklarımızı kontrol edemeyiz. Aşağıdaki kodda class Product yerine struct Product yazsaydık if bloğunda kontrol işlemi yapamazdık.

```swift
class Product {
    var title: String
    var detail: String
    
    init(title: String, detail: String) {
        self.title = title
        self.detail = detail
    }
}

var p1 = Product(title: "A", detail: "B")
var p2 = Product(title: "A", detail: "B")

if p1 === p2 {
    print("ok")
}
```

**4-)** Class'lar referans (**reference**) tipiyken structlar değer (**value**) tipidir. Aslında bilinmesi gereken en temel farklardan birisi budur. Şimdi öncelikle referans ve değer tiplerini kısaca tanımlayalım.

### **Reference Type**

Kısaca bir değişkenin hafızadaki yerinin bir adres belirleyicisi ile hafızada tutulmasıdır diyebiliriz. Yani reference type olan bir veriyi ulaşmak için önce adresin kayıtlı olduğu kısma gidip adresi alır daha sonra o adrese gidip veriye ulaşırız.

### **Value Type**

Kısaca veri hafızada direkt olarak kaydedilir.

İkisi arasında farkı tam olarak anlamak için aşağıdaki kodları inceleyelim.

```swift
struct StructProduct {
    var title: String
    var detail: String
}

class ClassProduct {
    var title: String
    var detail: String
    
    init(title: String, detail: String) {
        self.title = title
        self.detail = detail
    }
}


//Class
var clsProduct = ClassProduct(title: "Yeni Ürün #1" , detail: "Yeni ürün #1 açıklama")
var clsProductNew = clsProduct

clsProductNew.title = "Güncellenen Yeni Ürün #1"

print(clsProduct.title) //Output Güncellenen Yeni Ürün #1


//Struct
var strProduct = StructProduct(title: "Yeni Ürün #2" , detail: "Yeni ürün #2 açıklama")
var strProductNew = strProduct

strProductNew.title = "Güncellenen Yeni Ürün #2"

print(strProduct.title) //Output Yeni Ürün #2
```

Hem class hemde struct yapısını kullanarak bire bir aynı şablonları oluşturduk. Görüldüğü üzere class yapımız için oluşturduğumuz değişkeni **clsProductNew** adlı bir değişkene atadık. Daha sonra atadığımız değişkenin title property'sini değiştirdik ve oluşturduğumuz ilk nesnenin title değişkenini görüntüledik. Burada bize dönen veride görüyoruz ki biz **clsProductNew** üzerinden title property'sini değiştirmiş olmamıza rağmen ilk nesnemizin de title property'si güncellenmiş. İşte aslında buradan yola çıkarak reference type yapılarının mantığını anlayabiliriz. Biz _**`var clsProductNew = clsProduct`**_ bu kod bloğunda aslında nesnemizin bir kopyasını değil referansımızın adresini atamış oluyoruz. Bu durumda her iki değişkende aynı adresleri kullandığı için birinde yapılan değişiklik her iki nesneyi de etkilemektedir. Structlarda ise bu durum tam tersidir. Görüldüğü üzere _**var strProductNew = strProduct**_ bu kod bloğunu çalıştırdığımızda artık birbirinden bağımsız iki yapı hafızada yer almaktadır. Birinde yapılan değişiklik diğerini etkilemez.

Apple genel olarak karmaşık olmayan ve class'ın kendi özel özelliklerini kullanmayacağımız senaryolarda struct kullanımını önermektedir. Önermesinin bazı nedenler şunlardır;

1- Hafızada stack mantığıyla tutulduklarından dolayı veri okunmak istendiğinde daha hızlı okunur.\
2- Basit ve hızlıdır.\
3- Ram sorunlarına yol açmaz.\
4-Threadsafe'tir.

Sturct yapısını anlatırken mutating function'dan kısa bir şekilde bahisedelim.

## Mutating Func

Eğer struct içerisinde bir fonksiyon ürettiysek ve bu fonksiyon struct içerisinde bulunan herhangi bir objeye erişiyorsa bunun kullanılabilmesi için mutating olarak işaretlenmesi gerekmektedir. Aşağıdaki kodu inceleyerek daha iyi anlayabiliriz.

```swift
struct Human 
{ 
   var name : String 

   init(name: String) 
   { 
      self.name = name 
   } 

   mutating func changeName(newName: String) { 
      name = newName 
   } 
} 

var human = Human(name: "kuyt") 
human.changeName(newName: "alex") 
```

Yukarıda bulunan **changeName** fonksiyonu struct genelinde tanımlanan name değişkenine eriştiğinden dolayı bu fonksiyonu dışarıdan kullanabilmek için mutating kullandık.
