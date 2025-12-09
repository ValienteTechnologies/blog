---
title: Cyber Kill Chain 
date: 2025-12-09 20:30:00 +0300
categories: [Hizmetlerimiz, Sızma Testi]
tags: [Hizmetlerimiz, Siber Güvenlik Temelleri]
author: rabia
---

![Image](/assets/img/2025-12-01/cyber_kill_chain_1.png)

## Giriş
Hiçbir başarı alelade gelişmez, arkada planlı birçok adım vardır. Her alanda olduğu gibi siber güvenliğin ofansif ve defansif cevaplarının arkasında adım adım planlanan ve hayata geçirilen metodolojiler vardır.

## Cyber Kill Chain
**Siber Ölüm Zinciri**, İngilizce adıyla Cyber Kill Chain, temeli ABD'nin askeri ölüm zincirine  *(The US Military Kill Chain)* dayanan; atakları anlamak ve bu ataklara cevap verebilmek için stratejiler üretmeye yarayan 7 aşamalı bir siber güvenlik metodolojisidir.

ABD askeri ölüm zinciri belirli aşamalardan oluşur. Bunlar ise; tespit et, teslim et, karar ver ve öldür olarak 4 parçaya ayrılır. Buradaki amaç ABD'nin savaş kuvvetlerinin saldırıları etkili bir şekilde hedefe doğrultmasıdır. 
Bu savunma konseptinin siber dünyaya yansıtılması ise **Lockheed Martin** adıyla tanınan bir teknoloji şirketinde çalışan **Eric Hutchins**, **Michael Cloppert** ve **Rohan Amin** adlı üç analist sayesindedir. Bu üç analist, "Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains" başlıklı bir dönüm noktası makalesi yayınladı ve bugün sektörde oldukça benimsenen bu metodolojinin temelleri atılmış oldu.

## İşleyiş Şekli
Giriş kısmında bahsettiğimiz gibi, hiçbir atak ve atağa verilen cevap alelade değildir, planlı onca basamaktan geçer. Siber ölüm zinciri de aynı şekilde akıllıca planlanması gerek 7 basamaktan oluşur. Şimdi bu 7 basamağa bir göz atalım.

![Image](/assets/img/2025-12-01/cyber-kill-chain_2.png)

## Keşif (Reconnaissance)
Yedi aşamalı metodolojinin ilk aşaması olmakla beraber hedef hakkında açık ve bilgi toplanmasının yapıldığı kısımdır. Hedef olarak görülen bir insan ya da kuruluşun hakkında bir zafiyet analizi yapmak için önemli miktarda araştırma yapılıp zaman ayırılması gerekmektedir. 

Hedefin varlığına göre keşfin alanında değişiklikler gerçekleşir. Eğer bir insan hedef ise; telefon numarası, e-postalar, sosyal medya hesapları veya kişisel hobiler gibi istihbaratlar daha elzemdir. Öte yandan, hedef bir organizasyon ise; iş saatleri, satış verileri, şirketin yıllardır ürettiği örüntüler veya organizasyonun politikaları daha ilgi çekicidir.

Yukarıda bahsettiklerim işin daha çok sosyal kısmı iken teknik kısmı da keşfin önemli bir parçasıdır. IP ya da MAC adresleri, alan adları, alt alan adları vb. gibi bilgileri Linux'un tarama araçları ile elde ederiz.

Bu yüzden keşif kısmı da kendi içinde ikiye ayrılmaktadır;

### Pasif Keşif 
Pasif keşif, hedefle doğrudan herhangi bir **etkileşime girmeden toplanan istihbaratı ifade eder. Bu aşamada hedef, bilgi toplandığının farkına varamaz; çünkü erişilen veriler genellikle halihazırda kamuya açık kaynaklarda bulunur. Pasif keşifte odak noktası, hedef sistem veya organizasyon üzerinde kimin hangi erişimlere sahip olduğudur.

