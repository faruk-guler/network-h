# 99 - Ağ Araçları ve Komutları: Ağ Yöneticisinin Çantası

Bir ağ yöneticisinin (veya meraklısının) çantasında bulunması gereken temel komutlar ve araçlar.

> 💡 **Benzetme:** Bu araçlar, doktorun stetoskop ve tansiyon aleti gibidir. Ağ problemlerini **teşhis etmek** için kullanılır.

---

## ⚡ Ping — "Yaşıyor mu?"

Bir hedefe "Erişebiliyor muyum?" diye sormak ve ne kadar sürede cevap geldiğini ölçmek.

- **Protokol:** ICMP (Internet Control Message Protocol)
- **Ne yapar:** Hedefe küçük bir paket gönderir, cevap bekler

### Ping Kullanımı

```bash
# Temel ping
ping google.com

# Belirli sayıda ping gönder
ping -c 4 google.com          # Linux/Mac (4 paket)
ping -n 4 google.com          # Windows (4 paket)

# Belirli boyutta paket gönder
ping -s 1500 google.com       # Linux (1500 byte)
ping -l 1500 google.com       # Windows (1500 byte)

# Sürekli ping
ping -t google.com             # Windows (Ctrl+C ile durdur)
```

### Ping Çıktısını Okuma

```text
Reply from 142.250.185.78: bytes=32 time=15ms TTL=118
       │                         │       │        │
       └─ Hedef IP               │       │        └─ Kaç hop
                                  │       └─ Gecikme (düşük=iyi)
                                  └─ Paket boyutu
```

**Sonuç Değerlendirme:**

| Süre (ms) | Değerlendirme |
| :--- | :--- |
| < 20ms | Mükemmel |
| 20-50ms | İyi |
| 50-100ms | Orta |
| > 100ms | Kötü |
| "Request Timed Out" | Erişilemiyor! |

---

## 👣 Tracert / Traceroute — "Hangi Yoldan Gidiyor?"

Hedefe giderken hangi router'lardan (duraklardan) geçtiğinizi gösterir.

### Tracert Kullanımı

```bash
# Windows
tracert google.com

# Linux/Mac
traceroute google.com

# Windows - detaylı yol analizi
pathping google.com
```

### Tracert Çıktısını Okuma

```text
  1    <1 ms    <1 ms    <1 ms   192.168.1.1       ← Modem/Router
  2    10 ms    12 ms    11 ms   10.0.0.1           ← ISP 1. nokta
  3    15 ms    14 ms    16 ms   46.234.100.1       ← ISP backbone
  4     *        *        *      Request timed out  ← Sorunlu nokta!
  5    25 ms    24 ms    26 ms   142.250.185.78     ← Google
```

> 💡 **İpucu:** `*` veya "Request timed out" gördüğünüz satırda sorun olabilir (veya sadece ICMP engellenmiştir).

---

## 📝 Ipconfig / Ifconfig — "Ben Kimim?"

Kendi cihazınızın ağ bilgilerini gösterir.

### Windows (Ipconfig)

```powershell
ipconfig                  # Temel bilgiler
ipconfig /all             # Detaylı (MAC, DNS, DHCP dahil)
ipconfig /release         # DHCP IP'yi bırak
ipconfig /renew           # DHCP'den yeni IP al
ipconfig /flushdns        # DNS önbelleğini temizle
ipconfig /displaydns      # DNS önbelleğini göster
```

### Linux (Ip addr)

```bash
ip addr show              # IP ve MAC bilgileri (modern)
ip a                      # Kısa hali
ifconfig                  # Eski yöntem (hala çalışır)
ip route show             # Routing tablosu
```

### Mac (Ifconfig)

```bash
ifconfig                  # Ağ bilgileri
networksetup -listallhardwareports  # Tüm interface'ler
```

---

## 🔍 Nslookup / Dig — "Bu Domain Nerede?"

DNS sorgusu yapar. Bir alan adının IP'sini veya bir IP'nin alan adını öğrenin.

### Nslookup

