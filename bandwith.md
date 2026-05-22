# 🛣️ Bant Genişliği (Bandwidth) ve Ağ Hızı.

Ağ dünyasında hızlardan bahsederken sıkça duyduğumuz kavramlar vardır: **Kbps, Mbps, Gbps**... İnternet sağlayıcılarının reklamlarında *"100 Megabit Fiber!"* diye bağırdığını mutlaka duymuşsunuzdur. Peki bu terimler gerçekten ne anlama geliyor? 

Network dünyasına adım atarken, bu ölçü birimlerini ve "Bant Genişliği" (Bandwidth) kavramını zihnimizde doğru oturtmamız çok önemlidir. 

---

## 🚰 Bant Genişliği (Bandwidth) Nedir?

Bant genişliğini anlamanın en kolay yolu onu bir **su borusu** veya **otoyol** ile kıyaslamaktır.

```text
       Düşük Bant Genişliği            Yüksek Bant Genişliği
          (Dar Boru)                        (Geniş Boru)
        ==============                 ========================
         veri -> veri                   veri -> veri -> veri 
        ==============                  veri -> veri -> veri 
                                       ========================
```

- **Otoyol Örneği:** Bant genişliği, bir otoyoldaki şerit sayısıdır. 2 şeritli bir yoldan aynı anda yan yana 2 araba geçebilirken, 4 şeritli bir yoldan 4 araba geçebilir. Bant genişliği ne kadar yüksekse, aynı anda o kadar fazla veri (araba) bir noktadan diğerine ulaşabilir.
- **Su Borusu Örneği:** Borunun çapı ne kadar genişse (yukarıdaki çizimdeki gibi), saniyede akan su miktarı o kadar fazla olur. 

Kısacası Bant Genişliği, **"bir saniyede aktarılabilecek maksimum veri kapasitesidir."**

---

## 1. Altın Kural: Bit mi, Byte mı? (b vs B)

Burada herkesin kafasını karıştıran o meşhur tuzağa düşmemek için çok önemli bir kuralımız var:

> **Küçük "b" Bit'i, Büyük "B" Byte'ı temsil eder!**

- **Bit (b):** Bilgisayarın anladığı en temel veri birimidir (1 veya 0). **Ağ hızları her zaman Bit cinsinden ölçülür.**
- **Byte (B):** 8 tane Bit'in yan yana gelerek oluşturduğu anlamlı veri paketidir (Örneğin bir harf 1 Byte'tır). **Dosya boyutları (hard disk kapasitesi, indirilen film vs.) her zaman Byte cinsinden ölçülür.**

> 💡 **Unutmayın:** 1 Byte = 8 Bit

---

## 2. Ağ Hızımızı Nasıl Ölçüyoruz?

Veriler saniyeler içinde aktığı için hız birimlerinin sonuna **"ps" (per second - saniyede)** eklenir.

- **Kbps (Kilobit per second):** Saniyede 1.000 bit.
  - *Nerede görülür?* Çok eski çevirmeli (dial-up) bağlantılarda veya çok az veri tüketen akıllı priz gibi cihazlarda.
- **Mbps (Megabit per second):** Saniyede 1.000.000 bit. (1 Mbps = 1.000 Kbps)
  - *Nerede görülür?* Evlerimizdeki ve telefonlarımızdaki standart internet hızlarında (Örn: 50 Mbps VDSL, 100 Mbps Fiber).
- **Gbps (Gigabit per second):** Saniyede 1.000.000.000 bit. (1 Gbps = 1.000 Mbps)
  - *Nerede görülür?* Veri merkezlerinde, sunucular arası iletişimde ve yavaş yavaş evlerimize giren ultra hızlı fiber hatlarda.
- **Tbps (Terabit per second):** Saniyede 1.000.000.000.000 bit.
  - *Nerede görülür?* Okyanus altı devasa fiber optik kablolarda ve küresel internet omurgasında (Backbone) görülür. Ev kullanıcıları için şimdilik bilim kurgu!

---

## 3. Dosya Boyutu Birimleri (Depolama)

Ağ hızımızı Bit ile ölçtük, peki indirdiğimiz dosyaların boyutu ne ile ölçülür? Tabii ki **Byte** ile. Tarayıcınızda veya diskinizde göreceğiniz birimler şunlardır:

- **KB (Kilobyte):** Metin belgeleri ve küçük resimler. (1 KB = 1024 Byte)
- **MB (Megabyte):** MP3 şarkılar, kısa videolar. (1 MB = 1024 KB)
- **GB (Gigabyte):** Yüksek çözünürlüklü filmler, bilgisayar oyunları. (1 GB = 1024 MB)
- **TB (Terabyte):** Yüksek kapasiteli hard diskler. (1 TB = 1024 GB)

> 🤓 **Geek Bilgisi (1000 mi, 1024 mü?):**
> Network hızlarında (Mbps) katsayı her zaman tam **1000**'dir. Ancak Windows gibi işletim sistemleri dosya boyutunu hesaplarken **1024** katlarını kullanır (Aslında buna *Kibibyte - KiB* denir ama herkes KB demeye alışmıştır). Hard disk üreticileri ise disk boyutunu 1000 üzerinden hesaplar. Bu yüzden aldığınız "1 TB (1000 GB)" harici disk, bilgisayara taktığınızda 931 GB görünür. Kayıp yoktur, sadece bilgisayarınız 1024'e bölerek hesaplıyordur!

---

## 4. "100 Mbps İnternetim Var, Neden Saniyede 100 MB İndiremiyorum?"

İşte milyonlarca insanın internet sağlayıcılarına isyan ettiği o meşhur an! 

İnternet sağlayıcınız size **100 Mbps (Megabit)** hız satar. Ancak siz bir dosya indirirken tarayıcınız size hızı **MB/s (Megabyte/saniye)** olarak gösterir.

Kuralları hatırlayalım: **1 Byte = 8 Bit**. 

Bu durumda operatörün size verdiği hızı **8'e bölerek** saniyede kaç Megabyte dosya indirebileceğinizi bulursunuz:

> **100 Mbps / 8 = 12.5 MB/s**

Yani saniyede en fazla 12.5 Megabyte indirebilirsiniz. 100 MB boyutundaki bir dosya, 1 saniyede değil tam 8 saniyede inecektir.

---

## 🎯 Kısa Özet

| Kavram | Temsil | Ne Ölçer? | Örnek |
| :--- | :--- | :--- | :--- |
| **Bit (b)** | Küçük "b" | Ağ aktarım kapasitesini | 100 M**b**ps internet hızı |
| **Byte (B)** | Büyük "B" | Dosya/Depolama boyutunu | 50 G**B** boyutunda bir oyun |
| **MB/s** | Megabyte/saniye | Gerçek indirme hızını | Saniyede 12.5 **MB/s** indirme hızı |

Artık hız testlerinde gördüğünüz o karmaşık rakamların arkasındaki mantığı, "Neden yavaş iniyor?" sorusunun cevabını ve "Flash belleğim neden eksik GB gösteriyor?" gizemini tam olarak biliyorsunuz!
