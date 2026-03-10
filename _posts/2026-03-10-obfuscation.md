---
title: Obfuscation
date: 2026-03-05 20:00:00 +0300
categories: [Siber Güvenlik Temelleri]
tags: [Siber Ölüm Zinciri, Sızma Testi, Siber Güvenlik Metodolojisi, MITRE ATT&CK, Siber Güvenlik Temelleri]
author: rabiacelikli
---

![Image](/assets/img/2026-03-05/obfuscation_1.png)

## Giriş
Şimdi şöyle bir senaryonun içine girdiğimizi varsayalım:

Evinizde huzurluca oturuyorsunuz. Sizi bir süredir gözlemleyen, ama varlığından haberdar olmadığınız bir hırsız var. Yeterince bilgi topladığını düşünen hırsız artık harekete geçmeye karar veriyor.
Bir anda kapı ziliniz çalıyor. Refleks olarak soruyorsunuz: "Kim o?"

Karşıdaki kişi elbette "Hırsızım" demiyor. Kendini bir kargocu olarak tanıtıyor. Kapı deliğinden baktığınızda üzerinde bir kargo firması logosu bulunan yelek var, elinde de aynı logoyla kaplanmış bir paket. Şüphelenmez ve kapıyı açarsanız, en güvenli alanınızı bir kargocuya değil, bir hırsıza açmış olursunuz.

Gerçek hayatta bu tür senaryolar görece nadir olabilir. Ancak siber güvenlik dünyasında bu yaklaşım sandığınızdan çok daha yaygındır. Saldırganlar gerçek niyetlerini gizler, masum gibi görünür ve savunma mekanizmalarını yanıltmaya çalışır.

İşte bu noktada karşımıza çıkan kavram: **obfuscation.**

## Obfuscation
Obfuscation, kelime olarak gizleme, örtme, karartma gibi anlamlara sahiptir (Tureng). Siber güvenlik dünyasında ise bu daha çok bir şeyi anlamayı zorlaştırmak anlamında kullanılır. Obfuscation aslında iki yüzü olan bir madeni paraya benzer çünkü obfuscation sadece malware gizlemeye yaramaz, verileri anonimleştirmek ve daha güvenli şekilde saklamak için de kullanılır. 

## Data Obfuscation
Data Obfuscation, Türkçeye çevirmek istersek veri gizleme, veriyi tamamen şifrelemekten farklı olarak, verinin işlevselliğini kısmen koruyarak anlaşılmasını zorlaştırmayı amaçlar. Bu sayede yetkisiz erişim gerçekleşse bile saldırganın elde ettiği veri doğrudan anlamlı olmayabilir. Data obfuscation'a olan ihtiyacı en güzel IBM'in "Cost of a Data Breach 2025" raporu gözler önüne seriyor. IBM'e göre 2025'te veri ihlallerinin küresel ortalama maliyeti 4,44 milyon dolara ulaştı ve maliyetin ileriki yıllarda katlanarak artacağı öngörülüyor. 

Öte yandan, Verizon tarafından yayımlanan Data Breach Investigations Report'a göre saldırıların önemli bir kısmı geçerli kullanıcı hesaplarının kötüye kullanılmasıyla başlamaktadır. Bu durum, saldırganların sistemlere yetkili kullanıcı gibi erişebilmesine olanak tanımaktadır. Böyle bir senaryoda saldırgan sistem içerisindeki veriye erişebilse bile data obfuscation teknikleri sayesinde hassas bilginin doğrudan okunabilir olmaması sağlanabilir.

### Önemli Data Obfuscation Teknikleri
**Data Masking (Veri Maskeleme):** Veri maskeleme, hassas bilgileri değiştirerek gerçek veriye benzer ancak güvenli bir veri seti oluşturma yöntemidir. Bu süreçte, verinin yapısı ve gerçekçiliği korunurken içerik çeşitli tekniklerle değiştirilir. Maskeleme uygulandıktan sonra ise orijinal verilere, yalnızca maskelenmiş veri üzerinden geri ulaşmak mümkün değildir. İki çeşidi vardır: Statik ve dinamik maskeleme.

**Statik Maskeleme**, orijinal veritabanındaki veriler maskelenir, yani maskeleme işlemi veritabanına yazılır ve artık gerçek veri kullanılmaz. Daha çok test ortamları, veri analizlerinde veya development ortamlarında kullanılır çünkü gerçek hassas verilerle çalışmak alınılabilecek bir risk değildir. 

