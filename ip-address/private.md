# Private IP Adresleri
 
Private IP adresleri yalnızca yerel ağ (LAN) içinde geçerlidir.
İnternete doğrudan çıkamazlar; router üzerinden NAT ile public IP'ye dönüştürülürler.
**RFC 1918** standardıyla üç aralık IANA tarafından özel kullanım için ayrılmıştır.
 
| Sınıf| Aralık | CIDR | Kullanım Yeri | Toplam Adres | Ağ Sayısı |
|---|---|---|---|---|---|
| A | 10.0.0.0 – 10.255.255.255 | /8 | Büyük kurumsal ağlar, veri merkezleri | 16.777.216 | 1 |
| B | 172.16.0.0 – 172.31.255.255 | /12 | Orta ölçekli kurumsal ağlar | 1.048.576 | 16 |
| C | 192.168.0.0 – 192.168.255.255 | /16 | Ev, küçük ofis ağları | 65.536 | 256 |
 
> **Not:** Bu adresler internette yönlendirilemez. İki farklı evde aynı 192.168.1.5 adresi
> bulunabilir — çünkü her ikisi de kendi yerel ağlarında geçerlidir, dışarıdan görünmezler.

## Loopback:
Hostların kendini test etmeleri ve iç ağında kullanmaları içindir.(servisler vb.) Tüm bu network Loopback için ayrılmıştır.
- Loopback: 127.0.0.1 - 127.255.255.255

## Extra:
- APIPA Link-Local addres: 169.254.0.0 – 169.254.255.255 > 🔹 DHCP servere ulaşılamadığında hostun KENDİNE atadığı otomatik IP adresidir.
