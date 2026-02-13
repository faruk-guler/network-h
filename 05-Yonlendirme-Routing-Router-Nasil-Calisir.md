# 05 - Yönlendirme (Routing): İnternetin Trafik Polisi

Farklı ağların (farklı subnetlerin) birbiriyle konuşmasını sağlayan işleme **Routing**, bu işi yapan donanıma **Router** denir.

> 💡 **Benzetme:** Router, şehirler arası kavşaklarda duran bir trafik polisidir. Her pakete "sen bu yoldan git" der ve en kısa/hızlı rotayı seçer.

---

## 🛣️ Router (Yönlendirici)

- **Görevi:** Farklı ağları birbirine bağlar ve paketleri "en iyi yoldan" hedefe ulaştırır
- **OSI Katmanı:** 3. Katman (Network) cihazıdır. IP adreslerine bakar
- **Benzetme:** Router bir "trafik polisi" veya "navigasyon cihazıdır (GPS)". Hangi yoldan giderseniz hedefe varacağınıza karar verir

### Router Ne Yapar?

1. Gelen paketteki **hedef IP adresini** okur
2. **Routing tablosuna** bakar → "Bu IP hangi yöndedir?"
3. Paketi **doğru interface**'den yollar
4. Gerekirse **TTL (Time to Live)** değerini 1 azaltır

```text
Ağ A (192.168.1.0/24) ←→ [Router] ←→ Ağ B (192.168.2.0/24)
                              ↕
                    Ağ C (10.0.0.0/8) → İnternet
```

---

## 🚪 Ağ Geçidi (Gateway)

- Bir ağdaki cihazların, "dış dünyaya" (kendi ağları haricindeki her yere, örn: İnternete) çıkmak için kullandıkları kapıdır
- Ev ağınızda Gateway, genellikle modem/router'ınızın IP adresidir (Örn: `192.168.1.1`)
- Bilgisayarınız hedef IP'nin kendi ağında olmadığını fark ederse, paketi direkt Gateway'e teslim eder: "Ben bunu tanımıyorum, sen ulaştır."

### Default Gateway Neden Önemli?

```text
PC (192.168.1.10) → google.com'a erişmek istiyor

Adım 1: PC, "142.250.185.78 benim ağımda mı?" → Hayır!
Adım 2: PC, paketi Default Gateway'e (192.168.1.1) gönderir
Adım 3: Router, paketi internete yönlendirir
```

---

## 📜 Yönlendirme Tablosu (Routing Table)

Router'ın içinde, hangi ağın hangi yönde olduğunu tutan bir harita (GPS veritabanı) vardır.

### Örnek Routing Tablosu

| Hedef Ağ    | Alt Ağ Maskesi | Ağ Geçidi          | Arayüz | Metrik |
| :---------- | :------------- | :----------------- | :----- | :----- |
| 192.168.1.0 | /24            | Directly Connected | Gi0/0  | 0      |
| 192.168.2.0 | /24            | Directly Connected | Gi0/1  | 0      |
| 10.0.0.0    | /8             | 192.168.1.254      | Gi0/0  | 10     |
| 0.0.0.0     | /0             | 203.0.113.1        | Gi0/2  | 1      |

> 💡 **`0.0.0.0/0`** = **Varsayılan Rota (Default Route)** = "Bilmediğim her şeyi buraya gönder" (İnternete çıkış)

---

## 🔀 Routing Türleri

### 1. Static Routing (Statik Yönlendirme)

Yolları **ağ yöneticisi elle** yazar.

**Komut (Cisco):**

```text
Router(config)# ip route 10.0.0.0 255.0.0.0 192.168.1.254
```

**Avantajları:**

- Basit ve güvenli
- CPU/bellek yükü yok
- Küçük ağlar için ideal

**Dezavantajları:**

- Büyük ağlarda yönetimi zordur
- Link kesintisinde otomatik yol değişikliği yapmaz
- Ölçeklenebilir değil

---

### 2. Dynamic Routing (Dinamik Yönlendirme)

Router'lar birbirleriyle konuşarak yolları **otomatik öğrenirler**.

**Yaygın Dinamik Routing Protokolleri:**

