---
title: Fabrikalar Neden Ransomware'in En Kolay Hedefi?
date: 2026-04-06 15:00:00 +0300
categories: [Siber Güvenlik Temelleri]
tags: [Malware, Fabrikalar, Siber Güvenlik Temelleri, Ransomware]
author: rabiacelikli
---

![Image](/assets/img/2026-04-06/ransomware_1.jpg)

## Giriş
Yine her sabah olduğu gibi saat 08.30’da fabrikanıza geliyorsunuz. Ancak mesainin başlamasının üzerinden dakikalar geçmesine rağmen hiçbir cihaz veya sistem çalışmıyor. İlk akla gelen, bunun basit bir elektrik ya da donanım arızası olduğu ve teknik ekibin kısa sürede müdahale ederek süreci normale döndüreceğidir.

Ancak IT ekibi sistemleri kontrol etmeye başladığında durumun çok daha farklı olduğu ortaya çıkar. Hiçbir dosyaya erişilemiyordur. Ekranlarda tek bir mesaj vardır:
**"Bilgileriniz şifrelendi."**

Mesaj bununla da sınırlı değildir. Altında, belirli bir süre içerisinde ödenmesi gereken yüksek tutarlı bir fidye ve ödeme talimatları yer almaktadır. Aksi takdirde fabrikanın kalbi olan sistemlere erişimin kalıcı olarak kaybedileceği belirtilir. Bu noktadan sonra geçen her dakika, sadece teknik bir problem değil; doğrudan üretim kaybı, operasyonel aksama ve itibar zedelenmesi anlamına gelir.

İlk bakışta bu senaryo bir korku hikayesi gibi gelebilir. Ancak üretim (manufacturing) sektöründe bu tür saldırılar sanıldığından çok daha yaygın ve her yıl ciddi finansal kayıplara yol açmaktadır. Bu yazımızda ransomware saldırılarının nasıl çalıştığını, fabrikaların neden öncelikli hedef haline geldiğini ve bu saldırıların işletmeler üzerindeki gerçek maliyetlerini ele alacağız.

## Ransomware Anatomisi
Ransomware, Türkçeye çevirmek istersek fidye yazılımı, saldırganların; kurbanların sistemlerine, dosyalarına veya ağlarına olan erişimi verileri şifreleyerek engellemesidir. Tekrar erişime ulaşmak için ise fidye adı altında ödeme talep ederler. Fidye ödenmediğinde verilere kalıcı olarak erişim kaybedilir hatta veri sızıntısı yaşanabilir. Kurban, istenilen fidyeyi ödediği takdirde saldırganlar, şifrelenmiş verileri çözmek için bir decryption key gönderir ancak ödeme yapıldıktan sonra kurbanın sisteme erişebileceğinin kesin bir garantisi yoktur. CyberEdge Group tarafından 2017'de yapılmış ankete göre katılımcı şirketlerin yalnızca %19.1'i fidye ödeyip verilerini kurtarabilmiştir. Diğer yüzdelik sonuçlar ise şu şekildedir:

![Image](/assets/img/2026-04-06/ransomware_2.png)


