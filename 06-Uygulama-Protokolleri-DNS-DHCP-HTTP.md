# 06 - Temel Uygulama Protokolleri: İnternetin Görünmez Kahramanları

İnterneti kullanırken arka planda sürekli çalışan hayati protokoller vardır. Bu protokoller olmadan web sitesi açamazsınız, e-posta gönderemezsiniz, hatta internete bile bağlanamazsınız!

> 💡 **Benzetme:** Protokoller, insanların birbirleriyle iletişim kurduğu "diller" gibidir. DNS Türkçe, HTTP İngilizce, DHCP Almanca... Her biri farklı bir işe yarar.

---

## 🌍 DNS (Domain Name System) - İnternetin Rehberi

### DNS Ne Yapar?

`google.com` gibi insan tarafından okunabilen alan adlarını, bilgisayarların anladığı IP adreslerine (`142.250.185.78`) çevirir.

- **Port:** UDP 53 (sorgular), TCP 53 (zone transfer)
- **Benzetme:** Telefon rehberi. "Ahmet" ismini ararsınız, rehber size Ahmet'in numarasını verir

### DNS Çözümleme Süreci

```text
Sen: "google.com nerede?"
   ↓
1. Yerel DNS Cache → Daha önce baktın mı? (Hızlı!)
   ↓ (Bulunamadı)
2. Recursive DNS Server (ISP'nin DNS'i)
   ↓
3. Root DNS Server → ".com nerede?"
   ↓
4. TLD Server (.com) → "google.com nerede?"
   ↓
5. Authoritative Server → "142.250.185.78!"
   ↓
Sen: Siteye bağlanıyorsun 🎉
```

### DNS Kayıt Türleri

| Kayıt | Açıklama | Örnek |
| :--- | :--- | :--- |
| **A** | Domain → IPv4 | google.com → 142.250.185.78 |
| **AAAA** | Domain → IPv6 | google.com → 2a00:1450:... |
| **CNAME** | Takma ad | <www.example.com> → example.com |
| **MX** | E-posta sunucusu | example.com → mail.example.com |
| **NS** | Name server | example.com → ns1.example.com |
| **TXT** | Metin bilgisi | SPF, DKIM doğrulama |
| **PTR** | IP → Domain (Ters DNS) | 1.1.1.1 → one.one.one.one |

### Popüler DNS Sunucuları

| Sağlayıcı      | Primary | Secondary       |
| :------------- | :------ | :-------------- |
| **Google**     | 8.8.8.8 | 8.8.4.4         |
| **Cloudflare** | 1.1.1.1 | 1.0.0.1         |
| **Quad9**      | 9.9.9.9 | 149.112.112.112 |

---

## 🏷️ DHCP (Dynamic Host Configuration Protocol)

### DHCP Ne Yapar?

Ağa bağlanan cihazlara otomatik olarak **IP adresi**, **alt ağ maskesi (Subnet Mask)**, **ağ geçidi (Gateway)** ve **DNS** bilgilerini dağıtır.

- **Port:** UDP 67 (Server) / UDP 68 (Client)
- **Faydası:** Elle tek tek IP yazmaktan (Static IP) sizi kurtarır. IP çakışmalarını önler

### DHCP DORA Süreci

DHCP, 4 adımlı bir süreç (DORA) ile IP dağıtır:

```text
Cihaz                          DHCP Server
  │                                │
  │─── 1. DISCOVER ──────────────→│  "IP arıyorum!" (Broadcast)
  │                                │
  │←── 2. OFFER ──────────────────│  "Sana 192.168.1.50 verebilirim"
  │                                │
  │─── 3. REQUEST ────────────────→│  "Tamam, onu istiyorum!"
  │                                │
  │←── 4. ACK ────────────────────│  "Onaylandı, IP senin!"
  │                                │
```

### DHCP'nin Dağıttığı Bilgiler

- **IP Adresi:** 192.168.1.50
- **Alt Ağ Maskesi (Subnet Mask):** 255.255.255.0
- **Varsayılan Ağ Geçidi (Default Gateway):** 192.168.1.1
- **DNS Sunucusu:** 8.8.8.8
- **Kira Süresi (Lease Time):** 24 saat

### DHCP Havuzu Örneği

```text
DHCP Pool: 192.168.1.100 - 192.168.1.200
→ Toplam 101 IP otomatik dağıtılabilir
→ Geri kalanı (1-99, 201-254) static IP için ayrılır
```

> ⚠️ **İpucu:** Sunucular, yazıcılar ve router'lara **static IP** verin. Normal kullanıcılara **DHCP** ile otomatik IP verin.

---

## 🌐 HTTP ve HTTPS (Web Protokolleri)

### HTTP (HyperText Transfer Protocol)

Web sitelerini görüntülemek için kullanılır. Veriler **şifresiz** (açık metin) gider.

- **Port:** TCP 80
- **Güvenlik:** ❌ Güvenli değil!

### HTTPS (HTTP Secure)

HTTP'nin **SSL/TLS** ile şifrelenmiş halidir. Tarayıcıda 🔒 kilit simgesi çıkar.

- **Port:** TCP 443
- **Güvenlik:** ✅ Şifreli iletişim

### HTTP İstek Metodları

| Metod      | Açıklama      | Örnek                       |
| :--------- | :------------ | :-------------------------- |
| **GET**    | Veri getir    | Bir sayfayı görüntüle       |
| **POST**   | Veri gönder   | Form doldur, login ol       |
| **PUT**    | Veri güncelle | Profil bilgilerini değiştir |
| **DELETE** | Veri sil      | Bir mesajı sil              |

