---
title: MITRE ATT&CK
date: 2026-02-20 20:00:00 +0300
categories: [Siber Güvenlik Temelleri]
tags: [Siber Güvenlik Temelleri, MITRE ATT&CK]
author: rabiacelikli
---

![Image](/assets/img/2026-02-20/mitre_attack_1.jpg)

## Giriş
Geçmişten günümüze ulaşabilen hiçbir zanaat tek başına ve bir anda doğmamıştır. Her insan, kendinden bir sonrakine bıraktığı mirasın üzerine yeni bir tuğla koyarak kümülatif bir ilerleme sağlamıştır. Bugünün konusu da tam olarak bu birikimin ürünüdür.

Şimdi kendinizi bir labirentin içinde hayal edin. Nereye gideceğinizi, nereden döneceğinizi ya da tam olarak nerede olduğunuzu bilmiyorsunuz. Ancak duvarlara kazınmış yazılar fark ediyorsunuz. Bu yazılarda, sizden önce bu labirentte dolaşmış insanların, arkalarından gelenler için bıraktığı uyarılar, taktikler ve çıkış yolları anlatılıyor.

Artık labirent size daha az karmaşık gelmeye başlıyor, değil mi?

MITRE ATT&CK, işte tam olarak bu duvar yazılarının sistematik hale getirilmiş hâlidir.

## MITRE ATT&CK
Siber güvenlikte hiçbir sistem yüzde yüz güvenli değildir. Bugün sisteminizin yeterince güvenli olduğunu düşünüyor olsanız bile, zaman içinde bunun değişmeyeceğinin bir garantisi yoktur; çünkü zaman, beraberinde yeni zaafiyetler getirir ve saldırganlar bu zaafiyetleri sömürebilecek yeni yöntemler geliştirir. MITRE ATT&CK *(Adversarial Tactics, Techniques, and Common Knowledge)*, saldırganların davranışlarını sistematik olarak sınıflandırma ihtiyacı üzerine doğmuştur. MITRE, bu ihtiyacı 2010 yılında kendi kurduğu ve **FMX** adını verdiği araştırma ortamında yaptığı saldırı simülasyonları sayesinde fark eder.

FMX araştırma ortamında saldırganları taklit eden egzersizler yapılmış, ağdan toplanan veriler incelenmiş ve saldırıların izleri aranmıştır. Bu kadar çaba tek bir soruda toplandı: **“Bilinen saldırgan davranışlarını ne kadar iyi tespit edebiliyoruz?”** 

Araştırmaların hedefi belirlendikten sonra gerçek saldırgan gruplarının sistemlere yönelik sergilediği davranışlar tek tek incelenmiş ve sınıflandırılmıştır. Bu sınıflandırmayı; ofansif ekipler senaryo geliştirme amacıyla, defansif ekipler ise ne kadar iyi tespit yaptıklarını ölçmek için kullandılar. FMX araştırmalarının bir diğer motivasyon kaynağı da buydu.

Eylül 2013'te ilk ATT&CK modeli oluşturuldu ancak ağırlıklı olarak Windows ortamına odaklanılmıştı. İlerleyen yıllarda çalışmalar genişletilerek Windows'un ötesine geçilmiş, Linux ve Mac ortamlarını da kapsayacak şekilde **ATT&CK for Enterprise** olarak adlandırıldı ancak sadece kurumsal ortamlarla yetinilmeyip mobil ve bulut sistemlere de yer verilmiştir. Günümüzde ATT&CK; **14 Taktik**, **216 Teknik** ve **475 Alt tekniği** bünyesinde barındırarak siber güvenlik dünyası için paha biçilemez bir bilgi tabanı oluşturmuştur.

## TTP
ATT&CK matrisini anlayabilmemiz için öncelikle TTP kavramını öğrenmek gerekir. **TTP**, açılım olarak **taktik, teknik ve prosedür** olarak karşımıza çıkar. İlk ATT&CK modelinden beri amaç bulguların organize edilmesi olduğundan dolayı bu sınıflandırma TTP olarak kısaltılır. MITRE ATT&CK Framework'ünde TTP şu şekil çalışır:

- Taktikler, bir saldırı sırasında saldırganın kısa vadeli, taktiksel hedeflerini ifade eder. Her taktik saldırganın neden onu kullandığını açıklayacak şekilde gerekçelendirilir. Örneğin, 14 taktikten biri olan yetki yükseltme (Privilege Escalation), "saldırgan daha üst düzey yetkiler elde etmeye çalışıyor." olarak açıklanmıştır. Matris içerisinde **TA00X** formatında gösterilir.

