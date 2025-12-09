---
title: Kritik Zafiyet Analizi : CVE-2025-55182 (REACT2SHELL)
date: 2025-12-9 2:00:00 +0300
categories: [Kritik Zafiyetler, CVE-2025-55182 (REACT2SHELL)]
tags: [Kritik Zafiyetler, React,CVE-2025-55182,REACT2SHELL ]
author: tamlata
---

# KRİTİK ZAFİYET ANALİZİ: CVE-2025-55182 (REACT2SHELL)

Bu makale, React Server Components (RSC) altyapısında keşfedilen ve **maksimum ciddiyet** seviyesine sahip olan, kimlik doğrulaması gerektirmeyen **Uzaktan Kod Yürütme (RCE)** açığı **CVE-2025-55182**’nin teknik detaylarını ve savunma yöntemlerini kapsamlı olarak incelemektedir. Güvenlik araştırmacıları bu zafiyete **React2Shell** adını vermiştir.

---

## 1. Temel Kavramlar ve Arka Plan

### 1.1. CVE ve Ciddiyet Puanı

**CVE (Common Vulnerabilities and Exposures):** Siber güvenlik açıklarını standardize etmek için kullanılan benzersiz tanımlayıcılardır. Bu zafiyet, React Server Components’teki kritik bir açığı temsil eder ve **maksimum Common Vulnerability Scoring System (CVSS) puanı 10.0** olarak belirlenmiştir.

### 1.2. React ve Next.js Ortamı

*   **React Server Components (RSC):** Kullanıcı arayüzleri oluşturmak için kullanılan bir yazılım çatısıdır. Zafiyet, React’in 19.0.0 , 19.1.0 , 19.1.1 ve 19.2.0 sürümlerindeki bu sunucu bileşenlerini etkilemektedir.
*   **Next.js:** React’e dayanan bir web geliştirme çatısıdır. Next.js'in **App Router** kullanan 15.x ve 16.x sürümleri de bu zafiyetten etkilenmiştir. (CVE-2025-66478)


### 1.3. Uzaktan Kod Yürütme (RCE) Nedir?

**Uzaktan Kod Yürütme (Remote Code Execution - RCE):** Bir saldırganın, zafiyetli sunucuda fiziksel erişime ihtiyaç duymadan, zararlı kodları uzaktan çalıştırmasına olanak tanıyan kritik bir saldırı vektörüdür. CVE-2025-55182, kimlik doğrulaması gerektirmeyen (Unauthenticated) bir RCE açığıdır.

---

## 2. CVE-2025-55182 (React2Shell) Teknik Analizi

CVE-2025-55182, React’in sunucu ve istemci arasındaki iletişimi yöneten **Flight Protokolü** içerisinde kullanıcı kontrollü yüklerin güvenli olmayan bir şekilde işlenmesinden (güvenli olmayan deserializasyon) kaynaklanmaktadır. Zafiyet, güvenlik araştırmacısı Lachlan Davidson tarafından keşfedilmiş ve 29 Kasım 2025’te React Ekibine bildirilmiştir.

**Deserializasyon Nedir?**
Serileştirilmiş verinin (HTTP isteği), uygulamanın kullanabileceği canlı bir nesne yapısına dönüştürülme sürecidir. Güvenli olmayan deserializasyon zafiyetleri, saldırganın manipüle edilmiş veriler göndererek nesnelerin yapısını değiştirmesine olanak tanır.

### 2.1. Zafiyet Zinciri: Path Traversal + Fake Chunk Injection + $B $B Handler Abuse

Saldırganlar, RCE elde etmek için bu zafiyet zincirini kullanır: **path traversal**  + **fake chunk injection**  + **$B handler abuse**  ile **`Function(attacker_code)`** yürütür.

#### Aşama 1: Prototip Zinciri Geçişi (Path Traversal)

Zafiyetin ilk adımı, React’in dahili **`getOutlinedModel()`** işlevinde, referans çözümleme sırasında **`hasOwnProperty` kontrolünün olmamasından** kaynaklanır. Bu, nesne prototip zincirinde (Object Prototype Chain) gezinmeye izin verir.

Saldırganlar, `$1:constructor:constructor` gibi özel hazırlanmış bir referans yolu kullanarak, nihayetinde **JavaScript `Function` yapıcısına** (`Function` constructor) erişim sağlar.

#### Aşama 2: Sahte Thenable ve `_response` Enjeksiyonu

