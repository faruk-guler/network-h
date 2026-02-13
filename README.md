# 🌐 Network -h (Network Humanity

<p align="center">
  <strong>🌐 Network -h: İnsanlar için Networking 🌐</strong><br>
</p>

> **"www.farukguler.com faruk-guler"**

Network -h (humanity), ağ teknolojilerini (IP, CIDR, Subnetting, Routing vb.) **gerçek hayat örnekleriyle**, **sıfırdan** ve **herkesin anlayabileceği şekilde** öğreten geniş kapsamlı bir Türkçe dokümantasyon projesidir.

---

## 🎯 Hedef Kitle

Bu dokümantasyon **sizin için** hazırlandı:

- 🎓 **Bilgisayar öğrencileri** - Ağ derslerinde konuları pekiştirmek isteyenler
- 💼 **Junior network yöneticileri** - Gerçek hayatta uygulama yapmadan önce kavramları anlamak isteyenler
- 🔧 **Sistem yöneticileri** - Ağ konularında hızlıca bilgi tazelemek isteyenler
- 🤔 **Meraklılar** - "İnternet nasıl çalışıyor?" diye merak edenler

**Ön koşul:** Hiçbir ön bilgi gerekmiyor! Sıfırdan başlayabilirsiniz.

---

## 📚 Öğrenme Yolu (Sıralı Okuma Önerilir)

### 🌱 Temel Seviye (Başlangıç)

| Modül | Konu | Açıklama |
| :---: | --- | --- |
| **00** | [Network Nedir?](./00-Giris-Network-Nedir.md) | Ağların temelini ve LAN/WAN kavramlarını öğrenin |
| **01** | [OSI ve TCP/IP Modelleri](./01-Temel-Kavramlar-OSI-ve-TCPIP-Modelleri.md) | Katmanlı yapının mantığını kavrayın |
| **02** | [Fiziksel Bağlantı](./02-Fiziksel-Baglanti-Kablolama-ve-Medya.md) | Kablolar, fiber optik ve Wi-Fi nasıl çalışır? |
| **03** | [MAC Adresi ve Switch](./03-Veri-Baglanti-Katmani-MAC-Adresi-ve-Switching.md) | Yerel ağda cihazlar nasıl iletişim kurar? |

### 🚀 Orta Seviye (IP ve Subnetting - **En Önemli Bölüm!**)

| Modül | Konu | Açıklama |
| :---: | --- | --- |
| **04.1** | [IP Adresi ve CIDR](./04-IP-Adresleme-ve-Subnetting-IP-Adresi-ve-CIDR.md) | IP adresinin mantığını öğrenin (Apartman metaforu) |
| **04.2** | [Subnetting Mantığı](./04-IP-Adresleme-ve-Subnetting-Subnetting-Mantigi.md) | Ağları neden ve nasıl böleriz? (Site yönetimi metaforu) |
| **04.3** | [Pratik Subnetting Örnekleri](./04-IP-Adresleme-ve-Subnetting-Pratik-Ornekler.md) | 🆕 Gerçek senaryolarla adım adım hesaplama |
| **04.4** | [VLSM](./04-IP-Adresleme-ve-Subnetting-VLSM.md) | 🆕 Esnek subnet boyutları (Custom pizza dilimleri) |
| **04.5** | [Supernetting](./04-IP-Adresleme-ve-Subnetting-Supernetting.md) | 🆕 Ağları birleştirme (Rota Özeti / Supernetting) |
| **04.6** | [IPv6 Derinlemesine](./04-IP-Adresleme-ve-Subnetting-IPv6-Derinlemesine.md) | 🆕 Geleceğin IP standardı (IPv6) |
| **04.7** | [Gerçek Hayat Senaryosu](./04-7-Gercek-Hayat-Ag-Planlama-Atolyesi.md) | 🆕 **Atölye:** Sıfırdan 5 Katlı Bina Ağ Planlama |

### 🔥 İleri Seviye (Routing, Güvenlik ve WAN)

