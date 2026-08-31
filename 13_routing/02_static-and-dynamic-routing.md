# 🗺️ Statik ve Dinamik Routing

Router, bir paketi nereye göndereceğine **Routing Table (Yönlendirme Tablosu)**'na bakarak karar verir.  
Bu tablonun nasıl doldurulduğu iki farklı yöntemle olur: **elle (statik)** veya **otomatik (dinamik)**.

---

## 1. Statik Routing (Elle Yönlendirme)

Ağ yöneticisinin rotaları **manuel olarak** girdiği yöntemdir. Router kendi başına hiçbir şey öğrenmez.

```
Örnek: 10.0.2.0/24 ağına ulaşmak için 192.168.1.2'den geç

Router(config)# ip route 10.0.2.0 255.255.255.0 192.168.1.2
```

### Ne Zaman Kullanılır?

| Durum | Neden Statik? |
|:---|:---|
| Küçük ağ (1–2 router) | Karmaşıklık gereksiz |
| Stub ağ (tek çıkış noktası) | Dinamik protokole gerek yok |
| Güvenlik gereksinimi | Routing güncellemeleri ağda dolaşmaz |
| Default route (0.0.0.0/0) | ISP'ye çıkış için tek satır yeterli |

### Avantajları ve Dezavantajları

| | Statik |
|:---|:---|
| ✅ Basit, öngörülebilir | Konfigürasyon tamamen kontrol altında |
| ✅ Düşük CPU/RAM kullanımı | Protokol overhead'i yok |
| ❌ Ölçeklenemiyor | 100 ağ = 100 satır elle giriş |
| ❌ Arıza toleransı yok | Hat koparsa rota otomatik güncellenmez |

---

## 2. Dinamik Routing (Otomatik Yönlendirme)

Router'ların birbirleriyle **konuşarak** ağ bilgisini otomatik öğrendiği yöntemdir. Bir ağ değiştiğinde (yeni subnet, arıza vb.) tüm router'lar otomatik güncellenir.

```
Router-A ←── "10.0.2.0/24 ağını ben biliyorum" ──→ Router-B
Router-B artık bu bilgiyi kendi tablosuna yazar — elle giriş gerekmez.
```

---

## Yaygın Dinamik Routing Protokolleri

### RIP (Routing Information Protocol)

- **Metrik:** Hop sayısı (maksimum **15 hop**)
- **Güncelleme:** Her 30 saniyede bir tüm tabloyu komşulara gönderir
- **Kapsam:** Küçük ağlar
- **Durum:** Eski, modern ağlarda artık kullanılmıyor

```
A → B → C → D → ...  (her ok = 1 hop)
15 hop'tan fazlası "ulaşılamaz" sayılır.
```

> ⚠️ RIP'in 15 hop sınırı onu büyük ağlarda kullanılamaz kılar.

---

### OSPF (Open Shortest Path First)

- **Metrik:** Bant genişliği (bandwidth) — daha hızlı = daha iyi
- **Algoritma:** Dijkstra (SPF — Shortest Path First)
- **Kapsam:** Orta ve büyük kurumsal ağlar
- **Standart:** Açık (vendor-bağımsız), RFC 2328

```
Router-A, tüm ağın haritasını çıkarır.
En kısa yolu (en yüksek band genişliği) seçer.
Hat koparsa saniyeler içinde alternatif yolu hesaplar.
```

> 💡 OSPF bugün kurumsal ağların büyük çoğunluğunda kullanılan **standart** protokoldür.

---

## Karşılaştırma Tablosu

| | Statik | RIP | OSPF |
|:---|:---:|:---:|:---:|
| **Konfigürasyon** | Elle | Otomatik | Otomatik |
| **Ölçek** | Küçük | Küçük | Büyük |
| **Arıza Toleransı** | ❌ Yok | ✅ Var | ✅ Hızlı |
| **CPU/RAM** | Çok az | Az | Orta |
| **Metrik** | — | Hop sayısı | Bandwidth |
| **Güncel mi?** | ✅ | ❌ (eski) | ✅ |

---

## Default Route — Sihirli Satır

Routing tablosunda eşleşen bir rota yoksa paketi nereye göndereceğini söyleyen özel giriştir.

```
ip route 0.0.0.0 0.0.0.0 192.168.1.1
         ───────────────  ───────────
         "Tüm adresler"   ISP Router (next-hop)
```

> 💡 Ev modeminizdeki tek router'ın routing tablosunda genellikle yalnızca bu tek satır vardır. Nereden gelirse gelsin tüm paketleri ISP'ye gönderir.

---

## Diğer Dinamik Routing Protokolleri

Temel ağ eğitiminin kapsamı dışında kalan ancak adını bilmeniz gereken önemli protokoller de vardır:

| Protokol | Kapsam | Kısa Açıklama |
|:---|:---|:---|
| **BGP** | İnternet (ISP'ler arası) | İnternetin omurga protokolü. Farklı otonom sistemleri birbirine bağlar. |
| **EIGRP** | Kurumsal (Cisco) | Cisco'ya özgü, hızlı yakınsama sağlayan gelişmiş protokol. |
| **IS-IS** | Büyük ISP / Telekom | OSPF'e benzer; büyük servis sağlayıcı ağlarında tercih edilir. |

> 💡 Bu protokoller ileri düzey ağ yönetimi konularıdır ve ayrı bir çalışma gerektirir.

---

## Özet

```
Statik   → Küçük ağ, elle kontrol, arıza toleransı yok
RIP      → Eski, küçük ağ, hop sayısı, 15 hop sınırı
OSPF     → Kurumsal standart, bandwidth metriği, hızlı yakınsama
```
