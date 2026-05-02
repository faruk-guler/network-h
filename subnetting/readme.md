# 📘 IP Subnetting (Alt Ağlara Bölme) Rehberi

## 1. Konu Özeti: Subnetting Nedir?
Subnetting, büyük bir IP bloğunu, daha yönetilebilir küçük ağlara (subnets) bölme işlemidir.

### 🔑 Temel Kavramlar
*   **Network ID (Ağ Adresi):** Subnet'in başlangıç noktasıdır. Cihazlara verilmez.
*   **Broadcast Adresi:** Subnet'in bitiş noktasıdır. Tüm cihaza mesaj atmak için kullanılır, cihazlara verilmez.
*   **CIDR (/xx):** Ağ maskesinin kaç bitlik olduğunu gösterir. (Örn: /24, /26)
*   **Artış Sayısı (Block Size):** Bir alt ağın kaç IP adresinden oluştuğunu belirleyen sihirli sayıdır.

---

## 2. Hesaplama Mantığı: "Sihirli Sayı" Yöntemi
Bir subnet'in sınırlarını bulmak için şu formülü kullanırız:

> **Artış Sayısı = 256 - Subnet Mask Değeri**
> *(veya 256 - CIDR'nin son oktet değeri)*

Örneğin `/26` maskesi için:
1.  `/24` = `255.255.255.0`
2.  `/26` = 2 bit daha ödünç alındı → `11000000` (Binary) = `192` (Decimal)
3.  **Artış Sayısı:** `256 - 192 = 64`

Bu demektir ki ağlar 64'er 64'er artarak ilerler: `0, 64, 128, 192...`

---

## 3. Örnek Analiz: 192.168.75.128 / 26

Elimizdeki veri: `192.168.75.128` ve `Mask: /26`.
Bu ağın sınırlarını ve kullanılabilir IP'lerini bulalım.

### ️ Adım Adım Çözüm

**1. Maske ve Artış Sayısını Belirle:**
*   CIDR `/26` olduğu için son oktet maskesi **192**'dir.
*   **Artış Sayısı (Blok Büyüklüğü):** 64 IP.

**2. Ağın Konumunu Tespit Et:**
Ağlar 64'er 64'er arttığına göre sıralama şöyledir:
1.  Ağ: `192.168.75.0`
2.  Ağ: `192.168.75.64`
3.  Ağ: **`192.168.75.128`** 👈 *Bizim Ağımız Burası!*
4.  Ağ: `192.168.75.192`

**3. Sınırları Çiz (Network ve Broadcast):**
*   **Network ID:** `192.168.75.128` (Başlangıç)
*   **Sonraki Ağın Başlangıcı:** `128 + 64 = 192`
*   **Broadcast Adresi:** Bir sonraki ağın 1 eksiği → `192 - 1 = 191`

**4. Kullanılabilir (Host) IP'leri Belirle:**
*   **İlk IP:** Network + 1 → `128 + 1 = 129`
*   **Son IP:** Broadcast - 1 → `191 - 1 = 190`

---

## 4. Sonuç Tablosu

Aşağıda `192.168.75.128/26` ağına ait teknik detaylar bulunmaktadır:

| Özellik | Değer | Açıklama |
| :--- | :--- | :--- |
| **Ağ Adı (Network ID)** | `192.168.75.128` | Bu subnet'in kimliği (atanamaz). |
| **Subnet Mask** | `255.255.255.192` | CIDR karşılığı `/26`. |
| **Broadcast Adresi** | `192.168.75.191` | Bu subnet'in son adresi (atanamaz). |
| **İlk Kullanılabilir IP** | `192.168.75.129` | İlk cihaza verilecek IP. |
| **Son Kullanılabilir IP** | `192.168.75.190` | Son cihaza verilecek IP. |
| **Toplam Host Sayısı** | 62 Adet | `64 (Blok) - 2 (Network & Broadcast)`. |

---

## 💡 Özet ve Püf Noktası
Bir IP adresi verildiğinde (`...128`), hemen **64** katlarını aklına getir:
*   `0, 64, 128, 192`
*   Eğer IP `.128` ise, bu bir **Network ID**'dir (çünkü artış sayısına tam bölünüyor).
*   Eğer IP `.130` olsaydı, bu da aynı ağda (128-191 arası) bulunan **bir cihazın IP'si** olurdu.
