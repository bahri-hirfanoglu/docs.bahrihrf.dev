# promise

Promise kısaca asenkron çalışarak içerisinde yapılacak işlem eğer başarılı ise **resolved** başarısız ise **rejected** tiplemelerini kullanarak geri değer döndüren yapıdır. Bir Promise sadece bir defa resolved (başarılı) veya sadece bir defa rejected (başarısız) geri dönüş yapabilir.

Bir örnekle promise yapısını daha iyi anlayabiliriz.

```javascript
function checkUsername(username) {
    return new Promise((resolve, reject) => {
        if (username === "admin") {
            resolve(username)
        } else {
            reject("Username Invalid")
        }
    })
}
```

Yukarıdaki örnekte görüldüğü gibi **checkUsername** adında bir fonksiyon oluşturduk ve geriye bir Promise yapısı döndürmesini istedik. Promise yapısı içerisine resolve, reject adında iki fonksiyon tanımladık. if bloğumuz ile gelen username parametresini **admin** denk olup olmadığını kontrol ettik. Eğer denk yani işlemimiz başarılı ise **resolve** fonksiyonu ile geriye username parametresini döndürdük. Eğer gelen parametre koşulları sağlamıyorsa **reject** ile geriye "Username Invalid" mesajını döndürdük. Bu şekilde bir promise yapısı oluşturmuş olduk. Gelelim bu promise yapısını kullanmaya

```javascript
const inputUsername = document.querySelector("#username").value;

checkUsername(inputUsername)
.then(result => {
    console.log(result)
})
.catch(error => {
    console.warn(error)
})

/* 
inputUsername = "admin"
-- output --
admin

------------------------------

inputUsername = "bahri"
-- output --
Username Invalid

*/
```

dom üzerinde bulunan bir input nesnesinden kullanıcı adını aldık. Daha sonra **checkUsername** fonksiyonunu çağırdık ve içerisine parametremizi verdik. Burada kullandığımız **then** bloğu geri dönecek olan promise yapısında **resolve** yani başarılı işlemi yakalamamızı sağlıyor. Eğer girilen username admin ise **then** yapısı içerisine girerek result parametresine resolve içerisine girdiğimiz değer atanacaktır. Farklı bir username girildiği taktirde bu sefer **then** bloğu atlanarak **catch** bloğuna gelecektir. Yani **reject** yapımız çalışmış olacak ve **catch** içerisinde bulunan error parametresine reject içerisine verdiğimiz değer atanacaktır.

### **Promise Zinciri** <a href="#promise-zinciri" id="promise-zinciri"></a>

Promise yapısı gereği asenkron çalışır fakat biz promise ile oluşturulan işlemleri sıralı olarak yani senkron olarak çalıştırmak isteyebiliriz. İşte bu durumda promise zincirini kullanabiliriz. Bir örnekle durumu anlayalım.

```javascript
const post = new Promise((resolve, reject) => {
    axios.get("https://jsonplaceholder.typicode.com/posts")
    .then(result => {
        resolve(result.data.length)
    }).catch(error => {
        reject(error)
    })
})

const comment = new Promise((resolve, reject) => {
    axios.get("https://jsonplaceholder.typicode.com/comments")
    .then(result => {
        resolve(result.data.length)
    }).catch(error => {
        reject(error)
    })
})

post.then(result => {
    console.log("post: " + result)
})

comment.then(result => {
    console.log("comment: " + result)
})

/* output 
comments: 500
posts: 100 */
```

Yukarıdaki kodda görüldüğü üzere ilk önce **post** promise yapısı çağırılsa da ilk işlemi sonlanan **comment** promise yapısı oldu. Tabii ki bu durum bu işlemi her çalıştırdığımızda farklılık gösterir çünkü her ikisi de birbirinden bağımsız yani asenkron şekilde çalışmaktadır. Her iki promise yapısı içerisinde farklı url'den axios ile veri çektiğimiz için istek attığımız url'lerden hangisi bize ilk dönüşü yaparsa o promise yapısı sonlanacaktır ve console.log çıktısını yazacaktır. Şimdi bunları sıralı hale getirelim ve önce post işlemini daha sonra comment işlemini sonuçlandıralım.