Küçük bir örnek olarak test ortamında elimizde farazi bir e-posta adresi olduğunu düşünelim:

```
E-mail: ayse.fatma@gmail.com
```

Statik maskeleme sonrasında:

```
E-mail: user_102@test.com
```

Böylece test ortamında gerçek e-posta kullanılmamış olur.

**Dinamik Maskeleme**, statik maskelemenin aksine gerçek veriler değiştirilmez. Kullanıcılar eriştikçe veya sorguladıkça mevcut hassas verileri dinamik olarak değiştirir, böylece uygulamalar ve kullanıcılar maskelenmiş verileri görür ancak verilerin gerçek kopyasına yalnızca yetkili roller erişebilir. Uzun lafın kısası, veriler veritabanında orijinal hallerini korur, yetkisi olmayanlar ise bu veriyi maskelenmiş olarak görür.

SQL'de bir kredi kartı bilgilerini şu şekilde maskeleyebiliriz:

```
ALTER TABLE Customers
ALTER COLUMN CreditCard
ADD MASKED WITH (FUNCTION = 'partial(0,"**** **** **** ",4)');
```

Sonuç: 
```
**** **** **** 1234
```

**Tokenization (Tokenizasyon):** Tokenizasyon, hassas verileri gizli olmayan başka verilerle değiştirilir. Değiştirilen verilere "token" denilir. Orijinal veri bir token ile değiştirildikten sonra sistem bu veriyi "token vault" denen iyi korunaklı bir sunucuya gönderir, böylece sistemde asıl veri değil token işlem görür. Sadece token vault'a erişim izni olan yetkili kişiler token ve orijinal veri arasındaki bağlantıyı görebilir.

Tokenizasyon özellikle ödeme sistemlerinde yaygın olarak kullanılmaktadır. Herhangi bir alışveriş sitesine kredi kartı bilgilerinizi kaydettiyseniz, mevzubahis site kart bilgilerini değil token'ı saklar.

Orijinal veri:
```
Kredi Kartı: 1234567890123456
```
Tokenized veri:
```
Kredi Kartı:TKN_91XK27A
```
**Data Encryption (Veri Şifreleme):** Şifrelemenin mutfağında üç ana malzeme vardır: Normal orijinal veri (plaintext), şifreleme algoritması (encryption algorithm) ve anahtar (key). Yani, elinizdeki normal veriyi (plaintext) matematiksel bir algoritma kullanarak okunamaz bir forma (ciphertext) dönüştürme işlemidir ve yalnızca doğru anahtara sahip sistemler tarafından tekrar çözülebilir.  

Şifreleme sayesinde veriler ister yerel bir sistemde ister bulut ortamında bulunsun güvenli şekilde saklanabilir. Ayrıca verilerin iletilmesi ve işlenmesi sırasında da korunmasını sağlar. Bu nedenle, şifreleme bulut güvenliği çalışmaları ve daha geniş anlamda siber güvenlik stratejileri için kritik önem taşımaktadır. IBM'in "Cost of a Data Breach 2025" raporuna göre , şifreleme kullanan kuruluşlar, veri ihlalinin finansal etkisini 200.000 ABD dolarından fazla azaltabilir. (IBM)

İki ana türü vardır: Simetrik ve asimetrik şifreleme.

**Simetrik şifreleme**nin mantığı oldukça basittir. Şifreleme yapılırken kullanılan key aynı şekilde çözmek için de kullanılır. Yani içeriye girmek için de çıkmak için de tek anahtar yeterlidir. Simetrik şifreleme hızlı ve verimli olsa da key'i bulan kişi tüm bilgileri çözebileceği için daha dikkatli olunmalıdır.

**Asimetrik şifreleme** ise simetrik şifrelemeye nazaran daha karmaşık ve yavaştır ancak daha güvenli olduğunu söyleyebiliriz. Bunun sebebi public key ve private key dediğimiz iki unsurun kombinasyonudur. Şifreleme kısmında public key kullanılabilir ancak private key sahibi kişi orijinal veriyi görebilir.

Küçük bir örnek üzerinden bunu görelim.

Veri (Plaintext):
```
Şifre: şifre123
```

Key ve şifreleme algoritmaları sonrasında veri:
```
U2FsdGVkX1+4sY8jK3vL8pR4...
```

Daha bir çok obfuscation tekniğinden bahsedebiliriz elbet ama hepsi genel olarak tek bir amaca hizmet ediyor: veriyi anonimleştirmek. Sistemlere yetkisiz erişim gerçekleşse bile, saldırganın eline geçen veri doğrudan okunabilir veya anlamlı değilse bu veri çoğu zaman pratik bir değer taşımaz.