```bash
nslookup farukguler.com            # Temel DNS sorgusu
nslookup -type=MX gmail.com       # MX (mail) kaydı sorgula
nslookup -type=NS example.com     # Name server sorgula
nslookup -type=TXT example.com    # TXT kaydı sorgula
nslookup 8.8.8.8                  # Ters DNS (IP → Domain)
```

### Dig (Linux/Mac - Daha Güçlü)

```bash
dig farukguler.com                     # Temel sorgu
dig farukguler.com +short             # Sadece IP göster
dig farukguler.com MX                 # MX kayıtları
dig @8.8.8.8 farukguler.com          # Google DNS ile sorgula
dig farukguler.com +trace             # DNS çözümleme adımları
```

---

## 🕵️ Nmap (Network Mapper) — "Ağda Neler Var?"

Ağ taraması yapar. Cihazlar, açık portlar ve işletim sistemleri hakkında bilgi toplar.

> ⚠️ **Dikkat:** Nmap güçlü bir araçtır. **Sadece kendi ağınızda** veya izin verilen ağlarda kullanın!

### Kurulum

```bash
# Windows: nmap.org'dan indir
# Linux:
sudo apt install nmap     # Debian/Ubuntu
sudo yum install nmap     # RHEL/CentOS
```

### Temel Taramalar

```bash
# Tek host tarama
nmap 192.168.1.1

# Ağ taraması (tüm aktif cihazlar)
nmap 192.168.1.0/24

# Hızlı tarama (en bilinen 100 port)
nmap -F 192.168.1.0/24

# Belirli port tarama
nmap -p 22,80,443 192.168.1.1

# Port aralığı tarama
nmap -p 1-1000 192.168.1.1

# Tüm portları tara
nmap -p- 192.168.1.1
```

### İleri Seviye Taramalar

```bash
# İşletim sistemi tespiti
sudo nmap -O 192.168.1.1

# Servis/versiyon tespiti
nmap -sV 192.168.1.1

# Gizli tarama (SYN scan)
sudo nmap -sS 192.168.1.0/24

# Agresif tarama (OS + Servis + Script + Traceroute)
sudo nmap -A 192.168.1.1

# Ping taraması (sadece aktif cihazlar)
nmap -sn 192.168.1.0/24
```

---

## 🎣 Paket Yakalama (Traffic Analysis)

Ağ trafiğini paket paket incelemek için kullanılan "röntgen" araçlarıdır.

### 1. Wireshark (Görsel Araç)

- **Görevi:** Ağ trafiğini yakalar ve her protokolü detaylıca analiz eder.
- **Kullanım:** Sorun giderme, güvenlik analizi.
- **Benzetme:** Ağ trafiği için bir mikroskop/röntgen cihazı.

### 2. Tcpdump (Komut Satırı)

- **Görevi:** Wireshark'ın komut satırı versiyonudur (Linux/Mac).
- **Örnek:**

  ```bash
  tcpdump -i eth0    # eth0 arayüzünü dinle
  tcpdump port 80    # Sadece web trafiğini göster
  ```

---

## 📡 Netstat / SS — "Hangi Bağlantılar Açık?"

Aktif ağ bağlantılarını ve dinleyen portları gösterir.

### Windows (Netstat)

```powershell
netstat -an              # Tüm bağlantılar (sayısal)
netstat -ano             # PID dahil
netstat -ab              # Uygulama adları ile
netstat -r               # Routing tablosu
```

### Linux (SS/Netstat)

```bash
ss -tulnp                # Tüm dinleyen portlar (modern)
  # -t: TCP
  # -u: UDP
  # -l: Listening (dinleyen)
  # -n: Numerical (sayısal)
  # -p: Process (hangi uygulama)

netstat -tulnp           # Eski yöntem (hala çalışır)
```

---

## MAC (Media Access Control) Alt Katmanı

Donanım adresleme, ortam erişimi ve frame'ler için hata tespitinden sorumlu, Data Link katmanının alt katmanı.

```bash
# ARP tablosunu göster
arp -a                    # Windows/Linux/Mac

# ARP önbelleğini temizle
arp -d *                  # Windows
sudo ip neigh flush all   # Linux
```

