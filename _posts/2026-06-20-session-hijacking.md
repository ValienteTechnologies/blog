---
title: Session Hijacking
date: 2026-06-20 12:30:00 +0300
categories: [Siber Güvenlik Temelleri, Siber Saldırı Metodolojileri]
tags: [Session Hijacking, Siber Güvenlik Metodolojisi, OSINT, Siber Güvenlik Temelleri]
author: rabiacelikli
---

![Image](/assets/img/2026-06-20/sessionhijacking_1.jpg)

## Giriş
Uzun zamandır dört gözle beklediğiniz bir oyun geçen hafta piyasaya sürüldü. Oynamak için can atıyordunuz ancak piyasa fiyatı sizi ve cüzdanınızı hüsrana uğrattı ancak bu, oyunu oynamanıza hala bir engel değil çünkü tarayıcınızda oyunun adını arattığınızda sonuçların en altında oyunun cracklenmiş (korsan) versiyonunu buldunuz.

Korsan yazılımlar, oyunlar veya programlar internetle beraber doğan olağan ve popüler bir kültür olduğundan çok düşünmeden indirip kuruyor ve merakla beklediğiniz oyunu oynamaya başlıyorsunuz. İlk etapta her şey yolunda, hiçbir problem yok gibi görünüyor.

Ancak ertesi sabah telefonunuza hesaplarınız için talep etmediğiniz garip doğrulama kodları gelmeye başlıyor. Sadece on dakika içerisinde e-postalarınız, sosyal medya hesaplarınız, iş hesaplarınız, hatta yıllar önce kaydolduğunuz ve varlığını unuttuğunuz uygulamalara bile birileri tarafından giriş yapılıyor. Şifreleriniz hızla değiştiriliyor ve tüm dijital kimliğiniz elinizden alınıyor.

Koca bir kabus gibi, öyle değil mi? En kötüsü de ne biliyor musunuz? Saldırganlar bu hesapların hiçbirinin şifresini tahmin etmedi veya kırmadı.

İşte bugün, geleneksel brute-force (kaba kuvvet) saldırılarının çoğunlukla yerini alan ve dijital dünyadaki en sinsi tehditlerden biri olan Session Hijacking (Oturum Çalma) konusunu ve arka planda dönen bu mekanizmayı inceleyeceğiz.

## Oturum (Session) 
Oturum, kullanıcı ve web sunucusu arasında kurulan geçici, bilgi alışverişi sağlayan bağlantıdır. Kullanıcı bir hizmete eriştiğinde veya giriş yaptığında başlar; çıkış yaptığında ya da bağlantı zaman aşımına uğradığında sona erer. 

Bir oturum başladığında sunucu, kullanıcıyı tanımak için benzersiz bir kimlik olan Session ID (Oturum Kimliği) tanımlar. Sunucu bunu tarayıcınızda bir çerez (cookie) olarak saklar veya URL'ye ekler. Böylece kullanıcı, her giriş yaptığında kullanıcı adı ve şifresini girmek zorunda kalmaz, bu benzersiz kimlik sayesinde zamandan tasarruf edilir ve kullanıcı deneyimi gelişir.

Ancak bu kolaylık birçok tehdit aktörünü de beraberinde getirir. Çalınan oturum sayesinde gerçek kullanıcı adı, şifre veya iki faktörlü koruma adımı olmaksızın izinsiz erişim sağlanabilir.

## Oturum Çalma (Session Hijacking)
Bir oturumun hem sunucu tarafında hem de kullanıcı tarafında işleri kolaylaştırdığı mutlaka doğrudur ancak tekrardan bunun saldırganlar için paha biçilemez bir açık kapı olduğunu hatırlatmak gerekir. 

Her şey kullanıcının oturum açması ile başlar. Daha sonra saldırganlar farklı vektörleri kullanarak çaldıkları oturumla beraber sunucuya gerçek kullanıcıymış gibi istekte bulunarak oturum açmaya çalışır. Sunucu, gelen Session ID doğru olduğu için saldırgandan şifre veya 2FA kodu istemeden kapıyı açar.

Bundan sonra saldırganlar genellikle şifreleri ve kullanıcı bilgilerini kendi istekleri doğrultusunda değiştirerek asıl, legal oturum sahibinin erişimini kaldırırlar.

Böylece hiçbir şifre, kullanıcı adı ve güvenlik doğrulaması olmadan içeri sızmış olurlar.

### Brute Force ve Session Hijacking
Brute Force (Kaba kuvvet) saldırısı, kısaca deneme yanılmanın üzerine kurulmuştur. Saldırgan, doğru kombinasyonu bulana kadar kullanıcı bilgileri ve şifreyi dener. Oldukça eski bir saldırı türü olmasına rağmen hala kullanılır ve test edilir.

Bu saldırının bel kemiğini **"wordlistler"** (kelime listeleri) oluşturur. Wordlist, potansiyel şifrelerin toplandığı bir havuzdur. Bu listeler, hedefli bir saldırı için **OSINT** (Açık Kaynak İstihbaratı) ile toplanan bilgiler ışığında özel olarak hazırlanabilir ya da "qwerty", "şifre123", "p4ssw0rd" gibi dünya genelinde en çok kullanılan basit şifrelerden oluşabilir. Saldırgan bu listeleri otomatik yazılımlara yükleyerek başarıya ulaşana kadar teker teker dener.

