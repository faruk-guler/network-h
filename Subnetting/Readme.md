# 🏡 Subnetting (Alt Ağlara Bölme) Nedir?
Subnetting, büyük bir IP adres aralığını daha küçük ve yönetilebilir parçalara (subnet’lere) bölme işlemidir.  
Amaç: IP adreslerini verimli kullanmak, ağı düzenlemek ve güvenliği artırmaktır.

---

## 📖 Günlük Hayat Metaforu
| Ağ Kavramı        | Günlük Hayat Karşılığı   | Açıklama |
|-------------------|--------------------------|----------|
| Büyük Ağ (IP Bloğu) | Devasa Konut Sitesi     | Binlerce daire (cihaz) için ayrılmış büyük adres aralığı |
| Subnetting        | Siteyi Bloklara Ayırmak  | Büyük IP aralığını A Blok, B Blok, C Blok gibi küçük parçalara bölmek |
| Alt Ağ Maskesi    | Kapıcı/Güvenlik Kuralı   | Bir IP adresinin hangi blokta olduğunu ve o blokta kaç daire (cihaz) olduğunu belirler |

---

## 🌟 Neden Önemli?
- **Adres Verimliliği:** Adresler boşa gitmez.  
- **Performans:** Bir bloktaki trafik diğerini etkilemez.  
- **Hızlı Yönlendirme:** Router, tek tek dairelere bakmak yerine doğrudan doğru bloğa gider.  

---

## Nasıl Çalışır? (Temel Mantık)

Subnetting, bir IP adresinin "Host" (kullanıcı) için ayrılan kısmından "bit" (dijital 1 veya 0) "ödünç alıp" bu bitleri "Alt Ağ" (Subnet) adresi olarak kullanma prensibine dayanır.

Bu ayırma işlemini **Subnet Mask (Alt Ağ Maskesi)** adı verilen bir adres belirler.

---

## 🔑 Temel Mantık
- **1’ler (Ağ kısmı):** Blok adresini gösterir, sabit kalır.  
- **0’lar (Host kısmı):** Daire numaralarını gösterir, değişebilir.  

Subnetting yaparken, **host kısmındaki bazı bitleri ağ kısmına taşırsın** → daha fazla blok oluşur ama her blokta daha az daire kalır.

---

## 🧮 Basit Formüller
| Hesaplama Türü         | Formül         | Açıklama                                      |
|------------------------|----------------|-----------------------------------------------|
| **Kullanılabilir Host Sayısı** | `2^n - 2` | `n` = Host bit sayısı (-2: Network ve Broadcast adresleri). |
| **Alt Ağ Sayısı**      | `2^s`         | `s` = Ödünç alınan bit sayısı (subnet maskına eklenen). |

---

## ⚡ Örnek: 192.168.1.0/24’ü 4 Alt Ağa Bölme
1. **Başlangıç**: `/24` (255.255.255.0) → 256 IP adresi.
2. **Alt Ağ Sayısı**: 4 subnet için 2 bit gerekir (`2^2 = 4`).
3. **Yeni Maske**: `/24 + 2 = /26` (255.255.255.192). Her subnet 64 IP içerir (`256 ÷ 4 = 64`).
4. **Subnet Aralıkları**:
   - 192.168.1.0 – 192.168.1.63 (Kullanılabilir: 192.168.1.1 - 192.168.1.62)
   - 192.168.1.64 – 192.168.1.127 (Kullanılabilir: 192.168.1.65 - 192.168.1.126)
   - 192.168.1.128 – 192.168.1.191 (Kullanılabilir: 192.168.1.129 - 192.168.1.190)
   - 192.168.1.192 – 192.168.1.255 (Kullanılabilir: 192.168.1.193 - 192.168.1.254)

---
## Hızlı Kural:
- **Alt ağ sayısı** = `2ⁿ` (n = ödünç alınan bit sayısı)  
- **Host sayısı** = `2ᵐ – 2` (m = kalan host biti; –2 çünkü network ve broadcast adresleri kullanılmaz)

> Örnek: `/26` → 26 network biti → 6 host biti → `2⁶ – 2 = 62` kullanılabilir IP

---

✅ **Özet:**  
- **Subnetting** = Büyük ağı küçük parçalara bölmek.
- Bit ödünç al → yeni mask oluştur → alt ağları listele.
- **Formüller**: Host sayısı = `2^(host bitleri) - 2`, Alt ağ sayısı = `2^(ödünç alınan bitler)`.
- **Pratik İpucu**: Subnet hesaplayıcıları (örn. subnet-calculator.com) veya Cisco CLI ile hızlıca yapabilirsin!

> Daha fazla bilgi için [farukguler.com Subnetting Toolu](https://farukguler.com/app/IPv4-subnet-calculator/) veya çevrimiçi araçları kullan!
