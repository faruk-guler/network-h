# 🖧 IP Adresi Nedir?

IP Adresi (Internet Protocol Address), bir ağa bağlı her cihazın sahip olduğu **sayısal kimlik numarasıdır.**
Tıpkı bir evin posta adresi gibi — veri paketi nereye gönderileceğini bu adres sayesinde bulur. OSI modelinde **3. katmanda (Ağ Katmanı)** çalışır. IPv4 adresleri **32 bit** uzunluğunda olup nokta (.) ile ayrılırken, IPv6 adresleri **128 bit** uzunluğunda olup iki nokta üst üste (:) ile ayrılır.

---

## Günlük Hayattan Örnek

Sen bir web sitesine girdiğinde aslında şu olur:

```
Senin cihazın              →    google.com sunucusu
(192.168.1.5)              →    (142.250.74.46)
"Bana ana sayfayı gönder"  →    "Tamam, işte veri"
```

İkisi de birbirini IP adresi sayesinde bulur.

---

## IP adresinin iki (2) versiyonu vardır

| | IPv4 | IPv6 |
|---|---|---|
| Örnek | 192.168.1.1 | 2001:0db8:85a3::8a2e |
| Format | 4 Byte/32 bit, 4 oktet | 128 bit |
| Toplam adres | ~4,3 milyar | Yaklaşık 340 Undesilyon |
| Durum | Hâlâ yaygın | Geçiş süreci devam ediyor |


## 🧪🧪 IP Adresi Formatı
IP "Network ID" ve "Host ID" olmak üzere iki bölümden oluşmaktadır ve Adres Sınıflarına göre farklılık göstermektedir. Network ağı, Host ise uç cihazları ifade eder.
```
xxx . xxx . xx .  xx
└─────────────┘ └──┘
 Network ID     Host ID
```
> 💡 Yukarıdaki örnek C sınıfı adresleme yapısını göstermektedir.

---

### 1. Sınıflı (Classful) IP Adresleme Yapısı
Bu sistem, IP adresinin hangi sınıf olduğuna ilk oktetine (bölümüne) bakarak karar verir:

| Sınıf | Oktet Aralığı | Varsayılan Yapı |
|---|---|---|
| *(Ayrılmış)* | 0 | Bu ağ — kaynak adres olarak kullanılmaz (RFC 1122) |
| **A** | 1 – 126 | Ağ.Host.Host.Host |
| *(Loopback)* | 127 | Cihazın kendisine dönüş adresi — `127.0.0.1` (RFC 1122) |
| **B** | 128 – 191 | Ağ.Ağ.Host.Host |
| **C** | 192 – 223 | Ağ.Ağ.Ağ.Host |
| **D** | 224 – 239 | Multicast — kullanıcılara atanmaz |
| **E** | 240 – 255 | Deneysel / Ayrılmış — atanmaz |

> 💡 `0.x.x.x` ve `127.x.x.x` blokları özel amaçlı (loopback) olduğundan A sınıfına dahil edilmez.
> 💡 D ve E sınıfları unicast host adresi olarak kullanılamaz.

### 2. Özel (Private) IP Blokları (RFC 1918)
Modemlerimizde veya iç ağlarımızda gördüğümüz, internete doğrudan çıkamayan adreslerdir. Üç ana aralık vardır: `10.x.x.x`, `172.16–31.x.x` ve `192.168.x.x`. Bu adresler internette yönlendirilemez; router üzerinden NAT ile public IP'ye dönüştürülürler.

> 💡 Host ID, teorik olarak min 0 (Network Adresi) ile max 255 (Broadcast Adresi) değerlerini alır. Bu iki uç adres cihazlara **atanamaz**; atanabilir aralık her subnet'te `.1` ile `.254` arasındadır.