## Malware Obfuscation
Obfuscation’dan bahsederken iki yüzü olan bir madeni paraya benzetmesi yapmıştık. Data obfuscation’ın ve verinin anonimleştirilmesinin önemini gördük. Ancak bu gizleme teknikleri yalnızca veriyi korumak için mi kullanılır?

Aslında hayır. Aynı teknikler saldırganlar tarafından zararlı yazılımları gizlemek ve güvenlik mekanizmalarından kaçınmak için de kullanılabilir. Hatta bu yaklaşım MITRE ATT&CK Framework'ünde Defense Evasion taktiği altında "Obfuscated Files or Information" (T1027) tekniği olarak yer almaktadır. Başlıca hedef kötü amaçlı yazılımın davranışını değiştirmeden görünümünü değiştirerek tespit edilmesini önlemeye çalışmaktır. Bu gizlemeyi birden çok şekilde yapabilirler, bu yüzden MITRE ATT&CK içerisinde tam tamına 17 alt teknikle beraber listelenir. 

Obfuscation tekniklerinin gerçek dünyadaki kullanımına verilebilecek en dikkat çekici örneklerden biri **SolarWinds** saldırısıdır. 2020 yılında ortaya çıkan bu saldırıda, saldırganlar SolarWinds Orion yazılımının güncelleme sürecine zararlı kod enjekte ederek bir supply chain saldırısı gerçekleştirmiştir. Güncelleme paketinin içine gizlenen bu zararlı kod, birçok güvenlik kontrolünden fark edilmeden geçebilmiştir. Zararlı yazılımın analizini zorlaştırmak için çeşitli obfuscation teknikleri kullanılmış ve böylece saldırı aylar boyunca fark edilmeden devam etmiştir.

Şimdi birkaç malware obfuscation yöntemlerine bakalım.

### Önemli Malware Obfuscation Yöntemleri
**Steganography (Steganografi):** Arkadaşınızın gönderdiği maile eklenmiş png dosyasını indirirken kaç kere durup düşünürsünüz? Steganofrafi yüzünden iki kez düşünmenizde fayda var çünkü bu yöntem sayesinde saldırganlar, tespit edilmemek için zararlı yazılımı başka veriler veya nesneler içine saklar. Steganografi; metin, resim, video veya ses içeriği dâhil olmak üzere neredeyse her tür dijital içeriği gizlemek için kullanılabilir. Bu gizli veriler hedefine ulaştıktan sonra çıkarılır. 

Steganografi tekniklerinin gerçek saldırılarda nasıl kullanılabildiğine dair dikkat çekici örneklerden biri 2016 yılında ortaya çıkan Stegano Exploit Kit saldırısıdır. Bu saldırıda saldırganlar, popüler web sitelerinde yayınlanan banner reklamlarını kullanarak zararlı kod dağıtmıştır.

Saldırganlar, JavaScript kodunu reklam görsellerinin pikselleri içerisine gizlemiştir. Kullanıcılar bu reklamların bulunduğu web sayfalarını ziyaret ettiğinde, farkında olmadan zararlı kodu tetikleyen bir süreç başlatılmıştır. Bu süreç sonucunda kullanıcı sistemine ek zararlı yazılımlar indirilebilmiştir.

Bu saldırının etkili olmasının en önemli nedeni, reklamların çok geniş bir kullanıcı kitlesine ulaşabilmesiydi. Ayrıca zararlı kodun doğrudan bir dosya içerisinde değil, bir görselin piksel verileri içerisine gizlenmiş olması, geleneksel antivirüs yazılımlarının bu tehdidi tespit etmesini oldukça zorlaştırmıştır.

**Stripped - Obfuscated Payloads:** Saldırganların kullandığı bir diğer obfuscation tekniği ise payload’un okunabilirliğini azaltmaktır. Bu yöntemde zararlı kod içerisindeki yorum satırları, değişken isimleri ve sembol bilgileri kaldırılır veya anlamsız hale getirilir. Böylece kod daha kısa ve karmaşık bir yapı kazanır.

Bu işlem sonucunda ortaya çıkan payload genellikle insanlar tarafından okunması oldukça zor bir hale gelir. Kodun işlevi aynı kalırken, analiz yapan güvenlik araştırmacılarının veya otomatik analiz araçlarının kodu anlaması daha fazla zaman ve çaba gerektirir.

