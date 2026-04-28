## 1. Private IP Adresleri
 
Private IP adresleri yalnızca yerel ağ (LAN) içinde geçerlidir.
İnternete doğrudan çıkamazlar; router üzerinden NAT ile public IP'ye dönüştürülürler.
**RFC 1918** standardıyla üç aralık IANA tarafından özel kullanım için ayrılmıştır.
 
| Aralık | CIDR | Sınıf | Kullanım Yeri | Toplam Adres |
|---|---|---|---|---|
| `10.0.0.0` – `10.255.255.255` | `/8` | A | Büyük kurumsal ağlar, veri merkezleri | 16.777.216 |
| `172.16.0.0` – `172.31.255.255` | `/12` | B | Orta ölçekli kurumsal ağlar | 1.048.576 |
| `192.168.0.0` – `192.168.255.255` | `/16` | C | Ev, küçük ofis ağları | 65.536 |
 
> **Not:** Bu adresler internette yönlendirilemez. İki farklı evde aynı `192.168.1.5` adresi
> bulunabilir — çünkü her ikisi de kendi yerel ağlarında geçerlidir, dışarıdan görünmezler.
 

