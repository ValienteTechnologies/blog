---
title: Sızma Testi̇ (Penetrasyon Testi̇) Nedi̇r Ve Nasıl Yapılır?
date: 2025-11-27 12:30:00 +0300
categories: [Hizmetlerimiz]
tags: [Hizmetlerimiz]
author: tamlata
---

Sızma testi, veya yaygın adıyla **Pentest hizmeti**, bilişim sistemlerindeki **sorun**, **hata** ve **zafiyetleri ortaya çıkararak** herhangi bir güvenlik zafiyetini önlemek ve sistemleri daha güvenli hale getirmek amacı ile alanında uzman kişiler tarafından gerçekleştirilen özel bir **siber güvenlik danışmanlık hizmetidir**.

Kurumların siber saldırılara karşı **güvenlik seviyelerini değerlendirmeyi** ve **tespit edilen riskleri yönetmeyi** amaçlayan sızma testleri, zafiyetleri tespit etmenin ötesinde, tespit edilen zafiyetleri kullanarak ilgili sistemde **yetkili erişimlerin** nasıl elde edilebileceğini ve nelerle sonuçlanabileceğini gösterir. Ayrıca sistemin **güçlü yönlerini** de göstererek tam bir **risk değerlendirmesi** yapılmasını sağlar.

Her bir varlık türüne göre önceden belirlenen senaryolar dahilinde uygulanan sızma testi, gerek ulusal gerekse de uluslararası **metodolojik yaklaşımlar** temel alınarak gerçekleştirilir.

---


## **HİZMET BİLEŞENLERİ VE TEMEL TEST METODOLOJİLERİ**

Sızma testlerinin başarısı, uygulanan **metodolojinin doğruluğuna** bağlıdır. **Black Box (kara kutu), White Box (beyaz kutu) ve Grey Box (gri kutu)** yaklaşımları, sistemlerin farklı açılardan test edilmesini sağlar. **OWASP** ve **NIST** gibi uluslararası standartlara uygun olarak, testlerin kapsamı belirlenir. Bu yaklaşımlar, hem **tehdit modellemesi** yaparak zafiyetleri önceden görmeyi hem de **saldırı simülasyonları** ile savunmanın zayıf noktalarını tespit etmeyi sağlar.

- **Black Box (Kara Kutu) Yaklaşımı:** Test uzmanına hedef sistem hakkında herhangi bir bilgi verilmez. Amaç, dışarıdan saldırgan perspektifiyle hareket ederek, kurumun dış yüzey (internet erişimi olan varlıklar) güvenlik seviyesini ölçmektir. DNS, IP blokları, açık portlar, uygulama endpoint’leri gibi unsurlar gerçek bir saldırgan gibi keşfedilir ve istismar edilmeye çalışılır.
  
- **White Box (Beyaz Kutu) Yaklaşımı:** Test uzmanına tüm iç yapıya dair kapsamlı bilgi verilir (ağ diyagramları, kaynak kod, kullanıcı erişimleri, yapılandırmalar vb.). Bu yaklaşım, iç ağda gerçekleşebilecek saldırıların etkisini ölçmek, servis mantığı ve kod güvenliğini analiz etmek ve en kritik zafiyetleri en hızlı şekilde açığa çıkarmak amacıyla uygulanır.

- **Grey Box (Gri Kutu) Yaklaşımı:** Test uzmanına sınırlı fakat kontrollü erişim veya bilgi verilir. Örneğin kullanıcı hesabı, API token veya belirli erişim seviyeleri sağlanabilir. Amaç, hem dış hem de iç tehdit aktörlerinin gerçekçi şekilde simüle edilmesi, yetki yükseltme (privilege escalation) senaryolarının ve yatay/dikey erişim suiistimallerinin değerlendirilmesidir.

---

### **Bilgi Toplama ve Derinlemesine Zafiyet Analizi**

- **Bilgi Toplama:** Sistem hakkında pasif (Arama motorları , DNS taramaları) ve aktif (Port taramaları , Açık servisler) araştırmalar yapılarak potansiyel saldırı yüzeyi belirlenir.

- **Zafiyet Analizi:** Otomatik tarama araçlarının yanı sıra manuel testlerle derinlemesine analizler gerçekleştirilir. Amaç, tüm güvenlik açıklarını önceden belirleyerek önlem almaktır.

