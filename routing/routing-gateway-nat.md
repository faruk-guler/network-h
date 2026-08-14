# 🌐 Routing, Gateway ve NAT

Bir veri paketinin kaynaktan hedefe ulaşması üç temel kavrama dayanır:  
**Gateway** paketin çıkış kapısıdır; **Routing** paketi nereye göndereceğine karar verir; **NAT** ise paketin kimliğini değiştirir.

---

## 1. Gateway (Ağ Geçidi)

Gateway genel bir ağ elemanıdır. Farklı protokoller, yapılar veya ağlar kullanan iki sistemi birbirine bağlayan bir "tercüman" veya "kapı" gibidir.

- Sadece IP yönlendirmesi yapmaz; gerekirse verinin formatını da değiştirir.
- Örnek: Şirket içi yerel ağınızı (LAN) internete (WAN) bağlayan router bir gateway'dir. Veya iki farklı haberleşme dilini konuşan (örneğin ses trafiği ile veri trafiği) sistemleri birbirine bağlayan cihaz bir "Voice Gateway"dir.

### 🚪 Default Gateway (Varsayılan Ağ Geçidi)

**Default Gateway**, bir cihazın kendi yerel ağı (subnet) dışına çıkmak istediğinde trafiği gönderdiği ilk router (yönlendirici) adresidir. 

Basit bir ifadeyle: **Cihazın "dış dünya kapısı"** veya **"varsayılan çıkış noktası"** dır.

- Yerel ağın **"çıkış kapısı"**dır. Genellikle router'ın LAN IP'sidir: `10.5.10.1`
- Cihaz, kendi subnet'inde olmayan **tüm paketleri** buraya gönderir.
- ⚠️ Gateway tanımlanmamışsa cihaz sadece yerel ağda çalışır; internete **çıkamaz.**

> **Örnek:** Evinizdeki bir bilgisayar Google'a (8.8.8.8) bağlanmak istiyorsa, önce bu paketi modeminize (default gateway) gönderir. Modem de sıradaki adıma iletir. Sıradaki adımda standart ev kullanıcıları için ISP Router olur.

### Görsel Örnek

Aşağıdaki şemada **default gateway** kavramını iki farklı seviyede görebilirsiniz:

```
                  INTERNET
                     │
                     │
          ┌──────────▼─────┐
          │   ISP Router   │ ← Default Gateway (Modem için)
          │                │
          └───────┬────────┘
                  │
                  │
    ┌─────────────|─────────────┐
    │          EV |             │
    │             |             │
    │    ┌────────|─────┐       │
    │    │ ADSL/Kablo   │       │
    │    │    MODEM     │ ← Default Gateway (Bilgisayar için)
    │    └──────────────┘       │
    │         │  │ │            │
    │  ┌──────┘  │ └──┐         │
    │  │         │    │         │
    │ Laptop    PC  Telefon     │
    │                           │
    └───────────────────────────┘
```

---

## 2. Routing (Yönlendirme)

Routing; veri paketlerinin kaynaktan hedefe giderken **en uygun yolu bulma** sürecidir.  
Bu kararı veren cihaz **router (yönlendirici)**'dır.

---

### 📍 Yerel Ağ mı, İnternet mi?

| Senaryo | Açıklama |
|:---|:---|
| **📍 Yerel Erişim** | `10.5.10.10` → `10.5.10.20`: Aynı ağda olduklarından gateway devreye **girmez**, cihazlar switch üzerinden doğrudan haberleşir. |
| **🌍 İnternet Erişimi** | `10.5.10.10` → `193.156.56.164`: Farklı ağda olduğu için paket önce `10.5.10.1` (Gateway) cihazına iletilir, oradan dış ağa (ISP) yönlendirilir. |

---

### 🧠 IP Yönlendirme Mantığı

Cihaz, paket göndermeden önce şu 3 adımlı kararı verir:

1. **Subnet Kontrolü:** Hedef IP, kendi Subnet Mask'i ile aynı ağda mı?
2. **✅ Aynı Ağda ise:** Doğrudan hedefe gönderilir.
3. **❌ Farklı Ağda ise:** Paket **Varsayılan Ağ Geçidi**'ne teslim edilir. Router, Routing Table'a bakarak en uygun çıkış portunu seçer.

---

### 🗺️ Routing Table (Yönlendirme Tablosu)

Router, her paketi nereye göndereceğini **Routing Table** adlı bir tabloya bakarak karar verir.

Basit bir örnek:

| Hedef Ağ | Subnet Mask | Gateway | Açıklama |
|:---|:---|:---|:---|
| `10.5.10.0` | `255.255.255.0` | — | Yerel ağ, doğrudan gönder |
| `0.0.0.0` | `0.0.0.0` | `193.156.56.1` | Diğer tüm paketler → ISP'ye gönder *(Default Route)* |

> 💡 `0.0.0.0` satırı **Default Route** olarak adlandırılır. "Başka bir kural yoksa buradan çık" anlamına gelir.

---

## 3. NAT (Network Address Translation — Ağ Adresi Çevirisi)

NAT, iç ağdaki cihazların **tek bir Public IP** üzerinden internete çıkmasını sağlayan mekanizmadır.  
Teknik olarak routing'den bağımsız bir işlemdir; ancak router üzerinde çalıştığı için ikisi birlikte ele alınır.

---

### ❓ Neden NAT'a İhtiyaç Var?

İç ağlarda kullanılan IP adresleri **özel (private)** adreslerdir ve internette geçersizdir.

| IP Aralığı | Türü |
|:---|:---|
| `10.0.0.0 – 10.255.255.255` | Private (Özel) |
| `172.16.0.0 – 172.31.255.255` | Private (Özel) |
| `192.168.0.0 – 192.168.255.255` | Private (Özel) |
| `193.156.56.164` gibi adresler | Public (Genel) — internette geçerli |

Evde 5 cihazın olduğunu düşün. Hepsinin farklı private IP'si var ama internete **tek bir public IP** ile çıkıyorlar. Bunu sağlayan NAT'tır.

---

### 🔄 NAT Nasıl Çalışır?

| Adım | İşlem |
|:---|:---|
| **İç Ağ** | Cihaz `10.5.10.10` IP'siyle paket oluşturur. |
| **Çıkış (SNAT)** | Router, kaynak IP'yi kendi Public IP'si `193.156.56.164` ile değiştirir ve NAT tablosuna kaydeder. |
| **İnternet** | Karşı sunucu paketi `193.156.56.164`'ten gelmiş gibi görür, cevabı oraya gönderir. |
| **Dönüş** | Router, NAT tablosundan hangi iç cihaza ait olduğunu bulur ve paketi `10.5.10.10`'a iletir. |

---

### ✅ NAT'ın Avantajları

- **IP Tasarrufu:** Tek Public IP ile onlarca cihaz internete çıkabilir.
- **Güvenlik:** İç ağ yapısı (private IP'ler) dışarıya gizlenir.

---

## 📌 Kısa Özet

> 🔹 **Gateway** → Cihazın dış dünya kapısı (genellikle router)  
> 🔹 **Aynı ağ** → Doğrudan git (Gateway yok)  
> 🔹 **Farklı ağ** → Gateway'e ver, router yönlendirir  
> 🔹 **Routing Table** → Router'ın karar defteri  
> 🔹 **NAT** → Private IP'yi Public IP'ye çevirerek internete çıkışı sağlar  
> 🔹 **Routing ≠ NAT** → İkisi farklı iş yapar, ikisi de router'da çalışır
