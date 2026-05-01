

## Local Broadcast Adresler

- Aynı Anda Yerel Alanda Tüm Cihazlara Veri Göndermek İçin Kullanılır.
- IP Adresinin Tüm Bitleri Binary "1" Yapılarak Elde Edilir.

**Binary:** `11111111.11111111.11111111.11111111`

**Decimal:** `255.255.255.255`

> Router Broadcast Paketlerini Geçirmez

**Örnek**: DHCP ip adresi talepleri "DHCP server farklı ağda ise routerler üzerinde IP Helper açılmalıdır."

---

## Directed Broadcast Adresler

- Belirli Bir Network'te Bulunan Tüm Cihazlara Veri Göndermek İçin Kullanılır
- IP Adresinin Kullanıcı İçin Ayrılmış Oktetlerinde Tüm Bitleri Binary "1" Yapılarak Elde Edilir.

**Network:** `172.16.0.0`

**Directed Broadcast Adres:** `172.16.255.255`
