# async/await

Async/await ES7 ile javascript'e kazandırılmış bir yapıdır. Bir önceki konumda promise yapılarını anlatmıştım. Promise yapılarını yakalamak için **then** ve **catch** bloklarını kullanıyorduk. Birden fazla **then** bloğunu birleştirerek bir zincir oluşturduğumuzda bir süre sonra kod okunamaz ve karmaşık hale gelmektedir. Bu yüzden asenkron işlemleri daha kolay tanımlayabilmemiz için **async/await** yapısı ortaya çıkmıştır.

Basit bir async/await yapısı tanımlayalım.

```javascript
const loadData = async () => {
  return { data: [1, 3, 4, 5, 6] };
};

const writeData = async () => {
  try {
    let data = await loadData();
    console.log(data);
  } catch (error) {
    console.warn(error);
  }
};

writeData();

//output { data: [ 1, 3, 4, 5, 6 ] }
```

**async** bir fonksiyon oluşturduk ve bunu loadData değişkenine atadık. Daha sonra farklı bir **async** bir fonksiyon içerisinde loadData'yı çağırdık. Fakat normal çağırma biçiminden farklı olarak başına **await** kelimesini ekledik. Bu kelime asenkron olan bir işlemin sonucu dönene kadar beklemesini sağlamaktadır. Sonuç döndükten sonra aşağıdaki kodları çalıştırmaya devam eder. Bu şekilde **then** bloğu kullanmadan tek satırda promise bir işlemin sonucunu alabildik. Kodumuzu **try catch** bloğuna alarak da olası bir hata yakalama durumunu gerçekleştirdik. NOT: **await** sadece async fonksiyonlar veya async yapılar içerisinde kullanılır. Yukarıdaki kodda writeData fonksiyonunu async olarak işaretlemeseydik **await** yapsını kullanamazdık.

async / await yapısını daha iyi anlamak için bir örnek yapalım.

```javascript
const axios = require("axios")

var data = []

async function fetchAlbums() {
   var result = await axios.get("https://jsonplaceholder.typicode.com/albums")
   data = result.data
   console.log("fetchAlbums() - data.length: " + data.length)
}

async function getAlbums() {
  fetchAlbums()
  console.log("getAlbums() - data.length: " + data.length)
}

getAlbums()

/* output
getAlbums() - data.length: 0
fetchAlbums() - data.length: 100
*/
```

**data** adında bir boş dizi tanımladık. Daha sonra **fetchAlbums** adında asenkron bir fonksiyon oluşturarak içerisinde **axios** ile endpoint'den veri çekmesini sağladık. Burada **axios.get** işlemi bir **promise** yani asenkron yapı olduğu için **then** bloğu kullanmadan direkt **await** kelimesini başına ekleyerek asenkron işlem tamamlanana kadar kodumuzu beklettik. Axios tarafından dönen veriyi data dizisine atadık ve bir console.log işlemi gerçekleştirdik. Daha sonra **getAlbums** adında farklı bir asenkron fonksiyon oluşturarak **fetchAlbums** fonksiyonunu çağırdık ve bir console.log işlemi gerçekleştirdik. **getAlbums** fonksiyonumuzu çalıştırdığımızda console çıktısı olarak birinci satırda **data.length: 0** ikinici satırda ise **data.length: 100** yazdığını gözlemleyeceğiz. Oysaki ikisi de aynı değişkenin eleman sayısını yazdırıyor. Yukarıdaki kodda unuttuğumuz bir **await** kelimesi ile asenkron olan fetchAlbums fonksiyonunu beklemedik. Bundan dolayı axios ile veri çekme işlemimiz sonuçlanmadan bir diğer satırdaki console.log işlemi çalışarak **data.length: 0** çıktısını vermiştir. Ayrıca normal şartlarda öncelikle **fetchAlbums** içerisindeki console.log çıktısı verilmesi gerekiyorken ilk çıktımız getAlbums fonksiyonu içerisindeki console.log çıktısı olmuştur. Bunun sebebi ise axios.get işlemini await ile beklememizdir. Yukarıdaki kodda bulunan hatamızı düzeltelim.

```javascript
async function getAlbums() {
  await fetchAlbums()
  console.log("getAlbums() - data.length: " + data.length)
}

/* output
fetchAlbums() - data.length: 100
getAlbums() - data.length: 100
*/
```

**fetchAlbums** fonksiyonumuzu çağırmadan önce başına **await** kelimesini ekledik. Böylece asenkron işlemlerimizi sıralı şekilde yaptık ve istediğimiz sonuçlara ulaştık.