---

## 🌐 Curl / Wget — "HTTP İsteği Gönder"

Web sunucularına istek göndermek ve yanıt almak için kullanılır.

```bash
# Sayfanın içeriğini getir
curl https://farukguler.com

# Sadece HTTP başlıkları
curl -I https://farukguler.com

# Dosya indir
curl -O https://example.com/dosya.zip
wget https://example.com/dosya.zip

# POST isteği gönder
curl -X POST -d "username=admin" https://example.com/login
```

---

## 📊 Komut Karşılaştırma Tablosu

| Komut | Windows | Linux/Mac | Görevi |
| :--- | :--- | :--- | :--- |
| **Ping** | `ping` | `ping` | Bağlantı testi |
| **Traceroute** | `tracert` | `traceroute` | Yol izleme |
| **IP bilgisi** | `ipconfig` | `ip a` / `ifconfig` | Ağ yapılandırması |
| **DNS sorgusu** | `nslookup` | `dig` / `nslookup` | DNS çözümleme |
| **Port kontrol** | `netstat -an` | `ss -tulnp` | Açık portlar |
| **ARP tablosu** | `arp -a` | `arp -a` | IP↔MAC eşleşme |
| **Ağ tarama** | `nmap` | `nmap` | Port/cihaz tarama |
| **Paket analizi** | `Wireshark` | `tcpdump` / `Wireshark` | Trafik röntgeni |
| **DNS temizle** | `ipconfig /flushdns` | `systemd-resolve --flush-caches` | DNS cache temizle |

---

## 🚨 Sorun Giderme Metodolojileri

Ağ sorunlarını çözerken rastgele deneme-yanılma yapmak yerine şu profesyonel yaklaşımları kullanın:

### 1. Aşağıdan Yukarıya (Bottom-Up)

**En alt katmandan (Fiziksel) başlar.**

- Kablo takılı mı? (L1)
- Link ışığı yanıyor mu? (L2)
- IP adresi var mı? (L3)
- Ping atılıyor mu? (L3)
- Uygulama çalışıyor mu? (L7)

> ✅ **Kullanım:** Fiziksel bir değişiklik yapıldıysa (kablo değişimi, yeni cihaz) idealdir.

### 2. Yukarıdan Aşağıya (Top-Down)

**Uygulamadan başlar.**

- Web sayfası açılıyor mu? (L7)
- DNS çözüyor mu?
- Ping gidiyor mu?

> ✅ **Kullanım:** Sorunun sadece tek bir uygulamada olduğunu düşünüyorsanız (örn: sadece Outlook çalışmıyor).

### 3. Böl ve Yönet (Divide and Conquer)

**Ortadan (Genellikle Network Katmanı / IP) başlar.**

- Doğrudan `ping 8.8.8.8` atarsınız.
- **Çalışırsa:** Sorun L4-L7 arasındadır (Fiziksel ve IP sağlam).
- **Çalışmazsa:** Sorun L1-L3 arasındadır (Kablo veya IP hatası).

> ✅ **Kullanım:** En hızlı ve yaygın yöntemdir.

---

## 🛠️ Pratik Sorun Giderme Sırası

```text
0. Fiziksel Kontrol    → Kablolar takılı mı? Işıklar yanıyor mu?
1. ping 127.0.0.1         → Kendi ağ kartın çalışıyor mu?
2. ping 192.168.1.1       → Ağ geçidine (Gateway) erişebiliyor musun?
3. ping 8.8.8.8           → İnternete çıkabiliyor musun?
4. ping google.com        → DNS çalışıyor mu?
5. nslookup google.com    → DNS çözümleme doğru mu?
6. tracert google.com     → Sorun nerede?
```

> 💡 **Eğer Adım 3 çalışıyor ama Adım 4 çalışmıyorsa** → **DNS problemi!** DNS sunucunuzu değiştirin (8.8.8.8).

---

**Navigasyon:**

- [⬅️ Önceki: Portlar ve Servisler](./ports/07-Portlar-ve-Servisler-Port-Nedir.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Terimler Sözlüğü](./Terminology.md)
