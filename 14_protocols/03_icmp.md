# 📮 ICMP (Internet Control Message Protocol)

Ağda her şey yolunda giderken kimse konuşmaz; sorun çıktığında **bildirim** gerekir. ICMP, IP altyapısının "iç yazışma dili"dir: paketler yolculuk sırasında bir yerde takıldığında, hedefe ulaşamadığında ya da geciktiğinde durumu **gönderene bildiren** hata ve teşhis protokolüdür.

> 💡 **Benzetme:** Kargoyu taşıyan kamyonet ICMP değil; kamyonetin kapınıza bırakamadığı paket için arkasında bıraktığı **"bulamadık, geri gönderiyoruz"** kâğıdıdır.

**Protokol numarası: 1** — IP başlığının Protocol alanı `1` ise taşınan yük ICMP'tir. TCP/UDP'nin aksine ICMP'nin **portları yoktur**; doğrudan IP'nin içine sarılır.

---

## ICMP Ne Zaman Konuşur?

| Durum | Kim Kime Ne Söyler? |
|:---|:---|
| Hedef IP yok / ağ bulunamadı | Router → Gönderen: "Destination Unreachable" |
| Paket router'larda dönerken TTL tükendi | Router → Gönderen: "Time Exceeded" |
| Paket büyük, DF bit set'li (parçalanamaz) | Router → Gönderen: "Fragmentation Needed" (MTU keşfinin temeli) |
| Ping atıyorsunuz | Herkes herkese: "Echo Request / Echo Reply" |
| Aynı IP'yi iki cihaz kaptı (ARP/ND) | İlgili host'lar: çakışma bildirimi |

### Başlık Yapısı (8 byte)

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
├───────────┬───────────┬─────────────────────────────────────────┤
│  Type (8) │ Code (8)  │            Checksum (16)                │
├───────────┴───────────┴─────────────────────────────────────────┤
│                     Değişken veri (Identifier, Sequence, veya   │
│               orijinal IP başlığı + ilk 64 bit veri...)          │
└─────────────────────────────────────────────────────────────────┘
```

- **Type:** Mesajın cinsi (aşağıdaki tablo)
- **Code:** Aynı cinsin alt nedeni ("neden ulaşılamadı?")
- **Checksum:** IPv4'te zorunludur.

### En Sık Görülen Type Kodları

| Type | Ad | Ne Anlama Gelir? |
|:---:|:---|:---|
| **0** | Echo Reply | "Buradayım, mesajını aldım" (ping yanıtı) |
| **8** | Echo Request | "Orada mısın?" (ping isteği) |
| **3** | Destination Unreachable | "Paketin hedefe varamadı" — Code: 0=ağ yok, 1=host yok, 3=port yok, 4=**Fragmentation Needed** |
| **5** | Redirect | "Sen yanlış kapıdan çıktın, asıl router şurası" (günümüzde çoğu firewall bunu yutar) |
| **11** | Time Exceeded | "TTL'n bitti, paket çöpe" — traceroute'un yakıtı |

> ⚠️ **Güvenlik notu:** ICMP bilgi sızdırabilir (ağ haritası çıkarmak için kullanılır). Kurumsal firewall'larda Echo Request dışarıdan içeriye genelde **engellenir**; içeriden dışarıya izin verilir. Bu yüzden bazı sunuculara ping atamazsınız — orada değiller, kapıları ICMP'ye kapalıdır.

---

## Ping Mutfakta Neler Döner?

```text
Siz:   ping 8.8.8.8
        │
        ▼
[1] İşletim sistemi ICMP Type 8 (Echo Request) üretir
    → içine Identifier + Sequence + veri koyar
[2] IP başlığına sarar (Protocol=1, TTL=128/64)
[3] Frame'e sarar → kablo/hava → hedef
        │
Hedef: [4] ICMP Type 0 (Echo Reply) geri gönderir
        │
Siz:   [5] "yanıt geldi, süre=14ms, TTL=57"
```

- **Süre (time):** Gidiş+geliş (RTT). Tek yönlü mesafe × ışık hızı + router gecikmeleri.
- **Gelen TTL:** Hedefin başlangıç TTL'inden (Windows 128 / Linux 64) yolda kaç router düştüğünün ipucu.
- **"Request timed out":** Ya yanıt yok ya da arada biri ICMP'yi sessizce düşürüyor.

## Traceroute'un Sırrı: Kasten TTL Bitirmek

```text
Adım 1 → TTL=1 gönder   → İlk router düşürür → "Time Exceeded" (Type 11)
           ↳ Bize kendini (router IP'si) tanıtıyor
Adım 2 → TTL=2 gönder   → 2. router aynı şeyi yapar
Adım 3 → TTL=3 ...      → Her satır = bir hop
...
Hedefe varınca → ICMP Echo Reply veya TCP SYN yanıtı → "ULAŞILDI"
```

Windows'ta `tracert`, Linux'ta `traceroute` bu **Type 11** yanıtlarını tabloya döker:

```text
C:\> tracert google.com
  1     1 ms     1 ms     1 ms  192.168.1.1
  2    12 ms    11 ms    12 ms  10.20.30.1
  3    13 ms    14 ms    13 ms  ankara-gw.isp.net
  ...
```

> 💡 Bir satırda `* * *` görüyorsanız cihaz ICMP'yi yanıtlamıyor (firewall) ya da o noktada paket kaybı var. Bu tek başına arıza demek değildir; son satırdan sonra yanıt zinciri bozulmuşsa sorun oradadır.

---

## IPv6'da ICMPv6 — Sadece Hata Değil, Her Şey

IPv6'da ICMP, yerini daha güçlü **ICMPv6**'ya (Protocol numarası: **58**) bırakır. Yeni yükleri:

- **NDP (Neighbor Discovery Protocol):** ARP'ın yerini aldı — komşu keşfi, adres çözümleme, router duyurusu (RA) artık ICMPv6 mesajlarıdır (Type 133–137).
- **MLD:** Multicast grubuna kimler abone, onu takip eder.
- PTB (Packet Too Big, Type 2): MTU keşfi IPv6'da zorunlu akışın parçası — çünkü IPv6 router'ları **paket parçalamaz**.

> 💡 IPv6 kurulumlarında "ping çalışmıyor" şikayetlerinin kökeni genelde ICMPv6'nın firewall'da engellenmesidir. IPv6'da ICMP **protokol altyapısıdır**; toplu olarak engellemek ağı bozar.

---

## Özet

```text
ICMP     = IP'nin (proto 1) hata + teşhis dili; portları YOKTUR
Type 8/0 = ping (Echo Request/Reply)
Type 11  = traceroute'un hammaddesi (Time Exceeded)
Type 3   = "ulaşamadım", Code 4 = MTU keşfi (Fragmentation Needed)
ICMPv6   = IPv6'nın her şeyi: NDP, RA, multicast — engelleme, çalışmaz
Ping yanıt vermiyorsa = orada olmadığı anlamına gelmez; kapıyı ICMP'ye kapatmış olabilir
```
