# 04 - Subnetting Mantığı: Site Yönetimi ve Güvenlik 🏢

**Subnetting** (Alt Ağlara Bölme), elinizdeki büyük bir ağı, daha küçük ve yönetilebilir parçalara ayırma işlemidir.

Bunu bir **"Konut Projesi / Site Yönetimi"** olarak düşüneceğiz.

---

## 🏗️ Metafor: Devasa Bir Site Kuruyoruz

Elinizde **192.168.1.0** adında devasa bir arazi var. Buraya binalar yapıp insanları yerleştireceksiniz.
Ama herkesi tek bir devasa bloğa koyarsanız kaos çıkar! Postacı kimi nerede bulacağını şaşırır, güvenlik zafiyeti olur.

**Çözüm:** Araziyi (Network) bloklara (Subnet) ayırmak.

| Ağ Terimi | Günlük Hayat Karşılığı | Açıklama |
|-----------|------------------------|----------|
| **Network (Ağ Adresi)** | Site Arazisi | Tüm binaların bulunduğu ana alan. |
| **Subnet (Alt Ağ)** | Bloklar (A Blok, B Blok) | Sitenin daha küçük, yönetilebilir parçaları. |
| **Host (Cihaz)** | Daireler | İnsanların yaşadığı yerler (Bilgisayarlar, Telefonlar). |
| **Alt Ağ Maskesi** | Güvenlik Kulübesi / Nizamiye | Hangi dairenin hangi blokta olduğunu bilen sistem. |

---

## 🛡️ Alt Ağ Maskesi: Güvenlik Görevlisi

**Alt Ağ Maskesi** (Subnet Mask), IP adresinin neresinin **Blok Adı**, neresinin **Daire Numarası** olduğunu belirleyen kuraldır.

Örneğin: `255.255.255.0` (veya `/24`)

Bu maske güvenlik görevlisine şunu der:
> "İlk 3 hane (192.168.1) Blok Adıdır, bunlara dokunma. Son hane (0-255) Daire Numarasıdır, buraya istediğini yerleştir."

Eğer maske değişirse, kurallar da değişir!

---

## ⚡ Neden Subnetting Yaparız?

1. **Güvenlik Çemberi:** Muhasebe departmanı (A Blok) ile Misafir Ağı (B Blok) birbirini görmesin.
2. **Performans:** Herkes aynı anda bağırırsa (Broadcast) kimse birbirini duyamaz. Bloklara ayırırsak gürültü azalır.
3. **Düzen:** "Arıza nerede?" diye ararken tüm siteye bakmak yerine sadece B Bloğa bakarsınız.

---

## 🔪 Pastayı Dilimlemek (Subnetting İşlemi)

Diyelim ki elinizde `/24` bir ağ (256 IP) var. Ama siz **4 tane ayrı departman** (Muhasebe, İK, IT, Satış) kurmak istiyorsunuz.

Her departmana ayrı bir "Blok" vermemiz lazım.

### Nasıl Yapılır? (Mantık)

IP adresindeki **"Daire Numarası"** (Host) kısmından ödünç yer alıp, **"Blok Adı"** (Network) kısmına ekleriz.

1. **Başlangıç:** `192.168.1.0/24` (Tek parça, 256 daire)
2. **Hedef:** 4 Parça
3. **İşlem:** Daire numarasından yer çal, blok adına ekle.

### Sonuç Tablosu

| Departman | Ağ Adresi (Network) | Kullanılabilir Daireler (IP) | Yayın Adresi (Broadcast) |
|-----------|-----------------------|------------------------------|--------------------|
| **Muhasebe** | 192.168.1.**0** | 1-62 | 63 |
| **İK** | 192.168.1.**64** | 65-126 | 127 |
| **IT** | 192.168.1.**128** | 129-190 | 191 |
| **Satış** | 192.168.1.**192** | 193-254 | 255 |

> ⚠️ **Dikkat:** Böldükçe "Blok Adı" (Network) ve "Duyuru Adresi" (Broadcast) için her seferinde 2 adres harcanır. Yani daire sayınız biraz azalır.

---

## 🧮 Meraklısına: Arkaplandaki Matematik (Binary)

> *Bu kısmı anlamak zorunda değilsiniz, ama mantığı kavramak için harikadır.*

Bilgisayarlar her şeyi 1 ve 0 olarak görür.
`/24` demek, **24 tane 1** demektir.

```text
/24 -> 11111111.11111111.11111111.00000000
       (Network Kısmı)           (Host Kısmı)
```

Eğer biz bunu 4 parçaya bölmek istersek, Host kısmından (Sıfırlardan) 2 tane bit ödünç alırız.

```text
/26 -> 11111111.11111111.11111111.11000000
                                  ^^
                                  Ödünç alınan 2 bit
```

Neden 2 bit? Çünkü `2^2 = 4` alt ağ eder.
Yeni maskemiz `/26` olur.

---

## 🔗 Hızlı Hesaplama İçin

Elle hesaplamak zordur ve hata yapmaya müsaittir. Gerçek hayatta biz de hesap makinesi kullanıyoruz!

- 🧮 [Subnet Hesaplayıcı](https://farukguler.com/app/IPv4-subnet-calculator/)

---

**Navigasyon:**

- [⬅️ Önceki: IP Adresi ve CIDR](./04-IP-Adresleme-ve-Subnetting-IP-Adresi-ve-CIDR.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Pratik Örnekler](./04-IP-Adresleme-ve-Subnetting-Pratik-Ornekler.md)
