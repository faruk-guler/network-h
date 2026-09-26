# 🌍 LAN ve WAN: Dünyayı Birbirine Bağlamak

Ağlar coğrafi büyüklüklerine ve kullanım amaçlarına göre sınıflandırılır. En temel ve yaygın iki ağ türü **LAN (Yerel Alan Ağı)** ve **WAN (Geniş Alan Ağı)**'dır.

> 💡 **Benzetme:** LAN evinizin veya ofisinizin içindeki odalar ve koridorlardır. WAN ise şehirleri ve ülkeleri birbirine bağlayan otoyollar ve hava yollarıdır. İnternet ise dünyadaki tüm bu yolların birleştiği en büyük WAN'dır.

---

## 1. LAN (Local Area Network — Yerel Alan Ağı)

Sınırlı bir coğrafi alanda (ev, ofis, okul, tek bir bina) bulunan cihazların birbirine bağlanmasıyla oluşan ağdır.

- **Kapsam:** Tek bir oda, ev veya bina.
- **Hız:** Çok yüksek (Genellikle 1 Gbps – 10 Gbps).
- **Sahiplik:** Ağ altyapısı (kablolar, switch'ler, access point'ler) tamamen size/kuruma aittir.
- **Gecikme:** Çok düşüktür (genellikle < 1 ms).

---

## 2. WAN (Wide Area Network — Geniş Alan Ağı)

Farklı şehirlerde, ülkelerde veya kıtalarda bulunan yerel ağları (LAN) birbirine bağlayan büyük ölçekli ağ yapısıdır.

- **Kapsam:** Şehirler arası, ülkeler arası veya küresel.
- **Hız:** LAN'a göre daha değişkendir ve servis sağlayıcının sunduğu bant genişliğine bağlıdır.
- **Sahiplik:** Altyapı telekomünikasyon şirketleri ve İnternet Servis Sağlayıcıları (ISP) tarafından sağlanır ve yönetilir.
- **Gecikme:** Mesafeye bağlı olarak LAN'dan daha yüksektir.

---

## 3. Diğer Ağ Türleri (Kısaca)

Temel ağ sınıflandırmasında sıkça duyabileceğiniz diğer iki kavram:

| Ağ Türü | Açılımı | Kapsam | Örnek |
|---|---|---|---|
| **PAN** | Personal Area Network | Kişisel alan (birkaç metre) | Bluetooth kulaklık - telefon bağlantısı |
| **WLAN** | Wireless LAN | Kablosuz yerel alan ağı | Evdeki Wi-Fi ağı |
| **MAN** | Metropolitan Area Network | Bir şehir veya büyük kampüs | Belediye veya üniversite kampüs ağı |

---

## 4. LAN vs WAN Karşılaştırma Tablosu

| Özellik | LAN (Yerel Ağ) | WAN (Geniş Ağ) |
| :--- | :--- | :--- |
| **Coğrafi Kapsam** | Ev, Ofis, Bina | Şehir, Ülke, Kıta, Dünya |
| **Bağlantı Hızı** | Çok Yüksek (1 / 10 Gbps) | Değişken (Mbps – Gbps) |
| **Gecikme (Latency)**| Çok Düşük (< 1 ms) | Daha Yüksek (Mesafeye bağlı) |
| **Maliyet** | Kurulum sonrası ücretsiz/düşük | Sürekli servis aboneliği (ISP) gerektirir |
| **Yönetim / Kontrol**| Yerel sistem yöneticisi | İnternet Servis Sağlayıcıları (ISP) |
| **Temel Cihazlar** | Switch, Access Point, Ethernet Kablosu | Router, Modem, Fiber Omurgalar |

---

## Özet

```
[ Ev / Ofis Cihazları ] ──► ( LAN ) ──► [ Router / Modem ] ──► ( WAN / İnternet ) ──► [ Uzak Sunucu ]
```

- Cihazlarınız yerel ağda (**LAN**) switch üzerinden konuşur.
- Dış dünyaya veya başka bir şubeye çıkmak gerektiğinde router üzerinden geniş alana (**WAN**) aktarılır.

