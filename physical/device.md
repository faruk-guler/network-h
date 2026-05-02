# Ağ Cihazları

Bir ağı oluşturan cihazların her birinin kendine özgü bir görevi vardır. Bu bölümde temel ağ cihazlarını tanıyacaksınız.

---

## 1) NIC — Ağ Arabirim Kartı

Bir cihazın ağa fiziksel olarak bağlanmasını sağlayan donanımdır.

Her NIC'in dünyada eşsiz bir **MAC adresi** vardır. Bilgisayar, telefon veya yazıcı gibi cihazlar ağa bu kart aracılığıyla dahil olur. Kablolu (Ethernet) veya kablosuz (Wi-Fi) olabilir.

**Özellikler:**

- Ağdaki cihazı tanımlayan MAC adresini taşır
- OSI modelinin 2. katmanında (Veri Bağlantısı) çalışır
- Günümüzde çoğu cihaza entegre olarak üretilir

---

## 2) Hub — Çoklayıcı

Ağdaki cihazları birbirine bağlayan en basit cihazdır.

Kendisine gelen veriyi **tüm portlara** iletir. Hangi cihazın hedef olduğunu bilmez, veriyi herkese gönderir. Bu nedenle gereksiz trafik oluşturur ve güvenlik zafiyeti yaratır. Günümüzde yerini Switch'e bırakmıştır.

**Özellikler:**

- OSI modelinin 1. katmanında (Fiziksel) çalışır
- Gelen veriyi tüm portlara kopyalar (Broadcast gibi davranır)
- Artık aktif olarak kullanılmamaktadır

---

## 3) Switch — Anahtar

Ağdaki cihazları akıllı biçimde birbirine bağlayan cihazdır.

Hub'ın aksine Switch, **MAC adreslerini öğrenir** ve veriyi yalnızca hedef cihaza iletir. Bu sayede ağ trafiği azalır, hız ve güvenlik artar.

**Özellikler:**

- OSI modelinin 2. katmanında (Veri Bağlantısı) çalışır
- MAC adres tablosu tutarak veriyi doğru porta yönlendirir
- Aynı ağ (LAN) içindeki cihazları birbirine bağlar

---

## 4) Router — Yönlendirici

Farklı ağları birbirine bağlayan ve veriyi doğru hedefe yönlendiren cihazdır.

Switch'in aksine Router, **IP adreslerine** göre çalışır. Evinizin ağını internete bağlayan cihaz bir Router'dır. Broadcast trafiğini bir ağdan diğerine geçirmez, böylece ağlar birbirinden izole kalır.

**Özellikler:**

- OSI modelinin 3. katmanında (Ağ) çalışır
- IP adreslerine göre en iyi rotayı hesaplar
- Farklı ağlar (LAN, WAN, internet) arasında köprü kurar

---

## 5) Modem — Modülatör/Demodülatör

İnternet servis sağlayıcısının (ISS) altyapısını ev veya iş ağına bağlayan cihazdır.

Analog sinyali dijitale, dijitali analoga çevirir. ADSL, fiber veya kablo altyapılarında farklı modem türleri kullanılır. Günümüzde çoğu zaman Router ile tek bir cihazda birleştirilmiş şekilde gelir.

**Özellikler:**

- İnternet bağlantısının giriş noktasıdır
- ISS'den gelen sinyali ağın anlayacağı formata dönüştürür
- Modem + Router birleşimi cihazlara "gateway" denir

---

## 6) Access Point — Erişim Noktası

Kablolu ağı kablosuz ağa (Wi-Fi) dönüştüren cihazdır.

Router'a kablo ile bağlanır ve çevresindeki cihazların Wi-Fi ile ağa dahil olmasını sağlar. Büyük ofis veya binalarda sinyal kapsamını genişletmek için birden fazla Access Point kullanılır.

**Özellikler:**

- OSI modelinin 2. katmanında (Veri Bağlantısı) çalışır
- SSID (ağ adı) ve şifre ile erişim kontrolü sağlar
- Router'dan farklıdır; yalnızca kablosuz erişim noktası görevi görür

---

## 7) Firewall — Güvenlik Duvarı

Ağa giren ve çıkan trafiği denetleyerek yetkisiz erişimleri engelleyen cihazdır.

Belirlenen kurallara göre trafiğe izin verir ya da engeller. Hem donanımsal (fiziksel cihaz) hem de yazılımsal (işletim sistemi üzerinde) olarak kullanılabilir.

**Özellikler:**

- OSI modelinin 3. ve 4. katmanlarında (Ağ ve Taşıma) çalışır
- IP adresi, port numarası ve protokole göre kural tanımlanır
- Ağın internet ile buluştuğu noktaya yerleştirilir

---

## Özet Tablo

| Cihaz | Görevi | OSI Katmanı |
|---|---|---|
| **NIC** | Cihazı ağa bağlar | Katman 2 |
| **Hub** | Tüm portlara veri iletir | Katman 1 |
| **Switch** | MAC adresine göre veri iletir | Katman 2 |
| **Router** | IP adresine göre ağlar arası yönlendirme | Katman 3 |
| **Modem** | İnternet bağlantısı sağlar | — |
| **Access Point** | Kablosuz ağ erişimi sağlar | Katman 2 |
| **Firewall** | Trafiği denetler ve filtreler | Katman 3–4 |