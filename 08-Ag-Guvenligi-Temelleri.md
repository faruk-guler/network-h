# 08 - Ağ Güvenliği Temelleri: Dijital Kalenizi Korumak 🛡️

Ağ güvenliği, ağınızı ve verilerinizi yetkisiz erişimlerden, saldırılardan ve hırsızlık risklerinden koruma sanatıdır.

> 💡 **Benzetme:** Evinizin kapısını kilitlemek, alarm taktırmak ve güvenlik kamerası koymak neyse; ağ güvenliği de dijital dünyadaki eviniz (ağınız) için aynısıdır.

---

## 🔒 CIA Üçlüsü (Güvenliğin Kutsal Üçgeni)

Siber güvenliğin en temel modelidir. Her güvenlik önlemi bu üç ilkeyi korumayı amaçlar:

| İlke | İngilizce | Anlamı | İhlal Örneği |
| :--- | :--- | :--- | :--- |
| **Gizlilik** | Confidentiality | Veriyi sadece yetkili kişiler görebilmeli. | Şifrenizin çalınması. |
| **Bütünlük** | Integrity | Veri yolda değiştirilmemeli veya bozulmamalı. | Birinin banka transferindeki tutarı değiştirmesi. |
| **Erişilebilirlik** | Availability | Sistem ihtiyaç duyulduğunda çalışır durumda olmalı. | Elektrik kesintisi veya sunucunun çökmesi. |

---

## 🧱 Güvenlik Duvarı (Firewall)

**Firewall**, ağınız ile güvensiz dış dünya (internet) arasında duran bir güvenlik görevlisidir.

> 💡 **Benzetme:** Bir gece kulübünün kapısındaki koruma. Listede adı olmayanları (zararlı paketleri) içeri almaz!

### Firewall Türleri

#### 1. Paket Filtreleme (Packet Filtering) - Eski Nesil

Sadece zarfa bakar, mektubu okumaz.

- **Mantık:** "IP 1.2.3.4'ten gelen paketleri engelle."
- **Durum:** Hızlı ama yetersiz.

#### 2. Durum Denetimli (Stateful Inspection) - Akıllı Koruma

Bağlantının geçmişini hatırlar.

- **Mantık:** "Bu paket içeriden başlatılan bir isteğin cevabı mı? Evetse geç, hayırsa dur!"
- **Durum:** Günümüzde standarttır.

#### 3. Yeni Nesil (Next-Generation / NGFW) - Tam Koruma

Zarfı açar, mektubu okur, hatta kimin yazdığına bakar.

