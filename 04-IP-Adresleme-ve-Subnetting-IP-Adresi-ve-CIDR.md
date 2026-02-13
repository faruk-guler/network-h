# 04 - IP Adresi ve CIDR: İnternet Adresleme için İnsancıl Rehber

## 🏠 IP Adresi Nedir? (Posta Sistemi Metaforu)

Hayal edin: Devasa bir şehirdesiniz ve bir arkadaşınıza mektup göndermek istiyorsunuz. Mektubu postaya verdiğinizde, posta servisinin arkadaşınızı bulabilmesi için bir **adrese** ihtiyacı var.

İnternette de aynı şey geçerli!

- **IP Adresi** = Dijital dünyadaki posta adresidir.
- Her bilgisayar, telefon, tablet vs. internete bağlandığında bir IP adresi alır.
- Bu adres sayesinde veri paketleri (mektuplar) kaybolmadan doğru cihaza ulaşır.

### 📍 IP Adresi Örneği

```text
192.168.1.10
```

**Gerçek hayat karşılığı:**

```text
Atatürk Mahallesi, Cumhuriyet Caddesi, No: 10, Daire: 5
```

---

## 🌍 İki Tip IP Adresi Var

### 1. IPv4 (Klasik Posta Kodu)

Günümüzde hala en yaygın kullanılan sistemdir.

- **Yapısı:** 4 adet sayıdan oluşur (her biri 0-255 arası).
- **Örnek:** `192.168.1.1`
- **Sorun:** Dünyada sadece 4.3 milyar tane var ve neredeyse tükendi!

### 2. IPv6 (Yeni Nesil Adresleme)

Geleceğin standardı, çünkü IPv4 yetmiyor.

- **Yapısı:** Çok daha uzun ve karmaşıktır.
- **Örnek:** `2001:db8::ff00:42:8329`
- **Avantajı:** Neredeyse sonsuz sayıda adres sağlar (Her kum tanesine IP versek yine bitmez!).

> 💡 **Not:** Bu rehberde şimdilik sadece **IPv4** üzerinde duracağız çünkü mantığı kavramak için en iyisi bu.

---

## 🏘️ Public vs Private IP: Cadde vs Ev İçi

Bu ikisini karıştırmak çok kolaydır, ama aslında çok basittir:

### Genel IP (Public IP) = Apartman Kapı Numarası 🏢

- Bu adres **tüm dünya** tarafından görülür ve bilinir.
- İnternet servis sağlayıcınız (Türk Telekom, Superonline vs.) size bu adresi verir.
- **Örnek:** `85.34.123.45`
- Dışarıdan biri size mektup gönderecekse bu adrese gönderir.

### Özel IP (Private IP) = Daire Numarası 🚪

- Bu adres sadece **sizin evinizin/ofisinizin içinde** geçerlidir.
- Modeminiz (Router) tarafından cihazlarınıza dağıtılır.
- **Örnek:** `192.168.1.10`, `192.168.1.20`
- Dünya genelinde milyonlarca evde "Daire: 5" olabilir, ama karışmaz çünkü hepsi farklı apartmanlardadır!

### 🌉 NAT: Kapıcı/Güvenlik Görevlisi

Modeminiz (Router) bir kapıcı gibi çalışır:

1. Telefonunuz (Daire 5) internetten bir site açmak ister.
2. Kapıcı (Modem) der ki: "Tamam, ben senin adına dışarıya (Apartman Adresiyle) çıkıp cevabı alıp geleyim."
3. Dış dünya sadece apartman adresini (Genel IP) görür.
4. Cevap gelince kapıcı bunu kime vereceğini bilir ("Bu paket Daire 5'in isteğiydi").

---

## 🍕 CIDR Nedir? (Classless Inter-Domain Routing)

CIDR (Sınıfsız Alanlar Arası Yönlendirme), IP adreslerini gruplamanın modern yoludur. Bunu bir **Pizza** 🍕 paylaşımı gibi düşünün.

### Sorun Neydi?

Eskiden pizzalar sabit boyutta satılırdı:

- **Small:** Çok küçük (254 kişi doyurur)
- **Large:** Çok büyük (16 milyon kişi doyurur)

Ya orta boy bir şirket 500 kişiyse? Small yetmiyor, Large çok fazla ve israf oluyor!

### Çözüm: CIDR (Dilimle Satış) 🎯

CIDR, pizzayı (IP bloğunu) tam ihtiyacınız kadar dilimlemenize izin verir.

**CIDR Notasyonu:**
Bir IP adresinin sonunda `/` ile başlayan bir sayı görürsünüz:

```text
192.168.1.0/24
```

Buradaki **/24**, "Pizzanın ne kadarı sabit (mahalle adı), ne kadarı değişken (daire numarası)" olduğunu söyler.

---

## 📊 /24, /16, /8 Ne Demek? (Popüler Dilimler)

Bu sayı ne kadar **BÜYÜKSE**, elinizdeki IP adresi sayısı o kadar **AZALIR**.
Çünkü sayı, "Sabit Kısım"ın uzunluğunu gösterir. Sabit kısım ne kadar uzunsa, kişilere dağıtacak yer o kadar az kalır.

| CIDR | Anlamı | Kullanılabilir Adres Sayısı | Kullanım Alanı |
|------|--------|-----------------------------|----------------|
| **/32** | Sadece 1 kişi | 1 | Tek bir cihaz (Özel IP) |
| **/30** | Çok küçük parça | 2 | İki router arası bağlantı |
| **/24** | Standart dilim | **254** | Evler, Küçük Ofisler (En yaygını!) |
| **/16** | Büyük dilim | 65,534 | Büyük Şirketler, Üniversiteler |
| **/8** | Devasa dilim | 16 Milyon | Ülke çapında ağlar, Dev kurumlar |

### Hızlı Ezber Taktiği: /24

En çok göreceğiniz yapı `/24` tür.

- `192.168.1.0/24`
- Anlamı: "192.168.1" kısmı **SABİT** (Ailenin soyadı gibi).
- Son numara **DEĞİŞKEN** (0-255 arası).
- Yani bu ağda 254 tane cihaz olabilir.

---

## 🚦 Özel IP Adresleri: Rezerve Edilenler

Bazı adresler teknik sebeplerle kullanılamaz veya özel anlamları vardır:

---

## 🎯 Özet: Aklınızda Bulunsun

1. **Genel IP (Public IP)** = Apartman adresi (Dünya görür).
2. **Özel IP (Private IP)** = Daire numarası (Sadece bina içi).
3. **CIDR** = IP bloğunun büyüklüğünü belirleyen sayı (`/24` gibi).
4. **Sayı Büyüdükçe Ağ Küçülür:** `/24` (254 cihaz) > `/30` (2 cihaz).

---

## 🔗 Pratik Araçlar

Hesaplama yapmak zor geliyorsa bu araçları kullanın:

- 🧮 [IPv4 Subnet Calculator](https://farukguler.com/app/IPv4-subnet-calculator/)
- 🌐 [IP Calculator](https://jodies.de/ipcalc)

---

**Navigasyon:**

- [⬅️ Önceki: MAC Adresi ve Switching](./03-Veri-Baglanti-Katmani-MAC-Adresi-ve-Switching.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: Subnetting Mantığı](./04-IP-Adresleme-ve-Subnetting-Subnetting-Mantigi.md)
