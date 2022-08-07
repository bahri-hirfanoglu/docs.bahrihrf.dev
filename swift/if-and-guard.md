# if & guard

## **if**

If diğer tüm programlama dillerinde olduğu gibi bir koşulu kontrol ederek belirli bir kod bloğunu çalıştıran yapıdır. Fakat swift içerisinde if'in kullanımını anlamak için öncelikle Optional yapısına göz atmamız gerek. Kısa bir örnekle Optinal yapısını açıklayayım.&#x20;

```swift
var name : String? = "baybars"
```

Yukarıda name değişkeninin tipini belirtirken **String?** kullandık. Buradaki soru işareti değişkenin string bir değere sahip olabileceğini vurgulamaktadır. Ancak string olmayabilir nil de olabilir. Bu durumda bu değişken **Optinal** bir değişkendir diyebiliriz. Ayrıca soru işaretini kaldırsaydık veya yerine **!** (ünlem) işaretini koysaydık bu değişkene atanacak değerin kesinlikle string olacağına emin olduğumuzu belirtmiş olurduk ve bu şekilde **non-optional** bir değişken elde ederdik. Fakat non-optinal değişken tanımlamak bazı durumlarda mantıklı değildir. Eğer değişken içerisine bir şekilde nil değeri atanırsa bu uygulamamızın çökmesine neden olabilir.&#x20;

{% hint style="info" %}
optional ve non-optional yapılarını ilerleyen yazılarda detaylı şekilde anlatacağım.
{% endhint %}

Bu tip durumlarda uygulamamızın çökmesini engellemek için **if let** yapısını kullanabiliriz. Örnek olarak şöyle bir senaryo düşünelim. Kullanıcıdan almamız gereken bir isim var kullanıcı isim alanını boş bıraktı ve onayla butonuna tıkladı. Uygulamamızın hata vermemesi için if let yapısını kullanmamız gerekmektedir. Örnek if let yapısı aşağıdadır.

```swift
func clickEvent() {
    let name : String? = textNameField.text
    if let newname = name {
        print("Name: \(newname)")
    } else {
        print("name not nullable")
    }
}
```

if let yapısı eğer name değişkeni **nil** değilse onu **newname** adlı bir sabite atayacak ve if içerisinde bulunan kod bloğunu çağıracaktır. Bu şekilde name değişkeninin olası nil gelme durumunda uygulamamızın ona göre aksiyon almasını ve çökme ihtimalini ortadan kaldırmış olacağız.&#x20;

## **guard** <a href="#guard" id="guard"></a>

Swift içerisinde if dışında guard adında bir değer kontrol yapısı daha bulunmaktadır. Aslında değer kontrolden ziyade şart kontrol diyebiliriz. Guard if'in aksine içerisine yazacağımız şart gerçekleşmezse alacağımız aksiyonları belirlediğimiz bir yapıdır. Yukarıda bulunan örneğinin aynısı **guard let** yapısı ile aşağıda bulunmaktadır.&#x20;

```swift
func clickEvebt() {
    let name : String? = textNameField.text
    guard let newname = name else {
        print("name not nullable")
        return
    }
    print("Name: \(newname)")
}
```

Yukarıdaki **guard let** mantığı şu şekildedir. else kadar olan kısım aslında if let yapısı ile aynı kontrolü yapmaktadır. Fakat daha sonra gelen else verdiğimiz şartın tam aksi olduğunda ne yapacağım demek istemektedir. Eğer name alanı nil gelirse **guard let** bloğunun içine girecektir ve "name not nullable" hatasını verecektir. Burada ekstra olarak return kullanmamız gerekir. Bunun amacı **guard let** bloğundan sonra gelen kodları çalıştırmadan fonksiyonumuzu sonlandırmaktır. Guard let içerisinde return kullanmak zorunludur aksi taktirde **guard let** kullanmanın bir amacı kalmaz. Kodumuzu uyarı mesajını verse de alt da bulunan kodları da çalıştırmayı deneyecektir ve bu durum kodun devamında yaptığımız işlemlere göre uygulamamızı çökertebilir.

Guard yapısını aslında geri değer döndüren bir fonksiyonda kullanmak daha mantıklıdır. Bir örnekle açıklayalım.

```swift
func isEven(number: Int) ->Bool {
    guard number % 2 == 0 else {
        return false
    }
    return true
}

print(isEven(number: 1))
```
