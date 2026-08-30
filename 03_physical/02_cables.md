# 🔌 Ağ Kabloları ve Bağlantı Temelleri

Ağ cihazlarının birbiriyle konuşabilmesi için fiziksel bir yola (ortama) ihtiyacı vardır. Kablosuz ağlar (Wi-Fi) çok yaygınlaşmış olsa da, kararlı ve yüksek hızlı altyapılar için **fiziksel kablolar** vazgeçilmezdir. 

Günümüzde ağ dünyasında iki temel kablo türü kullanılır: **Bakır (Twisted Pair) kablolar** ve **Fiber Optik kablolar**. Bu bölümde, temel bir ağ kurarken karşılaşacağınız kablo türlerini ve hangisini nerede kullanmanız gerektiğini en yalın haliyle inceleyeceğiz.

---

## 1. Bakır Kablolar (Twisted Pair - Bükümlü Çift)

Evlerimizde ve ofislerimizde modemden bilgisayara çektiğimiz klasik "internet kablosudur". İçerisinde birbirine sarılmış bakır teller bulunur.

* **Neden kıvrımlı (Twisted)?** Tellerin birbirine sarılması, dışarıdan gelen manyetik parazitleri (elektromanyetik girişim - EMI) engeller.
* **Soket Yapısı:** Uçlarında **RJ-45** adı verilen standart şeffaf plastik bir konnektör kullanılır.
* **Mesafe Sınırı:** Bakır kablolarla ağ verisi taşımak maksimum **100 metre** ile sınırlıdır. 100 metreden sonra sinyal zayıflar ve veri iletilemez.

### Korumalı mı, Korumasız mı? (UTP vs STP)
* **UTP (Korumasız - Unshielded):** Standart kablodur. Ev ve normal ofis kullanımı için idealdir. Esnek, ince ve uygun maliyetlidir.
* **STP (Korumalı - Shielded):** Kablonun içinde ekstra bir metal folyo veya zırh bulunur. Fabrika gibi elektrik motorlarının veya yüksek elektriksel gürültünün olduğu endüstriyel ortamlarda kullanılır.

### Hangi Kategoriyi (Cat) Seçmeliyiz?
Bakır kabloların kalitesi ve veri taşıma kapasitesi "Cat" (Kategori) olarak adlandırılır. 2026 standartlarına göre:

* ❌ **Cat 5 ve Cat 5e:** Artık eski teknoloji sayılmaktadır. Sadece eski bina altyapılarında karşılaşılır, yeni kurulumlarda kullanılmaz.
* ✅ **Cat 6:** Günümüzde ev ve standart ofisler için en yaygın ve yeterli kablodur (1 Gbps hız sağlar).
* 🚀 **Cat 6A:** **2026'nın yeni kurulum standardıdır.** Özellikle yeni nesil Wi-Fi 7 cihazları ve yüksek hızlı (10 Gbps) yerel ağlar kuruyorsanız altyapıda mutlaka Cat 6A tercih edilmelidir.
* 🏢 **Cat 7 ve Cat 8:** Ev kullanımı için değil, Veri Merkezleri (Data Center) için tasarlanmış çok kalın, esnemeyen ve pahalı özel kablolardır.

### RJ-45 Renk Sıralaması (T568B Standardı)
Ağ kablosunun ucuna şeffaf RJ-45 soketini takarken, içindeki 8 adet ince renkli tel belirli bir sıraya göre dizilmelidir. Dünya genelinde en yaygın kullanılan standart **T568B** standardıdır. Renk sıralaması soldan sağa (soketin tırnağı alttayken) şu şekildedir:

| Pin | Renk Adı | Görünüm |
| :---: | :--- | :--- |
| **1** | Turuncu-Beyaz | 🟠⚪ Çizgili |
| **2** | Turuncu | 🟠 Düz |
| **3** | Yeşil-Beyaz | 🟢⚪ Çizgili |
| **4** | Mavi | 🔵 Düz |
| **5** | Mavi-Beyaz | 🔵⚪ Çizgili |
| **6** | Yeşil | 🟢 Düz |
| **7** | Kahverengi-Beyaz | 🟤⚪ Çizgili |
| **8** | Kahverengi | 🟤 Düz |

> **T568A'da ne farklı?** Sadece yeşil ve turuncu tellerin yerleri kendi aralarında değişir. Ancak günümüzde kurulumların %99'unda **T568B** kullanılır.

> 💡 **Pratik Bilgi: Düz Kablo mu, Çapraz Kablo mu?** 
> Eskiden aynı tür cihazları (Örn: Bilgisayardan bilgisayara) bağlarken tellerin yeri değiştirilerek "Çapraz (Crossover)" kablo yapılırdı. Günümüzde tüm modern cihazlardaki **Auto-MDI/X** özelliği sayesinde bu ayrım tarihe karışmıştır. Artık her yerde standart "Düz (Straight)" kablo kullanabilirsiniz; cihazlar sinyali otomatik ayarlar.

---

## 2. Fiber Optik Kablolar

Veriyi elektrik sinyalleriyle değil, **ışıkla** taşırlar. İçerisindeki saç teli inceliğindeki cam veya plastik tüplerden ışık darbeleri gönderilir.

* **Avantajları:** Elektromanyetik parazitlerden **hiç** etkilenmez. Hızı çok daha yüksektir ve bakır kablodaki 100 metre sınırını aşarak **kilometrelerce** uzağa veri taşıyabilir.
* **Dezavantajları:** Kurulumu zordur, hassastır (kolay kırılabilir), sonlandırması için özel cihazlar gerektirir ve maliyetlidir. Uçlarına RJ-45 takılmaz; switch/router üzerindeki "SFP" yuvalarına giren özel fiber soketleri kullanılır.

### İki Temel Fiber Türü:
1. **Çok Modlu (Multi-Mode Fiber):** Işık, kablonun içinde yansıyarak (sekerek) ilerler. Bina içi, kampüs içi gibi nispeten kısa mesafelerde (genelde 500 metreye kadar) çok yüksek hızlar (10G, 40G, 100G) elde etmek için kullanılır.
2. **Tek Modlu (Single-Mode Fiber):** Işık, lazer ile çok ince bir çekirdekten ip gibi dümdüz gönderilir. Şehirler arası, okyanus altı hatlar veya internet servis sağlayıcılarının (ISP) ana omurgaları gibi **çok uzun mesafeler** (10 km'den yüzlerce km'ye kadar) için kullanılır.

---

## 3. Özet: Hangi Senaryoda Ne Kullanmalıyım?

| Kurulum Senaryosu | Ne Kullanmalı? | Neden? |
| :--- | :--- | :--- |
| **Ev ve Küçük Ofisler** | **Cat 6** veya **Cat 6A** | Maliyeti düşük, kurulumu kolay, güncel cihaz hızları için fazlasıyla yeterli. |
| **Yüksek Parazitli Ortam (Fabrika)**| **Cat 6A STP** | Makinelerin yaydığı parazitten (EMI) etkilenmemesi için metal korumalı olmalı. |
| **Büyük Kampüs ve Binalar Arası** | **Fiber Optik (Multi-Mode)** | 100 metre sınırını aştığı ve binalar arası elektriksel topraklama farklarından etkilenmediği için. |
| **Şehirler Arası Altyapı (Omurga)**| **Fiber Optik (Single-Mode)**| Sinyal kaybı yaşamadan kilometrelerce yüksek hızda veri taşıyabildiği için. |
