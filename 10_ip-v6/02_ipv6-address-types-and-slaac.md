# 🏷️ IPv6 Adres Kümeleri ve SLAAC

IPv6'da adresin **ilk haneleri**, onun ne işe yaradığını söyler. Bir de cihazın DHCP'ye ihtiyaç duymadan kendi adresini üretebilmesi vardır: **SLAAC**. Bu bölümün konusu sadece bunlar ikisi.

> 💡 **Benzetme:** Posta adresi gibi — **şehir** ISP'den gelir, **sokak** sizin alt ağınız, **kapı numarası** cihazın kendisidir.

---

## Baş Harflere Bak, Adresi Tanı

| Başlangıç | Adı | Karşılığı | Ne işe yarar? |
|:---:|:---|:---|:---|
| `2xxx:` | **Global** | Public IP | İnternete açık gerçek adres |
| `fdxx:` | **ULA** | `192.168.x.x` | Özel ağ; internette yönlendirilmez |
| `fe80::` | **Link-Local** | — | Her arayüzde otomatik oluşur; sadece aynı ağdaki komşularla konuşur |
| `ff..:` | **Multicast** | Broadcast yerine | Yalnızca ilgilenen gruba yayın |

> 💡 IPv6'da broadcast yoktur. `::1` ise loopback'tir.

---

## Global Adresin Anatomisi

```text
2a02:3344:33bb : 0042 : 021a:2bff:fe3c:4d5e
└──── şehir (ISP) ────┘ └sokak┘ └──── kapı numarası ────┘
```

Sokak kısmı sizindir: her kata/departmana bir alt ağ verirsiniz. **Altın kural:** her alt ağ **/64** olsun — kapı numarası 64 bite oturmak zorundadır, bu yüzden alt ağ bölgeleri IPv6'da küçültülmez.

---

## SLAAC — Adresini Kendi Üreten Cihaz

Router bir kere fısıldar, cihaz gerisini kendisi halleder:

1. **Router duyurusu (RA):** "Bu ağın sokak adı `2a02:3344:33bb:1::/64`" — periyodik olarak ilan eder.
2. **Cihaz yazar:** Sokak adının sonuna kendi kapı numarasını ekler (genelde MAC adresinden türetilir).
3. **Doğrulama (DAD):** "Bu adresi kullanan var mı?" diye sorar; itiraz gelmezse adresi kullanır.

> 💡 Sunucu hiçbir şey hatırlamaz — "durumsuz" (stateless) adının sebebi bu. Cihazlar aynı ağda `fe80::` üzerinden anlaşırlar; bu yüzden `ipconfig` çıktısında ağ geçidi `fe80::1` gibi görünür — **hata değil, doğaldır.** Takip edilmemek için işletim sistemleri bir de geçici (privacy) adres üretir; birden fazla `2xxx:` satır görmek normaldir.

---

## Özet

```text
2xxx: → Global | fdxx: → ULA | fe80:: → Link-Local | ff..: → Multicast (broadcast yok)
Her alt ağ /64 — küçültme yok
SLAAC: RA duyurur → cihaz kapı numarasını yazar → DAD ile doğrular → adres hazır
```
