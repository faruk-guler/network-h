# 🤝 TCP, UDP ve 3 Adımlı El Sıkışma (3-Way Handshake)

OSI modelinin **4. Katmanı (Taşıma / Transport Katmanı)**, verinin iki cihaz arasında **nasıl** taşınacağını belirleyen ana merkezdir. Uygulama katmanından gelen veriler burada segmentlere ayrılır, hedefe güvenli ya da hızlı bir şekilde ulaştırılması için paketlenir.

Bu katmanın omurgasını oluşturan iki dev protokol vardır: **TCP** ve **UDP**.

---

## 1. Port Mantığı ve Soketler

IP adresi verinin hangi **cihaza** gideceğini belirlerken; **Port numarası**, o cihaz üzerindeki hangi **uygulamaya / servise** teslim edileceğini belirler.

> 💡 **Benzetme:** IP adresi bir apartmanın sokak adresi ise, **Port numarası** o apartmandaki daire numarasıdır. Mektup (veri) binaya geldikten sonra doğru daireye teslim edilmek zorundadır.

```text
       IP: 192.168.1.50 (Cihaz)
      ┌─────────────────────────┐
      │  Port 80   → Web Sunucu │
      │  Port 22   → SSH Servisi│
      │  Port 53   → DNS Servisi│
      └─────────────────────────┘
```

### Kaynak Port vs. Hedef Port

Bir haberleşmede daima iki port numarası bulunur:

1. **Hedef Port (Destination Port):** Sunucuda çalışan standart servisin portudur (Örn: Web için `80` veya `443`).
2. **Kaynak Port (Source Port):** İstemcinin (PC, telefon) işletim sistemi tarafından rastgele atanan geçici (**ephemeral**) bir porttur (Örn: `52418`). Sunucu cevabı geri gönderirken bu portu hedef alır.

> 🔌 **Soket (Socket) Nedir?**  
> Bir IP adresi ile bir port numarasının birleşimidir (`IP:Port`).  
> *Örnek:* `192.168.1.100:54321` → İstemci Soketi | `142.250.185.78:443` → Google Web Soketi.

### IANA Port Aralıkları

| Aralık | Grup | Açıklama | Örnekler |
|---|---|---|---|
| **0 – 1023** | **Well-Known (Tanınmış)** | Temel sistem ve internet protokollerine ayrılmıştır. Sadece yetkili (root/admin) servisler dinleyebilir. | `21` FTP, `22` SSH, `25` SMTP, `53` DNS, `80` HTTP, `443` HTTPS |
| **1024 – 49151** | **Registered (Kayıtlı)** | Şirketlerin ve özel yazılımların IANA'ya kaydettirdiği portlardır. | `1433` MSSQL, `3306` MySQL, `3389` RDP, `8080` HTTP-Proxy |
| **49152 – 65535** | **Dynamic / Ephemeral (Geçici)** | İstemcilerin dışarıya istek yaparken geçici olarak kullandığı portlardır. İş bitince kapanır. | Web sitesine giren bilgisayarın tarayıcısına atanan rastgele portlar |

---

## 2. TCP vs. UDP — Büyük Karşılaştırma

Ağ trafiğinde hız mı yoksa yüzde yüz doğruluk mu gerektiğine göre iki yoldan biri seçilir:

| Kriter | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
|---|---|---|
| **Karakter** | Güvenilir, garantili, kurallı | Hızlı, hafif, kuralsız |
| **Bağlantı Tipi** | **Connection-Oriented** (Önce el sıkışılır) | **Connectionless** (Bağlantı kurulmaz, direkt fırlatılır) |
| **Paket Kaybı** | Kaybolan paketler **tekrar gönderilir** | Kaybolan paketler **umursanmaz** |
| **Paket Sıralaması** | Sıralama numarası (Seq No) ile sıraya dizilir | Paketler hangi sırayla gelirse öyle işlenir |
| **Başlık (Header)** | **20 – 60 Byte** (Ağır yük) | **8 Byte sabit** (Çok hafif) |
| **Akış Kontrolü** | Var (Sliding Window mekanizması) | Yok |
| **İdeal Kullanım** | Web, E-posta, Dosya İndirme | Canlı Yayın, Online Oyun, Sesli Görüşme (VoIP), DNS |

```text
TCP (İadeli Taahhütlü Mektup)           UDP (Megafonla Bağırmak)
────────────────────────────────        ────────────────────────
Gönderen: "Mektubu aldın mı?"           Gönderen: "Duyuru yapıyorum!"
Alıcı   : "Aldım, devam et."            (Biri duymasa da yayın devam eder,
                                         çünkü canlı yayında dün söylenenin
                                         anlamı yoktur.)
```

---

## 3. TCP Başlığı ve Kontrol Bayrakları (Flags)

TCP'nin iletişimi yönetebilmesi için başlığında (header) 1-bitlik özel kontrol bayrakları bulunur:

| Bayrak | Anlamı | Görevi |
|:---:|---|---|
| **SYN** | *Synchronize* | Bağlantı başlatma isteği ve başlangıç sıra numarasını (Seq) bildirme. |
| **ACK** | *Acknowledgment* | Karşı tarafın gönderdiği paketin teslim alındığını onaylama. |
| **FIN** | *Finish* | Veri aktarımının bittiğini ve bağlantının kapatılmak istendiğini bildirme. |
| **RST** | *Reset* | Hata, kapalı port veya ani kopma durumunda bağlantıyı zorla sıfırlama. |
| **PSH** | *Push* | Alıcıya gelen veriyi bekletmeden (buffer doldurmadan) hemen uygulamaya iletmesini söyleme. |
| **URG** | *Urgent* | Pakette öncelikli/acil veri olduğunu belirtme. |

