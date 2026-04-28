# 07 - Portlar ve Servisler: Port Referans Rehberi

IP adreslerini bir binanın dış kapı numarası (Public IP) veya daire numarası (Private IP) olarak düşünürsek, Portlar o dairenin içindeki pencereler veya kapılar gibidir.

Bir IP adresi verinin hangi cihaza gideceğini belirlerken, Port numarası o verinin cihaz içindeki hangi uygulamaya veya servise teslim edileceğini belirler.

Bu dizin, **IANA (Internet Assigned Numbers Authority)** tarafından kayıtlı tüm TCP/UDP portlarının kapsamlı listesini içerir.

> 💡 **Port Nedir?** Port, bir IP adresindeki "kapı numarası"dır. IP adresi binanın adresi, port ise daire numarasıdır.

---

## 📊 Port Aralıkları

| Aralık         | Ad                               | Açıklama                                       |
| :------------- | :------------------------------- | :--------------------------------------------- |
| **0-1023**     | **Bilinen Portlar (Well-Known)** | Standart servisler (HTTP, SSH, DNS vb.)        |
| **1024-49151** | **Kayıtlı Portlar (Registered)** | Kayıtlı uygulamalar (MySQL, PostgreSQL vb.)    |
| **49152-65535**| **Dinamik/Özel (Dynamic/Private)**| Geçici bağlantılar için otomatik atanan portlar |

---

## ⭐ En Sık Kullanılan Portlar

| Port        | Protokol | Servis      | Açıklama                        |
| :---------- | :------- | :---------- | :------------------------------ |
| 20          | TCP      | FTP-Data    | Dosya transferi (veri)          |
| 21          | TCP      | FTP         | Dosya transferi (kontrol)       |
| 22          | TCP      | SSH         | Güvenli uzak erişim             |
| 23          | TCP      | Telnet      | Güvensiz uzak erişim ❌          |
| 25          | TCP      | SMTP        | E-posta gönderme                |
| 53          | TCP/UDP  | DNS         | İsim çözümleme                  |
| 67/68       | UDP      | DHCP        | Otomatik IP dağıtımı            |
| 80          | TCP      | HTTP        | Web (şifresiz)                  |
| 110         | TCP      | POP3        | E-posta indirme                 |
| 123         | UDP      | NTP         | Zaman senkronizasyonu           |
| 143         | TCP      | IMAP        | E-posta okuma                   |
| 161/162     | UDP      | SNMP        | Ağ izleme                       |
| 389         | TCP      | LDAP        | Dizin hizmeti                   |
| 443         | TCP      | HTTPS       | Web (şifreli) ✅                 |
| 445         | TCP      | SMB         | Windows dosya paylaşımı         |
| 587         | TCP      | SMTP/TLS    | E-posta gönderme (güvenli)      |
| 993         | TCP      | IMAPS       | E-posta okuma (güvenli)          |
| 995         | TCP      | POP3S       | E-posta indirme (güvenli)       |
| 3306        | TCP      | MySQL       | MySQL veritabanı                |
| 3389        | TCP      | RDP         | Uzak masaüstü (Windows)         |
| 5432        | TCP      | PostgreSQL  | PostgreSQL veritabanı           |
| 5900        | TCP      | VNC         | Uzak masaüstü                   |
| 8080        | TCP      | HTTP-Alt    | Alternatif web portu            |
| 8443        | TCP      | HTTPS-Alt   | Alternatif güvenli web          |

---

## 📂 Tam Port Listesi (IANA)

Portlar, 1000'er satırlık dosyalar halinde bölünmüştür:

| Dosya     | Port Aralığı               |
| :-------- | :------------------------- |
| [0-1000.md](./07-Portlar-ve-Servisler-0-1000.md) | 0-1000 arası portlar |
| [1001-2000.md](./07-Portlar-ve-Servisler-1001-2000.md) | 1001-2000 arası portlar |
| [2001-3000.md](./07-Portlar-ve-Servisler-2001-3000.md) | 2001-3000 arası portlar |
| [3001-4000.md](./07-Portlar-ve-Servisler-3001-4000.md) | 3001-4000 arası portlar |
| [4001-5000.md](./07-Portlar-ve-Servisler-4001-5000.md) | 4001-5000 arası portlar |
| [5001-6000.md](./07-Portlar-ve-Servisler-5001-6000.md) | 5001-6000 arası portlar |
| [6001-7000.md](./07-Portlar-ve-Servisler-6001-7000.md) | 6001-7000 arası portlar |
| [7001-8000.md](./07-Portlar-ve-Servisler-7001-8000.md) | 7001-8000 arası portlar |
| [8001-9000.md](./07-Portlar-ve-Servisler-8001-9000.md) | 8001-9000 arası portlar |
| [9001-10000.md](./07-Portlar-ve-Servisler-9001-10000.md) | 9001-10000 arası portlar |
| [10001-11000.md](./07-Portlar-ve-Servisler-10001-11000.md) | 10001-11000 arası portlar |
| [11001-12000.md](./07-Portlar-ve-Servisler-11001-12000.md) | 11001-12000 arası portlar |
| [12001-13000.md](./07-Portlar-ve-Servisler-12001-13000.md) | 12001-13000 arası portlar |
| [13001-14000.md](./07-Portlar-ve-Servisler-13001-14000.md) | 13001-14000+ arası portlar |

Her dosya, IANA kayıtlı port numarasını, protokolünü, servis adını ve açıklamasını içerir.

---

## 🔍 Port Kontrol Komutları

```bash
# Açık portları kontrol et
netstat -an | findstr "LISTENING"    # Windows
ss -tulnp                            # Linux

# Belirli bir portu kontrol et
netstat -an | findstr "443"          # Windows
ss -tulnp | grep 443                 # Linux

# Port taraması (Nmap)
nmap -p 1-1000 192.168.1.1

# Bir portun erişilebilir olup olmadığını kontrol et
telnet server.com 443                # Windows/Linux
nc -zv server.com 443                # Linux (netcat)
Test-NetConnection server.com -Port 443  # PowerShell
```

---

**Navigasyon:**

- [⬅️ Önceki: VLAN Temelleri](../07-VLAN-Temelleri.md)
- [🏠 Ana Sayfa](../README.md)
- [➡️ Sonraki: Ağ Araçları](../99-Araclar-ve-Komutlar-Ping-Tracert-Nmap.md)
