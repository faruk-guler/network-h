# 🗣️ Ağda Trafik ve Haberleşme Türleri

Bir ağ üzerindeki cihazlar, hedefin kim olduğuna ve verinin nasıl dağıtılacağına bağlı olarak **4 temel iletim yöntemi** kullanırlar: **Unicast**, **Multicast**, **Broadcast** ve **Anycast**.

---

## 1. Unicast — Bire Bir İletim (1 → 1)

Bir kaynaktan **yalnızca tek bir hedef cihaza** yapılan doğrudan iletimdir. Ağdaki en yaygın trafik türüdür.

* **Nasıl Çalışır:** Veri paketi yalnızca hedef cihazın IP ve MAC adresine yönlendirilir. Ağdaki diğer cihazlar bu paketi görmez ve işlemez.
* **Gerçek Hayat Benzetmesi:** Bir arkadaşınıza doğrudan posta/mektup göndermek veya telefonla bire bir konuşmak.

**Kullanım Alanları ve Örnekler:**
- Bir web sitesini tarayıcıda açmak (HTTP/HTTPS)
- Birine özel mesaj göndermek (WhatsApp, e-posta)
- Dosya indirmek veya sunucuya dosya yüklemek (FTP, SSH)

---

## 2. Multicast — Gruba İletim (1 → Belirli Bir Grup)

Bir kaynaktan **yalnızca belirli bir gruba üye olan cihazlara** yapılan iletimdir.

* **Nasıl Çalışır:** Ağdaki her cihaz veriyi almaz. Yalnızca o yayın grubuna (Multicast Grubu) abone olmuş/katılmış cihazlar veriyi işler. Ağ bant genişliğini korur; aynı veriyi 100 kişiye 100 ayrı unicast paketle göndermek yerine tek bir multicast akışıyla iletir.
* **Gerçek Hayat Benzetmesi:** Bir radyo istasyonunun yayını veya bir WhatsApp grubuna mesaj atmak (yalnızca kanala/gruba katılanlar dinler).

**Kullanım Alanları ve Örnekler:**
- Canlı TV yayınları ve IPTV
- Kurumsal ağlarda çok katılımcılı video konferanslar
- Online çok oyunculu oyunlarda oyunculara eş zamanlı konum güncellemeleri
- Ağ cihazlarının birbirleriyle yönlendirme bilgisi paylaşması (OSPF: `224.0.0.5`, `224.0.0.6`)

---

## 3. Broadcast — Herkese İletim (1 → Herkes)

Bir kaynaktan **aynı yerel ağdaki (Broadcast Domain) tüm cihazlara** yapılan iletimdir.

* **Nasıl Çalışır:** Veri paketi yerel ağdaki istisnasız her cihaza ulaşır. Cihazlar istemeseler dahi bu paketi alıp incelemek zorundadır. Subnet içindeki tüm host bitlerinin `1` olduğu adres (örneğin `/24` için `.255`) veya genel broadcast adresi olan `255.255.255.255` kullanılır.
* **Kritik Kural:** Router'lar broadcast paketlerini **asla diğer ağlara geçirmez (bloke eder)**. Aksi takdirde dünya genelindeki tüm cihazlar birbirinin broadcast trafiğinde boğulurdu.
* **Gerçek Hayat Benzetmesi:** Bir okulda veya havalimanında hoparlörden tüm binaya anons yapmak.

**Kullanım Alanları ve Örnekler:**
- Bilgisayarın ağa ilk bağlandığında IP adresi istemesi (**DHCP Discover**)
- Bir IP adresinin kime ait olduğunu bulmak için MAC adresini sormak (**ARP Request**)
- Ağdaki yazıcı veya paylaşılan kaynakları otomatik keşfetmek

> ⚠️ **IPv6 Notu:** IPv6 mimarisinde ağ performansını düşürdüğü ve fırtınalara (Broadcast Storm) yol açtığı için **Broadcast tamamen kaldırılmıştır.** Yerine daha verimli olan **Multicast** ve **Anycast** getirilmiştir.

---

## 4. Anycast — En Yakına İletim (1 → En Yakın Olan)

Aynı IP adresinin **dünya genelindeki birden fazla sunucuya** atandığı ve kullanıcının paketi **coğrafi / ağsal olarak kendisine en yakın sunucuya** ilettiği modern bir yöntemdir.

> 💡 **Benzetme:** Bir kahve zincirinin şehirde onlarca şubesi vardır. Google Haritalar'dan "En yakın şube" dediğinizde harita sizi Kadıköy'deyseniz Kadıköy şubesine, Beşiktaş'taysanız Beşiktaş şubesine yönlendirir. İsim ve menü aynıdır ama gittiğiniz yer size en yakın olandır.

### Anycast Nasıl Çalışır?

```text
               [DNS Sunucu — Frankfurt]
               IP: 8.8.8.8
                    ▲
İstanbul'daki       │  BGP Yönlendirmesi: "En kısa yol Frankfurt (15ms)"
kullanıcı ──────────┤
                    │  BGP Yönlendirmesi: "Singapur uzak yol (140ms)"
                    ▼
               [DNS Sunucu — Singapur]
               IP: 8.8.8.8
```

1. Dünya çapındaki birçok veri merkezinde bulunan sunucular aynı IP adresini (örn: `8.8.8.8`) internete duyurur (BGP protokolü ile).
2. Kullanıcının internet sağlayıcısı, yönlendirme tablosuna bakarak paketi ağ açısından **en yakın/en hızlı** sunucuya iletir.
3. Bir veri merkezinde arıza olursa trafik otomatik olarak bir sonraki en yakın merkeze kayar.

**Kullanım Alanları ve Örnekler:**
- **DNS Sunucuları:** Google DNS (`8.8.8.8`), Cloudflare DNS (`1.1.1.1`)
- **CDN (İçerik Dağıtım Ağları):** Cloudflare, Akamai (Web sitelerini kullanıcıya en yakın ülkeden açar)
- **DDoS Koruması:** Gelen devasa saldırı trafiğini dünya geneline yayarak tek bir sunucunun çökmesini engeller.
- **IPv6:** IPv6 protokolünde Anycast mimari olarak yerel (native) desteklenir (RFC 4291).

## 📌 Kısa Özet

```text
Unicast   → Bire bir görüşme (Tek hedefe)
Multicast → Gruba özel yayın (Yalnızca ilgilenenlere)
Broadcast → Herkese anons (Ağdaki tüm cihazlara — IPv6'da yok)
Anycast   → En yakın noktaya yönlendirme (Aynı IP, çoklu lokasyon)
```