- Teknikler, saldırganların bu taktiksel hedeflere ulaşmak için kullandıkları yöntemleri tanımlar. Taktikler gibi teknikler de kısaca açıklanır ancak tekniklere bağlı birçok alt teknik bulunabilir. Örneğin, yetki yükseltme altında Hesap Manipülasyonu (Account Manipulation) tekniği listelenir ancak bu tekniğin altında 7 alt teknik daha vardır. Böylece Hesap Manipülasyonu alt teknikler için şemsiye terim haline gelir. Matris içerisinde teknikler **T1XX**, alt teknikler ise **T1XX.00X** formatında yer alır.

- Prosedürler, bir tekniğin saldırganlar tarafından gerçek dünyada hangi araçlar, komutlar ve yöntemlerle uygulandığını ifade eder ve saldırgan gruplara göre değişiklik gösterebilir. 

## ATT&CK Matrisi

![Image](/assets/img/2026-02-20/mitre_attack_2.png)

Önceden de bahsedildiği gibi üç ATT&CK matrisi bulunmaktadır; Enterprise, Mobile ve ICS. En büyük ve kapsayıcı olan ATT&CK for Enterprise'dır. On dört taktik bulunur. Mobil ve ICS için ise on ikişer taktik toparlanıp sınıflandırılmıştır. 

Enterprise matrisi, bir saldırının baştan sona hangi aşamalardan geçtiğini anlamak için güçlü bir çerçeve sunar. Ancak MITRE ATT&CK’i gerçekten değerli kılan şey, bu çerçevenin soyut kalmaması; gerçek saldırgan grupları, kullanılan zararlı yazılımlar ve yürütülen operasyonlarla desteklenmesidir. Böylece ATT&CK, yalnızca "nasıl saldırılır?" sorusuna değil, "kim, hangi araçlarla ve nasıl saldırıyor?" sorularına da cevap verebilir. Bu noktada Groups, Software ve Campaigns başlıkları ATT&CK’in pratik kullanımını ortaya koyan en önemli bileşenler olarak karşımıza çıkar.

### Gruplar (Groups)

![Image](/assets/img/2026-02-20/mitre_attack_3.png)

Gruplar, daha önce kamuya ya da özel sektöre yönelik saldırılarda bulunmuş ve tehdit istihbarat raporlarında yer alan topluluklar olarak ATT&CK içerisinde CTI kısmında listelenmiştir. Gruplar; genellikle hedefli ve kalıcı tehdit faaliyetlerini temsil eden, adlandırılmış istila kümeleri (intrusion sets), tehdit grupları, aktör grupları veya operasyonlar olarak tanımlanır.

ATT&CK ağırlıklı olarak APT (Gelişmiş Kalıcı Tehdit) gruplarına odaklanır; ancak finansal kazanç amacı güden saldırganlar gibi diğer gelişmiş grupları da içerebilir. Tablo içerisinde **GXXXX** şeklinde gösterilir. Tabloda ayrıca ilişkili gruplar (Associated Groups) kısmını da görürüz, bu kısım çoğunlukla alt gruplar olarak anlaşılır ama **hatalı** bir yaklaşımdır. İlişkili gruplar, bir APT grubunun farklı raporlarda veya kaynaklarda geçen diğer adlarını ve o grupla ilişkilendirilen isimleri ifade eder.

### Yazılımlar (Software)

![Image](/assets/img/2026-02-20/mitre_attack_4.png)

Saldırganlar bir saldırıyı gerçekleştirirken tek bir yazılım türüne bağlı kalmaz. Aksine, amaçlarına ulaşmak için farklı yazılımları bir arada ve stratejik şekilde kullanırlar. MITRE ATT&CK bu noktada yazılımları da teknikler gibi ele alır; çünkü kullanılan yazılım, çoğu zaman bir tekniğin ya da alt tekniğin sahadaki karşılığıdır. Yani bir tekniğin nasıl uygulandığını anlamak için, kullanılan yazılıma bakmak kritik bir ipucu sunar. Tablo içerisinde **SXXXX** şeklinde gösterilir.

ATT&CK Framework'unde yazılımlar iki ana başlık altında toplanır: araçlar **(tools)** ve kötü amaçlı yazılımlar **(malware).**