| Modül | Konu | Açıklama |
| :---: | --- | --- |
| **05** | [Routing (Yönlendirme)](./05-Yonlendirme-Routing-Router-Nasil-Calisir.md) | Router nasıl çalışır? Static vs Dynamic routing |
| **06** | [Uygulama Protokolleri](./06-Uygulama-Protokolleri-DNS-DHCP-HTTP.md) | DNS, DHCP, HTTP(S), FTP nedir? |
| **07** | [VLAN Temelleri](./07-VLAN-Temelleri.md) | 🆕 Sanal ağlar ve segmentasyon |
| **08** | [Ağ Güvenliği](./08-Ag-Guvenligi-Temelleri.md) | 🆕 Firewall, VPN, Saldırı Türleri |
| **09** | [WAN Teknolojileri](./09-WAN-Teknolojileri.md) | 🆕 MPLS, SD-WAN, Metro Ethernet |
| **07.5** | [Portlar ve Servisler](./ports/07-Portlar-ve-Servisler-Port-Nedir.md) | 🆕 Port numaraları, servisler ve IANA referansı |

### 🛠️ Araçlar ve Referans

| Modül | Konu | Açıklama |
| :---: | --- | --- |
| **99** | [Ağ Araçları](./99-Araclar-ve-Komutlar-Ping-Tracert-Nmap.md) | Ping, Tracert, Nslookup, Nmap kullanımı |
| **📖** | [Terminoloji Sözlüğü](./Terminology.md) | Tüm ağ terimlerinin açıklamaları |
| **📊** | [IPv4 Subnet Tablosu](./04-IP-Adresleme-ve-Subnetting-IPv4-Subnet-Tablosu.md) | /32'den /0'a tüm CIDR değerleri |
| **📊** | [IPv6 Subnet Tablosu](./04-IP-Adresleme-ve-Subnetting-IPv6-Subnet-Tablosu.md) | IPv6 prefix uzunlukları referansı |

> 🆕 **Yeni eklenen konular** işaretlenmiştir.

---

## 💡 Nasıl Kullanmalıyım?

### Seçenek 1: Sıfırdan Öğreniyorum

**00 numaradan başlayıp sırayla ilerleyin.** Her bölüm bir sonrakini anlamanız için gerekli temeli atar.

### Seçenek 2: Belirli Bir Konuyu Öğrenmek İstiyorum

Yukarıdaki tablodan ilgili konuyu bulun ve direkt okumaya başlayın. Her dosya kendi içinde anlaşılır şekilde yazılmıştır.

### Seçenek 3: Hızlı Referans

**Terminoloji** sözlüğünü kullanın veya **Subnet Tabloları**'na göz atın.

---

## 🎨 Öğrenme Felsefemiz

Network -h projesi, şu prensiplere göre hazırlanmıştır:

1. **🏠 Gerçek Hayat Metaforları**: Karmaşık kavramlar, günlük hayattan örneklerle açıklanır.
   - IP Adresi = Posta Adresi
   - CIDR = Pizza Dilimleme
   - Subnetting = Site Yönetimi

2. **🚫 Jargon'dan Kaçınma**: Teknik terimleri anlatırken "insan diline" çeviririz.

3. **📝 Pratik Odaklı**: Sadece teori değil, gerçek örnekler ve hesaplamalar.

4. **🎯 Progresif Öğrenme**: Basit kavramlardan karmaşık konulara doğru adım adım ilerleme.

---

## 🔗 Faydalı Kaynaklar

### Hesaplama Araçları

- 🧮 [IPv4 Subnet Calculator](https://farukguler.com/app/IPv4-subnet-calculator/)
- 🌐 [IP Calculator (Jodies)](https://jodies.de/ipcalc)

### İleri Okuma

- [RFC 791 - Internet Protocol](https://www.rfc-editor.org/rfc/rfc791)
- [RFC 4632 - CIDR](https://www.rfc-editor.org/rfc/rfc4632)

---

## 🙋 Katkıda Bulunma

Bu bir açık öğrenme projesidir. Katkılarınızı bekliyoruz:

- 🐛 Hata bildirimi
- 💡 İyileştirme önerileri
- 📝 Yeni konu talepleri
- 🌍 Çeviri yardımı

---

## 📄 Lisans

Bu dokümantasyon, eğitim amaçlı hazırlanmıştır ve özgürce kullanılabilir.

---

## ✨ Başlamak için Hazır mısınız?

👉 **[00 - Giriş: Network Nedir?](./00-Giris-Network-Nedir.md)** dosyasından başlayın!

veya

👉 **[04 - IP Adresi ve CIDR](./04-IP-Adresleme-ve-Subnetting-IP-Adresi-ve-CIDR.md)** ile direkt en popüler konuya atlayın!

---
