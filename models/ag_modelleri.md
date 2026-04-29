# Ağ Modelleri

Ağ iletişiminin nasıl çalışacağını tanımlayan standart çerçevelerdir.
Farklı üreticilerin cihazlarının birbiriyle konuşabilmesi için ortak bir dil sağlarlar.

## 1. OSI Modeli (7 Katman)..

ISO tarafından geliştirilen teorik referans modelidir.
"Veri nasıl iletilmeli?" sorusuna katmanlı bir cevap verir.
Pratikte doğrudan kullanılmaz; eğitim ve sorun giderme amaçlı referans olarak kullanılır.

| No | Katman | PDU | Görev | Örnek |
|---|---|---|---|---|
| 7 | Uygulama | Veri | Kullanıcıya en yakın katman | HTTP, FTP, DNS, SMTP |
| 6 | Sunum | Veri | Format, şifreleme, sıkıştırma | SSL/TLS, JPEG, ASCII |
| 5 | Oturum | Veri | Bağlantı açma/kapama/yönetme | NetBIOS, RPC |
| 4 | Taşıma | Segment | Uçtan uca iletim, hata kontrolü | TCP, UDP |
| 3 | Ağ | Paket | IP adresleme, yönlendirme | IP, ICMP, Router |
| 2 | Veri Bağlantı | Frame | MAC adresleme, hata tespiti | Ethernet, Switch |
| 1 | Fiziksel | Bit | Elektrik sinyali, kablo | UTP, Fiber, Hub |

### Enkapsülasyon (Veri Akışı)

Gönderici tarafta veri **yukarıdan aşağıya** inerek her katmanda başlık bilgisi eklenir:

```
Uygulama   →  Veri
Taşıma     →  TCP Başlığı  + Veri           (Segment)
Ağ         →  IP Başlığı   + Segment        (Paket)
Veri Bağ.  →  MAC Başlığı  + Paket          (Frame)
Fiziksel   →  101010...                      (Bit)
```

Alıcı tarafta ise **aşağıdan yukarıya** çıkarak her katman kendi başlığını söker (dekapsülasyon).

---

## 2. TCP/IP Modeli (4 Katman)

DARPA tarafından geliştirilen ve pratikte kullanılan gerçek modeldir. OSI'nin sadeleştirilmiş halidir. İnternetin çalıştığı model budur.

| No | Katman | OSI Karşılığı | Örnek |
|---|---|---|---|
| 4 | Uygulama | OSI 5 + 6 + 7 | HTTP, FTP, DNS, SMTP |
| 3 | Taşıma | OSI 4 | TCP, UDP |
| 2 | İnternet | OSI 3 | IP, ICMP |
| 1 | Ağ Erişimi | OSI 1 + 2 | Ethernet, Wi-Fi |

### TCP — Güvenilir İletim

Bağlantı odaklıdır. Veri göndermeden önce **3-way handshake** ile bağlantı kurar:

```
İstemci  →  SYN         →  Sunucu
İstemci  ←  SYN-ACK     ←  Sunucu
İstemci  →  ACK         →  Sunucu
           Bağlantı kuruldu
```

### TCP vs UDP

| | TCP | UDP |
|---|---|---|
| Bağlantı | Bağlantı odaklı | Bağlantısız |
| Güvenilirlik | Garantili | Garantisiz |
| Hız | Daha yavaş | Daha hızlı |
| Sıralama | Var | Yok |
| Kullanım | HTTP, FTP, SSH | DNS, VoIP, Video |

---

## 3. Diğer Modeller

Tarihsel süreçte geliştirilmiş, günümüzde büyük çoğunluğu kullanımdan kalkmış modellerdir.

| Model | Geliştiren | Dönem | Durum |
|---|---|---|---|
| **OSI** | ISO | 1984 | Teorik referans olarak aktif |
| **TCP/IP** | DARPA | 1970'ler | Aktif — internetin temeli |
| **DoD** | ABD Savunma Bakanlığı | 1970'ler | TCP/IP ile özdeş |
| **AppleTalk** | Apple | 1985 | Kullanımdan kalktı |
| **IPX/SPX** | Novell | 1980'ler | Kullanımdan kalktı |
| **NetBEUI** | Microsoft / IBM | 1985 | Kullanımdan kalktı |


> Günümüzde fiilen kullanılan tek model **TCP/IP'dir.**
> OSI ise öğretim ve sorun giderme amaçlı referans olarak yaşamaya devam eder.