`Function` yapıcısına erişim, kodun yürütülmesi için bir çağrı aracı gerektirir. Bu araç, **maple3142** tarafından bulunan zincirle sağlanır:

1.  **Öz-Referanslı Thenable:** Saldırgan, form verileri içinde sahte bir chunk (Chunk 0) oluşturur ve kendi `then` alanını, `$1:__proto__:then` referansını kullanarak React’in dahili **`Chunk.prototype.then`** işlevine yönlendirir. Bu, sahte chunk’ı geçerli bir *thenable* nesnesi yapar.
2.  **`initializeModelChunk` Tetikleyicisi:** Chunk'ın `status` alanı `"resolved_model"` olarak ayarlandığı için, `await` çağrıldığında `Chunk.prototype.then` çalışır ve **`initializeModelChunk(this)`** çağrılır.
3.  **Sahte `_response` Enjeksiyonu:** `initializeModelChunk` işlevi içinde, `reviveModel` çağrılırken saldırganın kontrol ettiği **`chunk._response`** objesi doğrudan kullanılır.

#### Aşama 3: $B İşleyicisi ile Kod Yürütme (RCE)

RCE, Flight Protokolü'ndeki **$B işleyicisinin** kötüye kullanılmasıyla tamamlanır.

1.  **$B Tetikleyicisi:** Sahte chunk'ın `value` alanı, bir sonraki thenable'ı tetikler: `{"then": "$B1337"}`.
2.  **RCE Çağrısı:** `$B` öneki çözülürken, `parseModelString()` işlevi şunları çağırır: `return response._formData.get(response._prefix + id)`.
3.  **Payload Enjeksiyonu:** Saldırgan, enjekte edilen sahte `_response` nesnesinde:
    *   `_formData.get` özelliğini Path Traversal ile elde edilen **`Function` yapıcısına** (`$1:constructor:constructor`) ayarlar.
    *   `_prefix` alanına ise yürütülmek istenen **kötü amaçlı kodu** yerleştirir.

Bu, **`Function(code + "1337")`** şeklinde başarılı bir şekilde sunucuda kod yürütme ile sonuçlanır. Zafiyet, yalnızca `Next-Action` başlığına sahip bir POST isteği gönderilerek, yani eylem doğrulanmadan önce tetiklenebilir.

---

## 3. Aktif Tehditler ve İstismar Faaliyetleri

CVE-2025-55182'nin 3 Aralık 2025'te kamuoyuna açıklanmasından **saatler sonra**, Amazon tehdit istihbarat ekipleri, aralarında **Earth Lamia** ve **Jackpot Panda**'nın da bulunduğu birden fazla Çin devlet bağlantılı siber tehdit grubunun aktif sömürü girişimlerini gözlemlemiştir. Çin'in, devlet destekli siber tehdit faaliyetlerinin en üretken kaynağı olmaya devam ettiği ve aktörlerin kamuya açık zafiyetleri açıklanmasından saatler veya günler sonra rutin olarak operasyonelleştirdiği belirtilmektedir.

### 3.1. Tehdit Aktörleri ve Teknikleri

*   **Earth Lamia:** Çin merkezli bir aktör olup, Latin Amerika, Orta Doğu ve Güneydoğu Asya'daki finans, lojistik, perakende ve IT şirketleri gibi sektörleri hedef almaktadır.
*   **Jackpot Panda:** Esas olarak Doğu ve Güneydoğu Asya'daki kuruluşları hedefleyen, Çin'le bağlantılı bir diğer tehdit aktörüdür.
*   **Hız Odaklı Yaklaşım:** Tehdit aktörleri, kapsamlı test yerine hızlı operasyonelleştirmeyi önceliklendirmişlerdir. Hatta bazı aktörler, gerçek dünya senaryolarında çalışmayan halka açık PoC'leri (Proof-of-Concept) bile kullanmaya çalışmışlardır.
*   **Metodik Hata Ayıklama:** Gözlemlenen bazı saldırı desenleri, yalnızca otomatik taramadan ibaret değildir; bir tehdit kümesi, neredeyse bir saat boyunca (52 dakika) 116 istek göndererek sömürü tekniklerini **sistematik olarak canlı hedefler üzerinde hata ayıklama** çabası göstermiştir.
*   **Gözetleme Komutları:** Saldırganlar, başarılı RCE elde ettikten sonra sistem hakkında bilgi toplamak için `whoami` ve `id` gibi Linux komutlarını yürütme veya `/etc/passwd` dosyasını okuma girişimlerinde bulunmuştur.
*   **Eş Zamanlı İstismar:** Bu gruplar, bu zafiyetle sınırlı kalmayıp, şanslarını maksimize etmek için aynı anda diğer N-gün zafiyetlerini (örneğin CVE-2025-1338) de istismar etmeye çalışmıştır.

