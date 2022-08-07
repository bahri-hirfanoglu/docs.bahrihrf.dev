# array & dictionary & set

### **Array** <a href="#array" id="array"></a>

Array yani diziler içerisinde aynı veya farklı türlerde verileri depolaya bilen yapılardır. Aşağıda bazı dizi tanımlama tiplerini görebiliriz.&#x20;

```swift
var data : [String] = [] 

var days = [1, 4, 2, 6] 

var numbers : [Int] = [1, 1, 1, 1] 

var names : Array<String> = ["bahri", "ali", "cevdet"] 

var anyArray : [Any] = [0, "bahri", false] 
```

Örneklerde olduğu gibi dizi tanımlarken köşeli parantezler içerisinde elemanlarımızı yazabiliriz. Ayrıca boş bir dizi oluşturmak istiyorsak dizi tipini belirtmemiz gerekmektedir.

Otomatik değer ataması yaparak bir dizi oluşturma

```swift
var digitCounts = Array(repeating: 0, count: 10) 
//[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

**Dizilerin Bazı Propertyleri**

```swift
var numbers : [Int] = [13, 1, 3, 1] 

numbers.isEmpty // true|false 

numbers.count // dizi eleman sayısı 

numbers.first //ilk eleman 

numbers.last //son eleman 

numbers.append(4) //bir eleman ekleme 

numbers.append(contentsOf: [1, 4]) //toplu eleman ekleme 

numbers.insert(4, at: 3) //belirli bir indexe eleman ekleme 

numbers.remove(at: 3) //index numarasını kullanarak eleman silme 

numbers.removeLast() //son elemanı silme 

numbers.removeFirst() //ilk elemanı silme 

numbers.firstIndex(of: 5) //bir elemanın dizi içerisindeki index numarasını alma 
```

Diziler içerisindeki tüm elemanları listeleme

```swift
for number in numbers {
    print(number)
}
```

### **Dictionary** <a href="#dictionary" id="dictionary"></a>

Dictionary içerisine key ve value tanımlayabildiğimiz birden fazla boyutlanabilen collection type’lerinden bir tanesidir. Aşağıda bazı dictionary tanımlama tiplerini görebiliriz. Dizilerde olduğu gibi boş bir dictionary oluşturmak için veri tiplerini belirtmemiz gerekmektedir. Dictionary'de key value mantığı vardır. Value'ler istediğimiz veri tipinde olabilirken key'ler any tipinde olamazlar. Any yerine swift içerisinde [AnyHashable ](https://developer.apple.com/documentation/swift/anyhashable)denilen bir yapı ile kullanılabilirler.

```swift
var user = 
[
"A": "Bahri", 
"C": "Cevdet", 
"H": "Halil"
]

var data : [Int:String] =
[
30: "30 karakter",
40: "40 karakter",
50: "50 karakter"
]

var emptyDict: [String: String] = [:]

var anyEmptyDict: [Int: Any] = [:]
```