Pasif keşfin en yaygın yöntemlerinden biri **OSINT** *(Open Source Intelligence)* yani Açık Kaynak İstihbaratıdır. OSINT, hedefle herhangi bir bağlantı kurmadan; internette, kamuya açık veri tabanlarında, sosyal medya platformlarında, basılı yayınlarda ve sızdırılmış veri setlerinde bulunan herkesin erişebileceği bilgilerin sistematik şekilde toplanması ve analiz edilmesidir. **Bu yöntemle:**

Domain ve DNS kayıtları,
Çalışanların sosyal medya davranışları,
LinkedIn’deki organizasyon yapısı,
Şirketle ilgili haberler, dokümanlar ve basın bültenleri,
Veri sızıntılarında görünen e-postalar ve parolalar 
gibi kritik bilgiler elde edilerek saldırı zincirinin sonraki aşamalarında kullanılacak kapsamlı bir profil oluşturulur.

### Aktif Keşif
Aktif keşifte, pasif keşfin aksine daha fazla bilgi toplamak amacıyla hedef sistemle **doğrudan etkileşim** kurulur. Bu aşamada genellikle **tarama (scanning)** teknikleri kullanılır. Yapılan taramalar sonucunda; açık portlar, çalışan servisler, kullanılan işletim sistemleri ve sürümleri, ağ topolojisi hakkında ipuçları ve güvenlik duvarının paketlere nasıl davrandığı gibi daha detaylı bilgiler elde edilir. Bu sayede potansiyel zaafiyetler hakkında çıkarımlar yapılabilir. Ancak aktif keşif, hedef sistemde log kaydı oluşturduğu veya IDS/IPS alarmlarını tetiklediği için, hedefin bu etkileşimin farkına varma olasılığı **yüksektir.**

## Silahlanma (Weaponization)
Bu kısımda hala bir saldırı söz konusu **değildir**, elde edilen istihbaratlar ışığında nasıl bir teknik, nasıl bir saldırı adımları izlenmesi gerektiği bu adımda belirlenir ve buna uygun araç geliştirilir. Bulunan zafiyetleri en iyi şekilde nasıl sömürebileğine göre silah değişebilir. Bu, zafiyetin istismarında kullanılabicek payloadtan tutun, masum görünümlü bir excel dosyasının içine gömülmüş bir makroya veya psikolojik manipülasyon sağlayabilecek iyi kurgulanmış bir oltalama mailine kadar uzanabilir. 

## Teslimat (Delivery)
Silahlanma adımında geliştirilen uygun araç bu adımda hedefe teslim edilir. Teslimat kısmı büyük ölçüde keşif kısmında toplanan istihbarata bağlıdır. Saldırının başarıya ulaşması için teslimat kısmı kritik önem taşır çünkü hedef sistem gelitirilen payload ile etkileşime girmelidir. Bu etkileşim birçok şekilde oluşturulabilir. Örneğin; iyi tasarlanmış bir phishing maili, hedefi ikna ederek e-postanın içine eklenmiş masum görünümlü ekleri indirtebilir veya belirli bir linke tıklaması halinde indirilecek kötü amaçlı yazılıma yönlendirilebilir ancak saldırganlar başarı oranını arttırabilmek için **birden fazla** teslim yöntemi kullanır.

## Sömürü (Exploitation)
Hazırlanan ve geliştirilen kötü amaçlı yazılım hedef sisteme başarıyla ulaştıktan sonra sömürü adımı başlar. Buradaki gaye, kötü amaçlı yazılımın sisteme kurulabilmesi için gerekli koşulları hazırlamaktır. Yani saldırgan, sisteme sızmak için uygun ortamı oluşturur. Sömürü adımı doğrudan zararlı yazılımı kurmaz ancak bunun için bir zemin hazırlar. Bu zemini kurabilmek için başlıca üç gereksinim vardır.

