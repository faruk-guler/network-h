# Private IP Adresleri

Private IP adresleri yalnızca yerel ağ (LAN) içinde geçerlidir.
İnternete doğrudan çıkamazlar; router üzerinden NAT ile public IP'ye dönüştürülürler.
**RFC 1918** standardıyla üç aralık IANA tarafından özel kullanım için ayrılmıştır.

## RFC 1918 Aralıkları

| Sınıf | Aralık | CIDR | Kullanım Yeri | Toplam Adres | Ağ Sayısı |
|---|---|---|---|---|---|
| A | 10.0.0.0 – 10.255.255.255 | /8 | Büyük kurumsal ağlar, veri merkezleri | 16.777.216 | 1 |
| B | 172.16.0.0 – 172.31.255.255 | /12 | Orta ölçekli kurumsal ağlar | 1.048.576 | 16 |
| C | 192.168.0.0 – 192.168.255.255 | /16 | Ev, küçük ofis ağları | 65.536 | 256 |

> **Not:** Bu adresler internette yönlendirilemez. İki farklı evde aynı `192.168.1.5` adresi
> bulunabilir — çünkü her ikisi de kendi yerel ağlarında geçerlidir, dışarıdan görünmezler.
> 
> 💡 Sınıfları belirleyen Subnet Mask'tır.
---

ℹ️ Aşağıdaki aralıklar RFC 1918 kapsamında değildir; ancak yerel kullanım amacıyla ayrılmış olduğundan private adreslerle birlikte ele alınmaktadır.

## Loopback

Bir cihazın **kendine** paket göndermesi için kullanılan özel adres aralığıdır. Servis testleri ve iç ağ uygulamaları için ayrılmıştır. Bu bloktaki hiçbir adres başka bir cihaza atanmaz.

- Loopback: `127.0.0.0` – `127.255.255.255`
- En yaygın kullanımı: `127.0.0.1` (localhost)

## APIPA (Link-Local)

DHCP sunucusuna ulaşılamadığında işletim sisteminin cihaza **otomatik olarak atadığı** geçici IP adresidir. Bu adresle yalnızca aynı yerel ağdaki cihazlarla haberleşilebilir; internete çıkılamaz.

- APIPA Aralığı: `169.254.0.0` – `169.254.255.255`
- ⚠️ Bir cihazın `169.254.x.x` adresi aldığı görülüyorsa DHCP sunucusuna ulaşılamıyor demektir.

## Multicast-IP addres:

224.0.0.0 – 239.255.255.255 aralığında bulunur. Bu sistemde veri, tek bir bilgisayara gönderilmek yerine bu aralıktaki sanal bir grup adresine postalanır. O veriye ihtiyacı olan tüm cihazlar ise aynı adrese akort olup beklemeye geçer. Böylece kaynak cihaz sadece bir kez yayın yapar, ama o adrese kulak kabartan herkes veriyi aynı anda ve ağ trafiğini hiç yormadan alır.