Araçlar; ticari, açık kaynaklı, işletim sistemine gömülü ya da herkese açık yazılımlardan oluşur. Bu araçların önemli bir özelliği, yalnızca saldırganlar tarafından değil; savunma ekipleri, sızma test uzmanları ve red team'ler tarafından da kullanılabilmesidir. Metasploit, Mimikatz veya PsExec gibi araçların yanı sıra, Windows sistemlerde varsayılan olarak bulunan Net, netstat ve Tasklist gibi yardımcı programlar da bu kategoriye girer. Başka bir deyişle, saldırganlar çoğu zaman sisteme ekstra bir zararlı yüklemek yerine, zaten mevcut olan meşru araçları kullanarak faaliyetlerini sürdürür.

Kötü amaçlı yazılımlar ise doğrudan saldırı amacıyla geliştirilmiş yazılımlardır. Bunlar ticari, kapalı kaynak ya da açık kaynak olabilir ve genellikle saldırganın hedef sistem üzerinde kalıcılık sağlaması, veri sızdırması veya uzaktan erişim elde etmesi için kullanılır. PlugX ve CHOPSTICK gibi zararlı yazılımlar bu gruba örnek olarak gösterilebilir.

### Operasyonlar (Campaigns)

![Image](/assets/img/2026-02-20/mitre_attack_5.png)

Operasyon (Campaign), bir saldırgan grubun belirli bir zaman aralığında, ortak hedefler ve amaçlar doğrultusunda yürüttüğü ilişkili saldırı faaliyetlerini ifade eder. Aynı grup uzun yıllar boyunca birçok farklı saldırı gerçekleştirebilir; ancak bu saldırılar zaman, hedef veya kullanılan teknikler bakımından ayrıştığında farklı operasyonlar olarak değerlendirilir. ATT&CK kapsamında operasyonlar, saldırıların yalnızca "kim tarafından" yapıldığını değil, "hangi dönemde, hangi bağlamda ve nasıl" gerçekleştirildiğini anlamayı sağlar. Bu yaklaşım, saldırganların zaman içindeki davranış değişimlerini takip etmeyi kolaylaştırırken, savunma ekiplerinin geçmiş operasyonlardan yola çıkarak benzer saldırıları daha erken aşamada tespit edebilmesine katkı sağlar. Tabloda **CXXXX** formatında gösterilir.

Herhangi bir operasyona tıklayıp daha çok bilgi almak istediğimizde, bizi bu operasyonun hangi grup tarafından yürütüldüğüne, kullanılan yazılımlara, tekniklere ve alt tekniklere dair detaylı bir analiz sayfası karşılamaktadır.

## Cyber Kill Chain vs MITRE ATT&CK

![Image](/assets/img/2026-02-20/cyber-kill-chain-vs-mitre-att&ck.png)

