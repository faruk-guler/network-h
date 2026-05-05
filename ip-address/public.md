# Public IP Adresleri

Public IP adresleri, internette **küresel olarak benzersizdir**.
IANA (İnternet Tahsisli Sayılar Kurumu) → RIR (Bölgesel İnternet Kayıt Kuruluşu) → ISP (İnternet Servis Sağlayıcısı) zinciriyle dağıtılır.

> 💡 **Dağıtım Zinciri:** IANA büyük blokları RIR'lara (Avrupa için RIPE NCC, Kuzey Amerika için ARIN vb.) dağıtır.
> RIR'lar bu blokları Türk Telekom, Superonline gibi ISP'lere tahsis eder; ISP'ler de son kullanıcılara iletir.

IPv4'te public adresler **classful (sınıflı) adresleme** sistemiyle 5 sınıfa ayrılmıştır:

| Sınıf | Başlangıç IP | Bitiş IP | CIDR | Kullanım | Toplam Adres |
|---|---|---|---|---|---|
| **A** | 1.0.0.0 | 126.255.255.255 | /8 blokları | Unicast, Çok büyük ağlar (Google, devlet, büyük ISP'ler) | ~2,1 milyar |
| **B** | 128.0.0.0 | 191.255.255.255 | /16 blokları | Unicast, Orta-büyük kurumlar, üniversiteler | ~1,07 milyar |
| **C** | 192.0.0.0 | 223.255.255.255 | /24 blokları | Unicast, Küçük-orta ölçekli ağlar, bireysel ISP tahsisleri | ~536 milyon |
| **D** | 224.0.0.0 | 239.255.255.255 | — | Multicast (grup yayınları) — kullanıcılara atanmaz | 268 milyon |
| **E** | 240.0.0.0 | 255.255.255.255 | — | Reserved / deneysel, gelecek kullanım için ayrılmış — atanmaz | 268 milyon |

> **Önemli:** D ve E sınıfları son kullanıcılara atanmaz.
> Gerçek anlamda kullanılabilen public IP'ler yalnızca **A, B ve C sınıflarındadır**
> (içlerindeki private aralıklar olan `10.x.x.x`, `172.16.x–172.31.x`, `192.168.x.x` hariç tutularak).

> 💡 `127.0.0.0 – 127.255.255.255` Loopback aralığı A sınıfından çıkarılmıştır.

> ⚠️ **IPv4 Tükenmesi:** IANA'nın merkezi IPv4 havuzu **Şubat 2011**'de tamamen tükendi.
> Bölgesel kayıt kuruluşları (RIR'lar) da sırasıyla 2011–2019 yılları arasında havuzlarını bitirdi.
> Bu sorunun kalıcı çözümü için neredeyse sınırsız adres alanı sunan **IPv6** geliştirilmiştir.

## Örnek Public IP Adresleri 🌍

- `8.8.8.8` → Google DNS
- `142.250.190.78` → Google
- `104.18.7.35` → Cloudflare