---

## 4. Savunma Yöntemleri ve Yama Kılavuzu

Bu zafiyetin kritik doğası nedeniyle, **uygulamaları yamalamak tek ve en güvenilir çözümdür**.

### 4.1. Kritik Yama Sürümleri

| Bileşen | Savunmasız Sürümler | Yama Yapılan Minimum Sürümler | Referans |
| :--- | :--- | :--- | :--- |
| **React** | 19.0.0, 19.1.0, 19.1.1, 19.2.0 | **19.2.1+** (veya 19.0.1+, 19.1.2+) | |
| **Next.js (App Router)** | 15.x, 16.x, 14.3.0-canary.77+ | **15.0.5+, 15.1.9+, 15.2.6+, 16.0.7+** | |

React’teki düzeltme (React 19.2.1), Facebook tarafından yapılan bir commit ile uygulanmıştır [React Fix Commit]. Next.js'teki düzeltme ise Vercel tarafından yayınlanmıştır [Next.js Fix Commit].

### 4.2. Zafiyetin Düzeltilmesi (Patch)

React’in 19.2.1 yaması, zafiyet zincirini kırmak için kritik düzeltmeler içerir:

1.  **Güvenli Yanıt Objeleri (RESPONSE\_SYMBOL):** Saldırganın kontrol ettiği `chunk._response` yerine, JSON ile taklit edilemeyen bir sembol tabanlı yanıt objesine geçiş yapılmıştır.
2.  **Path Traversal Engeli:** **`getOutlinedModel()`** işlevine, prototip zincirinde gezinmeyi engellemek için **`hasOwnProperty` kontrolü** eklenmiştir. Bu, `$1:constructor:constructor` gibi yolların `Function` yapıcısına çözülmesini engeller.

### 4.3. WAF Kısıtlamaları ve Geçici Önlemler

Geleneksel imzaya dayalı WAF'lar, bu saldırıyı tamamen engellemekte zorlanır. Bu nedenle WAF korumaları, yamanın yerini tutmaz.

#### A. WAF Atlatma (Bypass) Teknikleri

