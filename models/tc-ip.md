## TCP/IP Modeli (4 Katman)

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


> 💡 Günümüzde fiilen kullanılan tek model **TCP/IP'dir.** OSI ise öğretim ve sorun giderme amaçlı referans olarak yaşamaya devam eder.