Saldırganlar sadece sıfırdan şifre tahmin etmekle de uğraşmaz; **Credential Stuffing** (Kimlik Bilgisi Doldurma) denen tekniği de kullanabilirler. Cybernews'ün Haziran 2026 verilerine göre milyarlarca sızdırılmış şifre internette çoktan dolaşımda. Saldırganlar bu hazır kullanıcı verilerini farklı sitelerde otomatik olarak deneyerek açık ararlar.

Brute force basit ve etkili olsa da modern sistemler güvenlik alt yapılarını bunu engelleyecek şekilde inşa ederek güncellemektedir. Çoğu uygulama ve banka 2FA önerir, bu da şifre bilinse bile ekstra bir güvenlik önlemi olarak bir doğrulama yapılmadan kullanıcıyı içeri almaz. Öte yandan birden fazla hatalı girişi tespit eden platformlar hesabı kitleyerek IP adresini engeller. Bu da kaba kuvvet saldırılarına bir ket vurur.

İşte tam olarak bu güvenlik önlemleri yüzünden brute force saldırıları popülerliğini yavaş yavaş session hijacking'e bırakıyor. Saldırganlar her zaman en az eforla en hızlı sonucu almak isterler. Brute force artık çok daha zahmetli ve engellenebilir bir yöntemken; session hijacking, halihazırda doğrulanmış (2FA'yı çoktan geçmiş) bir oturumu kopyaladığı için saldırganların tercihi bu yönde oluyor.

## Session Hijacking Yöntemleri
Amaç oturumu çalmak olsa da tek bir yöntem yoktur burada. Hedefe ve koşullara göre bu taktikler değişkenlik gösterir. Bir kaçını kısaca inceleyelim.

- **Cross-Site Scripting (XSS):** Saldırganlar, web uygulamalarındaki güvenlik zafiyetlerinden yararlanarak kullanıcıların ziyaret ettiği sayfalara kötü amaçlı komut dosyaları (scripts) yerleştirirler. Bu kodlar, doğrudan kurbanın tarayıcısı üzerinde çalışarak oturum kimliklerini ele geçirmek için kullanılır.

XSS saldırılarının en tehlikeli yönü, tarayıcıların temel güvenlik mekanizması olan "Aynı Kaynak Politikası"nı (Same-Origin Policy) aşabilmesidir. Bu sayede saldırganlar, doğrudan web sunucusunu hacklemekle uğraşmadan, tamamen sessiz bir şekilde kullanıcı oturumlarını ele geçirebilir ve hassas verilere erişim sağlayabilirler.

- **Session Side Hijacking:** Bu yöntem, saldırganların "packet sniffing" (paket koklama/izleme) yöntemini kullanarak iki taraf arasındaki ağ trafiğini gizlice dinlemesi ve oturum çerezini (cookie) çalması üzerine kuruludur.

Birçok web sitesi, şifrenizi korumak için sadece giriş (login) sayfalarında güvenli TLS/HTTPS şifrelemesi kullanır. Ancak giriş yaptıktan sonra, sitenin geri kalanında bu şifrelemeyi kapatırlar. İşte tehlike tam olarak burada başlar: Ağ trafiğini okuyabilen bir saldırgan, sunucuya gönderdiğiniz veya sunucudan aldığınız tüm verileri kabak gibi görebilir. Bu verilerin içinde oturum çerezleriniz de yer aldığı için, saldırgan şifrenizi hiç bilmese bile saniyeler içinde sizin kimliğinize bürünebilir.

Şifresiz ve halka açık Wi-Fi ağları (hotspots) bu saldırı için biçilmiş kaftandır. Aynı kafede veya havalimanında ortak ağı paylaştığınız herhangi biri, özel bir çaba sarf etmeden diğer cihazlar ile internet modem arasındaki tüm trafiği rahatça okuyabilir ve oturumunuzu tek tıkla çalabilir.

- **Man-in-The-Browser:** Hatırlarsanız yazının başında, o çok beklediğiniz oyunu oynamak için internetten indirdiğiniz korsan yazılımdan bahsetmiştik. İşte o masum görünen dosyanın içinde saklanan bir Trojan (Truva Atı), bilgisayarınıza sızdığı an tam olarak bu saldırıyı başlatır: Man-in-the-Browser (MitB).

Geleneksel aradaki adam (Man-in-the-Middle) saldırılarına benzer ancak çok daha sinsidir. Zararlı yazılım bilgisayarınıza bir kez kurulduktan sonra sessizce pusuda bekler ve sizin bankacılık, e-ticaret veya sosyal medya sitelerine girmenizi gözler. Siz hedef siteyi açtığınız an, tarayıcınız ile web sitesi arasına sızar.

Bu saldırıyı kabusa çeviren şey ise şudur:

