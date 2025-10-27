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

## 🔑 Temel Mantık
- **1’ler (Ağ kısmı):** Blok adresini gösterir, sabit kalır.  
- **0’lar (Host kısmı):** Daire numaralarını gösterir, değişebilir.  

Subnetting yaparken, **host kısmındaki bazı bitleri ağ kısmına taşırsın** → daha fazla blok oluşur ama her blokta daha az daire kalır.

---

## 🧮 Basit Formüller
| Hesaplama Türü       | Formül                        | Açıklama |
|-----------------------|-------------------------------|----------|
| Kullanılabilir Host   | 2^(Host bit sayısı) - 2       | −2: Network ve Broadcast için |
| Alt Ağ Sayısı         | 2^(Ödünç alınan bit sayısı)   | Yeni oluşturulan blok sayısı |

---

## 🧮 Basit Formüller
| Hesaplama Türü         | Formül         | Açıklama                                      |
|------------------------|----------------|-----------------------------------------------|
| **Kullanılabilir Host Sayısı** | `2^n - 2` | `n` = Host bit sayısı (-2: Network ve Broadcast adresleri). |
| **Alt Ağ Sayısı**      | `2^s`         | `s` = Ödünç alınan bit sayısı (subnet maskına eklenen). |

---

✅ **Özet:**  
Subnetting = Büyük bir ağı küçük parçalara bölmek.  
Mantık = **1’ler ağı, 0’lar cihazı gösterir.**