Mesela XSS saldırılarında kullanılan JsFuck yöntemi ilginç bir örnektir. JSFuck, JavaScript kodunu yalnızca altı farklı karakter kullanarak yazmaya imkân veren bir obfuscation tekniğidir. Bu karakterler şunlardır:


```
[ ] ( ) ! +
```
Normalde JavaScript kodu harfler, sayılar ve çeşitli semboller içerir. Ancak JSFuck tekniğinde bu karakterler yerine yalnızca yukarıdaki altı sembol kullanılarak aynı işlemler gerçekleştirilebilir. Bu da ortaya çıkan kodun insanlar tarafından okunmasını ve anlaşılmasını oldukça zorlaştırır.

Bu teknik, JavaScript’in bazı ilginç özelliklerinden faydalanır. Örneğin JavaScript’te boolean değerler, diziler ve tip dönüşümleri kullanılarak harfler ve sayılar üretilebilir. Bu sayede yalnızca birkaç sembolle oldukça karmaşık ifadeler oluşturmak mümkündür.

Örneğin basit bir JavaScript komutu şu şekilde yazılabilir:
```
alert(1)
```

Ancak JSFuck kullanıldığında aynı komut çok daha karmaşık ve anlaşılması zor bir hale dönüşebilir:
```
[][(![]+[])[+[]]+(![]+[])[!+[]+!+[]]]
```
**Binary Padding:** Binary padding, zararlı bir dosyanın içerisine işlevsel olmayan ek veri yerleştirilerek dosyanın yapısının değiştirilmesi tekniğidir. Bu yöntemde dosyaya eklenen veriler programın çalışma mantığını değiştirmez; ancak dosyanın boyutunu, hash değerini ve ikili yapısını değiştirir.

Bu tekniğin temel amacı, özellikle imza tabanlı güvenlik sistemlerini zorlaştırmaktır. Birçok antivirüs veya güvenlik aracı zararlı yazılımları tespit ederken dosyaların hash değerlerinden veya belirli byte dizilerinden faydalanır. Ancak bir dosyanın içerisine rastgele veriler eklenirse, dosyanın hash değeri tamamen değişir ve daha önce oluşturulmuş tespit imzaları etkisiz hale gelebilir.

Binary Padding'in gerçek saldırılarda nasıl kullanıldığına dair örneklerden biri Emotet malware zararlı yazılımıdır. Bazı Emotet örneklerinde saldırganlar, dosya boyutunu yapay olarak büyütmek için 00-byte padding tekniğini kullanmıştır. Bu yöntemde zararlı yazılımın içerisine çok sayıda 00 byte eklenerek dosyanın overlay bölümüne gereksiz veri yerleştirilir. Böylece orijinalde yaklaşık 616 KB olan PE dosyası, padding işlemi sonrası 548 MB gibi oldukça büyük bir boyuta ulaşabilmektedir.


## Sonuç
Siber güvenlikte çoğu kavram gibi obfuscation da tek taraflı bir araç değildir. Aynı teknikler hem sistemleri korumak hem de sistemlere sızmak için kullanılabilir. Yazının başında verdiğimiz örneğe dönersek; bazen bir kargo görevlisi gerçekten kargodur, bazen de sadece öyle görünür.

Veri tarafında obfuscation teknikleri; maskeleme, tokenizasyon ve şifreleme gibi yöntemlerle hassas bilgilerin korunmasını sağlar. Bir saldırgan sisteme erişim sağlasa bile eline geçen verinin doğrudan okunabilir olmaması, veri ihlallerinin etkisini önemli ölçüde azaltabilir.

Ancak işin diğer tarafında saldırganlar da benzer yöntemlerden faydalanır. Zararlı yazılımlar steganografi ile görsellerin içine saklanabilir, JSFuck gibi tekniklerle okunamaz hâle getirilebilir veya binary padding gibi yöntemlerle güvenlik araçlarının - antivirüslerin analizini zorlaştırabilir. Amaç genellikle aynıdır: gerçek niyeti gizlemek ve tespit edilmeden sistem içinde kalabilmek.

Bu yüzden obfuscation’ı yalnızca bir **gizleme tekniği** olarak görmek eksik kalır. Aslında bu kavram, siber güvenliğin hem savunma hem de saldırı tarafında sürekli kullanılan bir stratejidir; önemli olan ise bu teknikleri sadece uygulamak değil, aynı zamanda saldırganların nasıl kullandığını da anlayabilmektir.