### **Kimlik Doğrulama ve Erişim Yönetimi Testleri**

- **Çok Faktörlü Kimlik Doğrulama (MFA)** ve **oturum yönetimi** gibi kritik mekanizmalar test edilir.

- **Rol Tabanlı Erişim Kontrolü (RBAC)** gibi modellerin doğru şekilde uygulandığı doğrulanır. Erişim kontrollerinde zafiyet olup olmadığı tespit edilerek **yetkisiz erişimlerin** önüne geçilir.

#### **Ağ Güvenliği ve Şifreleme Protokolleri Analizi**

**HTTPS**, **TLS** gibi güvenli iletişim protokollerinin etkinliği doğrulanır.

Bu aşamanın amacı; kurum ağ yapısının **dış tehditlere** ve **iç tehditlere** karşı dayanıklılığını ölçmek, **kritik sistemlerin doğru şekilde ayrıştırıldığını** ve **iletişimin güvenli olarak sağlandığını** teyit etmektir. İnceleme, **ağ mimarisi**, **segmentasyon**, **erişim izinleri**, **şifreleme teknolojileri** ve **güvenlik politikalarının** bütüncül değerlendirilmesini içerir.

Kapsam dahilinde hızlı ve odaklı kontroller yapılır:

- **Ağ segmentasyonu** ve **VLAN izolasyonunun** doğrulanması
- **Güvenlik duvarı (Firewall) kurallarının** uygunluğu ve **gereksiz erişimlerin tespiti**
- **VPN ve uzak erişim yöntemlerinin güvenliği** (MFA, erişim kısıtlamaları vb.)
- **IDS/IPS yapılandırmalarının** etkinlik kontrolleri
- **DNS güvenliği** ve **zone transfer açıklıklarının analizi**
- **Ağ servislerinin** (SMB, RDP, SSH, FTP, LDAP vb.) **port, yetki ve erişim seviyelerinin değerlendirilmesi**
- **Sertifika yönetimi** ve **TLS sürüm kontrolleri** (zayıf/protokol dışı sürümler)
- **Kablosuz ağ güvenliği** ve **rogue erişim noktası analizleri**

Sonuç olarak ağın; **saldırıya açıklık düzeyi**, **kritik varlıklara ulaşılabilirlik**, **yanal ilerleme (lateral movement) potansiyeli** ve **olası ihlallerin etkileri** raporlanır ve gerekli **iyileştirme önerileri** sunulur.


### **Sızma (Exploitation) ve Yetki Yükseltme**

Bu evrede, tespit edilen zafiyetler üzerinden sistemlere sızma girişimleri gerçekleştirilir. **Saldırgan perspektifiyle** yapılan testler, zafiyetlerin gerçek dünyada nasıl kullanılabileceğini gösterir. **Hak yükseltme** adımlarıyla, yetkili erişim elde edilip sistemde daha yetkili seviyelere (Örn, **AD, FW, KVM**) ulaşılması sağlanır.

### **Detaylı Raporlama ve Çözüm Önerileri**

Testlerin sonunda, tespit edilen zafiyetlerin ve risklerin detaylı bir raporu hazırlanır.

Raporlar, her zafiyetin **önem derecesini** belirterek **önceliklendirme** yapar.

Her bir zafiyet için **teknik çözüm önerileri** sunulur ve **iyileştirme yolları** açıklanır.

### **Sürekli Güvenlik ve Uyumluluk Denetimi**

Periyodik sızma testleri ve **otomatik zafiyet taramalarıyla**, yeni ortaya çıkan tehditlere karşı proaktif savunma sağlanır.

**PCI DSS, GDPR, ISO 27001, BDDK** gibi standartlara uyumluluk denetimleri gerçekleştirilerek, **yasal düzenlemelere tam uyum** garanti altına alınır.

---

## **SIK SORULAN SORULAR (SSS)**

**Sızma testi nedir?**  
Sızma testi, bir organizasyonun ağ, uygulama veya sistem güvenliğini değerlendirmek amacıyla gerçekleştirilen **kontrollü siber saldırılardır**. Testler ile, sistemdeki güvenlik zayıflıklarını belirlemek için saldırganların yöntemleri simüle edilir.

