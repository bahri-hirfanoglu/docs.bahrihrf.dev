# array methods

```javascript
let array1 = [1, 2, 3, 4, 5];
let array2 = [5, 5, 6, 4];
```

### concat

Dizileri elemanlarını birleştirerek tek bir dizi içerisinde döndürür.

```javascript
array1.concat(array2);
/* Output: 
[
  1, 2, 3, 4, 5,
  5, 5, 6, 4
]
/*
```

### entries

Dizinin elemanlarını (key,value) şeklinde sırayla döndürür.

```javascript
for (let [key, value] of array1.entries()) {
console.log(`${key} - ${value}`);
}
/*
[ 0, 1 ]
[ 1, 2 ]
[ 2, 3 ]
[ 3, 4 ]
[ 4, 5 ]
*/
```

### every

Dizi içerisinde bulunan elemanların belirtilen testi başarıyla geçip geçmediğinin kontrol eder. (Elemanlardan herhangi birinin testi geçmesi yeterlidir.)

```javascript
console.log(array1.every((i) => {
    return i > 3;
})); //false
```

### fill

Dizi içerisinde belirli bir veriyi veya tüm verileri istenilen değer ile değiştirir. Bu işlemden sonra herhangi bir atama yapmaya gerek yoktur. İşleme tabi tutulan array'ın değerleri güncellenir.

```javascript
// Tüm elemanları 0 olarak günceller
console.log(array1.fill(0)); //Output [ 0, 0, 0, 0, 0 ]

// 1. ile 3. index numarası arasında olan elemanları 0 olarak günceller.
// fill(value, start_index, end_index)
console.log(array2.fill(0, 1, 3)); //Output [ 5, 0, 0, 4 ]
```

### filter

Belirtilen kuralları karşılayan array elemanlarından oluşan bir dizi döndürür.

```javascript
console.log(array1.filter((x) => x < 3)); //Output [ 1, 2 ]
```

### find

Belirtilen kuralları karşılayan ilk dizi elemanını döndürür.

```javascript
console.log(array1.find((x) => x > 0)); //Output 1
```

### findLast

find işlemini dizinin sonundan başlayarak gerçekleştirir ve şartı sağlayan ilk elemanı döndürür.

```javascript
console.log(array1.find((x) => x > 3)); //4
```

### findIndex

Belirli kuralları karşılayan ilk dizi elemanının index numarasını döndürür. (yoksa -1)

```javascript
console.log(array1.findIndex((x) => x == 3)); //Output 0
```

### forEach

Tüm dizi elemanını sırayla döndürür.

```javascript
array1.forEach((item) => console.log(item));
/* Output
1
2
3
4
5
*/
```

### includes

Dizi içerisinde bir değer araması yapmak için kullanılır. (Belirli bir index numarasından aramaya başlatmak için ikinci parametre kullanılabilir.)

```javascript
console.log(array1.includes(1)); //true
```

### indexOf

Dizi içerisinde bulunan bir elemanın index numarasını döndürür. (Belirli bir index numarasından aramaya başlatmak için ikinici parametre kullanılabilir.)

```javascript
console.log([].indexOf(1)); //0
```

### lastIndexOf

Sondan başlayarak dizi içerisinde aranan bir elemanın index numarasını döndürür.

```javascript
console.log([4,3,5,3,2,3].lastIndexOf(3)); //5
```

### isArray

Bir nesnenin dizi olup olmadığını kontrol eder.

```javascript
console.log(Array.isArray(array1)); //true
```

### join

Bir dizinin tüm elemanlarını bir string içerisinde sıralı şekilde almamızı sağlar. Bu işlemi yaparken her bir elemanın arasına eklenecek bir ayraç belirlenir.

```javascript
console.log("join", array1.join("-")); //1-2-3-4-5
```

### keys

Dizinin her bir elemanlarından oluşan bir **Iterator** döndürür.

```javascript
console.log(array1.keys());
```

### length

Dizinin eleman sayısın döndürür.

```javascript
console.log(array1.length); //5
```

### map

Dizinin tüm elemanlarını sırayla döndürür ve bu döndürme işleminde dizi elemanlarının değerlerini güncellememize olanak sağlar.

```javascript
console.log(array1.map((x) => x * 2)); //[ 2, 4, 6, 8, 10 ]
```

