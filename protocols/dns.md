# 🌐 DNS (Domain Name System) — İnternetin Telefon Rehberi

## DNS Nedir?

DNS (Domain Name System), alan adlarını (domain) IP adreslerine çeviren dağıtık bir sistemdir. İnsanlar `google.com` gibi isimleri hatırlar, ama bilgisayarlar yalnızca `142.250.185.78` gibi sayısal adresleri anlar. DNS bu iki dünya arasındaki çevirmendir.

> 💡 **Benzetme:** Telefon rehberinizde "Ahmet" diye ararsınız, rehber size `0532 xxx xx xx` numarasını verir. DNS de tam olarak bunu yapar — ismi alır, IP adresini verir.

**Port:** UDP/TCP 53

---

## DNS Nasıl Çalışır?

Tarayıcınıza `google.com` yazdığınızda arka planda şu adımlar gerçekleşir:

### Adım 1: DNS Önbellek Kontrolü

Bilgisayarınız önce kendi hafızasına (cache) bakar: *"Bu adresi daha önce sormuş muyduk?"*

```
Kontrol sırası:
1. Tarayıcı önbelleği
2. İşletim sistemi DNS önbelleği
3. Router önbelleği
```

Eğer kayıt bulunursa sorgu burada biter — hızlı ve verimlidir.

### Adım 2: Recursive DNS Sunucusu

Önbellekte yoksa sorgu **Recursive DNS Sunucusu**'na iletilir. Bu genellikle ISP'nizin DNS sunucusu veya `8.8.8.8` (Google DNS), `1.1.1.1` (Cloudflare DNS) gibi genel DNS sunucularıdır.

### Adım 3: Hiyerarşik Sorgulama

Recursive sunucu cevabı bilmiyorsa, sırasıyla 3 farklı sunucuya danışır:

```
1. Root DNS Sunucusu (.):
   "google.com'u bilmem ama .com masasının adresini bilirim."

2. TLD DNS Sunucusu (.com):
   ".com masasıyım. google.com'un yetkili sunucu adresini veriyorum."

3. Yetkili DNS Sunucusu (Authoritative):
   "google.com'un IP adresi: 142.250.185.78"
```

Recursive sunucu bu cevabı alır, **önbelleğe kaydeder** (TTL süresi boyunca) ve bilgisayarınıza iletir.

---

## DNS Kayıt Türleri

Her domain'in DNS sunucusunda farklı türde kayıtları bulunur:

| Kayıt Türü | Açıklama | Örnek |
|---|---|---|
| **A** | Domain → IPv4 adresi | `google.com → 142.250.185.78` |
| **AAAA** | Domain → IPv6 adresi | `google.com → 2a00:1450:401b::200e` |
| **CNAME** | Takma ad (alias) | `www.google.com → google.com` |
| **MX** | Mail sunucusu | `google.com → smtp.google.com` |
| **NS** | Yetkili DNS sunucusu | `google.com → ns1.google.com` |
| **PTR** | IP → Domain (ters DNS) | `142.250.185.78 → google.com` |
| **TXT** | Metin kaydı (SPF, DKIM vb.) | Doğrulama ve güvenlik bilgileri |
| **SOA** | Bölge yetkili bilgisi | Seri no, yenileme süresi vb. |

> 💡 **A** kaydı en yaygın olanıdır. Bir web sitesini ziyaret ettiğinizde arka planda genellikle bir A kaydı sorgulanır.

---

## DNS Önbellek (DNS Cache)

DNS sorguları her seferinde tüm hiyerarşiyi dolaşmaz. Çözümlenen kayıtlar **TTL (Time to Live)** süresi boyunca önbellekte tutulur.

### DNS Önbellek Komutları

```cmd
:: Windows
ipconfig /displaydns      # Önbellekteki kayıtları göster
ipconfig /flushdns        # DNS önbelleğini temizle

:: Belirli bir domain sorgula
nslookup google.com
nslookup -type=MX google.com    # MX kaydını sorgula
nslookup -type=NS google.com    # NS kayıtlarını sorgula
```

```bash
# Linux
dig google.com            # Detaylı DNS sorgusu
dig google.com MX         # MX kaydını sorgula
host google.com           # Basit DNS sorgusu

# DNS önbelleğini temizle
sudo systemd-resolve --flush-caches
```

---

## Popüler Genel DNS Sunucuları

| Sağlayıcı | Birincil DNS | İkincil DNS | Özellik |
|---|---|---|---|
| **Google** | `8.8.8.8` | `8.8.4.4` | Hızlı, güvenilir |
| **Cloudflare** | `1.1.1.1` | `1.0.0.1` | Gizlilik odaklı, en hızlı |
| **Quad9** | `9.9.9.9` | `149.112.112.112` | Zararlı siteleri filtreler |
| **OpenDNS** | `208.67.222.222` | `208.67.220.220` | Aile koruma filtresi var |

> 💡 ISP'nizin DNS sunucusu yavaş veya sorunluysa, yukarıdaki genel DNS sunucularından birini kullanabilirsiniz. Cihazınızın veya modeminizin ağ ayarlarından değiştirilebilir.

---

## DNS Güvenliği

| Tehdit | Açıklama | Çözüm |
|---|---|---|
| **DNS Spoofing** | Sahte DNS yanıtı ile yanlış IP'ye yönlendirme | DNSSEC kullanımı |
| **DNS Hijacking** | DNS sorgularının kötü niyetli sunucuya yönlendirilmesi | Güvenilir DNS sunucusu kullanma |
| **DNS Tunneling** | DNS protokolü üzerinden veri sızdırma | DNS trafiğini izleme |

---

## Özet

| Kavram | Açıklama |
|---|---|
| **DNS** | Alan adlarını IP adreslerine çevirir |
| **A Kaydı** | Domain → IPv4 eşleşmesi |
| **MX Kaydı** | Domain → Mail sunucusu eşleşmesi |
| **DNS Cache** | Sorgu sonuçlarının geçici olarak saklanması |
| **TTL** | Bir DNS kaydının önbellekte ne kadar süre kalacağı |
| **Recursive DNS** | Sizin adınıza tüm hiyerarşiyi sorgulayan aracı sunucu |
| **Root DNS** | DNS hiyerarşisinin en üst noktası (dünyada 13 grup) |
