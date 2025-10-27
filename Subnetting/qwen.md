# Subnetting Nedir? (En Kısa ve Basit Anlatım)

**Subnetting (alt ağ oluşturma)**, büyük bir IP ağını daha küçük, yönetilebilir parçalara (alt ağlara) bölmek demektir.

---

## Neden Yapılır?
- Ağ trafiğini azaltmak  
- Güvenliği artırmak  
- IP adreslerini verimli kullanmak  

---

## Nasıl Yapılır? (Adım Adım – Basit Örnek)

### 1. Başlangıç: Bir IP ve Subnet Maskesi Al
Örnek:  
- IP: `192.168.1.0`  
- Subnet Maskesi: `255.255.255.0` → `/24` (yani 24 bit network, 8 bit host)

### 2. Alt Ağ Sayısı Belirle
Diyelim **2 alt ağ** istiyoruz.  
2 alt ağ için en az **1 bit** gerekir (`2¹ = 2`).

### 3. Yeni Subnet Maskesi Hesapla
- Eski mask: `/24` → `11111111.11111111.11111111.00000000`  
- 1 bit daha al: `/25` → `11111111.11111111.11111111.10000000`  
- Yeni subnet maskesi: `255.255.255.128`

### 4. Alt Ağları Belirle
- **1. Alt Ağ**: `192.168.1.0/25`  
  - Kullanılabilir IP’ler: `192.168.1.1` – `192.168.1.126`  
  - Broadcast: `192.168.1.127`

- **2. Alt Ağ**: `192.168.1.128/25`  
  - Kullanılabilir IP’ler: `192.168.1.129` – `192.168.1.254`  
  - Broadcast: `192.168.1.255`

---

## Hızlı Kural:
- **Alt ağ sayısı** = `2ⁿ` (n = ödünç alınan bit sayısı)  
- **Host sayısı** = `2ᵐ – 2` (m = kalan host biti; –2 çünkü network ve broadcast adresleri kullanılmaz)

> Örnek: `/26` → 26 network biti → 6 host biti → `2⁶ – 2 = 62` kullanılabilir IP

---

✅ **Özet**: Subnetting = Büyük ağı küçük parçalara bölmek.  
Bit ödünç al → yeni mask oluştur → alt ağları listele.