```javascript
post
  .then((result) => {
    console.log(result);
    return comment;
  })
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.warn(error);
  });
```

**post** promise yapısı için **then** işlemi oluşturduk. Eğer post promise yapısı resolved (başarılı) bir dönüş yaparsa console.log çıktısını verdik ve daha sonra **return comment** diyerek diğer promise yapımızı çalıştırdık. Bunu da birinci then yapımızın bitişinde yeni bir then bloğu açarak yakaladık. Tüm bu then zincirlemesinin en altında olası **rejected** dönüşler için **catch** bloğumuzu oluşturduk. Bu catch blog her iki promise için rejected dönüşlerini yakalayacaktır.

### **Promise Metodları** <a href="#promise-metodlari" id="promise-metodlari"></a>

Promise içerisinde hazır metodlar bulunmaktadır. Bunları bir promise nesnesi oluşturmadan static bir metod gibi kullanabiliriz. Aşağıdaki örnekleri inceleyerek detaylandıralım.

**1- Promise.resolve()**

Bu yapı başarılı bir şekilde sonuçlanmış bir promise yapıdır ve **then** ile yakalanarak değere ulaşılabilir.

```javascript
const success = Promise.resolve({ data: [1, 2, 3, 4, 5] });

success
  .then((result) => {
    console.log(result);
  })

//output { data: [ 1, 2, 3, 4, 5 ] }
```

**2- Promise.reject()**

Bu yapı başarısız bir şekilde sonuçlanmış bir promise yapıdır ve catch ile yakalanarak değere ulaşılabilir.

```javascript
const error = Promise.reject({data: null})
const error = Promise.reject({ data: null });

error.catch((error) => {
  console.warn(error);
});

//output { data: null }
```

**3- Promise.all()**

Bu yapı içerisine bir promise dizisi verilir. Verilen bu promise dizisi içerisinde işlemler tek bir promise yapısına aktarılarak toplu ve asenkron olarak çalıştırılır. Dizi içerisine verdiğimiz tüm promise yapıları eğer **resolved** (başarılı) şekilde sonuçlandıysa **then** ile dizi şeklinde dönen değerleri sırayla alabiliriz. Eğer işlemlerden herhangi biri rejected (başarısız) olursa bunu catch yapısı ile yine yakalayabiliriz.

```javascript
const updateUsername = new Promise((resolve, reject) => {
  resolve("update username");
});

const updateEmail = new Promise((resolve, reject) => {
  resolve("update email");
});

const updateUserActivity = new Promise((resolve, reject) => {
  resolve("update user activity");
});

const allUpdate = Promise.all([
  updateUsername,
  updateEmail,
  updateUserActivity,
]);

allUpdate
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.warn(error);
  });

//output [ 'update username', 'update email', 'update user activity' ]
```

**4- Promise.race()**

Bu yapı içerisine de all gibi bir promise dizisi verilir. Bu yapının all'dan farklı tüm promise işlemlerinden ziyade içerisindeki herhangi bir promise'den cevap aldığı anda o promise değeri racePromise atanır. Yani kısaca en hızlı cevap veren kazanır diyebiliriz. Burada bilinmesi gereken en önemli husus cevap resolved (başarılı) veya rejected (başarısız) olsa bile kazanan ilk cevap veren olarak belirlenir.

```javascript
avconst updateUsername = new Promise((resolve, reject) => {
  resolve("update username");
});

const updateEmail = new Promise((resolve, reject) => {
  resolve("update email");
});

const updateUserActivity = new Promise((resolve, reject) => {
  resolve("update user activity");
});

const racePromise = Promise.race([
  updateUsername,
  updateEmail,
  updateUserActivity,
]);

racePromise
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.warn(error);
  });

//output update username
```