- **Özellikler:** Uygulama kontrolü (Facebook'a gir ama oyun oynama), IPS (Saldırı önleme), Antivirüs.
- **Durum:** Kurumsal ağların vazgeçilmezi.

#### 🛡️ IDS ve IPS (Alarm ve Müdahale)

Sadece trafiği engellemek yetmez, saldırıyı tanımak da gerekir.

- **IDS (Intrusion Detection System):** "Saldırı Tespit Sistemi". Polise haber verir ama hırsızı durdurmaz (Alarm çalar).
- **IPS (Intrusion Prevention System):** "Saldırı Önleme Sistemi". Hem haber verir hem de saldırıyı anında durdurur (Kapıyı kilitler).

---

## 🚇 VPN (Sanal Özel Ağ / Virtual Private Network)

VPN, halka açık internet üzerinde **şifreli bir tünel** oluşturur.

> 💡 **Benzetme:** Şeffaf bir cam boru (internet) yerine, içi görünmeyen çelik bir boru (VPN) içinden su (veri) göndermek gibidir. Dışarıdakiler borunun varlığını görür ama içinden ne geçtiğini göremez.

### VPN Türleri

#### 1. Site-to-Site VPN (Şubeler Arası)

İki ofisi birbirine bağlar.

- **Örnek:** İstanbul ofisindeki yazıcıdan, Ankara ofisindeki çalışan çıktı alabilir.
- **Kullanıcı:** Fark etmez, arka planda router'lar yapar.

#### 2. Remote Access VPN (Uzaktan Erişim)

Evden çalışanların ofis ağına bağlanmasını sağlar.

- **Örnek:** Kafede otururken şirketin dosya sunucusuna güvenle erişmek.
- **Kullanıcı:** Bilgisayarına VPN yazılımı kurar ve bağlanır.

---

## ☠️ Yaygın Ağ Saldırıları

Düşmanınızı tanımazsanız kendinizi koruyamazsınız!

### 1. DoS / DDoS (Hizmet Engelleme)

Bir sunucuyu o kadar çok meşgul etmek ki, gerçek müşterilere hizmet veremez hale gelmesi.
> 💡 **Benzetme:** Bir pizzacıyı 1000 kişinin aynı anda arayıp sipariş vermeden telefonu meşgul etmesi. Gerçek müşteriler aradığında ulaşamaz.

### 2. Phishing (Oltalama)

Sizi kandırarak şifrelerinizi çalmaya çalışmak.
> 💡 **Benzetme:** Bankadan gelmiş gibi görünen sahte bir mektup: "Hesabınız bloke oldu, şifrenizi şu zarfa koyup gönderin."

### 3. Man-in-the-Middle (Ortadaki Adam)

İki kişi arasındaki konuşmayı gizlice dinlemek ve değiştirmek.

- **Çözüm:** Şifreleme (HTTPS, VPN) kullanmak.

### 4. ARP Poisoning (ARP Zehirlemesi)

Saldırganın kendini "Gateway" (Modem) gibi tanıtması.

- **Sonuç:** Sizin tüm internet trafiğiniz önce saldırganın bilgisayarına gider, oradan modeme gider. Saldırgan her şeyi görebilir!

---

---

## 📋 Erişim Kontrol Listeleri (Access Control Lists - ACL)

Güvenlik duvarının (Firewall) atasıdır. Router veya Switch üzerinde paketleri filtrelemek için kullanılır.

> 💡 **Benzetme:** Bir gece kulübünün kapısındaki "Bodyguard". Elindeki listeye bakar: "Sen girebilirsin, sen giremezsin."

### ACL Türleri (Cisco)

#### 1. Standart ACL (1-99)

Sadece **Kaynak IP**'ye bakar. Çok basittir.

- **Kural:** "Ahmet girsin, Mehmet giremesin." (Nereye gittiği önemsiz).
- **Yerleşim:** Hedefe en yakın yere konulmalıdır.

#### 2. Genişletilmiş (Extended) ACL (100-199)

**Kaynak IP, Hedef IP, Port ve Protokol**'e bakar. Çok yeteneklidir.

- **Kural:** "Ahmet, Muhasebe Sunucusuna (Hedef) sadece Web (80) ile erişsin, ama FTP (21) yapamasın."
- **Yerleşim:** Kaynağa en yakın yere konulmalıdır (Gereksiz trafik ağda dolaşmasın).

### "Deny All" Kuralı 🚫

Her ACL listesinin sonunda **görünmez bir "Her şeyi reddet"** kuralı vardır.

- Eğer bir ACL yazıp içine sadece "Ahmet'i engelle" derseniz, **herkes engellenir!**
- Mutlaka en sona "Diğerlerine izin ver" (`permit any`) eklemelisiniz.

**Örnek Konfigürasyon:**

```text
Router(config)# access-list 10 permit 192.168.1.10   ! PC-A'ya izin ver
Router(config)# access-list 10 deny 192.168.1.20     ! PC-B'yi engelle
! (Görünmez Deny All buradadır, diğer herkes engellenir)
```

---

## 📡 Kablosuz Ağ Güvenliği (Wi-Fi)

Wi-Fi sinyalleri havadan yayıldığı için çalınması en kolay verilerdir.

### Şifreleme Standartları

| Standart | Durum | Açıklama |
| :--- | :--- | :--- |
| **WEP** | 💀 ÖLÜ | Çok kolay kırılır. Asla kullanmayın! |
| **WPA** | ⚠️ ZAYIF | Güvenlik açıkları var. |
| **WPA2** | ✅ STANDART | Günümüzde en yaygın ve güvenli (AES şifreleme ile). |
| **WPA3** | 🚀 EN İYİ | Yeni nesil, süper güvenli. Cihazlarınız destekliyorsa bunu seçin. |

> 💡 **İpucu:** Ev modeminizde şifrelemeyi **WPA2-AES** veya **WPA3** yapın. "TKIP" seçeneğinden uzak durun (eski ve yavaştır).

---

## 🛡️ Savunma Hattı Oluşturmak (Kişisel Öneriler)

1. **Güçlü Şifreler:** `123456` şifre değildir! En az 12 karakter, karışık harf/rakam kullanın.
2. **2FA (İki Aşamalı Doğrulama):** Şifreniz çalınsa bile telefonunuza gelen kod olmadan kimse giremez.
3. **HTTPS:** Web sitelerinde kilit 🔒 simgesini görmeden kredi kartı bilgisi girmeyin.
4. **Halka Açık Wi-Fi:** Kafelerde bankacılık işlemi yapmayın veya VPN kullanın.

---

**Navigasyon:**

- [⬅️ Önceki: VLAN Temelleri](./07-VLAN-Temelleri.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: WAN Teknolojileri](./09-WAN-Teknolojileri.md)
