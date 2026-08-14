# >_ Komutlar

Bir ağın nasıl çalıştığını anlamak için; IP adresleri, DNS, subnetting ve `ping`, `nslookup`, `traceroute` gibi temel araçları ve komutları öğrenmekte yarar vardır. Bu bölümde ağ dünyasında kullanılan bazı komutları sade ve anlaşılır şekilde inceleyeceğiz.

## 1. ipconfig / ip addr — Ağ Yapılandırmasını Görme

Cihazınızın IP adresi, subnet mask, default gateway ve DNS sunucusu gibi temel ağ bilgilerini görmek için kullanılan en temel komuttur. Bir ağ sorununu çözmeye başlamadan önce **ilk bakılacak yer** burasıdır.

| Bilgi | Açıklama |
|---|---|
| IP Adresi | Cihazın ağdaki kimliği |
| Subnet Mask | Ağ ve host kısmını ayıran maske |
| Default Gateway | Dış ağlara çıkış kapısı (router) |
| DNS Sunucusu | Alan adlarını IP'ye çeviren sunucu |

### Kullanım

```cmd
:: Windows
ipconfig                  # Temel ağ bilgilerini göster
ipconfig /all             # Tüm detayları göster (MAC, DNS, DHCP bilgileri)
ipconfig /release         # DHCP ile alınan IP adresini bırak
ipconfig /renew           # DHCP'den yeni IP adresi al
ipconfig /flushdns        # DNS önbelleğini temizle
ipconfig /displaydns      # DNS önbelleğini göster
```

```bash
# Linux
ip addr                   # Tüm arayüzlerin IP bilgilerini göster
ip addr show eth0         # Belirli bir arayüzün bilgilerini göster
ifconfig                  # Eski yöntem (hâlâ yaygın)
```

### Örnek Çıktı (Windows)

```
C:\> ipconfig

Windows IP Yapılandırması

Ethernet bağdaştırıcısı Ethernet:

   Bağlantıya Özgü DNS Son Eki  . :
   IPv4 Adresi. . . . . . . . . . : 192.168.1.100
   Alt Ağ Maskesi . . . . . . . . : 255.255.255.0
   Varsayılan Ağ Geçidi . . . . . : 192.168.1.1
```

> **💡 İpucu:** Bir cihazın `169.254.x.x` adresini aldığını görüyorsanız, DHCP sunucusuna ulaşılamıyor demektir (APIPA). Önce kablo bağlantısını kontrol edin, ardından `ipconfig /renew` komutunu deneyin.

---

## 2. ping — Bağlantı Testi

**Ping**, bir ağ üzerindeki cihazların erişilebilir olup olmadığını test etmek için kullanılan temel araçtır. 1983 yılında *Mike Muuss* tarafından geliştirilmiştir.

Hedef cihaza **ICMP Echo Request** paketi gönderilir ve geri dönen yanıt analiz edilir. Windows'ta varsayılan veri (payload) boyutu **32 byte**, Linux'ta ise **56 byte**'tır. Bu veriye ICMP başlığı (8 byte) ve IP başlığı (20 byte) eklenerek toplam paket oluşur:

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

## 3. tracert / traceroute — Rota İzleme

> 🪟 **Windows:** `tracert` | 🐧 **Linux/macOS:** `traceroute`

Paketlerin hedefe ulaşırken **hangi güzergahı izlediğini** ve **hangi router'lardan geçtiğini** gösterir. Ağdaki gecikme veya kopukluğun tam olarak nerede yaşandığını tespit etmek için kullanılır.

| Bilgi | Açıklama |
|---|---|
| İzlenen Rota | Paketin geçtiği ağ cihazları (hop) |
| Gecikme (ms) | Her atlamadaki yanıt süresi |
| Sorun Tespiti | Gecikme veya bağlantı kopukluğunun oluştuğu nokta |

> **💡 Hop (Atlama):** Paketin geçtiği her router bir **hop** olarak adlandırılır. Her hop'ta paketin **TTL (Time to Live)** değeri 1 azalır. TTL değeri 0 olduğunda paket düşürülür ve böylece sonsuz yönlendirme döngüleri önlenir.

### Kullanım

```cmd
:: Windows
tracert google.com
tracert 192.168.1.1
tracert -d google.com     # DNS çözümlemesi yapma, daha hızlı sonuç
```

```bash
# Linux / macOS
traceroute google.com
traceroute 192.168.1.1
traceroute -n google.com    # DNS çözümlemesi yapma
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

> **💡 İpucu:** Bir satırda `* * *` görüyorsanız, o router ICMP paketlerine yanıt vermiyor, güvenlik duvarı tarafından engelleniyor veya o noktada paket kaybı yaşanıyor olabilir.

---

## 4. arp -a — MAC Adresi Tablosu

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

## 5. nslookup — DNS Sorgulama

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
