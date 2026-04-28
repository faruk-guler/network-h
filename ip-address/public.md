## 2. Public IP Adresleri
 
Public IP adresleri, internette **küresel olarak benzersizdir**.
ISP'ler (Türk Telekom, Superonline vb.) tarafından IANA → RIR → ISP zinciriyle dağıtılır.
 
IPv4'te public adresler **classful (sınıflı) adresleme** sistemiyle 5 sınıfa ayrılmıştır:
 
| Sınıf | Başlangıç IP | Bitiş IP | CIDR | Kullanım | Toplam Adres |
|---|---|---|---|---|---|
| **A** | `1.0.0.0` | `126.255.255.255` | `/8` blokları | Çok büyük ağlar (Google, devlet, büyük ISP'ler) | ~2,1 milyar |
| **B** | `128.0.0.0` | `191.255.255.255` | `/16` blokları | Orta-büyük kurumlar, üniversiteler | ~1,07 milyar |
| **C** | `192.0.0.0` | `223.255.255.255` | `/24` blokları | Küçük-orta ölçekli ağlar, bireysel ISP tahsisleri | ~536 milyon |
| **D** | `224.0.0.0` | `239.255.255.255` | — | Multicast (grup yayınları) — kullanıcılara atanmaz | 268 milyon |
| **E** | `240.0.0.0` | `255.255.255.255` | — | Deneysel / gelecek kullanım için ayrılmış — atanmaz | 268 milyon |
 
> **Önemli:** D ve E sınıfları son kullanıcılara atanmaz.
> Gerçek anlamda kullanılabilen public IP'ler yalnızca **A, B ve C sınıflarındadır**
> (içlerindeki private aralıklar hariç tutularak).
 
=======
## 2. Public IP Adresleri
 
Public IP adresleri, internette **küresel olarak benzersizdir**.
ISP'ler (Türk Telekom, Superonline vb.) tarafından IANA → RIR → ISP zinciriyle dağıtılır.
 
IPv4'te public adresler **classful (sınıflı) adresleme** sistemiyle 5 sınıfa ayrılmıştır:
 
| Sınıf | Başlangıç IP | Bitiş IP | CIDR | Kullanım | Toplam Adres |
|---|---|---|---|---|---|
| **A** | 1.0.0.0 | 126.255.255.255 | /8 blokları | Çok büyük ağlar (Google, devlet, büyük ISP'ler) | ~2,1 milyar |
| **B** | 128.0.0.0 | 191.255.255.255 | /16 blokları | Orta-büyük kurumlar, üniversiteler | ~1,07 milyar |
| **C** | 192.0.0.0 | 223.255.255.255 | /24 blokları | Küçük-orta ölçekli ağlar, bireysel ISP tahsisleri | ~536 milyon |
| **D** | 224.0.0.0 | 239.255.255.255 | — | Multicast (grup yayınları) — kullanıcılara atanmaz | 268 milyon |
| **E** | 240.0.0.0 | 255.255.255.255 | — | Deneysel / gelecek kullanım için ayrılmış — atanmaz | 268 milyon |
 
> **Önemli:** D ve E sınıfları son kullanıcılara atanmaz.
> Gerçek anlamda kullanılabilen public IP'ler yalnızca **A, B ve C sınıflarındadır**
> (içlerindeki private aralıklar hariç tutularak).
 