**Neden sızma testi yaptırmalıyım?**  
Sızma testleri, organizasyonların **veri güvenliğini** sağlamak için kritik bir araçtır. Potansiyel zafiyetleri tespit ederek bu zayıflıkları kapatmanıza ve olası siber saldırılara karşı **proaktif bir savunma** oluşturmanıza yardımcı olur. Ayrıca, **yasal düzenlemelere uyum** sağlamak ve **müşteri güvenini artırmak** da önemli faydalarındandır.

**Sızma testi ile otomatik zafiyet taraması arasındaki fark nedir?**  
Otomatik zafiyet taramaları, bilinen güvenlik açıklarını tespit eden araçlardır; ancak sızma testleri daha **derinlemesine analiz** sunar. Sızma testleri, **gerçek saldırı senaryolarını simüle ederek** daha kapsamlı bir güvenlik değerlendirmesi yapar.

**Sızma testi ne sıklıkla yapılmalıdır?**  
Sızma testlerinin, genellikle **altı ayda bir** defa yapılması önerilmektedir. Ancak önemli sistem değişiklikleri veya yeni uygulama dağıtımı gibi durumlarda daha sık yapılması tavsiye edilir.

**Sızma testi sırasında sistemlerim etkilenir mi?**  
İyi planlanmış bir sızma testi, sistemler üzerinde **minimum etki** bırakarak gerçekleştirilir. İş operasyonlarını aksatma riski en aza indirilir ve çoğu durumda **operasyonel süreklilik** devam eder. Kullanılabilirliği etkileyebilecek bir sistem test edilirken, bu durum şirkete bildirilir ve ihtiyaçlara göre hareket edilir.

**Sızma testini kimler gerçekleştiriyor?**  
Valiente Technologies sızma testi ulusal ve uluslararası (TSE, OSCP gibi) geçerlilikte
sertifikasyonlara sahip personellerimiz tarafından gerçekleştirilmektedir.
Uzman ekibimiz çeşitli işletim sistemleri, ağlar ve uygulamalar hakkında güçlü bir
anlayışa, güvenlik açıkları ve istismarları hakkında derin bir bilgiye, çeşitli güvenlik test
araçları ve tekniklerinde yetkinliğe sahiptir.

---

## **13 ADIMDA KAPSAMLI SIZMA TESTİ EVRELERİ**

1. **Zafiyet Seviyelendirmesi**  
2. **Bilgi Toplama**  
3. **Pasif Bilgi Toplama**  
4. **Aktif Bilgi Toplama**  
5. **Port Tarama**  
6. **Zafiyet Tarama**  
7. **Enumeration (Sayıklama)**  
8. **Exploitation (İstismar)**  
9. **Hak ve Yetki Yükseltme**  
10. **Post Exploitation (İstismar Sonrası)**  
11. **Yapılan İşlemleri Geri Alma**  
12. **Raporlama**  
13. **Sunum**

---

## **KULLANILAN METODOLOJİLER VE ULUSLARARASI STANDARTLAR**

Sızma testleri, güvenlik zafiyetlerini ortaya çıkarmak için hem dışarıdan (**Internet**) hem de içeriden (**Internal**) sızma testleri uygulanarak, uluslararası **metodolojik yaklaşımlar** temel alınarak gerçekleştirilir.

Testler, hedef sistemin aktif, dinamik ve statik analizini içeren şu güvenlik normlarına, metodolojilerine ve standartlarına dayanır:

**OWASP (Open Web Application Security Project)**  : Yaygın olarak bilinen bu standart, en son siber tehditlere ayak uyduran bir
topluluk tarafından geliştirilir ve güncellenir. Uygulama açıklarının yanı sıra
süreçlerdeki mantık hatalarını da hesaba katar.

**PTES (Penetration Testing Execution Standard)**  : Bilgi güvenliği uzmanlarından oluşan bir ekip tarafından tasarlanan bir pentest
metodolojisidir. PTES'in amacı, sızma testleri için kapsamlı ve güncel bir standart
oluşturmanın yanı sıra işletmeler arasında bir sızma testinden ne bekleneceği
konusunda farkındalık yaratmaktır.

**OSSTMM (Open Source Security Testing Methodology Manual)**  :En yaygın kullanılan ve tanınan sızma testi standartlarından biridir. Test
uzmanları için uyarlanabilir kılavuzlar içeren sızma testine yönelik bilimsel bir
yaklaşıma dayanır.

