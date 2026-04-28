# WAN Teknolojileri: Dünyayı Birbirine Bağlamak 🌍

**LAN (Yerel Ağ)** bir binayı bağlar, **WAN (Geniş Alan Ağı)** ise dünyayı! İnternet, dünyanın en büyük WAN'ıdır. Ancak şirketler, ofislerini birbirine bağlamak için internet dışında özel WAN teknolojileri de kullanır.

> 💡 **Benzetme:** LAN evinizin içindeki koridorlardır. WAN ise şehirleri birbirine bağlayan otoyollar, tren rayları ve uçak rotalarıdır.

---

## 🌐 LAN vs WAN

| Özellik | LAN (Local Area Network) | WAN (Wide Area Network) |
| :--- | :--- | :--- |
| **Kapsam** | Ev, Ofis, Bina | Şehir, Ülke, Kıta |
| **Hız** | Çok Yüksek (1/10/40 Gbps) | Değişken (Mbps - Gbps) |
| **Maliyet** | Kurulumu ucuz (Kablo+Switch) | Aylık kira ödenir (ISP'ye) |
| **Yönetim** | Tamamen sizde | Servis sağlayıcı (ISP) yönetir |

---

## 🛤️ MPLS (Multiprotocol Label Switching)

MPLS, verileri taşımak için **IP adresleri yerine etiketleri (labels)** kullanan özel bir WAN teknolojisidir.

> 💡 **Benzetme:** Bir paketi kargoya verirken üzerine sadece adres yazmak yerine (IP Routing), "Kırmızı renkli - Ekspres Hat" diye özel bir etiket (Label) yapıştırmak gibidir. Kargo şubeleri adresi okumakla uğraşmaz, etikete bakar ve hemen "Hızlı Hat"a atar.

### MPLS Avantajları

1. **Hız:** Router'lar IP tablosuna bakmak yerine kısa etiketlere bakar.
2. **QoS (Hizmet Kalitesi):** Ses ve video trafiğine "Öncelikli" etiketi yapıştırılabilir.
3. **Güvenlik:** İnternetten ayrı, özel bir tünel gibidir.

---

## ☁️ SD-WAN (Software-Defined WAN) - Modern Çözüm

Geleneksel WAN (MPLS) pahalı ve hantaldır. SD-WAN ise zeki ve çeviktir.

**Nasıl Çalışır?**
SD-WAN, elindeki tüm bağlantı türlerini (MPLS, Fiber İnternet, 4G/LTE) **tek bir havuzda** birleştirir ve trafiği akıllıca yönetir.

> 💡 **Benzetme:** GPS Navigasyonu (Yandex/Google Maps). Eskiden sadece tek bir ana yol (MPLS) vardı. Şimdi GPS (SD-WAN) trafiğe bakıyor; kaza varsa ara yola (İnternet) sapıyor, yol boşsa ana yoldan gidiyor. En hızlı yolu anlık olarak seçiyor.

### Neden Popüler?

- **Maliyet:** Pahalı MPLS hatları yerine ucuz internet hatlarını kullanmanızı sağlar.
- **Performans:** Zoom görüşmesini kaliteli hattan, dosya indirmeyi ucuz hattan yapar.
- **Yedeklilik:** Bir hat koparsa, hissettirmeden diğerine geçer.

---

## 🚇 Metro Ethernet

Şirketler için "Fiber İnternet"in profesyonel versiyonudur.

- **Özellik:** Evdeki fiber gibi paylaşımlı değildir. Size özel, dedike (dedicated) bir hattır.
- **Hız:** 5 Mbps'den 100 Gbps'ye kadar çıkabilir.
- **Simetrik:** İndirme (Download) ve Yükleme (Upload) hızları eşittir (Evde upload düşüktür).

---

## 📡 Leased Line (Kiralık Hat / Point-to-Point)

İki nokta arasında **fiziksel, size özel bir kablo** çekilmesi gibidir (Sanal değil, gerçektir).

- **Güvenlik:** Maksimum (Hat sadece size ait).
- **Maliyet:** Çok Pahalı 💰.
- **Kullanım:** Bankalar, finans kurumları gibi güvenliğin paradan önemli olduğu yerler.

---

## ⚖️ WAN Teknolojileri Karşılaştırması

| Teknoloji | Maliyet | Performans | Güvenlik | Kurulum Zorluğu |
| :--- | :--- | :--- | :--- | :--- |
| **MPLS** | 💸 Yüksek | ⭐⭐⭐⭐⭐ (Garantili) | ⭐⭐⭐⭐⭐ (Özel Ağ) | Zor (Haftalar sürer) |
| **İnternet VPN** | 💵 Düşük | ⭐⭐ (Dalgalı) | ⭐⭐⭐ (Şifreli) | Kolay |
| **SD-WAN** | 💰 Orta | ⭐⭐⭐⭐ (Optimize) | ⭐⭐⭐⭐ | Orta |
| **Metro Ethernet** | 💸 Yüksek | ⭐⭐⭐⭐⭐ (Yüksek Bant) | ⭐⭐⭐ | Zor |

---

## 🎯 Özet: Hangisini Seçmeli?

1. **Küçük Ofis:** Standart Fiber İnternet + VPN.
2. **Çok Şubeli Mağaza Zinciri:** SD-WAN (Merkezi yönetim ve maliyet avantajı).
3. **Banka / Hastane:** MPLS veya Leased Line (Kesinti ve gecikme kabul edilemez).

---

## ☁️ Bulut Ağı (Cloud Networking) Temelleri

Modern ağ dünyası artık sadece ofisleri değil, bulutu da (AWS, Azure, Google Cloud) kapsıyor.

### Temel Kavramlar

#### 1. VPC (Virtual Private Cloud)

Bulut sağlayıcısının veri merkezinde size ayrılmış **sanal özel ağdır**. Kendi IP bloğunuzu seçer, subnet'lere böler ve router'ları yönetirsiniz. Sanki bulutta kendi fiziksel veri merkeziniz varmış gibi!

#### 2. Region (Bölge) ve Zone (Alan)

- **Region:** Coğrafi konum (Örn: Frankfurt, İstanbul).
- **Zone (Availability Zone):** Bir region içindeki birbirinden bağımsız, yedekli veri merkezleri. Biri yanarsa diğeri çalışır.

#### 3. Hybrid Cloud (Hibrit Bulut)

Ofisinizdeki fiziksel sunucular ile Bulut'taki sunucuların birbirine VPN veya Direct Connect (özel hat) ile bağlanmasıdır.

---
