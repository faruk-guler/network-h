# Ağda Haberleşme Türleri

Haberleşme türleri bağlama göre farklılık gösterir:

| Kapsam | Türler |
|---|---|
| Temel eğitim (IPv4) | 3 — Unicast, Multicast, Broadcast |
| IPv6 | 3 — Unicast, Multicast, Anycast |
| Modern genel ağ | 4 — Unicast, Multicast, Broadcast, Anycast |
| İleri düzey | 5 — + Incast |

---

## 1) Unicast

Bir cihazdan **sadece bir** cihaza yapılan iletim.

Gönderici ile alıcı arasında bire bir iletişim kurulur. Veri paketi yalnızca hedef cihaza ulaşır, ağdaki diğer cihazlar bu iletimi görmez.

**Gerçek hayattan örnekler:**

- Tarayıcınızdan bir web sitesine istek göndermek (HTTP/HTTPS)
- WhatsApp'ta birine mesaj atmak
- Bir sunucuya SSH bağlantısı açmak
- E-posta göndermek (SMTP)
- VoIP ile bire bir sesli arama yapmak

---

## 2) Multicast

Bir cihazdan **belirli bir gruba** üye cihazlara yapılan iletim.

Veri paketi, ilgili gruba kayıtlı olan cihazlara iletilir. Gruba üye olmayan cihazlar bu veriyi almaz. Böylece bant genişliği verimli kullanılır.

**Gerçek hayattan örnekler:**

- Canlı yayın platformlarında video akışı (IPTV, online konser)
- Kurumsal ağlarda videokonferans (sadece toplantıya katılanlar alır)
- Borsa veri akışları (abone olan kullanıcılara anlık fiyat gönderimi)
- Yönlendiriciler arasındaki routing protokolleri (OSPF, RIP v2)
- Online oyunlarda aynı sunucudaki oyunculara konum güncellemesi

---

## 3) Broadcast

Bir cihazdan **ağdaki tüm** cihazlara yapılan iletim.

Veri paketi, ağdaki her cihaza gönderilir. Yalnızca IPv4'te desteklenir; IPv6'da broadcast yoktur, yerini Multicast almıştır. Ağın son host IP adresi (`.255`) broadcast için kullanılır.

**Gerçek hayattan örnekler:**

- DHCP: Bilgisayarın ağa bağlandığında IP adresi istemesi (`192.168.1.255`)
- ARP: Bir cihazın MAC adresini öğrenmek için tüm ağa sorması
- Ağdaki yazıcıları veya paylaşılan kaynakları keşfetme (NetBIOS)
- Yönlendiricinin ağ yapılandırmasını duyurması
- Wake-on-LAN: Ağdaki bir cihazı uzaktan uyandırma paketi

---

## 4) Anycast

Bir cihazdan **en yakın veya en uygun** cihaza yapılan iletim.

Aynı IP adresine sahip birden fazla sunucu farklı konumlarda bulunur. Gönderilen paket, ağ topolojisine göre bu sunucuların en yakınına yönlendirilir. IPv6'da native olarak desteklenir; IPv4'te BGP protokolü üzerinden uygulanabilir.

**Gerçek hayattan örnekler:**

- Google DNS (`8.8.8.8`): Dünyada onlarca sunucu aynı IP'yi paylaşır, sorgu en yakınına gider
- Cloudflare DNS (`1.1.1.1`): Aynı mantıkla küresel ölçekte çalışır
- CDN (Content Delivery Network): İçerik isteği coğrafi olarak en yakın sunucudan karşılanır
- IPv6 yönlendirici keşfi: Cihaz, en yakın yönlendiriciye ulaşmak için anycast kullanır
- DDoS koruması: Saldırı trafiği anycast ile birden fazla noktaya dağıtılarak absorbe edilir

---

## 5) Incast

**Birden fazla kaynaktan tek bir hedefe** eş zamanlı yapılan iletim.

Unicast'ın tersi gibi düşünülebilir: çok-tek (many-to-one) iletişimdir. Özellikle veri merkezi ağlarında karşılaşılır. Çok sayıda sunucunun aynı anda aynı hedefe veri göndermesi ağda tıkanıklığa (incast collapse) yol açabilir.

**Gerçek hayattan örnekler:**

- Bir depolama sunucusundan paralel veri okuma yapan birden fazla uygulama sunucusu
- MapReduce iş yüklerinde tüm worker node'ların sonuçları master node'a göndermesi
- Mikro servis mimarisinde bir servisin paralel API çağrılarının tek noktada toplanması
- Dağıtık veritabanlarında küme içi senkronizasyon trafiği
- CDN'de orijin sunucuya ani ve yoğun geri dönüş trafiği

---

## Karşılaştırma

| Özellik | Unicast | Multicast | Broadcast | Anycast | Incast |
|---|---|---|---|---|---|
| Yön | 1 → 1 | 1 → grup | 1 → hepsi | 1 → en yakın | çok → 1 |
| Bant genişliği | Düşük | Orta | Yüksek | Düşük | Yüksek |
| Ölçeklenebilirlik | Yüksek | Orta | Düşük | Çok yüksek | Düşük |
| IP Sürümü | IPv4/IPv6 | IPv4/IPv6 | Yalnızca IPv4 | Ağırlıklı IPv6 | IPv4/IPv6 |
| Örnek IP | `192.168.1.5` | `224.0.0.1` | `192.168.1.255` | `8.8.8.8` | — |
| Kullanım | HTTP, SSH, e-posta | IPTV, OSPF | DHCP, ARP | DNS, CDN | Veri merkezi |