**NIST**  : Testin doğruluğunu artırmaya yardımcı olmak için test ekibine çok özel sızma
testi yönergeleri sunar. Çeşitli sektörlerdeki hem büyük hem de küçük şirketler, sızma
testi için bu çerçeveden yararlanabilir.

**ISSAF (Information Applications Security Assessment Framework)** : Open Information Systems Security Group tarafından desteklenen bir
pentesting kılavuzudur. Bu metodoloji artık güncellenmemektedir,bununla birlikte,
kapsamlı doğası nedeniyle hala kullanılmaktadır.

---

## **SIZMA TESTİ GEREKEN KRİTİK SEKTÖRLER**

Hassas verileri işleyen veya siber saldırı riski yüksek olan şirketlerin (Örn: **Sağlık kuruluşları, kamu kurumları, finans kurumları, e-ticaret işletmeleri**), katı uyumluluk gereksinimleri nedeniyle düzenli olarak sızma testi yaptırması önerilmektedir.

Sızma testi, şirketinizin belirli **yerel ve küresel güvenlik uyumluluklarını** sağlamak amacıyla çeşitli endüstrilerde zorunludur. Penetrasyon testi gerektiren başlıca endüstri standartları şunlardır:

* **HIPAA (Sağlık kuruluşları)** 
* **PCI-DSS, TSE (Ödeme işleyen şirketler)**  
* **RBI-ISMS, BDDK, SPK, TSE (Bankalar ve bankacılık dışı finans kuruluşları)**  
* **SGT, TSE (Sivil Havacılık şirketleri)**  
* **SOC 2 (Hizmet kuruluşları)**  
* **ISO 27001 (Bilgi güvenliği etrafında iş yapmaya istekli herhangi bir kuruluş)**

---

## **TEST SONRASI ALINMASI GEREKEN ÖNLEMLER**

Penetrasyon testi raporunu aldıktan sonra, güvenlik açıklarını **önceliklendirmek**, **düzeltme planı oluşturmak** ve gerekli güvenlik önlemlerini hızla devreye sokmak kritik öneme sahiptir:

**Güvenlik Açıklarına Öncelik Verin**  : Raporda belirttiğimiz güvenlik açıklarını, risk
seviyelerine ve etkilerine göre önceliklendirin ve hangilerini önce ele alacağınıza karar
verin.

**Sorumlulukları Atayın**  : Güvenlik açıklarını düzeltme sorumluluklarını geliştiriciler, BT
personeli veya üçüncü taraf satıcılar gibi ilgili taraflara atayın. Düzeltmenin hedeflerini,
kapsamını, zaman çizelgesini, beklenen sonuçlarını ve her bir tarafın rol ve
sorumluluklarını iletin.

**Önerileri Uygulayın**  : Güvenlik açıklarını gidermek için penetrasyon testi raporumuzda
bulunan önerileri uygulayın, herhangi bir sorunuz veya şüpheniz varsa bizimle iletişime
geçin.

**Düzeltmeyi Doğrulayın ve Onaylayın** : Düzeltmenin başarılı olduğunu ve güvenlik
açıklarının giderildiğini onaylayın. Ayrıca, belge ve kayıtlarınızı sistemin mevcut
durumunu yansıtacak şekilde güncelleyin

---

## **TEST SÜRESİ VE RAPORLAMA TAKVİMİ**

**Test Süresi:** Süre; hedeflere, yaklaşıma ve test edilecek ortamın (saldırı yüzeyinin) büyüklüğüne ve karmaşıklığına bağlıdır.

**Raporlama Süresi:** Bir sızma testinin tamamlanıp raporlanması ortalama **1 ila 2 hafta** sürer. Rapor, **yönetici özeti** ile başlar, güvenlik açıklarını ve bunların **iş üzerindeki etkilerini** özetler ve açıkları düzeltmek için **önerilerde bulunur**.

---

## **VERİ KORUMA VE GİZLİLİK**

Sızma testi sırasında elde edilen verilerin korunması için hem ulusal hem de uluslararası **standartlara uygun güvenlik protokolleri** uygulanır. Müşterilerle imzalanan **Gizlilik Sözleşmesi (NDA)** kapsamında, bu veriler kesinlikle üçüncü kişilerle paylaşılmaz.

**Veri Saklama:** Doğrulama testi tamamlandıktan sonra müşteriye sunulan rapor, **güvenli veri silme yöntemleri** ile sistemlerden kalıcı olarak imha edilir ve **tutanak altına alınır**.
