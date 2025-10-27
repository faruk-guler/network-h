# 🌐 Subnetting Nedir?

Subnetting, büyük bir IP ağını daha küçük alt ağlara (**subnet**) bölme işlemidir.  
**Amaç:** IP adreslerini verimli kullanmak, ağ trafiğini düzenlemek ve güvenliği artırmak.

---

## 🔑 Temel Mantık
- IP adresi = **Ağ kısmı** (sabit, hangi bloğa ait olduğunu gösterir) + **Host kısmı** (değişken, cihazları tanımlar).
- Subnetting: Host kısmından bit alarak ağ kısmını büyütürsün → Daha fazla subnet, ama her subnet’te daha az cihaz.

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

## ✅ Özet
- Subnetting = Büyük ağı küçük parçalara bölme.
- **Formüller**: Host sayısı = `2^(host bitleri) - 2`, Alt ağ sayısı = `2^(ödünç alınan bitler)`.
- **Pratik İpucu**: Subnet hesaplayıcıları (örn. subnet-calculator.com) veya Cisco CLI ile hızlıca yapabilirsin!

> Daha fazla bilgi için [Cisco Subnetting Rehberi](https://www.cisco.com) veya çevrimiçi araçları kullan!