1.  **Çok Katmanlı Kodlama (Encoding Bypass):** Exploit yükü, WAF tarafından taranan ham HTTP baytlarında tanınabilir anahtar kelimeler içermez. Saldırganlar, karakterleri **Unicode kaçış dizileri** (`\u0063onstructor` gibi) kullanarak kodlayabilir. WAF, kodlanmış baytları taradığında, bu kaçış dizileri geleneksel imzalarla eşleşmez, ancak sunucuda geçerli JavaScript komutlarına dönüşür.
2.  **Gövde İnceleme Sınırlarının Aşılması (Oversize Bypass):** Çoğu WAF (örneğin, AWS WAF'ın varsayılan limiti 8 KB veya 16 KB olabilir), performansı korumak için HTTP gövdesinin yalnızca bir kısmını inceler. Saldırganlar, zararsız dolgu verisi (padding) kullanarak exploit payload'unu WAF'ın inceleme sınırının ötesine itebilirler. Eğer WAF, limiti aşan istekler için `OversizeHandling: CONTINUE` olarak ayarlandıysa (ki bu yaygın bir varsayılan olabilir), atlatma (bypass) gerçekleşir.

#### B. Geçici WAF Çözümleri

*   **AWS WAF:** Yönetilen kural setlerinin varsayılan sürümü (AWSManagedRulesKnownBadInputsRuleSet sürüm 1.24 veya üstü), bu zafiyete karşı otomatik koruma sağlamak üzere güncellenmiştir.
*   **Google Cloud Armor:** Müşteriler, yama yapılana kadar geçici bir koruma olarak `cve-canary` önceden yapılandırılmış WAF kuralını dağıtabilirler. Bu kural, `next-action` veya `rsc-action-id` başlıklarını içeren POST isteklerini hedefler.
*   **WAF Önerisi:** Eğer WAF kullanılıyorsa, `OversizeHandling` ayarının `MATCH` olarak değiştirilmesi önerilir. Bu, boyutu aşan isteklerin engellenmesini sağlayarak bypass riskini azaltır.

### 4.4. Olay Müdahalesi ve Göstergeler

Uygulama ve web sunucusu günlüklerinin şüpheli faaliyetler açısından kontrol edilmesi kritik öneme sahiptir.

**Saldırı Göstergeleri (IOC'ler):**
*   **Ağ Göstergeleri:** Uygulama uç noktalarına gönderilen ve `next-action` veya `rsc-action-id` başlıklarını içeren HTTP POST istekleri. İstek gövdelerinde `$@` veya `"status":"resolved_model"` gibi kalıpların bulunması.
*   **Sunucu Tabanlı Göstergeler:** Beklenmedik keşif komutlarının yürütülmesi (`whoami`, `id`). `/etc/passwd` okuma girişimleri veya `/tmp/` dizinine şüpheli dosya yazma girişimleri (örneğin `pwned.txt`). Node.js/React uygulamaları tarafından beklenmeyen yeni süreçlerin başlatılması.

---




## 5. CVE-2025-55182 (React2Shell) PROOF OF CONCEPT

Bu bölüm, zafiyetin test ortamında (Proof-of-Concept) nasıl istismar edildiğini görsel adımlarla göstermektedir.

---

### Adım 1: Test Ortamının Hazırlanması

İlk olarak, zafiyetin PoC kodunu içeren GitHub deposu klonlanır ve etkilenen Next.js projesinin sunucusu ayağa kaldırılır.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 1** | `https://github.com/msanft/CVE-2025-55182` reposunu klonluyoruz. |
| **[RESİM 1 YERİ]** | ![](/assets/img/2025-12-9/1.png) |
| **Görsel 2** | `test-server` klasörüne girip `npm run dev` komutu ile React projemizi çalıştırıyoruz. Next.js 16.0.6 (App Router kullanan etkilenen sürüm) yerel ağda dinlemeye başlıyor. |
| **[RESİM 2 YERİ]** | ![](/assets/img/2025-12-9/2.png) |

### Adım 2: Zafiyetli Uygulamanın Doğrulanması

Zafiyetli sunucu, yerel ağda veya `localhost:3000` portunda erişilebilir hale getirilir.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 3** | Gördüğümüz gibi `localhost:3000` portunda proje çalışıyor. Tarayıcıda uygulamanın arayüzünü görebiliriz. |
| **[RESİM 3 YERİ]** | ![](/assets/img/2025-12-9/3.png) |

### Adım 3: PoC Scriptinin İncelenmesi ve Kötü Amaçlı Yükün Tanımlanması

`poc.py` scripti incelenerek RCE'yi tetikleyecek komut tanımlanır. Script, Path Traversal ve $B işleyicisi kötüye kullanımını içeren Flight Protokolü'nü taklit eden bir POST isteği oluşturur.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 5** | `poc.py` scriptini Sublime Text ile açtığımızda scripti okuyabilir, hatta uzaktan çalıştırılacak kodu değiştirebiliriz. Ben burada `uname -a` komutunu kullandım. Script, RCE için kritik olan `prefix` ve `formData` alanlarını görüleceği üzere özel olarak yapılandırmıştır. |
| **[RESİM 5 YERİ]** | ![](/assets/img/2025-12-9/5.png) |

### Adım 4: Zafiyetin Başarılı Tetiklenmesi (whoami Komutu)

`poc.py` scripti ilk defa çalıştırılarak, basit bir sistem keşif komutu (`whoami` varsayılan komut) yürütülür.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 4** | `poc.py` scriptini çalıştırdığımızda ise RCE ile serverda komut çalıştırabiliyoruz. Burada varsayılan komut çalışmıştır ve kullanıcı (UID/GID) bilgileri dönmüştür. |
| **[RESİM 4 YERİ]** | ![](/assets/img/2025-12-9/4.png) |

### Adım 5: Uzaktan Komut Yürütme Kanıtı (uname -a Komutu)

Scriptte tanımlanan `uname -a` komutu çalıştırılarak, sunucunun işletim sistemi detayları elde edilir.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 6** | Burada tekrar `poc.py | lolcat` komutunu çalıştırınca `uname -a` komutunun serverda çalıştığını ve Linux OS detaylarını içeren yanıtı görebiliyoruz. |
| **[RESİM 6 YERİ]** | ![](/assets/img/2025-12-9/6.png) |

### Adım 6: Sunucu Tarafı Kanıtı (Log Analizi)

Saldırının başarısı, yalnızca istemci yanıtıyla değil, aynı zamanda etkilenen sunucunun (Next.js) terminal loglarından da doğrulanabilir.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 7** | Server loglarından, RCE sonucu yürütülen `uname -a` komutunun çıktısı olan Linux OS bilgisinin (`Linux huawei 5.15.0-163-generic...`) bir hata digest'i içinde göründüğünü tespit edebiliriz. Bu, uygulamanın kod yürütme esnasında yanıt oluşturmaya çalıştığını ve bunu doğrulayan kritik bir sunucu tarafı göstergesidir. |
| **[RESİM 7 YERİ]** | ![](/assets/img/2025-12-9/7.png) |

### Adım 7: Script ile zafiyet keşfi 

https://github.com/fatguru/CVE-2025-55182-scanner Scripti ile hedef makinada tarama yapabilirsiniz.

| Görsel No | Açıklama |
| :--- | :--- |
| **Görsel 7** | İlgili scripti çalıştırarak localhost:3000 'i taratıyoruz, Eğer makina zafiyetli ise `EXPOSED` çıktısını göreceksiniz.  |
| **[RESİM 7 YERİ]** | ![](/assets/img/2025-12-9/8.png) |


### KAYNAKLAR

| Açıklama | URL |
| :--- | :--- |
| **AWS Security Bulletin: CVE-2025-55182** | `https://aws.amazon.com/security/security-bulletins/AWS-2025-030/` |
| **Responding to CVE-2025-55182: Secure your React and Next.js workloads** | `https://cloud.google.com/blog/products/identity-security/responding-to-cve-2025-55182` |
| **React Team Security Advisory** | `https://react.dev/blog/2025/12/03/react-server-components-security-advisory` |
| **Next.js CVE-2025-66478 Duyurusu** | `https://nextjs.org/blog/CVE-2025-66478` |
| **React Yama Commit Detayı (Fix)** | `https://github.com/facebook/react/commit/7dc903cd29dac55efb4424853fd0442fef3a8700` |
| **Next.js Yama Commit Detayı (Fix)** | `https://github.com/vercel/next.js/commit/6ef90ef49fd32171150b6f81d14708aa54cd07b2` |
| **React Prototype Chain Patch Commit** | `https://github.com/facebook/react/pull/35277/commits/e2fd5dc6ad973dd3f220056404d0ae0a8707998d` |
| **MDN Object Prototypes Referansı** | `https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Advanced_JavaScript_objects/Object_prototypes` |
| **China-nexus cyber threat groups rapidly exploit React2Shell vulnerability (CVE-2025-55182)** | `https://aws.amazon.com/blogs/security/china-nexus-cyber-threat-groups-rapidly-exploit-react2shell-vulnerability-cve-2025-55182/` |
| **AWS WAF Dokümantasyonu** | `https://docs.aws.amazon.com/waf/` |
| **React Server Functions Referansı** | `https://react.dev/reference/rsc/server-functions` |
| **React Flight Protocol Açıklaması** | `https://tonyalicea.dev/blog/understanding-react-server-components/` |
| **maple3142'nin X (Twitter) Hesabı** | `https://x.com/maple3142` |

---

**Özetleyici Analoji:**

Bu zafiyet, bir kargo şirketinin (React Flight Protocol), taşıdığı bir paketin (Chunk) içeriği sayesinde, kendi iç prosedürlerini (Chunk.prototype.then) manipüle etmesini sağlamasına benzetilebilir. Bu manipülasyon sonucunda, sistem kendi kendini çağırır ve paket içindeki gizli bir talimatı (malicious code) kullanarak, kritik bir sistem aracını (`Function` constructor) çalıştırmasını emreder. Saldırının bu kadar tehlikeli olmasının temel nedeni, WAF'ların geleneksel imzalarla tespit edemeyeceği **karmaşık kodlama yöntemleri** ve **büyük veri yükleri** kullanılarak kolayca atlatılabilmesidir. Bu durum, yalnızca temel sistem mantığının yamalanmasıyla (yani uygulamanın güncellenmesiyle) tamamen çözülebilir.
*   **Kritik Detay:** Uygulamalar, sunucu işlevlerini (Server Functions) açıkça kullanmasalar bile, React Server Components’ı destekledikleri sürece bu zafiyete karşı savunmasızdır.
```