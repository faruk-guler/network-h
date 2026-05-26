## 1. ping — Bağlantı Testi

**Ping**, bir ağ üzerindeki cihazların erişilebilir olup olmadığını test etmek için kullanılan temel araçtır. 1983 yılında *Mike Muuss* tarafından geliştirilmiştir.

Hedef cihaza **32 byte** boyutunda bir **ICMP paketi** gönderilir ve geri dönen yanıt analiz edilir:

| Bilgi | Açıklama |
|---|---|
| Erişilebilirlik | Hedef cihaz açık ve aktif mi? |
| Paket Kaybı | Ağda veri kaybı yaşanıyor mu? |
| Gecikme (ms) | İki cihaz arasındaki iletişim süresi |

> **💡 TTL (Time to Live):** Paketin geçtiği her ağ cihazında 1 azalır. Değer **0**'a ulaşınca cihaz paketi düşürür. Bu mekanizma sonsuz döngüleri engeller.

### Kullanım

```cmd
ping google.com
ping 192.168.1.1
ping -t google.com        # Sürekli ping (durdurmak için CTRL+C)
ping -n 10 google.com     # 10 paket gönder
```

### Örnek Çıktı

```
C:\> ping google.com

google.com [142.250.185.78] için ping atılıyor 32 bayt veriyle:
142.250.185.78 yanıtı: bayt=32 süre=14ms TTL=117
142.250.185.78 yanıtı: bayt=32 süre=13ms TTL=117
142.250.185.78 yanıtı: bayt=32 süre=15ms TTL=117
142.250.185.78 yanıtı: bayt=32 süre=14ms TTL=117

142.250.185.78 için Ping istatistikleri:
    Paketler: Gönderildi = 4, Alındı = 4, Kayıp = 0 (%0 kayıp),
Gidiş dönüş sürelerinin yaklaşık değeri (milisaniye cinsinden):
    En az = 13ms, En fazla = 15ms, Ortalama = 14ms
```

---

## 2. tracert — Rota İzleme

Paketlerin hedefe ulaşırken **hangi güzergahı izlediğini** ve **hangi router'lardan geçtiğini** gösterir. Ağdaki gecikme veya kopukluğun tam olarak nerede yaşandığını tespit etmek için kullanılır.

### Kullanım

```cmd
tracert google.com
tracert 192.168.1.1
tracert -d google.com     # DNS çözümlemesi yapma, daha hızlı sonuç
```

### Örnek Çıktı

```
C:\> tracert google.com

google.com [142.250.185.78] için rota izleniyor,
En fazla 30 atlama:

  1     1 ms     1 ms     1 ms  192.168.1.1          ← Modem/Router
  2    12 ms    11 ms    12 ms  10.20.30.1           ← ISS ilk geçidi
  3    13 ms    14 ms    13 ms  ankara-gw.isp.net    ← ISS Ankara
  4    20 ms    19 ms    21 ms  istanbul-gw.isp.net  ← ISS İstanbul
  5    22 ms    22 ms    23 ms  72.14.203.1          ← Google ağı girişi
  6    14 ms    13 ms    14 ms  142.250.185.78       ← Hedef

İzleme tamamlandı.
```

> **💡 İpucu:** Eğer bir satırda `* * *` görüyorsanız, o router ICMP paketlerine yanıt vermiyordur ya da paket kaybolmuştur.

---

## 3. arp -a — MAC Adresi Tablosu

Ağdaki cihazlarla haberleşmek için IP adresi yeterli değildir, **MAC adresi** de gerekir. ARP protokolü bu iki bilgi arasındaki köprüyü kurar ve öğrenilen eşleşmeleri **ARP önbelleğinde** saklar. Böylece her seferinde broadcast yapmak zorunda kalınmaz.

### Kullanım

```cmd
arp -a                    # Tüm ARP tablosunu göster
arp -a 192.168.1.1        # Belirli bir IP için ARP kaydı
arp -d                    # ARP önbelleğini temizle
```

### Örnek Çıktı

```
C:\> arp -a

Arabirim: 192.168.1.100 --- 0x5
  İnternet Adresi       Fiziksel Adres        Tür
  192.168.1.1           d4-6e-0e-1a-2b-3c     dinamik   ← Modem/Router
  192.168.1.105         a8-51-5b-7f-9d-11     dinamik   ← Ağdaki başka cihaz
  192.168.1.255         ff-ff-ff-ff-ff-ff     statik    ← Broadcast adresi
  224.0.0.22            01-00-5e-00-00-16     statik
  255.255.255.255       ff-ff-ff-ff-ff-ff     statik
```

---

## 4. nslookup — DNS Sorgulama

**nslookup**, domain adları ile IP adresleri arasındaki ilişkiyi sorgulamak için kullanılan bir DNS aracıdır. TCP/IP protokol paketiyle birlikte gelir.

Temel kullanım alanları:
- Bir domain'in hangi IP adresine çözümlendiğini öğrenmek
- DNS sunucusunun düzgün çalışıp çalışmadığını kontrol etmek
- A, MX, NS gibi DNS kayıtlarını incelemek

### Kullanım

```cmd
nslookup google.com                     # Temel sorgu
nslookup google.com 8.8.8.8             # Belirli DNS sunucusu üzerinden sorgula
nslookup -type=MX google.com            # Mail sunucusu kaydını sorgula
nslookup -type=NS google.com            # Name server kayıtlarını sorgula
```

### Örnek Çıktı

```
C:\> nslookup google.com

Sunucu:  dns.google
Address:  8.8.8.8

Yetkili olmayan yanıt:
Ad:      google.com
Addresses:  2a00:1450:401b:804::200e    ← IPv6 adresi
            142.250.185.78              ← IPv4 adresi
```

```
C:\> nslookup -type=MX google.com

Sunucu:  dns.google
Address:  8.8.8.8

google.com    MX preference = 10, mail exchanger = smtp.google.com
```

---

## 📋 Komut Özet Tablosu

| Komut | Amaç | Temel Kullanım |
|---|---|---|
| `ping` | Bağlantı ve gecikme testi | `ping google.com` |
| `tracert` | Rota ve atlama noktalarını izleme | `tracert google.com` |
| `arp -a` | ARP önbelleğini görüntüleme | `arp -a` |
| `nslookup` | DNS sorgulaması | `nslookup google.com` |