---

## 4. TCP 3-Way Handshake (3 Adımlı El Sıkışma)

TCP, iki cihaz arasında tek bir bayt veri aktarmadan önce mutlaka **3 adımlı el sıkışma** gerçekleştirir. Bu süreçte iki taraf sıra numaralarını (Sequence Number) eşitler.

```text
İstemci (Client)                                Sunucu (Server)
    │                                                  │
    │  1. [SYN]  Seq=X                                 │
    │ ───────────────────────────────────────────────► │ (Bağlantı talebi)
    │                                                  │
    │  2. [SYN, ACK]  Seq=Y, Ack=X+1                   │
    │ ◄─────────────────────────────────────────────── │ (Kabul + Kendi talebi)
    │                                                  │
    │  3. [ACK]  Seq=X+1, Ack=Y+1                      │
    │ ───────────────────────────────────────────────► │ (Teyit)
    │                                                  │
    ▼                                                  ▼
═════════════════ BAĞLANTI KURULDU (ESTABLISHED) ═════════════════
```

### Adım Adım İşleyiş ve Sıra Numaraları (Seq & Ack Mantığı):

1. **1. Adım — SYN (Synchronize):**
   * İstemci sunucuya bağlanmak ister.
   * `SYN` bayrağı `1` yapılır. Rastgele bir başlangıç sıra numarası belirler: `Seq = X` (Örn: `1000`).
   * *"Seninle konuşmak istiyorum, benim sayacım 1000'den başlıyor."*

2. **2. Adım — SYN + ACK:**
   * Sunucu isteği alır ve kabul eder.
   * Hem istemcinin numarasını onaylar: `Ack = X + 1` (`1001` → *"1000'i aldım, sıradaki 1001'i bekliyorum"*).
   * Hem de kendi rastgele başlangıç numarasını üretir: `Seq = Y` (Örn: `5000`).
   * `SYN` ve `ACK` bayrakları birlikte `1` olarak gönderilir.

3. **3. Adım — ACK (Acknowledgment):**
   * İstemci sunucunun onayını alır.
   * Sunucunun sayacını teyit eder: `Ack = Y + 1` (`5001` → *"5000'ini aldım, hazırım"*).
   * Kendi sırasını günceller: `Seq = X + 1`.
   * Bu adımdan sonra soketler **ESTABLISHED** durumuna geçer ve gerçek veri (HTTP, dosya vb.) akışı başlar.

---

## 5. Bağlantıyı Kapatma (Teardown) ve Reset

### A) Düzgün Kapanış: 4 Aşamalı Veda (FIN - ACK)

Veri transferi bittiğinde bağlantı tek taraflı pat diye kesilmez. İki taraf da karşılıklı birbirine veda eder:

```text
İstemci                                         Sunucu
   │                                               │
   │  1. [FIN]      (Benim gönderecek verim bitti) │
   │ ────────────────────────────────────────────► │
   │  2. [ACK]      (Tamam, anladım)               │
   │ ◄──────────────────────────────────────────── │
   │                                               │
   │  3. [FIN]      (Benim de işim bitti)          │
   │ ◄──────────────────────────────────────────── │
   │  4. [ACK]      (Güle güle)                    │
   │ ────────────────────────────────────────────► │
   ▼                                               ▼
               [BAĞLANTI TAMAMEN KAPANDI]
```

### B) Ani Kapanış: RST (Reset) Bayrağı

Eğer bir istemci, sunucuda açık olmayan (dinlenmeyen) bir porta bağlanmaya çalışırsa ya da oturum aniden çökerse sunucu **RST** döner:
> *"Böyle bir açık kapı veya geçerli bir oturum yok, bağlantıyı derhal sıfırla!"*

---

## 6. Akış Kontrolü (Flow Control) ve Sliding Window

TCP'nin en zeki tarafı **Akış Kontrolü**'dür.

Hızlı bir sunucu, yavaş bir cep telefonuna saniyede gigabaytlarca veri gönderirse telefonun tampon belleği (buffer) taşar ve paketler çöpe gider.

Bunu önlemek için alıcı her onay (ACK) paketinde **Window Size (Pencere Boyutu)** alanını doldurur:
* Alıcı: `Ack=5000, Win=64000` → *"Bana tek seferde en fazla 64 KB veri gönder, belleğim bu kadar alıyor."*
* Alıcının belleği doldukça pencere boyutunu küçültür; bellek boşalınca büyütür. Sıfırlanırsa (`Win=0`) gönderici tamamen durur.

---

## 📌 Özet / Altın Kurallar

1. **IP adresi binayı, Port numarası binanın içindeki odayı/uygulamayı bulur.**
2. **TCP:** Garanti, sıra ve hatasız iletim gerektiren işlerde kullanılır (HTTP, SSH, Veritabanı).
3. **UDP:** Hız ve anlık veri akışı gerektiren, eski paketin önemsiz olduğu işlerde kullanılır (DNS, Oyun, Ses/Video).
4. **3-Way Handshake (`SYN` → `SYN-ACK` → `ACK`):** TCP'nin konuşmaya başlamadan önceki zorunlu protokol el sıkışmasıdır.
5. **Kapanış:** Normalde `FIN-ACK` ile kibarca, beklenmedik arızalarda `RST` ile sertçe sonlandırılır.
