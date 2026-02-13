# 07 - VLAN Temelleri: Sanal Apartman Blokları

**VLAN (Virtual Local Area Network)**, fiziksel bir ağı **mantıksal olarak** küçük ağlara bölme tekniğidir. Güvenlik ve performans için hayati öneme sahiptir!

> 💡 **Metafor:** Tek bir dev apartmanda (fiziksel switch) birden fazla **sanal bina** (VLAN) oluşturmak gibidir.

---

## 🏢 VLAN Nedir?

### Geleneksel Ağ (VLAN Olmadan)

Bir ofiste 3 departman olsun:

- **IT Ekibi**
- **Muhasebe**
- **Satış**

**Sorun:** Hepsi aynı switch'e bağlıysa, **aynı Yayın Alanındadır (Broadcast Domain)**. Yani:

- IT'nin broadcast'i muhasebe de alır (gereksiz trafik!)
- Güvenlik zafiyeti (Herkes herkesi "görebilir")

### VLAN ile Ağ ✅

Aynı fiziksel switch'te **3 ayrı VLAN** oluştururuz:

- **VLAN 10:** IT Ekibi
- **VLAN 20:** Muhasebe
- **VLAN 30:** Satış

**Sonuç:**

- Her VLAN kendi broadcast domain'i → Performans artışı
- VLAN'lar birbirini göremez → Güvenlik
- IT ile Muhasebe iletişimi için **router** gerekir (inter-VLAN routing)

---

## 🎯 Neden VLAN Kullanırız?

### 1. 🔒 Güvenlik

**Senaryo:** Misafir Wi-Fi ile şirket ağı aynı switch'te.

- **VLAN yoksa:** Misafirler şirket sunucularına erişebilir! ❌
- **VLAN varsa:** Misafirler VLAN 99'da, sunucular VLAN 10'da → **Erişim yok!** ✅

### 2. ⚡ Performans

**Broadcast Storm (Fırtınası) Önleme:**

- Bir ağda 200 cihaz varsa, bir broadcast paketi **199 cihaza** gider (gereksiz!)
- VLAN ile 4 ağa bölersen, broadcast sadece **kendi VLAN'ına** gider (örn: 50 cihaz)

### 3. 📐 Esneklik

**Fiziksel konuma bağlı kalmama:**

- Muhasebe departmanı 3. katta, ama cihazları VLAN 20'de
- Yeni muhasebeci 1. kata taşınsa bile, yine VLAN 20'ye konfigüre edilir
- **Fiziksel yer ≠ Ağ yapısı**

### 4. 💰 Maliyet Tasarrufu

Her bir departman için ayrı switch almak yerine, **tek switch** + VLAN kullanırsınız.

---

## 🔧 VLAN Türleri

### 1. Data VLAN (Normal VLAN)

Kullanıcı verileri için standart VLAN.

**Örnek:**

```text
VLAN 10: IT Ekibi
VLAN 20: Muhasebe
VLAN 30: Satış
```

### 2. Voice VLAN (Ses Trafiği)

VoIP telefonları için özel VLAN.

**Neden ayrı?**

- Ses trafiği **gecikmeye hassastır** (latency kritik!)
- QoS (Quality of Service) ile öncelik verilir

**Örnek:**

```text
VLAN 100: IP Telefonları
```

### 3. Management VLAN (Yönetim)

Switch'in kendisini yönetmek için kullanılan VLAN.

**Örnek:**

```text
VLAN 99: Switch Yönetimi (SSH/Telnet erişimi)
```

### 4. Native VLAN

Trunk port'larda, **tag'siz** (etiketlenmemiş) trafiğin ait olduğu VLAN.

**Varsayılan:** VLAN 1  
**Güvenlik için:** VLAN 1'den farklı bir değer kullanın (örn: VLAN 999)

---

## 🚪 VLAN Port Tipleri

### 1. Erişim Portu (Access Port)

**Kullanım:** Son kullanıcı cihazlarını (PC, telefon) bağlar.

