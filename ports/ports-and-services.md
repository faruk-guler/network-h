# 🔗 Portlar ve Servisler

> 💡 **Port Nedir?** Port, bir IP adresindeki "kapı numarası"dır. IP adresi binanın adresi, port ise daire numarasıdır.

Bir IP adresi verinin hangi cihaza gideceğini belirlerken, Port numarası o verinin cihaz içindeki hangi uygulamaya veya servise teslim edileceğini belirler. Port numaralarının hangi servislere ayrılacağını ve standartlarını IANA (Internet Assigned Numbers Authority) belirler ve bu listeyi kendi web sitesinde herkese açık şekilde günceller.

<https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml>

---

## 🏆 En Kritik Well-Known Portlar (0–1023)

| Port | Protokol | Servis | Açıklama |
| :---: | :--- | :--- | :--- |
| **20** | TCP | FTP-Data | Dosya transferi — veri kanalı |
| **21** | TCP | FTP-Control | Dosya transferi — kontrol kanalı |
| **22** | TCP | SSH | Güvenli uzak bağlantı ve dosya transferi (SFTP) |
| **23** | TCP | Telnet | Güvensiz uzak bağlantı — artık kullanılmaz |
| **25** | TCP | SMTP | Sunucular arası e-posta gönderimi |
| **53** | UDP/TCP | DNS | Alan adı → IP çözümleme |
| **67** | UDP | DHCP Server | Otomatik IP dağıtımı (sunucu) |
| **68** | UDP | DHCP Client | Otomatik IP alımı (istemci) |
| **69** | UDP | TFTP | Basit dosya transferi (ağ cihazı firmware) |
| **80** | TCP | HTTP | Web sayfası iletimi |
| **110** | TCP | POP3 | E-posta alma |
| **143** | TCP | IMAP | E-posta alma (sunucuda tut) |
| **161** | UDP | SNMP | Ağ cihazı izleme |
| **162** | UDP | SNMP Trap | Ağ cihazı alarm bildirimi |
| **443** | TCP | HTTPS | Güvenli (TLS) web iletimi |
| **445** | TCP | SMB | Windows dosya paylaşımı |
| **514** | UDP | Syslog | Log iletimi |
| **587** | TCP | SMTP (TLS) | E-posta gönderimi (kullanıcı → sunucu) |
| **993** | TCP | IMAPS | Güvenli IMAP |
| **995** | TCP | POP3S | Güvenli POP3 |

> 💡 **Port Aralıkları:**  
> 
> - **0–1023** → Well-Known Ports (sistem servisleri, root gerektirir)  
> - **1024–49151** → Registered Ports (uygulama servisleri)  
> - **49152–65535** → Dynamic/Ephemeral Ports (istemci tarafı geçici portlar)

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
tnc server.com -port 443             # PowerShell
```
