# 🌐 Routing (Yönlendirme)

Veri paketlerinin kaynaktan hedefe giderken en uygun yolu bulma sürecidir.
---

### 📍 Yerel vs İnternet Erişimi
| Senaryo | Açıklama |
|:---|:---|
| **📍 Yerel Erişim** | `10.5.10.10` → `10.5.10.20`: Aynı ağda oldukları için **gateway devreye girmez**, switch üzerinden doğrudan haberleşirler. |
| **🌍 İnternet Erişimi** | `10.5.10.10` → `193.156.56.164`: Farklı ağda olduğu için paket önce `10.5.10.1` (Gateway) cihazına iletilir, oradan dış ağa (ISP) yönlendirilir. |

---

### 🧠 IP Yönlendirme Mantığı (3 Adım)
Cihaz paket göndermeden önce şu kararı verir:
1. **Subnet Kontrolü:** Hedef IP, kendi `Subnet Mask` ile aynı ağda mı?
2. **✅ Aynı Ağda ise:** Doğrudan hedefe gönderilir (ARP ile MAC adresi bulunur).
3. **❌ Farklı Ağda ise:** Paket **Varsayılan Ağ Geçidi**'ne teslim edilir. Router, `Routing Table`'a bakarak en uygun çıkış portunu seçer.

---

### 🚪 Varsayılan Ağ Geçidi (Default Gateway)
- Yerel ağın **"çıkış kapısı"**dır (Genellikle router LAN IP'si: `10.5.10.1`).
- Cihaz, kendi subnet'inde olmayan **tüm paketleri** buraya gönderir.
- ⚠️ Gateway tanımlanmamışsa cihaz sadece yerel ağda çalışır; internete çıkamaz.

---

### 🔄 NAT (Network Address Translation)
| Adım | İşlem |
|:---|:---|
| **Private IP** | İç ağda `10.x.x.x` gibi özel IP'ler kullanılır (internette geçersiz). |
| **Çıkış (SNAT)** | Router, paketi dışarı gönderirken kaynak IP'yi kendi **Public IP**'si (`193.156.56.164`) ile değiştirir. |
| **Dönüş** | Gelen cevapta router, NAT tablosundan hangi iç cihaza ait olduğunu bulur ve paketi doğru hedefe iletir. |
| **✅ Avantaj** | Tek Public IP ile çoklu cihaz internete çıkar + İç ağ yapısı dışarıya gizlenir (Güvenlik). |

---

> 📌 **Kısa Özet:**  
> 🔹 Aynı ağ → Doğrudan git  
> 🔹 Farklı ağ → Gateway'e ver  
> 🔹 Dışarı çıkış → NAT ile kimliği değiştir  
> 🔹 Router → Routing Table kurallarına göre yönlendirir