Bir önceki yazımızda siber güvenliğin önemli metodolojilerinden biri olan  [Cyber Kill Chain'i](https://valientetechnologies.com/blog/posts/cyber-kill-chain/) işlemiştik. Cyber Kill Chain, bir saldırganın sisteme sızmak adına izlediği adımları 7 aşamada bize aktararak bir saldırının yaşam döngüsünü gözler önüne serer. Cyber Kill Chain'in önemi siber güvenlik dünyası için yadsınamaz bir gerçek ancak sahada işler her zaman bu kadar lineer işlemez. Saldırganlar her zaman belirli bir reçeteyi sabit şekilde takip etmezler; bazı adımları atlayabilir, geriye dönebilir veya aynı aşamayı defalarca tekrarlayabilir. MITRE ATT&CK, bu karmaşık davranışları tek bir çizgiye hapsetmek yerine, saldırganın sergilediği her davranışı ayrı ayrı ele alır. Bu yönüyle ATT&CK, Cyber Kill Chain’in alternatifi değil; onu tamamlayan ve derinleştiren bir model olarak değerlendirilmelidir.

İki model arasındaki en belirgin fark ayrıntı düzeyleridir. Cyber Kill Chain, saldırının yaşam döngüsüne daha kuşbakışı bir açıdan bakarak genel bir çerçeveyi 7 adımda bize aktarır. Tehdit tespiti ve önlenmesinin erken aşamalarında sıklıkla kullanılabilir ancak spesifik bir saldırıyı açıklamak veya analiz etmek için gerekli derinlikten yoksundur. Öte yandan MITRE ATT&CK, bir saldırının her aşamasını siber suçlular tarafından kullanılan belirli tekniklere ayırarak, güvenlik ekiplerine saldırıların nasıl geliştiğine dair daha derin bir anlayış sağlar. Böylece iz sürmek, davranışları anlamlandırmak ve buna yönelik önlemleri almak daha da kolaylaşır. 

Bir diğer önemli fark, bu iki yaklaşımın modern tehditlere uyum sağlama kabiliyetinde ortaya çıkar. Cyber Kill Chain, geliştirildiği dönemin ihtiyaçları doğrultusunda daha çok geleneksel ağ güvenliği senaryolarını merkeze alır. Bu durum, modeli içeriden gelen tehditler, bulut tabanlı saldırılar ve gelişmiş kalıcı tehditler (APT’ler) karşısında sınırlı kılabilir. MITRE ATT&CK ise kurumsal ağların yanı sıra mobil cihazlar ve bulut altyapıları gibi farklı ortamları da kapsayacak şekilde sürekli güncellenir. Böylece ATT&CK, yalnızca mevcut tehditleri değil, zamanla ortaya çıkan yeni saldırı yöntemlerini de takip edebilen yaşayan bir model hâline gelir.

Ancak burada yapılan karşılaştırılmada "hangisi daha iyi?" gibi bir yaklaşım yoktur. Her iki model de farklı şekilde farklı amaçlara hizmet eder ve birçok şirket de kendi güvenliklerini sağlarken bu iki modeli birlikte kullanır. 

## MITRE ATT&CK Kullanım Alanları
ATT&CK, tekrar tekrar belirttiğimiz gibi siber güvenlik için önemli bir bilgi tabanıdır ve siber güvenliğin birçok alt disiplini de ATT&CK'ten yararlanarak kendi disiplini için kullanır.

- **Saldırgan Emülasyonu (Adversary Emulation)**, belirli saldırgan grupların bilinen davranışları taklit edilerek, bir organizasyonun bu faaliyetleri ne kadar iyi tespit edip engelleyebildiğinin ölçülmesidir. MITRE ATT&CK, gerçek saldırgan tekniklerine dayalı emülasyon senaryoları oluşturmak için kullanılır.

- **Red Teaming**, bilinen tehdit istihbaratına dayanmadan saldırgan bakış açısıyla gerçekleştirilen güvenlik tatbikatlarıdır. ATT&CK, bu operasyonların planlanmasında ve savunmalardan kaçınacak yöntemlerin geliştirilmesinde yol gösterici olur.

- **Davranışsal Analitik Geliştirme**, imza ve IoC'lere bağlı kalmadan saldırgan davranışlarını tespit etmeyi hedefler. ATT&CK, bu analitiklerin davranış odaklı şekilde tasarlanması için temel bir referans sunar.

- **Savunma Boşluk Analizi (Defensive Gap Assessment)**, bir organizasyonun hangi saldırgan davranışlarına karşı yeterli görünürlüğe veya savunmaya sahip olmadığını ortaya koyar. ATT&CK, bu boşlukların belirlenmesi ve önceliklendirilmesi için kullanılır.

- **SOC Olgunluk Değerlendirmesi**, bir Güvenlik Operasyon Merkezi’nin saldırıları tespit etme ve müdahale etme yetkinliğini ölçer. ATT&CK, bu yetkinliğin davranış bazlı olarak değerlendirilmesini sağlar.

- **CTI Zenginleştirme**, ATT&CK ile saldırgan grupların araçlardan bağımsız olarak davranış temelli profillerinin çıkarılmasına yardımcı olur. Ancak yalnızca kullanılan tekniklere bakarak bir saldırıyı belirli bir gruba atfetmek doğru değildir.

## Sonuç 
Siber saldırılar, tek bir çizgide ilerleyen basit süreçler değildir; çoğu zaman bir labirent gibi karmaşık, tekrar eden ve öngörülmesi zor yollar içerir. MITRE ATT&CK, bu labirentin çıkışını göstermez; ancak duvarlara kazınmış tüm izleri, yolları ve uyarıları tek bir çerçevede toplar. Savunma ekipleri için asıl değer de burada ortaya çıkar: aynı hataları tekrar etmemek, bilinen yolları tanımak ve saldırganın bir sonraki adımını daha erken fark edebilmek. Bu izleri okuyabilen ekipler için labirent hâlâ karmaşıktır, ama artık **rastgele** değildir.

---

Bu yazıda *"MITRE ATT&CK: Design and Philosophy"* kaynağından yararlanılmıştır.

