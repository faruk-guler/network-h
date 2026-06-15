# 🌐 Routing ve NAT (Yönlendirme ve Adres Çevirisi)

Bir veri paketinin kaynaktan hedefe ulaşması iki temel mekanizmaya dayanır:  
**Routing** paketi nereye göndereceğine karar verir; **NAT** ise paketin kimliğini değiştirir.

---

## 1. Routing (Yönlendirme)

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
2. **✅ Aynı Ağda ise:** Doğrudan hedefe gönderilir. *(→ Bkz. ARP Bölümü: MAC adresi bu aşamada devreye girer.)*
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

### 🚪 Varsayılan Ağ Geçidi (Default Gateway)

- Yerel ağın **"çıkış kapısı"**dır. Genellikle router'ın LAN IP'sidir: `10.5.10.1`
- Cihaz, kendi subnet'inde olmayan **tüm paketleri** buraya gönderir.
- ⚠️ Gateway tanımlanmamışsa cihaz sadece yerel ağda çalışır; internete **çıkamaz.**

---

## 2. NAT (Network Address Translation — Ağ Adresi Çevirisi)

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

> 🔹 **Aynı ağ** → Doğrudan git (Gateway yok)  
> 🔹 **Farklı ağ** → Gateway'e ver, router yönlendirir  
> 🔹 **Routing Table** → Router'ın karar defteri  
> 🔹 **NAT** → Private IP'yi Public IP'ye çevirerek internete çıkışı sağlar  
> 🔹 **Routing ≠ NAT** → İkisi farklı iş yapar, ikisi de router'da çalışır