> 💡 **Benzetme:** Daire kapısı. Sadece o daireye (VLAN'a) girer/çıkar.

**Özellik:**

- **Tek bir VLAN**'a aittir
- Trafik **tag'siz** (untagged) gelir/gider

**Konfigürasyon (Cisco):**

```text
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

**Örnek:**

```text
Port Fa0/1 → VLAN 10 (IT)
Port Fa0/2 → VLAN 20 (Muhasebe)
```

---

### 2. Taşıyıcı Port (Trunk Port)

**Kullanım:** Switch-to-switch veya switch-to-router bağlantıları.

> 💡 **Benzetme:** Binanın ana asansörü. Her kattan (VLAN'dan) insan taşır.

**Özellik:**

- **Birden fazla VLAN** trafiğini taşır
- Trafik **tag'li** (802.1Q etiketiyle) gider

**Konfigürasyon (Cisco):**

```text
Switch(config)# interface gi0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
```

**Örnek:**

```text
Switch A                    Switch B
[Trunk Port] ←─────────→ [Trunk Port]
 VLAN 10, 20, 30           VLAN 10, 20, 30
```

---

## 🏷️ VLAN Etiketleme (Tagging - 802.1Q)

### Nasıl Çalışır?

Trunk port üzerinden bir paket gönderildiğinde, switch **4 byte'lık bir tag** ekler:

```text
Ethernet Frame:
┌──────────┬──────────┬─────────┬──────┬──────┐
│ Dest MAC │ Src MAC  │ 802.1Q  │ Data │ FCS  │
│          │          │ (VLAN)  │      │      │
└──────────┴──────────┴─────────┴──────┴──────┘
                       ↑
                  4 byte (VLAN ID)
```

**VLAN Tag İçeriği:**

- **TPID** (Tag Protocol ID): 0x8100 (802.1Q olduğunu belirtir)
- **PCP** (Priority): QoS önceliği (0-7)
- **VLAN ID**: 1-4094 arası (12 bit)

---

## 🌉 Inter-VLAN Routing (VLAN'lar Arası İletişim)

**Problem:** VLAN 10'daki bir PC, VLAN 20'deki sunucuya erişmek istiyor.

**Çözüm:** Router veya Layer 3 Switch kullanarak **routing** yapılır.

### Yöntem 1: Router-on-a-Stick

**Tek router interface** + **alt interface'ler (subinterface)**

**Konfigürasyon:**

```text
Router(config)# interface gi0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0

Router(config)# interface gi0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
```

### Yöntem 2: Layer 3 Switch (SVI)

**Switch'in kendisi routing yapar** (daha hızlı!).

**Konfigürasyon:**

```text
Switch(config)# ip routing
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0

Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
```

---

## 📊 VLAN Planlama Örneği

### Senaryo: Orta Ölçekli Ofis

**Departmanlar:**

- IT: 30 kişi
- Muhasebe: 15 kişi
- Satış: 40 kişi
- Yönetim: 10 kişi
- Misafir Wi-Fi: 50 cihaz

**VLAN Tasarımı:**

| VLAN ID | Departman  | Subnet           | Gateway      |
| ------- | ---------- | ---------------- | ------------ |
| 10      | IT         | 192.168.10.0/24  | 192.168.10.1 |
| 20      | Muhasebe   | 192.168.20.0/27  | 192.168.20.1 |
| 30      | Satış      | 192.168.30.0/26  | 192.168.30.1 |
| 40      | Yönetim    | 192.168.40.0/28  | 192.168.40.1 |
| 99      | Misafir    | 192.168.99.0/26  | 192.168.99.1 |
| 999     | Management | 10.0.99.0/29     | 10.0.99.1    |

---

## 🔐 VLAN Güvenlik İpuçları

1. **Native VLAN'ı değiştirin:** VLAN 1 yerine kullanılmayan bir VLAN kullanın (örn: 999)
2. **Kullanılmayan portları kapatın:** Shutdown veya dummy VLAN'a atayın
3. **VLAN 1 kullanmayın:** Cisco switch'lerde varsayılan, saldırı hedefi!
4. **Private VLAN:** Aynı VLAN içinde bile cihazları izole edin
5. **VACL (VLAN ACL):** VLAN içindeki trafiği filtreleyin

---

## 💡 VLAN Best Practices

1. **Dokümante edin:** Hangi VLAN hangi departmanda kullanılıyor, mutlaka yazın.
2. **Standartlaşın:** Tüm ofislerde aynı VLAN ID'leri kullanın (10=IT, 20=Muhasebe vb.)
3. **QoS ayarlayın:** Voice VLAN'ına yüksek öncelik verin.
4. **Test edin:** VLAN konfigürasyonunu prod'a almadan önce test ortamında deneyin.

---

## 🔗 VLAN Komutları (Cisco Hızlı Referans)

### VLAN Oluşturma

```text
Switch(config)# vlan 10
Switch(config-vlan)# name IT-Department
```

### Access Port Ayarlama

```text
Switch(config)# interface fa0/5
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

### Trunk Port Ayarlama

```text
Switch(config)# interface gi0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 999
Switch(config-if)# switchport trunk allowed vlan 10,20,30
```

### VLAN Görüntüleme

```text
Switch# show vlan brief
Switch# show interfaces trunk
```

---

## 🎓 Özet

- **VLAN = Fiziksel ağı mantıksal olarak bölme**
- **Access Port:** Tek VLAN, son kullanıcı
- **Trunk Port:** Çoklu VLAN, switch/router arası
- **802.1Q:** VLAN tagging standardı
- **Inter-VLAN Routing:** Router veya Layer 3 Switch gerekir

---

**Navigasyon:**

- [⬅️ Önceki: Uygulama Protokolleri](./06-Uygulama-Protokolleri-DNS-DHCP-HTTP.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Portlar ve Servisler](./ports/07-Portlar-ve-Servisler-Port-Nedir.md)