Bazen saldırganlar bıraktıkları notlar sayesinde kurbanların onlarla iletişime geçmesini sağlayarak pazarlık yaparlar. Ransomware hakkında örnekler görmek için [ransomware.live'ı](https://www.ransomware.live/) ziyaret edebilirsiniz. Burada "Negotiations" ve "Ransom Notes" kısımlarında saldırganların bıraktığı örnek fidye notlarını ve pazarlıkları görebilirsiniz. 

### Sistemler Nasıl Enfekte Oluyor?
Birkaç farklı yol ile sistemler enfekte edilse de sorunun çekirdeğinde yine insanın en zayıf halka olması yatıyor. Ransomware, ağırlıklı olarak phishing e-postaları ile sistemlere bulaşmaktadır. Dikkat edilmeden indirilen bir dosya eki tüm sisteminizi kilitleyecek bir ransomware saldırısının başlangıcı olabilir.

Bir diğer yaygın bulaş yolu ise Malvertising (zararlı reklamcılık) ve exploit kit'lerdir. Ransomware yaymak için sıklıkla birlikte kullanılır. Saldırganlar, zararlı kod içeren sahte reklamlar veya pop-up’lar oluşturur. Kullanıcı bu reklamlara tıkladığında, farkında olmadan exploit kit’in bulunduğu sayfaya yönlendirilir. Exploit kit burada sistemi sessizce tarayarak güvenlik açıklarını tespit eder. Uygun bir zafiyet bulunursa, ransomware yükü sisteme gönderilerek enfeksiyon başlatılır.

Bu yöntemler otomatik çalıştığı için saldırganlar arasında oldukça yaygındır. Ayrıca zararlı kodun doğrudan belleğe enjekte edilmesi sayesinde geleneksel antivirüs çözümleri tarafından tespit edilmeleri zorlaşır. Düşük teknik bilgiyle dahi kullanılabilmeleri, ransomware saldırılarını daha erişilebilir ve yaygın hale getirmektedir.

Bulaşma şekli ne olursa olsun üç adımlık bir döngü izler; enfeksiyon, şifreleme ve fidye.

Sisteme sızan ransomware, ilk aşamada değerli dosyaları tespit ederek şifrelemeye başlar. Ancak modern ransomware varyantları yalnızca tek bir cihazla sınırlı kalmaz. Ağ içerisinde yeterli erişim elde edildiğinde, saldırganlar diğer sistemlere yayılma fırsatı arar. Bu süreç, siber güvenlikte **"lateral movement"** olarak adlandırılır. Bu aşamada saldırgan, ele geçirilen sistem üzerinden ağ içindeki diğer cihazları keşfeder, yetkilerini genişletir ve mümkün olduğunca fazla sisteme erişim sağlamaya çalışır. Amaç, saldırının etkisini büyütmek ve tek bir cihaz yerine tüm organizasyonu etkileyebilecek bir noktaya ulaşmaktır.

### WannaCry
Ransomware'in gerçek hayattaki en büyük örneklerinden biri de WannaCry'dır. 12 Mayıs 2017'de WannaCry ransomware solucanı, 150'den fazla ülkede 200.000'den fazla bilgisayara yayıldı. Windows'ta SMB protokolünde bulunan **"EternalBlue"** açığı hedef alındı. WannaCry'ın ilk fidye miktarı 300 dolar Bitcoin'di ve belirli bir süre içinde ödenmezse 600 dolara yükseliyordu. Dosyalara ve verilere erişimi engelleyerek, WannaCry saldırıdan etkilenen işletmelerdeki BT sistemlerini kolayca devre dışı bırakabiliyordu.

**WannaCry**, bir solucan gibi yayılan, yani bir ana bilgisayar dosyasına veya insan müdahalesine ihtiyaç duymadan hızla yayılabilen bir tür kötü amaçlı yazılım olmasıyla fidye yazılımları arasında benzersizdir. Enfekte olmuş bir bilgisayarda, kötü amaçlı yazılımı dağıtan ve kuran bağımsız bir program olan "dropper" olarak ortaya çıktı. WannaCry dropper'ının içindeki dosyalar arasında veri şifreleme ve şifre çözme uygulaması, şifreleme anahtarları içeren dosyalar ve fidye yazılımı operatörlerinin komuta ve kontrol (C2) iletişimi için kullandığı Tor'un bir kopyası yer alıyordu. Kötü amaçlı yazılım bir cihazda yerleştikten sonra, yayıldı ve enfekte bilgisayarla iletişim kuran diğer yamalanmamış cihazları etkiledi.

Halbuki Microsoft saldırıdan neredeyse 2 ay önce, 14 Mart'ta, EternalBlue için bir yama yayınlamıştı ancak saldırı sırasında birçok cihaz için gerekli güncellemeler uygulanmamıştı. 

## Üretim Sektörü ve Ransomware
Üretim sektörü ve fabrikalar, ransomware saldırganları için adeta bir hazine niteliğindedir. Bunun en temel nedeni, üretim hattındaki duraksamanın tolere edilemez olmasıdır. Kaybedilen her dakika; üretimin durması, siparişlerin aksaması ve müşteri memnuniyetinin hızla düşmesi anlamına gelir. Kısa ya da uzun süreli olması fark etmeksizin, her kesinti doğrudan finansal kayba dönüşür. Üstelik bu kayıplara yalnızca üretim duruşu değil; itibar kaybı, müşteri güveninin zedelenmesi ve operasyonel kaos da eklenir. Bu nedenle birçok şirket için karar noktası teknik değil, tamamen iş sürekliliği odaklıdır: Sistemleri sıfırdan inşa etmek mi, yoksa üretimi hızla ayağa kaldırmak için fidyeyi ödemek mi?

The State of Ransomware in Manufacturing and Production 2025 verileri, bu baskının ne kadar gerçek olduğunu açıkça ortaya koyuyor. 17 ülkeden 332 üretim şirketinin katılımıyla hazırlanan rapora göre, bir ransomware saldırısından sonra sistemleri tekrar ayağa kaldırmanın ortalama maliyeti **1.3 milyon dolar** seviyesindedir. Bununla da kalmayıp mağdur kuruluşların %51'i fidyeyi ödemiştir. **(Sophos)**

Bu rakamı somutlaştırmak gerekirse: Yalnızca kurtarma süreci için harcanan bu bütçe, 2000’den fazla asgari ücretlinin bir aylık maaşına denk gelmektedir. Başka bir deyişle, tek bir siber saldırının maliyeti, orta ölçekli bir fabrikanın tüm çalışanlarının aylık maaş yükünü karşılayabilecek seviyededir.

Kurtarma süreci ise oldukça sancılıdır, yedekleme ve disaster recovery'e (felaket kurtarma planlaması) yatırım yapmış olan kuruluşlar bile stratejilerinin gerçek bir saldırı karşısında işe yaramadığını sıklıkla fark ederler. İlk akla gelen çözüm yedeklere dönmek olacaktır ancak şu gerçeği unutmamak gerekir: Üretim hatlarındaki ağ devasadır ve birçok cihaz senkron çalışacak şekilde birbirine bağlıdır. Yedekler alınırken saldırganların zaten sistem içinde olup olmadığını kestirmek kolay değildir. Daha da kötüsü, birçok yedekleme ortamı, üretim ortamıyla aynı kimlik sistemlerini ve ağ kontrollerini paylaşıyor. Bir saldırgan Active Directory'yi ele geçirirse, genellikle yedekleme altyapısına da erişim sağlar.

Kısacası yedeklerinizin güvenliğinden de tam olarak emin olamayabilirsiniz. Bu nedenle saldırı gerçekleşmeden önce zafiyetlerin tespit edilmesi, saldırı sonrası müdahaleden çok daha kritik hale gelmektedir.

### BT - OT Güvenliği ve Ransomware
Üretim şirketlerinin karşı karşıya olduğu en büyük güvenlik problemlerinden biri, iki farklı dünyanın kesişmesidir: BT (Bilgi Teknolojileri) ve OT (Operasyonel Teknolojiler).

BT sistemleri; e-posta, kullanıcı hesapları ve veri akışı gibi bağlantı odaklı çalışacak şekilde tasarlanmıştır. Bu nedenle düzenli güncellemeler, yamalar ve erişim kontrolleri bu sistemlerin doğal bir parçasıdır. Ancak OT sistemleri bambaşka bir öncelikle geliştirilmiştir: süreklilik. Üretim hatlarının durmaması için tasarlanan bu sistemler, çoğu zaman yıllarca güncellenmeden çalışmaya devam eder.

Tam da bu noktada kritik bir güvenlik boşluğu ortaya çıkar.

BT sistemleri sürekli **değişirken**, OT sistemleri **statik** kalır. Bu da saldırganlar için öngörülebilir ve zayıf hedefler yaratır. Üstelik modern üretim ortamlarında bu iki dünya artık tamamen ayrık değildir. Operasyonel verimlilik için birbirine bağlanan bu sistemler, aslında saldırganlar için bir köprü görevi görür.

Birçok ransomware saldırısı BT ortamında başlasa da, asıl etki saldırganın ağ içinde ilerleyerek OT sistemlerine ulaşmasıyla ortaya çıkar. Bu noktada saldırı, veri kaybından çıkıp doğrudan üretim kesintisine dönüşür.

Gerçek dünyada bu durumun ne kadar yaygın olduğuna dair çarpıcı bir örnek vermek gerekirse: Bir üretim firmasında yapılan güvenlik değerlendirmesinde, PLC cihazlarının kurumsal ağ üzerinden varsayılan şifrelerle erişilebilir olduğu tespit edilmiştir. Üstelik bu yapı yıllardır değiştirilmeden kullanılmaktadır.

Bu tarz zafiyetler düşündüğümüzden çok daha yaygındır. OT ortamlarında sık karşılaşılan güvenlik problemleri şunlardır:

- Şifrelenmemiş cihazlar arası iletişim
- Birden fazla sistemde kullanılan ortak hesaplar
- BT ağı ile üretim ağı arasında doğrudan bağlantılar
- Yetersiz ağ izleme ve loglama
- Güncel olmayan veya hiç tutulmayan varlık envanteri

Sorunun çözümü ise sistemleri tamamen izole etmek değildir. Günümüz üretim dünyasında veri entegrasyonu bir zorunluluktur. Ancak bu entegrasyon, güvenlik göz ardı edilerek değil; doğru ağ segmentasyonu, sürekli izleme ve OT ortamlarına özel güvenlik kontrolleri ile sağlanmalıdır.

Aksi takdirde, basit bir BT ihlali tüm üretim hattını durdurabilecek bir krize dönüşebilir. Bu nedenle yalnızca BT sistemlerini kapsayan klasik güvenlik yaklaşımları, üretim ortamları için yeterli değildir. Saldırıların gerçek etkisi OT tarafında ortaya çıktığı için, BT ve OT ortamlarını birlikte ele alan kapsamlı sızma testleri kritik hale gelmiştir.

## Sonuç ve Öneriler
Ransomware saldırıları artık yalnızca veri kaybı riski taşıyan teknik olaylar değil, doğrudan iş sürekliliğini hedef alan operasyonel krizlerdir. Özellikle üretim sektöründe, saldırının gerçek etkisi verilerin şifrelenmesinden çok üretimin durmasıyla ortaya çıkar.

Bugün birçok saldırı, bilinmeyen tekniklerden ziyade; yamalanmamış sistemler, zayıf erişim kontrolleri ve yanlış yapılandırılmış ağlar üzerinden gerçekleşmektedir. Bu da kurumların büyük bir kısmının aslında önlenebilir riskler nedeniyle hedef haline geldiğini göstermektedir.

BT ve OT ortamlarını birlikte ele alan kapsamlı sızma testleri, bu sorunun proaktif cevabını sunar. Gerçek saldırgan bakış açısıyla yapılan testler sayesinde, üretim hatlarını durdurabilecek zafiyetler henüz istismar edilmeden tespit edilebilir.

Bu noktada güçlü bir güvenlik yaklaşımının temelinde etkili bir varlık yönetimi (asset management) süreci yer alır. Kurumların sahip olduğu tüm donanım ve yazılım envanterinin eksiksiz şekilde bilinmesi, hangi cihazın nerede konumlandığının, hangi servislerin çalıştığının ve kimlerin hangi yetkilere sahip olduğunun net olarak ortaya konması gerekir. Aksi takdirde, görünmeyen sistemler saldırganlar için kolay hedefler haline gelir.

Etkili bir asset management yaklaşımı sayesinde saldırı yüzeyi küçülür, yamalama süreçleri hızlanır, anomali tespiti kolaylaşır ve olası bir saldırı durumunda müdahale süresi ciddi ölçüde azalır. Güvenliğin ilk adımı, neye sahip olduğunu bilmektir. Çünkü görünmeyen bir varlığı korumak mümkün değildir.

Unutulmamalıdır ki, bir ransomware saldırısının maliyeti yalnızca fidye değildir. Asıl maliyet, kaybedilen üretim süresi, bozulan iş süreçleri ve zedelenen müşteri güvenidir.
