### Yetki 
Hazırlanan kötü amaçlı yazılımın yeterince yetkisi yoksa hedef sisteme kurulamaz. Bir programın sisteme kurulması için bazen yüksek izinler gerekir. *(Örneğin; yönetici/administrator yetkisi).*

### Uyumluluk
Buradaki kilit soru, **“Bu anahtar bu kapıya uygun mu?”**. Bir kötü amaçlı yazılım, hangi sistem için tasarlandıysa **sadece** o sistemde çalışır. Linux için yazılmış bir malware windowsta, 64-bit'lik program 32-bit'lik sistemde, IPhone için yazılmış kod Android'te **çalışmaz**. 

### Fark Edilmemezlik
Eğer saldırganın hazırladığı kötü amaçlı yazılım antivirüsler veya güvenlik duvarı tarafından fark edilirse kurulum başlamadan biter ve saldırı başarısızlıkla sonuçlanır. Bu yüzden saldırganlar malware’i gizlemek için şifreleme, paketleme, obfuscation *(kodu anlaşılmaz hâle getirme)* gibi teknikler kullanır.

## Kurulum (Installation)
Hedef sistem tam da bu esnada **enfekte** olur. Teslimat kısmında zararlı yazılım hedef sisteme ulaştı, sömürü aşamasında ise gerekli zemin hazırlandı. Artık kurulumun gerçekleşmesini engelleyecek bir durum kalmamıştır. Kurulum kısmında zararlı yazılım, işletim sisteminin kütüphanelerini kullanır veya ihtiyaç duyduğu dosyaları **dropper/downloader** üzerinden indirir. Ardından dosya izinlerini değiştirir, görünümünü gizler veya formatını değiştirerek tespiti zorlaştırır. Gelişmiş tehditler bellek yapılarını değiştirerek sandbox ve davranış tabanlı antivirüsten kaçabilir.

## Komuta ve Kontrol (Command and Control, C2)
Command and Control (C2) aşamasında saldırgan, hedefe bulaşan zararlı yazılımla iletişim kurar. Bu iletişim genellikle sunucular, P2P ağlar veya sosyal medya gibi kanallar üzerinden sağlanır. Amaç, zararlıyı uzaktan yönetmek ve ihtiyaç duyulan komutları verebilmektir. C2’nin en yaygın amaçlarından biri, hedef sistemden şifre, finansal bilgi veya önemli dosyalar gibi verileri çalmaktır. Bunun yanında saldırgan, zararlı yazılımın yayılması, çalıştırılması veya fidye yazılımlarında dosyaların şifrelenmesi gibi işlemleri başlatmak için de komut gönderebilir.

Bu aşama, savunma ekipleri için saldırıyı engellemek adına son fırsattır. Çünkü C2 trafiği genellikle normal internet trafiğine benzer şekilde görünür. Bu nedenle hem uç nokta güvenliği hem de ağ izleme sistemleri, zararlı bir iletişim olup olmadığını tespit etmekte kritik rol oynar.

## Hedef Odaklı Eylemler (Actions on Objectives)
Cyber Kill Chain'in son halkasıdır ve saldırganın nihai amaçlarının uygulanmaya konulduğu noktadır. Zararlı yazılım hedef sisteme yerleşmişse, artık planlanan görevleri yerine getirmeye başlar. Bunu ya C2 sunucusundan gelen komutlarla ya da kendi kodunda tanımlı otomatik işlevlerle gerçekleştirir. Artık bu kısımda saldırganın malesef başarılı olduğundan bahsedebiliriz.

Hedef sisteme saldırganın motivasyonuna göre zarar verilir. Bu; veri sızıntısı, fidye yazılımı saldırıları (Ransomware) veya sistemi çalıştırılamaz hale getirilmesi gibi kötü senaryolar olabilir.

---


Bu yazıda *"Computer and Network Security Essentials - Kevin Daimi"* kaynağından yararlanılmıştır.