### pop

Dizinin son elemanını siler ve silinen elamanı döndürür.

```javascript
console.log(array1.pop()); //5
```

### shift

Dizinin ilk elemanını siler ve silinen elamanı döndürür.

```javascript
console.log(array1.shift()); //1
```

### push

Diziye yeni bir eleman ekler.

```javascript
array1.push(9);
console.log(array1) //[ 1, 2, 3, 4, 5, 9 ]
```

### of

Girilen tüm argümanlardan oluşan bir dizi döndürür. Argümanlar herhangi bir tipe sahip olabilir ve istenildiği kadar argüman girilebilir.

```javascript
console.log(Array.of('1', false, 'ABC', 'FS'))
```

### reduce

Sırayla dizinin tüm elemanlarını kullanarak yapılan işlemi bir sonraki dizi elemanıyla işlem yapmak için aktarılır. _(Aşağıda bulunan örnekte 0 olarak belirtilen kısımn result değerinin başlangıç değeridir. Eğer bu değer belirtilmezse result değerinin başlangıç değeri dizinin 0. indexinde elemanı olacaktır. Bundan dolayı value'nin başlangıç değer dizinin 1. indexinde bulunan eleman olacaktır.)_

```javascript
array1.reduce((result, value) => {
  console.log(`${result} - ${value} = ${result - value}`)
  return result - value;
}, 0)

/*
 0 - 3 = -3
-3 - 2 = -5
-5 - 3 = -8
-8 - 4 = -12
-12 - 5 = -17
*/
```

### reduceRight

reduce ile aynı işlemi yapmaktadır. Tek fark işleme dizinin sonundan başına doğru giderek gerçekleştirir.

```javascript
array1.reduceRight((result, value) => {
  console.log(`${result} - ${value} = ${result - value}`)
  return result - value;
}, 0)

/*
 0 - 5 = -5
-5 - 4 = -9
-9 - 3 = -12
-12 - 2 = -14
-14 - 3 = -17
*/
```

### reverse

Dizinin eleman sıralamasını tersine çevirir.&#x20;

```javascript
console.log(array1.reverse()); //[ 5, 4, 3, 2, 3 ]
```

### slice

Belirtilen index numaraları arasındaki elemanlardan oluşan yeni bir dizi döndürür.

```javascript
console.log(array1.slice(1, 3)); //[ 2, 3 ]
/* 1. index dahil 3. index dahil değildir.
```

### some

Dizi içerisinde bulunan elemanların belirtilen testi başarıyla geçip geçmediğini kontrol eder. (Elemanlardan herhangi birinin testi geçmesi yeterlidir.)

```javascript
console.log(array1.some((x) => x == 2));
```

### sort

Dizi elemanlarını artan şekilde sıralar ve mevcut diziyi sıralanmış elemanları ile günceller.

```javascript
console.log(array1.sort()); //[ 2, 3, 3, 4, 5 ]
```

### splice

Diziye eleman ekleme veya elemen silme için kullanılır.&#x20;

1\. parametre başlangıç index numarası

2\. parametre silinecek eleman sayısı&#x20;

3\. ve daha fazlası ise eklenecek elemen değerleridir.

```javascript
 console.log(array1.splice(1, 0, 3, 4, 5));

/*
old: [3, 2, 3, 4, 5]

[
  3, 3, 4, 5,
  2, 3, 4, 5
]
*/
```

### unshift

Dizinin başına yeni bir eleman ekler ve dizinin güncel eleman sayısını döndürür.

```javascript
console.log(array1.unshift(1)) //6
```

### at

Verilen index numarasına ait dizi elemanını döndürür. Pozitif değerler dizinin başından negatif değerle dizinin sonunda başlayarak eleman arar.&#x20;

```javascript
console.log(array1.at(-1)) //5
console.log(array1.at(0)) //3
```

## copyWithin

Dizinin bir bölümünü aynı dizide farklı bir konuma taşır. Dizinin eleman sayısını değiştirmez taşınacak indexlerin üzerine yazar.

```javascript
console.log(array1.copyWithin(0, 3, 4))
/* 3. ve 4. index arasında olan tüm elemanları 0. elemana taşır.
old: [3, 2, 3, 4, 5]
new: [ 4, 2, 3, 4, 5 ]

```