| Protokol  | Tür             | Kullanım Alanı           | Metrik                  |
| :-------- | :-------------- | :----------------------- | :---------------------- |
| **RIPv2** | Distance Vector | Küçük ağlar              | Hop Count (maksimum 15) |
| **OSPF**  | Link State      | Orta-büyük ağlar         | Cost (bant genişliği)   |
| **EIGRP** | Hybrid          | Cisco ağları             | Bandwidth + Delay       |
| **BGP**   | Path Vector     | İnternet (ISP'ler arası) | AS Path                 |

**Avantajları:**

- Otomatik yol keşfi
- Link kesintisinde otomatik yeniden yönlendirme
- Büyük ağlarda ölçeklenebilir

**Dezavantajları:**

- CPU ve bellek kullanır
- Konfigürasyonu daha karmaşık

---

## 🎯 Routing Kavramları

### Longest Prefix Match (En Uzun Önek Eşleşmesi)

Bir paket birden fazla route ile eşleşirse, router **en spesifik route**'u seçer.

**Örnek:**

```text
Routing tablosunda:
  - 10.0.0.0/8    → Gateway A
  - 10.1.0.0/16   → Gateway B
  - 10.1.1.0/24   → Gateway C

Paket hedefi: 10.1.1.50
→ En spesifik: 10.1.1.0/24 → Gateway C seçilir ✅
```

> 💡 **/24 > /16 > /8** → En uzun prefix = en spesifik route = kazanan!

---

### Metrik (Routing Cost / Maliyet)

Router'ın birden fazla yolu varsa, **metrik değeri en düşük** olanı (en ucuz/hızlı yolu) seçer.

> 💡 **Benzetme:** Otoyol (ücretli ama hızlı) vs Köy Yolu (ücretsiz ama yavaş). Router her zaman "maliyeti" en az olanı seçer.

**Metrik türleri:**

- **Hop Count:** Kaç router'dan geçilecek? (RIP)
- **Bandwidth:** Bağlantının hızı (OSPF)
- **Delay:** Gecikme süresi (EIGRP)
- **Cost:** Genel maliyet hesabı

```text
Yol A: 3 hop, 100 Mbps → Metrik: 30
Yol B: 2 hop, 1 Gbps   → Metrik: 10  ← Bu seçilir!
```

---

### Administrative Distance (AD)

Birden fazla routing protokolü aynı hedefe farklı yollar sunarsa, **AD değeri en düşük** olan kazanır.

| Kaynak             | AD Değeri |
| :----------------- | :-------- |
| Directly Connected | 0         |
| Static Route       | 1         |
| EIGRP              | 90        |
| OSPF               | 110       |
| RIP                | 120       |
| Unknown            | 255       |

---

## 🌐 NAT (Network Address Translation)

Router'ların en hayati görevlerinden biri de **NAT** yapmaktır. Bu teknoloji sayesinde, evinizdeki onlarca cihaz tek bir internet hattı üzerinden dünyaya bağlanabilir.

### Neden Gerekli?

IPv4 adresleri (yaklaşık 4 milyar adet) dünya nüfusuna yetmiyor. NAT, **Private (Özel)** IP adreslerinizin internete çıkarken tek bir **Public (Genel)** IP adresine dönüşmesini sağlar.

### Nasıl Çalışır? (Resepsiyon Metaforu)

Bir otelde kaldığınızı düşünün. Otelin dışarıdan tek bir adresi vardır, ama içeride yüzlerce oda (PC’ler) bulunur.

1. Dışarıdan size (302 nolu oda) bir paket gelirse, önce resepsiyona (Router) gelir.
2. Resepsiyon, paketin hangi odaya ait olduğunu bildiği bir tabloya (NAT Table) bakar.
3. Paketi size ulaştırır.

### Temel NAT Türleri

- **Static NAT:** Bir yerel IP, her zaman aynı dış IP'ye çevrilir (Sunucular için).
- **Dynamic NAT:** Bir havuzdaki dış IP'ler, cihazlara sırayla atanır.
- **PAT (Port Address Translation):** En yaygın türdür. Tüm iç cihazlar aynı dış IP üzerinden, farklı **Port** numaralarıyla internete çıkar.

---

## 🔍 Routing Sorun Giderme

### Temel Komutlar

**Windows:**

```text
route print           # Routing tablosunu göster
tracert google.com    # Paket rotasını izle
pathping google.com   # Detaylı yol analizi
```

**Linux:**

```text
ip route show         # Routing tablosunu göster
traceroute google.com # Paket rotasını izle
mtr google.com        # Sürekli rota izleme
```

**Cisco Router:**

```text
show ip route          # Routing tablosu
show ip protocols      # Çalışan routing protokolleri
show ip interface brief # Interface durumları
```

---

## 💡 Routing İpuçları

1. **Küçük ağlar** (< 10 subnet): Static routing yeterlidir
2. **Orta ağlar** (10-100 subnet): OSPF kullanın
3. **Büyük ağlar** (şirket): OSPF + redistribution
4. **İnternet/ISP**: BGP zorunludur
5. **Her zaman** default route tanımlayın (`0.0.0.0/0`)

---

**Navigasyon:**

- [⬅️ Önceki: IPv6 Derinlemesine](./04-IP-Adresleme-ve-Subnetting-IPv6-Derinlemesine.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Uygulama Protokolleri](./06-Uygulama-Protokolleri-DNS-DHCP-HTTP.md)
