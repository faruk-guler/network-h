# 📡 Anycast — En Yakına İletim

## Anycast Nedir?

Aynı IP adresinin **birden fazla sunucuya** atandığı ve paketin bu sunucuların **coğrafi olarak en yakınına** iletildiği iletim yöntemidir.

> 💡 **Benzetme:** Starbucks'ın şehirde 10 şubesi var ve hepsinin adresi aynı: "Starbucks, İstanbul". Siz Kadıköy'deyseniz Kadıköy şubesine, Beşiktaş'taysanız Beşiktaş şubesine yönlendirilirsiniz. Paket her seferinde en yakın noktaya ulaşır.

---

## Diğer İletim Türleriyle Karşılaştırma

| | Unicast | Multicast | Broadcast | Anycast |
|:---|:---|:---|:---|:---|
| **Hedef** | Tek, belirli cihaz | Belirli bir grup | Ağdaki herkes | En yakın cihaz |
| **IP** | Tekil | `224.x.x.x` grubu | `255.255.255.255` | Birden fazla cihazda aynı IP |
| **Örnek** | Web sitesi açmak | IPTV yayını | DHCP isteği | DNS sorgusu (`8.8.8.8`) |
| **IPv6 desteği** | ✅ | ✅ | ❌ (IPv6'da yok) | ✅ Yerel destek |

---

## Nasıl Çalışır?

```
           [DNS Sunucu — Frankfurt]
           IP: 8.8.8.8
                ▲
İstanbul'daki   │  BGP: "Ben 8.8.8.8'im, 10ms"
kullanıcı ──────┤
                │  BGP: "Ben de 8.8.8.8'im, 120ms"
                ▼
           [DNS Sunucu — Singapur]
           IP: 8.8.8.8
```

1. Hem Frankfurt hem Singapur'daki sunucu aynı IP'yi (`8.8.8.8`) duyurur.
2. İnternet router'ları (BGP aracılığıyla) en yakın/en iyi yolu seçer.
3. İstanbul'daki kullanıcı Frankfurt'a, Tayland'daki kullanıcı Singapur'a yönlendirilir.
4. Kullanıcı hiçbir şey fark etmez — her zaman aynı `8.8.8.8`'i kullanır.

---

## Nerede Kullanılır?

### DNS (En yaygın kullanım)

Google DNS (`8.8.8.8`) ve Cloudflare DNS (`1.1.1.1`) anycast adreslerdir.  
Dünya genelinde düzinelerce sunucu aynı IP'yi duyurur; sorgu en yakın sunucuya gider.

### CDN (İçerik Dağıtım Ağları)

Cloudflare, Akamai gibi CDN sağlayıcıları anycast ile içeriği dünya genelinde dağıtır.  
Türkiye'deki bir kullanıcı Frankfurt veya Amsterdam'daki sunucuya değil, İstanbul'daki PoP'a bağlanır.

### DDoS Koruması

Bir saldırı tek bir sunucuya odaklanamaz — trafik dünya genelindeki onlarca sunucuya dağıtılır,  
her sunucu yükün küçük bir parçasını taşır.

---

## IPv6 ve Anycast

IPv6'da anycast **resmi olarak tanımlıdır** (RFC 4291). IPv4'te ise anycast'i BGP sağlar — adresleme seviyesinde resmi bir kavram değildir.

```
IPv6 Anycast adresi: 2001:db8::1/128
→ Aynı adres birden fazla cihaza atanabilir
→ Paket en yakın cihaza yönlendirilir
```

> 💡 IPv6 Router'ının Anycast adresi: Her IPv6 subnet'inde subnet-router anycast adresi otomatik tanımlanır (`<prefix>::0`). Bu adrese gönderilen paket subnet'teki herhangi bir router'a ulaşır.

---

## Özet

```
Anycast  = Aynı IP → Birden fazla sunucu → En yakına git
Kullanım = DNS, CDN, DDoS koruması
Mekanizma= BGP (IPv4) / Yerel adres tanımı (IPv6)
Fayda    = Düşük gecikme + Yüksek erişilebilirlik + Yük dağılımı
```
