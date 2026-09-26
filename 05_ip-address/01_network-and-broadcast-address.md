# 🖧 Network ve Broadcast Adresleri

## 🖥️ Network Adres

Alt ağın (subnet'in) kendisini tanımlayan adrestir; bir host'a atanamaz. Subnet'in ilk adresidir ve tüm host bitleri 0'dır. Routing tablolarında hedef ağ olarak bu adres geçer.

Örneğin, 192.168.1.0

- Her subnet'te bir Network adresi ve bir Broadcast adresi bulunur.
- Bu iki adres hiçbir host'a **atanamaz**.

---

## 📢 Broadcast Adres

Bir subnet içindeki son IP adresi broadcast adresidir, bu adrese gönderilen paket tüm hostlara iletilir. Host bitlerinin tamamı 1 olduğunda oluşur.

## Local Broadcast Adresler

- Aynı Anda Yerel Alanda Tüm Cihazlara Veri Göndermek İçin Kullanılır.
- IP Adresinin Tüm Bitleri Binary "1" Yapılarak Elde Edilir.

**Binary:** `11111111.11111111.11111111.11111111`

**Decimal:** `255.255.255.255`

> Router Broadcast Paketlerini Geçirmez

**Örnek:** DHCP Discover bir broadcast'tir. DHCP sunucusu farklı ağdaysa broadcast bu sınırı aşamaz; bu durumda router üzerine **IP Helper (DHCP Relay)** yapılandırılarak istek sunucuya unicast olarak taşınır.

---

## Directed Broadcast Adresler

- Belirli Bir Network'te Bulunan Tüm Cihazlara Veri Göndermek İçin Kullanılır
- IP Adresinin Kullanıcı İçin Ayrılmış Oktetlerinde Tüm Bitleri Binary "1" Yapılarak Elde Edilir.

**Network:** `172.16.0.0/16`

**Directed Broadcast Adres:** `172.16.255.255`

> Router Broadcast Paketlerini Geçirmek için yapılandırılabilir.
