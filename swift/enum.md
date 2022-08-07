# enum

## Enum

Enum kısaca birbirleriyle alakalı değerleri bir arada tutmak için oluşturulan yapılardır. Swift'de bir enum içerisine bulunan değere hem adı hemde rawValue ile erişebiliriz. Diğer programlama dillerinin aksine swift'de bulunan enum yapıları daha esnektir.&#x20;

### **Enum Tanımlama**

```swift
enum Package {
    case sendMesssage
    case openMessage
    case deleteMessage
}

print(Package.deleteMessage) //output deleteMessage
```

Yukarıda **Package** adında bir **enum** tanımladık ve içerisine 3 adet sabit ekledik. **Package** içerisinde bulunan bir sabite erişmek için **enum** adımızı yazıp erişmek istediğimiz sabitin adını yazdık. Şimdi sabitlerimize değer ataması yapalım. Bunun için öncelikle hangi veri türünde atama yapacağımızı belirtmemiz gerek.

### **Enum Sabitlerine Değer Atama**

```swift
enum Package : Int {
    case sendMesssage = 1
    case openMessage
    case deleteMessage
}

print(Package.SendMesssage.rawValue)  //output  1
print(Package.openMessage.rawValue)   //output  2
print(Package.deleteMessage.rawValue) //output  3
```

enum adımızdan sonra : (iki nokta) koyarak veri türümüzü belirttik. Daha sonra ilk sabitimiz olan **sendMesssage'a** 1 değerini atadık. En altta bulunan print işleminde görüldüğü üzere enum yapılarında sabitlere atanan değerlere erişmek için **rawValue** kullandık. Ayrıca enum yapılarında sabitlerimizin herhangi birine değer ataması yaptığımızda ondan sonra gelen tüm sabitlere otomatik değer ataması yapmaktadır. Biz yukarıda sadece **sendMessage** sabitine 1 değerini atadık fakat diğer sabitlerinde değerlerini görüntülediğimizde sıralı bir şekilde arttığını gözlemledik. (Sadece Int türünde oluşturulan enum yapılarında otomatik değer atama işlemi yapılır.)

### **RawValue İle Erişme**

Enum içerisinde bulunan bir sabite atadığımız rawValue ilede erişebiliriz. Yada enum içerisinde belirteceğimiz rawValue ait bir sabit var mı bunu görebiliriz.

```swift
print(Package(rawValue: 1)) //Optional(Enum_Test.Package.sendMesssage)
```

enum adımızdan sonra parantez açarak **rawValue:** şeklinde enum içerisinde arama yapabiliriz. Eğer belirttiğimiz **rawValue** sahip bir sabit varsa bunu bize döndürecektir. Bu durumun kesinliği olmadığından dolayı bize döndürülen değer Optional olarak gelmektedir. Eğer optional yapısına hakim değilseniz önceki yazılarımdan inceleyebilirsiniz.

### **Switch & Enum Kullanımı**

Switch ile enum içerisinde sabitlere göre işlemler yapabiliriz.

```swift
enum Package : Int {
    case sendMesssage = 1
    case openMessage = 2
    case deleteMessage = 3
}

var selectedPackage = Package.openMessage

switch selectedPackage {
case .sendMesssage:
    print("selected package sendMessage")
case .openMessage:
    print("selected package openMessage")
case .deleteMessage:
    print("selected package deleteMessage")
}
```

Yukarıda bir değişken oluşturduk ve bu değişkene Package enum içerisinde bulunan bir sabiti atadık. Daha sonra aşağıda bulunan switch yapımız ile değişkene atanan değer hangi sabitimiz ise ona göre print işlemi yaptık.

### **Enum İlişkili Değerler**

```swift
enum MathOperation {
    case addition(Int, Int)
    case square(Int)
}

var operation = MathOperation.addition(1, 2)

switch operation {
case .addition(let num1, let num2):
    print(num1 + num2)
case .square(let num):
    print(num * num)
}
```

Enum içerisine parametre alacak ilişkili değeler oluşturabiliriz. Yukarıdaki örnekte **MathOperation** adında bir enum oluşturduk ve içerisine 2 adet matematik işlemeni tanımladık. Daha sonra bu işlemlerden birini seçtik ve seçtiğimiz işleme göre switch kullanarak işlem sonucunu print ettik. (NOT: İlişkili değerlerin parametrelerine yukarıda olduğu gibi switch kullanarak erişebiliriz ve aksiyonlarımızı alabiliriz.)
