# Bölüm: Ağ Hızı ve Veri Ölçü Birimleri

İnternet paketlerini incelerken veya bir dosya indirirken sürekli karşımıza çıkan bazı terimler vardır: **Kbps, Mbps, GB, MB...** İlk bakışta karmaşık görünse de, dijital dünyadaki hız ve boyut kavramlarını anlamak aslında çok kolaydır. Bu bölümde, bir ağın hızını nasıl ölçeceğimizi ve bu birimlerin ne anlama geldiğini en basit haliyle öğreneceğiz.

---

## 1. Temel Kural: Bit mi, Byte mı?

Ağ teknolojilerinde hız ve boyut kavramlarını karıştırmamak için bilmeniz gereken en önemli kural şudur: **Küçük "b" harfi Bit'i, Büyük "B" harfi ise Byte'ı temsil eder.**

* **Bit (b):** Bilgisayarların anladığı en küçük veri birimidir (Sadece `0` veya `1` olabilir). **Ağ hızlarını** ifade ederken genellikle Bit kullanılır.
* **Byte (B):** 8 tane Bit'in bir araya gelmesiyle oluşan bir karakterlik veri kümesidir (Örneğin klavyeden bastığınız "A" harfi hafızada 1 Byte kaplar). **Dosya boyutlarını** ifade ederken Byte kullanılır.

> **Altın Formül:** > 1 Byte = 8 Bit

---

## 2. Ağ Hızı Birimleri (Saniyede Aktarılan Veri)

Ağ hızı, **verinin bir saniyede bir noktadan diğerine ne kadar hızlı aktarıldığı** ile ölçülür. Bu yüzden birimlerin sonuna "saniyede" anlamına gelen **ps (per second)** veya **/s** takısı gelir.

Küçükten büyüğe ağ hızı birimleri şu şekildedir:

### Kbps (Kilobit per second - Saniyede Kilobit)
* **Nedir?:** Saniyede bin bitlik veri aktarımıdır.
* **Nerede Kullanılır?:** Çok eski çevirmeli (dial-up) internet bağlantılarında veya günümüzde çok düşük veri tüketen akıllı ev cihazlarının (IoT) iletişiminde karşımıza çıkar. 
* **Örnek:** 56 Kbps eski bir modem hızıdır.

### Mbps (Megabit per second - Saniyede Megabit)
* **Nedir?:** Saniyede bir milyon bitlik veri aktarımıdır (1 Mbps = 1024 Kbps).
* **Nerede Kullanılır?:** Günümüz ev ve iş yeri internet hızlarını tanımlamak için kullanılan **en standart** birimdir.
* **Örnek:** Evinizdeki internet paketiniz 24 Mbps, 50 Mbps veya 100 Mbps hızında olabilir.

### Gbps (Gigabit per second - Saniyede Gigabit)
* **Nedir?:** Saniyede bir milyar bitlik veri aktarımıdır (1 Gbps = 1024 Mbps).
* **Nerede Kullanılır?:** Çok yüksek hızlı fiber internet altyapılarında, büyük veri merkezlerinde ve modern şirket ağlarında kullanılır.

---

## 3. Dosya Boyutu Birimleri (Depolama)

İnternetten bir şey indirirken hızımız Mbps olsa da, indirdiğimiz dosyanın bilgisayarımızda kapladığı alan **Byte (B)** cinsinden ölçülür.

* **KB (Kilobyte):** Küçük metin belgeleri veya düşük çözünürlüklü görseller. (1 KB = 1024 Byte)
* **MB (Megabyte):** MP3 şarkılar, kısa videolar, fotoğraflar. (1 MB = 1024 KB)
* **GB (Gigabyte):** Yüksek çözünürlüklü filmler, modern bilgisayar oyunları. (1 GB = 1024 MB)
* **TB (Terabyte):** Büyük sabit diskler, tüm bilgisayarın yedekleri. (1 TB = 1024 GB)

---

## 4. Pratik Bilgi: "100 Mbps İnternetim Var, Neden Saniyede 100 MB İndiremiyorum?"

Kullanıcıların en çok düştüğü yanılgı budur. İnternet sağlayıcınız size **100 Mbps** hız tanımladığında, saniyede 100 Megabyte dosya indirebileceğinizi düşünebilirsiniz. Ancak ağ hızı **Bit**, dosya boyutu **Byte** cinsindendir.

Gerçek indirme hızınızı bulmak için operatörün verdiği hızı **8'e bölmeniz** gerekir.



**Örnek Hesaplama:**
* İnternet Hızınız: **100 Mbps** (Megabit)
* Saniyedeki İndirme Hızınız: 100 / 8 = **12.5 MB/s** (Megabyte)

Yani 100 Mbps hızındaki bir internetle, 100 MB boyutundaki bir dosyayı 1 saniyede değil, yaklaşık 8 saniyede indirebilirsiniz.

---

### Özet Tablo

| Birim (Kısaltma) | Anlamı | Kullanım Alanı | Gerçek Dünyadan Örnek |
| :--- | :--- | :--- | :--- |
| **Kbps** | Kilobit (Saniyede) | Çok eski/yavaş ağ hızları | Eski sesli aramalar, basit sensörler |
| **Mbps** | Megabit (Saniyede) | Standart ev/mobil internet hızı | YouTube'dan video izlemek, webde gezinmek |
| **Gbps** | Gigabit (Saniyede) | Ultra hızlı fiber ağlar | Büyük veri merkezleri, modern şehir altyapıları |
| **MB / GB** | Megabyte / Gigabyte | Dosya ve Depolama Boyutu | Bilgisayara indirilen oyunlar, filmler |