### HTTP Durum Kodları

| Kod     | Anlamı                | Açıklama              |
| :------ | :-------------------- | :-------------------- |
| **200** | OK                    | Başarılı!             |
| **301** | Moved Permanently     | Kalıcı yönlendirme    |
| **403** | Forbidden             | Erişim yasak          |
| **404** | Not Found             | Sayfa bulunamadı      |
| **500** | Internal Server Error | Sunucu hatası         |
| **503** | Service Unavailable   | Sunucu meşgul/bakımda |

---

## 📁 FTP (File Transfer Protocol)

### FTP Ne Yapar?

Bilgisayarlar arası **dosya transferi** yapmak için kullanılır.

- **Port:** TCP 20 (Data) / TCP 21 (Kontrol)
- **Güvenlik:** ❌ Şifresiz! (Kullanıcı adı ve şifre açık gider)

### FTP Alternatifleri

| Protokol | Port    | Güvenlik | Açıklama                        |
| :------- | :------ | :------- | :------------------------------ |
| **FTP**  | 20/21   | ❌       | Eski, güvensiz                  |
| **SFTP** | 22      | ✅       | SSH üzerinden dosya transferi   |
| **FTPS** | 990     | ✅       | FTP + SSL/TLS şifreleme         |
| **SCP**  | 22      | ✅       | SSH üzerinden güvenli kopyalama |

> 💡 **Tavsiye:** FTP yerine her zaman **SFTP** veya **SCP** kullanın!

---

## 📧 E-Posta Protokolleri

### SMTP (Simple Mail Transfer Protocol)

- **Görevi:** E-posta **göndermek** için kullanılır
- **Port:** TCP 25 (düz), TCP 587 (TLS/STARTTLS)
- **Benzetme:** Postacı → mektubu alır ve ilgili posta ofisine götürür

### POP3 (Post Office Protocol v3)

- **Görevi:** E-posta **indirmek** için kullanılır
- **Port:** TCP 110 (düz), TCP 995 (SSL)
- **Özellik:** E-postayı indirir ve sunucudan **siler** (varsayılan)

### IMAP (Internet Message Access Protocol)

- **Görevi:** E-posta **okumak** için kullanılır (sunucuda kalır)
- **Port:** TCP 143 (düz), TCP 993 (SSL)
- **Özellik:** E-postalar sunucuda kalır, birden fazla cihazdan erişim

| Özellik           | POP3              | IMAP           |
| :---------------- | :---------------- | :------------- |
| E-posta nerede?   | İndirilir (Lokal) | Sunucuda kalır |
| Çoklu cihaz       | ❌                | ✅             |
| Çevrimdışı erişim | ✅                | Sınırlı        |
| Depolama          | Lokal disk        | Sunucu         |

---

## 🔒 SSH (Secure Shell)

- **Görevi:** Uzak sunuculara **güvenli komut satırı** erişimi sağlar
- **Port:** TCP 22
- **Benzetme:** Şifreli bir telefon hattı ile uzaktaki bilgisayarı kontrol etmek

```bash
ssh kullanici@192.168.1.100    # Uzak sunucuya bağlan
ssh -p 2222 admin@server.com   # Farklı port ile bağlan
```

> 💡 **Telnet** (Port 23) SSH'ın şifresiz halidir. **Asla kullanmayın!**

---

## ⏱️ NTP (Network Time Protocol)

- **Görevi:** Ağdaki cihazların saatlerini **senkronize** eder
- **Port:** UDP 123
- **Neden önemli?** Loglar, sertifikalar ve kimlik doğrulama saate bağlıdır

---

## 📊 SNMP (Simple Network Management Protocol)

- **Görevi:** Ağ cihazlarını (switch, router, sunucu) **uzaktan izlemek** ve yönetmek
- **Port:** UDP 161 (sorgular), UDP 162 (trap'ler)
- **Versiyonlar:**
  - SNMPv1/v2c: Community string (güvensiz)
  - **SNMPv3:** Şifreli, güvenli ✅

---

## 🔗 Protokol Özet Tablosu

| Protokol | Port    | TCP/UDP | Görevi                |
| :------- | :------ | :------ | :-------------------- |
| DNS      | 53      | UDP/TCP | İsim → IP çözümleme   |
| DHCP     | 67/68   | UDP     | Otomatik IP dağıtımı  |
| HTTP     | 80      | TCP     | Web (şifresiz)        |
| HTTPS    | 443     | TCP     | Web (şifreli)         |
| FTP      | 20/21   | TCP     | Dosya transferi       |
| SSH      | 22      | TCP     | Güvenli uzak erişim   |
| SMTP     | 25/587  | TCP     | E-posta gönderme      |
| POP3     | 110/995 | TCP     | E-posta indirme       |
| IMAP     | 143/993 | TCP     | E-posta okuma         |
| NTP      | 123     | UDP     | Zaman senkronizasyonu |
| SNMP     | 161/162 | UDP     | Ağ izleme ve yönetim  |
| Syslog   | 514     | UDP     | Sistem günlükleri     |

---

**Navigasyon:**

- [⬅️ Önceki: Routing](./05-Yonlendirme-Routing-Router-Nasil-Calisir.md)
- [🏠 Ana Sayfa](./README.md)
- [➡️ Sonraki: VLAN Temelleri](./07-VLAN-Temelleri.md)
