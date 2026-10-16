# 🗺️ Ağ Topolojileri

**Ağ topolojisi**, bir bilgisayar ağındaki cihazların **fiziksel veya mantıksal düzenlemesini** ifade eder. Farklı düğümlerin (bilgisayarlar, anahtarlar ve yönlendiriciler gibi) nasıl bağlandığını ve aralarında **veri akışının** nasıl gerçekleştiğini tanımlar.

---

## Yaygın Ağ Topolojisi Türleri

### 1. Veri Yolu (Bus) Topolojisi

* Tüm cihazlar, **omurga** olarak bilinen **tek bir merkezi kabloya** bağlıdır.
* Veri, kablo boyunca **her iki yönde** hareket eder.
* **Avantajları**: Küçük ağlar için basit ve uygun maliyetlidir.
* **Dezavantajları**: Omurgada meydana gelen bir arıza tüm ağı çökertebilir.

### 2. Yıldız (Star) Topolojisi

* Tüm cihazlar **merkezi bir hub veya anahtara** bağlıdır.
* Cihazlar arasındaki iletişim **merkezi cihaz üzerinden** geçer.
* **Avantajları**: Yönetimi ve sorun gidermesi kolaydır; bir cihazın arızası diğerlerini etkilemez.
* **Dezavantajları**: Hub/anahtar arızalanırsa, tüm ağ çöker.

### 3. Halka (Ring) Topolojisi

* Cihazlar **dairesel bir döngü** şeklinde bağlanır.
* Veriler halka etrafında **tek yönde** hareket eder.
* **Avantajları**: Tahmin edilebilir veri akışı.
* **Dezavantajları**: Halkadaki bir kopma iletişimi tamamen bozabilir.
  
### 4. Örgü (Mesh) Topolojisi

* Her cihaz ağdaki **diğer her cihaza** bağlıdır.
* Veriler **birden fazla yoldan** geçebilir.
* **Avantajları**: Yüksek güvenilirlik ve hata toleransı.
* **Dezavantajları**: Kurulumu ve bakımı pahalı ve karmaşıktır.

### 5. Hibrit (Hybrid) Topoloji

* **İki veya daha fazla topolojinin** birleşimi (örneğin, **yıldız-bus** veya **yıldız-halka**).
* Belirli kurumsal ihtiyaçları karşılamak için kullanılır.
* **Avantajları**: Esnek ve ölçeklenebilir.
* **Dezavantajları**: Tasarımı ve yönetimi karmaşık olabilir.

---

> 💡 **Günümüzde Hangileri Kullanılıyor?**  
> 
> - **Ev, Ofis ve Okul:** Neredeyse tamamı **Yıldız** ve **Hibrit** topolojidir.  
> - **Diğerleri:** Tamamen yok olmadı; otomotiv, telekom omurgası ve veri merkezleri gibi özel alanlarda kullanılmaya devam ediyor.
