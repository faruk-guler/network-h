# Reserved (Özel Amaçlı) IP Aralıkları

Ne private ne de normal public sayılan; belirli teknik işlevler için **IANA tarafından ayrılmış**, kullanıcılara atanmayan aralıklardır.

| Sınıf | Aralık | CIDR | Açıklama | RFC |
|---|---|---|---|---|
| A | 0.0.0.0 – 0.255.255.255 | /8 | Geçersiz — kaynak adres olarak kullanılmaz | RFC 1122 |
| A | 100.64.0.0 – 100.127.255.255 | /10 | Shared Address Space — ISP'lerin CGN (Carrier-Grade NAT) altyapısı için ayrılmıştır | RFC 6598 |
| A | 127.0.0.0 – 127.255.255.255 | /8 | Loopback — cihazın kendisi (`127.0.0.1`) | RFC 1122 |
| B | 169.254.0.0 – 169.254.255.255 | /16 | Link-local / APIPA — DHCP bulunamazsa otomatik atanır | RFC 3927 |
| C | 192.0.0.0 – 192.0.0.255 | /24 | IETF protokol atamaları | RFC 6890 |
| C | 192.0.2.0 – 192.0.2.255 | /24 | TEST-NET-1 — dokümantasyon ve örnekler için ayrılmış, gerçek trafikte kullanılmaz | RFC 5737 |
| C | 192.88.99.0 – 192.88.99.255 | /24 | IPv6'dan IPv4'e geçiş (kullanımdan kalktı) | RFC 7526 |
| C | 198.18.0.0 – 198.19.255.255 | /15 | Ağ cihazı benchmark testleri | RFC 2544 |
| C | 198.51.100.0 – 198.51.100.255 | /24 | TEST-NET-2 — dokümantasyon ve örnekler için ayrılmış, gerçek trafikte kullanılmaz | RFC 5737 |
| C | 203.0.113.0 – 203.0.113.255 | /24 | TEST-NET-3 — dokümantasyon ve örnekler için ayrılmış, gerçek trafikte kullanılmaz | RFC 5737 |
| D | 224.0.0.0 – 239.255.255.255 | /4 | Multicast — grup yayınları | RFC 5771 |
| E | 240.0.0.0 – 255.255.255.254 | /4 | Gelecek kullanım, deneysel | RFC 1112 |
| — | 255.255.255.255 | /32 | Sınırlı broadcast — tüm ağa yayın | RFC 919 |

> 💡 **Not:** TEST-NET aralıkları (`192.0.2.x`, `198.51.100.x`, `203.0.113.x`) teknik dokümanlarda
> ve kitaplarda örnek IP olarak kullanılmak üzere ayrılmıştır — tıpkı telefon numaralarındaki
> `555-xxxx` gibi düşünebilirsiniz.
