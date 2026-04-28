# 07 - Portlar ve Servisler: Port Referans Rehberi

IP adreslerini bir binanın dış kapı numarası (Public IP) veya daire numarası (Private IP) olarak düşünürsek, Portlar o dairenin içindeki pencereler veya kapılar gibidir.

Bir IP adresi verinin hangi cihaza gideceğini belirlerken, Port numarası o verinin cihaz içindeki hangi uygulamaya veya servise teslim edileceğini belirler.

Bu dizin, **IANA (Internet Assigned Numbers Authority)** tarafından kayıtlı tüm TCP/UDP portlarının kapsamlı listesini içerir.

> 💡 **Port Nedir?** Port, bir IP adresindeki "kapı numarası"dır. IP adresi binanın adresi, port ise daire numarasıdır.

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
