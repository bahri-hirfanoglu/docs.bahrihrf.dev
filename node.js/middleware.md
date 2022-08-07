# Middleware

Middleware (ara katman) sistem ile uygulama arasında bulunana katmandır diyebiliriz. Bu katmanı anlamak için öncelikle bir örnek oluşturalım.

Örneğimiz için öncelikle express kütüphanesini projemize ekliyoruz ve daha sonra aşağıda bulunan kodları yazarak http sunucumuzu ayağa kaldırıyoruz.

```javascript
const express = require("express");
const app = express();

const SERVER_PORT = process.env.SERVER_PORT || 5000

app.get('/admin',(req, res) => {
    res.send("Admin Page")
})


app.listen(SERVER_PORT, () => {
    console.log(`Server started! Listening port ${SERVER_PORT}`);
});
```

5000 portunu dinleyen ve **localhost:5000/admin** path'ini tarayıcımızda çalıştırdığımızda **Admin Page** yanıtını gönderecek basit bir http sunucumuz mevcut.

Şimdi şöyle bir senaryo düşünelim. /admin bölümüne sadece belirli kullanıcıların erişmesini istiyoruz. Bu yüzden bir session kontrolü yapmamız gerekiyor. Peki bu kontrolü nerede yapacağız. Bunun için en mantıklı kısım middleware katmanıdır. Peki midddleware katmanını nasıl oluşturabiliriz. Şimdi bunun cevabını kodlarımız ile basit şekilde gösterelim.

```javascript
const express = require("express");
const app = express();

const SERVER_PORT = process.env.SERVER_PORT || 5000

//Middleware
const adminMiddleware  = (req, res, next) => {
    console.log("adminMiddleware")
    next()
}

app.get('/admin', adminMiddleware,(req, res) => {
    console.log("/admin get")
    res.send("Admin Page")
})


app.listen(SERVER_PORT, () => {
    console.log(`Server started! Listening port ${SERVER_PORT}`);
});
```

Yukarıda **adminMiddleware** adında bir fonksiyon oluşturduk ve içerisine **(req, res, next)** parametresini almasını istedik. Daha sonra **/admin** path'inin get isteklerini dinleyen yapımızda path adı ile **(req, res)** yapısının arasına ara katman fonksiyonu adımızı yazdık. Aslında buradan da gözüktüğü gibi **middleware** request geldikten sonra istek get gövdesine ulaşmadan önce iletişime geçilen katmandır diyebiliriz. Şimdi bu kodlardan sonra bir tarayıcı açarak http://localhost:5000/admin url'ine istek atalım ve daha sonra consol çıktımızı kontrol edelim.

![](https://bahrihirfanoglu.com.tr/wp-content/uploads/2022/02/image.png)

Görüldüğü üzere istek geldiğinde önce middleware katmanına daha sonra get gövdesine ulaşmaktadır. Middleware içerisinde bulunan **next** ise işlemin bir sonraki katmana geçmesini sağlamaktadır. Eğer middleware içerisinde **next()** işlemini belirtmezsek istek get gövdesine ulaşmaz.

```javascript
const adminMiddleware  = (req, res, next) => {
    console.log("adminMiddleware")
    res.send("middleware send")
}
```

Ayrıca middleware içerisinde sadece next ile değil response yapısına herhangi bir cevap yanıtı göndererek de isteğin get gövdesine ulaşmasını engelleyebiliriz. Response yanıtlarını kullandığımızda next'i çağırmaya gerek yoktur.

Şimdi genel middleware mantığını öğrendik. Kodumuzu içerisinde gerçek bir kontrol yaparak işlemlerimizi sonlandıralım. Öncelikle cookie kontrol işlemi yapmak için **jwt web token** kütüphanesini projemize dahil ediyoruz. Bunun için **npm i jsonwebtoken** komutunu kullanabiliriz. Ayrıca tokeni cookie'lere kaydedeceğimiz ve oradan okuyarak kontrol edeceğimiz için cookie-parser kütüphanesini de projemize eklememiz gerekmektedir. **npm i cookie-parser** komutu ile ekleme işlemini yapabiliriz. Tüm işlemlerden sonra kodumuz aşağıdaki gibi olacaktır.

```javascript
jaconst express = require("express");
const cookieParser = require("cookie-parser")
const jwt = require('jsonwebtoken')
const app = express();

app.use(cookieParser())

const SERVER_PORT = process.env.SERVER_PORT || 5000
const userKey = "9Lm4L8ULhQ"

//Middleware
const adminMiddleware  = (req, res, next) => {
    const token = req.cookies.jwt
    if(token) {
        jwt.verify(token, userKey, (err, decodedToken) => {
            if(err) {
                res.send("user verify error")
            } else {
                next()
            }
        })
    } else {
        res.send("token not found")
    }
}

app.get('/admin', adminMiddleware,(req, res) => {
    res.send("Admin Page")
})

app.listen(SERVER_PORT, () => {
    console.log(`Server started! Listening port ${SERVER_PORT}`);
});
```

Projemizin en üst kısmına jwt ve cookieParser bağlantılarımızı yaptık. **app.use(cookieParser())** kodu ile aslında express içerisine bir middleware tanımlamış olduk. Çünkü artık bu yapı ile expresse gelen tüm istekler içerisinde bulunan cookie'leri otomatik olarak parse edecek. Yani **req.cookies.cookieAdimiz** şeklinde gelen isteklerin cookie'lerine erişebileceğiz. adminMiddleware yapısı içerisinde jwt.verify fonksiyonu ile tokenimizi kontrol ettik ve geçerli bir token ise next() diyerek get gövdesine gidişine izin verdik. Fakat tokenimiz bulunmuyorsa veya hatalıysa kullanıcımıza uyarı mesajımızı gönderdik. Basit mantıkta middleware yapısı bu şekildedir. Tabii ki middleware sadece bu işlemler için değil proxy, log, cookie, session kontrolü vb işlemler içinde kullanılmaktadır.