Siz banka hesabınızdan bir arkadaşınıza 100 TL göndermeye çalışırken, tarayıcınızın içindeki bu zararlı yazılım arka planda işlem detaylarını gizlice değiştirerek saldırganın hesabına 10.000 TL transfer edebilir. Üstelik siz ekranda hala sadece "100 TL gönderiliyor" ibaresini görürsünüz.

Peki sistem bunu nasıl fark edemez? Çünkü yapılan tüm sahte istekler doğrudan sizin kendi bilgisayarınızdan, kendi tarayıcınızdan ve halihazırda açtığınız yasal oturumun içinden çıkmaktadır. Web sunucusu gelen isteğin sahibini siz sandığı için hiçbir şeyden şüphelenmez ve radarın tamamen altında kalan bu dolandırıcılığı tespit etmek neredeyse imkansız hale gelir.

- **Tahmin Edilebilir Oturum Kimlikleri:** Bu yöntem, web sunucularının Session ID üretirken kullandığı zayıf ve hatalı algoritmaları istismar eder. Güvenlik altyapısı zayıf olan sistemler; zaman damgaları veya ardışık numaralar gibi tahmin edilebilir kalıplarla oturum kimliği oluşturur.

Saldırganlar bu örüntüyü çözdükten sonra, sistemin üreteceği geçerli Session ID'leri önceden hesaplar. Böylece kurbanın cihazına müdahale etmeye veya ağ trafiğini dinlemeye gerek kalmadan, sadece doğru kod kombinasyonunu kullanarak aktif kullanıcı oturumlarını ele geçirirler.

- **Oturum Sabitleme (Session Fixation):** Saldırganların şifre çalmak veya kod tahmin etmek yerine, kurbana kendi belirledikleri bir oturum kimliğini (Session ID) kullandırdığı yöntemdir.

Süreç oldukça nettir: Saldırgan önce hedef web sitesinden geçerli bir Session ID elde eder. Ardından bu ID'yi içeren tuzak bir linki (örneğin sosyal mühendislik veya e-posta yoluyla) kullanıcıya gönderir. Kullanıcı bu linke tıklayıp kendi bilgileriyle sisteme giriş yaptığında, saldırganın önceden belirlediği oturum kimliğini aktif etmiş olur.

Kullanıcı giriş yaptığı an oturum zaten saldırganın elinde olduğundan, hiçbir şifre kırmaya veya çerez çalmaya gerek kalmadan hesaba doğrudan erişim sağlanır.

## Sonuç ve Öneriler
Session Hijacking (Oturum Çalma), iki faktörlü doğrulamayı (2FA) bile bypass edebildiği için günümüz siber dünyasının en kritik tehditlerinden biridir. Şifrelerinizin karmaşık olması bu saldırıları engellemek için tek başına yeterli değildir. Hem kullanıcı hem de sistem tarafında sıkı tedbirler alınması gerekir.

### Kullanıcılar İçin Güvenlik Önlemleri
- **Korsan Yazılımlardan Uzak Durun:** Cihazınıza sızacak bir Trojan (Truva Atı), tüm yerel tarayıcı çerezlerinizi saniyeler içinde saldırgana aktarabilir.

- **Halka Açık Wi-Fi Ağlarında VPN Kullanın:**  Şifresiz ağlarda paket koklama (sniffing) yöntemlerine karşı trafiğinizi mutlaka şifreleyin.

- **Şüpheli Linklere Tıklamayın:** E-posta veya mesaj yoluyla gelen, içinde oturum kimliği (Session ID) barındıran tuzak linklerden uzak durun.

- **Düzenli Olarak Çıkış Yapın:** Bankacılık veya hassas iş hesaplarınızı kullandıktan sonra tarayıcıyı kapatmak yerine mutlaka "Güvenli Çıkış" butonunu kullanın. Bu işlem sunucudaki Session ID'yi geçersiz kılar.

### Web Geliştiricileri ve Sistemler İçin Önlemler:
- **Giriş Sonrası ID Yenileme:** Kullanıcı başarılı bir şekilde giriş (login) yaptığı an, mevcut Session ID'yi iptal edip tamamen yeni ve güçlü bir ID tanımlayın (Session Fixation koruması).

- **Güçlü Rastgelelik (CSPRNG):** Oturum kimliklerini ardışık sayılar veya zaman damgaları yerine, tahmin edilmesi imkansız kriptografik rastgele sayı üreteçleri ile oluşturun.

- **Güvenli Çerez (Cookie) Bayrakları:** Oturum çerezlerinde HttpOnly (XSS'e karşı tarayıcı betik erişimini engeller), Secure (Sadece HTTPS üzerinden iletim sağlar) ve SameSite=Strict bayraklarını mutlaka aktif edin.

- **Uçtan Uca Şifreleme:** TLS/HTTPS protokolünü sadece giriş sayfasında değil, web sitesinin tamamında zorunlu kılın.

Dijital dünyada kolaylık ve güvenlik her zaman ters orantılıdır. Tarayıcınızın sizi hatırlaması ne kadar konforluysa, o oturum kimliğinin çalınması da o kadar tehlikelidir. Sorumlu bir internet kullanıcısı olarak tedbiri elden bırakmamak, siber kabusların önüne geçmenin en etkili yoludur.

