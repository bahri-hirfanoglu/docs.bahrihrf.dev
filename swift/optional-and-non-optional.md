# optional & non-optional

### **Optional** <a href="#optional" id="optional"></a>

Optional kavramı bir değişken tanımlarken değişkenin tipini örtülü olarak atamamızı sağlayan yapıdır. Bir örnekle durumu detaylandıralım.&#x20;

Aşağıdaki kodda normal şartlarda değişkeni tanımlarken **: Int** şeklinde değişkenin tipini belirtmek zorunda değiliz. Fakat değişkene bir değer ataması yapmamız gerekiyor aksi taktirde uygulamamız bize hata verecektir.

```swift
var number: Int

print(number)
```

Eğer değişkeni tanımlarken **** tip adının sonuna **?** işaretini eklersek değişkenimiz artık opsiyonel olacaktır ve boş olması durumunda default olarak nil değerini döndürecektir.

```swift
var number: Int?

print(number)

//output nil
```

Ayrıca değişkenimizi optional olarak tanımlayıp bir değer ataması yaptığımızda aslında değişkenimizi bir kutu içerisine alıyormuşuz gibi düşünebiliriz. Değişkenimizi kullanabilmek için kutudan çıkarmamız gerek. Bunun için bir kaç yöntem bulunmaktadır.

```swift
var number: Int? = 5

print(number)

//output Optional(5)
```

1- Değişkenimizi kullanacağımız yerde sonuna **! (ünlem işareti)** ekleyebiliriz.

```swift
var number: Int? = 5

print(number!)

//output 5
```

2- Bir önceki yazımda bahsettiğim if let ve guard let yapıları ile değişkenimizi kutudan çıkartabiliriz.

```swift
let number : Int? = 5
if let newNumber = number {
    print(newNumber)
}

//output 5
```

```swift
let number : Int? = 5
guard let newNumber = number else {
  return
}
print(newNumber)

//output 5
```

3- Bir diğer yöntem ise değişkenimizi kullanırken **??** operatörü ile varsayılan değer ataması yapabiliriz. Bu yapı değişkenimizin değerini değiştirmez. Sadece değişkenimizin nil gelmesi durumunda kullanılacak bir değer belirtir.

```swift
let number : Int? = 5

print(number ?? 0)

//output 5
```
