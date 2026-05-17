# 📣 Broadcast Adres:
Bir subnet içindeki son IP adresi broadcast adresidir, bu adrese gönderilen paket tüm hostlara iletilir. Host bitlerinin tamamı 1 olduğunda oluşur.

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

> Router Broadcast Paketlerini Geçirmek için yapılandırılabilir.

# 🖥️ Network Adres:
Subnet içindeki cihazların iletişimi için kullanılır ve hiçbir host 'a atanamaz. Genellikle subnet’in ilk adresidir ve tüm host bitleri 0’dır.

Örneğin, 192.168.1.0

- Her subnet'te bir Network adresi ve bir Broadcast adresi bulunur
- Broadcast adresi hiçbir host 'a atanamaz.
