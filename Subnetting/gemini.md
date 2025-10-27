# Subnetting Nedir? (En Basit Anlatım)

Subnetting (Alt Ağlara Bölme), büyük bir bilgisayar ağını daha küçük, yönetilebilir alt ağlara (subnet) ayırma işlemidir.

## Neden Yapılır?

1.  **Verimlilik:** IP adresi israfını önler. Büyük bir ağı (örn: 254 adresli) 30'ar bilgisayarlı 4 ayrı ofise bölmek istediğinizde, herkese ayrı büyük bir ağ vermek yerine, o büyük ağı 4 küçük parçaya bölersiniz.
2.  **Güvenlik:** Ağları bölerek, bir alt ağdaki sorunun veya güvenlik açığının diğerlerine yayılmasını zorlaştırırsınız.
3.  **Organizasyon:** Ağı departmanlara (Muhasebe, IT, İnsan Kaynakları vb.) veya konumlara (Kat 1, Kat 2) göre ayırmayı sağlar.

## Nasıl Çalışır? (Temel Mantık)

Subnetting, bir IP adresinin "Host" (kullanıcı) için ayrılan kısmından "bit" (dijital 1 veya 0) "ödünç alıp" bu bitleri "Alt Ağ" (Subnet) adresi olarak kullanma prensibine dayanır.

Bu ayırma işlemini **Subnet Mask (Alt Ağ Maskesi)** adı verilen bir adres belirler.

## En Basit Subnetting Örneği

**Senaryo:** Elimizde `192.168.1.0` ağı var ve bu ağı 4 eşit parçaya bölmek istiyoruz.

### 1. Başlangıç Durumu (Bölünmemiş Ağ)

* **Ağ Adresi:** `192.168.1.0`
* **Normal Subnet Mask:** `255.255.255.0`
    * Bu maske, ilk 3 bölümün (`192.168.1`) **Ağ Adresi**, son bölümün (`0`) ise **Host (Kullanıcı) Adresi** olduğunu söyler.
    * Bu ağda **254** adet kullanılabilir IP adresi (`192.168.1.1`'den `192.168.1.254`'e kadar) vardır.

### 2. Bölme İşlemi (Subnetting)

Ağı 4 parçaya bölmek için Host kısmından **2 bit** "ödünç" almamız gerekir. (Çünkü $2^2 = 4$)

* Host kısmı için ayrılan son bölüm normalde `00000000` (8 bit) idi.
* İlk 2 bit'i "ödünç alıyoruz": `NN HHHHHH` (N=Yeni Subnet Biti, H=Yeni Host Biti)

### 3. Yeni Subnet Mask

* Ödünç aldığımız 2 bit'i `1` yaparak yeni maskemizi oluştururuz.
* Binary (İkili) olarak: `11000000`
* Decimal (Onluk) olarak: `192`
* **Yeni Subnet Mask:** `255.255.255.192`

### 4. Ortaya Çıkan Yeni 4 Alt Ağ (Subnet)

Yeni maskemiz (`255.255.255.192`) sayesinde `192.168.1.0` ağı şu 4 alt ağa bölünmüş olur:

**Alt Ağ 1:**
* **Ağ Adresi:** `192.168.1.0`
* Kullanılabilir IP'ler: `192.168.1.1` - `192.168.1.62`
* Yayın (Broadcast) Adresi: `192.168.1.63`

**Alt Ağ 2:**
* **Ağ Adresi:** `192.168.1.64`
* Kullanılabilir IP'ler: `192.168.1.65` - `192.168.1.126`
* Yayın (Broadcast) Adresi: `192.168.1.127`

**Alt Ağ 3:**
* **Ağ Adresi:** `192.168.1.128`
* Kullanılabilir IP'ler: `192.168.1.129` - `192.168.1.190`
* Yayın (Broadcast) Adresi: `192.168.1.191`

**Alt Ağ 4:**
* **Ağ Adresi:** `192.168.1.192`
* Kullanılabilir IP'ler: `192.168.1.193` - `192.168.1.254`
* Yayın (Broadcast) Adresi: `192.168.1.255`

**Özetle:** 254 IP'lik tek bir büyük ağı, 62'şer IP'lik 4 ayrı küçük ağa bölmüş olduk.
