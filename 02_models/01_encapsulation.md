# 📦 Enkapsülasyon ve Dekapsülasyon

Bir uygulama veri gönderdiğinde, o veri fiziksel kabloya ulaşmadan önce her katmanda bir "zarf" daha geçirilir. Buna **enkapsülasyon** denir.

> 💡 **Benzetme:** Kargo gönderiyorsunuz. Ürünü naylona sararsınız, kutuya koyarsınız, üstüne adres etiketini yapıştırırsınız. Her adımda bir katman daha eklenir. Alıcı ise tam tersine — önce etiketi, sonra kutuyu, sonra naylonu açar. Ağda da aynı mantık geçerlidir.

---

## Her Katmanın Bir PDU'su Var

Veri her katmandan geçerken farklı bir isim alır:

| Katman | PDU Adı | Ne Eklenir? |
|:---|:---:|:---|
| 7 — Uygulama | **Veri** | Ham uygulama verisi (HTTP isteği, e-posta) |
| 4 — Taşıma | **Segment** | Port numaraları (kaynak & hedef) |
| 3 — Ağ | **Paket** | IP adresleri (kaynak & hedef), TTL |
| 2 — Veri Bağlantı | **Frame** | MAC adresleri + hata kontrol (FCS) |
| 1 — Fiziksel | **Bit** | Elektrik sinyali / ışık / radyo dalgası |

---

## Enkapsülasyon: Gönderici (Yukarıdan Aşağıya)

```text
Uygulama  →  [ Veri ]
Taşıma    →  [ TCP Başlığı | Veri ]
Ağ        →  [ IP Başlığı | TCP Başlığı | Veri ]
Veri Bağ. →  [ MAC | IP Başlığı | TCP Başlığı | Veri | FCS ]
Fiziksel  →  01001000 01010100 ...
```

Her katman **yalnızca kendi başlığını** ekler; altındaki katmana ne olduğuyla ilgilenmez.

## Dekapsülasyon: Alıcı (Aşağıdan Yukarıya)

```text
Fiziksel  →  Bitleri alır, frame'e çevirir
Veri Bağ. →  MAC adresini kontrol eder, FCS ile hata denetler, MAC başlığını soyar
Ağ        →  Hedef IP'yi kontrol eder, IP başlığını soyar
Taşıma    →  Port numarasına bakarak uygulamayı belirler, TCP başlığını soyar
Uygulama  →  Ham veriyi alır → tarayıcı sayfayı çizer
```

---

## Router'da Ne Olur?

Router bir paket aldığında yalnızca **IP başlığını** okur, routing tablosuna bakar ve paketi doğru porta yönlendirir. Bunu yaparken:

- **IP adresleri değişmez** — kaynak ve hedef tüm yolculuk boyunca aynı kalır
- **MAC adresleri her atlamada değişir** — her router yeni bir MAC başlığı takar

```text
Cihaz → [MAC: Router] → Router → [MAC: Sunucu] → Sunucu
         MAC değişti              MAC değişti
         IP aynı kaldı            IP aynı kaldı
```

---

## Özet

| Terim | Açıklama |
|:---|:---|
| **Enkapsülasyon** | Göndericide her katman başlık ekler (yukarı → aşağı) |
| **Dekapsülasyon** | Alıcıda her katman kendi başlığını soyar (aşağı → yukarı) |
| **PDU** | Her katmandaki verinin adı (Veri / Segment / Paket / Frame / Bit) |
| **Altın Kural** | IP adresleri değişmez — MAC adresleri her hop'ta yenilenir |
