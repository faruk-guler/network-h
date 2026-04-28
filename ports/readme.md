# Portlar ve Servisler:

> 💡 **Port Nedir?** Port, bir IP adresindeki "kapı numarası"dır. IP adresi binanın adresi, port ise daire numarasıdır.

Bir IP adresi verinin hangi cihaza gideceğini belirlerken, Port numarası o verinin cihaz içindeki hangi uygulamaya veya servise teslim edileceğini belirler. Port numaralarının hangi servislere ayrılacağını ve standartlarını IANA (Internet Assigned Numbers Authority) belirler ve bu listeyi kendi web sitesinde herkese açık ve güncel bir şekilde yayınlar. "https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml"

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
