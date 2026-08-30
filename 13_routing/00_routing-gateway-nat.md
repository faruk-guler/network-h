# 🌐 Routing, Gateway ve NAT

Bir veri paketinin kaynaktan hedefe ulaşması üç temel kavrama dayanır:  
**Gateway** paketin çıkış kapısıdır; **Routing** paketi nereye göndereceğine karar verir; **NAT** ise paketin kimliğini değiştirir.

---

## 1. Gateway (Ağ Geçidi)

Gateway genel bir ağ elemanıdır. Farklı protokoller, yapılar veya ağlar kullanan iki sistemi birbirine bağlayan bir "tercüman" veya "kapı" gibidir.

- Sadece IP yönlendirmesi yapmaz; gerekirse verinin formatını da değiştirir.
- Örnek: Şirket içi yerel ağınızı (LAN) internete (WAN) bağlayan router bir gateway'dir. Veya iki farklı haberleşme dilini konuşan (örneğin ses trafiği ile veri trafiği) sistemleri birbirine bağlayan cihaz bir "Voice Gateway"dir.

### 🚪 Default Gateway (Varsayılan Ağ Geçidi)

**Default Gateway**, bir cihazın kendi yerel ağı (subnet) dışına çıkmak istediğinde trafiği gönderdiği ilk router (yönlendirici) adresidir. 

Basit bir ifadeyle: **Cihazın "dış dünya kapısı"** veya **"varsayılan çıkış noktası"** dır.

- Yerel ağın **"çıkış kapısı"**dır. Genellikle router'ın LAN IP'sidir: `10.5.10.1`
- Cihaz, kendi subnet'inde olmayan **tüm paketleri** buraya gönderir.
- ⚠️ Gateway tanımlanmamışsa cihaz sadece yerel ağda çalışır; internete **çıkamaz.**

> **Örnek:** Evinizdeki bir bilgisayar Google'a (8.8.8.8) bağlanmak istiyorsa, önce bu paketi modeminize (default gateway) gönderir. Modem de sıradaki adıma iletir. Sıradaki adımda standart ev kullanıcıları için ISP Router olur.

### Görsel Örnek

Aşağıdaki şemada **default gateway** kavramını iki farklı seviyede görebilirsiniz:

```
                  INTERNET
                     │
                     │
          ┌──────────▼─────┐
          │   ISP Router   │ ← Default Gateway (Modem için)
          │                │
          └───────┬────────┘
                  │
                  │
    ┌─────────────|─────────────┐
    │          EV |             │
    │             |             │
    │    ┌────────|─────┐       │
    │    │ ADSL/Kablo   │       │
    │    │    MODEM     │ ← Default Gateway (Bilgisayar için)
    │    └──────────────┘       │
    │         │  │ │            │
    │  ┌──────┘  │ └──┐         │
    │  │         │    │         │
    │ Laptop    PC  Telefon     │
    │                           │
    └───────────────────────────┘
```

---

## 2. Routing (Yönlendirme)

Routing; veri paketlerinin kaynaktan hedefe giderken **en uygun yolu bulma** sürecidir.  
Bu kararı veren cihaz **router (yönlendirici)**'dır.

---

### 📍 Yerel Ağ mı, İnternet mi?

| Senaryo | Açıklama |
|:---|:---|
| **📍 Yerel Erişim** | `10.5.10.10` → `10.5.10.20`: Aynı ağda olduklarından gateway devreye **girmez**, cihazlar switch üzerinden doğrudan haberleşir. |
| **🌍 İnternet Erişimi** | `10.5.10.10` → `193.156.56.164`: Farklı ağda olduğu için paket önce `10.5.10.1` (Gateway) cihazına iletilir, oradan dış ağa (ISP) yönlendirilir. |

---

### 🧠 IP Yönlendirme Mantığı

Cihaz, paket göndermeden önce şu 3 adımlı kararı verir:

1. **Subnet Kontrolü:** Hedef IP, kendi Subnet Mask'i ile aynı ağda mı?
2. **✅ Aynı Ağda ise:** Doğrudan hedefe gönderilir.
3. **❌ Farklı Ağda ise:** Paket **Varsayılan Ağ Geçidi**'ne teslim edilir. Router, Routing Table'a bakarak en uygun çıkış portunu seçer.

---

### 🗺️ Routing Table (Yönlendirme Tablosu)

Router, her paketi nereye göndereceğini **Routing Table** adlı bir tabloya bakarak karar verir.

Basit bir örnek:

| Hedef Ağ | Subnet Mask | Gateway | Açıklama |
|:---|:---|:---|:---|
| `10.5.10.0` | `255.255.255.0` | — | Yerel ağ, doğrudan gönder |
| `0.0.0.0` | `0.0.0.0` | `193.156.56.1` | Diğer tüm paketler → ISP'ye gönder *(Default Route)* |

> 💡 `0.0.0.0` satırı **Default Route** olarak adlandırılır. "Başka bir kural yoksa buradan çık" anlamına gelir.

---

## 3. NAT ve PAT (Network Address Translation — Ağ Adresi Çevirisi)

Private (Özel) IP adreslerinin internete doğrudan çıkamadığını öğrenmiştik. Akla hemen şu soru gelir: *"Benim bilgisayarımın IP'si 192.168.1.5 ise, ben şu an bu web sitesine nasıl bağlanıyorum?"*

İşte bu sorunun cevabı **NAT (Network Address Translation)** protokolüdür. NAT, evinizdeki veya şirketinizdeki router'ın (modemin) kapısında duran bir çevirmendir. İç ağdaki özel adresleri, internette geçerli olan tek bir Public (Genel) adrese çevirir. Teknik olarak routing'den bağımsız bir işlemdir; ancak router üzerinde çalıştığı için ikisi birlikte ele alınır.

---

### ❓ Neden NAT'a İhtiyaç Var?

İç ağlarda kullanılan IP adresleri **özel (private)** adreslerdir ve internette geçersizdir.

| IP Aralığı | Türü |
|:---|:---|
| `10.0.0.0 – 10.255.255.255` | Private (Özel) |
| `172.16.0.0 – 172.31.255.255` | Private (Özel) |
| `192.168.0.0 – 192.168.255.255` | Private (Özel) |
| `193.156.56.164` gibi adresler | Public (Genel) — internette geçerli |

Evde 5 cihazın olduğunu düşün. Hepsinin farklı private IP'si var ama internete **tek bir public IP** ile çıkıyorlar. Bunu sağlayan NAT'tır.

Ağ dünyasında bu çeviri işleminin üç farklı yöntemi vardır:

---

### 1. Static NAT (Birebir Eşleştirme)

İç ağdaki belirli bir cihazın, **her zaman** aynı Public IP adresi ile dışarı çıkmasını sağlayan sistemdir. Birebir (1:1) eşleştirme yapılır.

* **Nasıl Çalışır:** Şirketin bir Web Sunucusu (`192.168.1.10`) vardır. Router'a "Bu sunucu dışarı çıkarken veya dışarıdan biri bu sunucuya gelirken her zaman `88.22.33.44` Public IP'sini kullan" denir.
* **Nerede Kullanılır:** İnternetten sürekli ve sabit bir adresten erişilmesi gereken sunucularda (Web, Mail sunucuları) kullanılır.

---

### 2. Dynamic NAT (Havuz Mantığı)

İçerideki cihazların, dışarı çıkmak için ISP'den satın alınan Public IP **havuzunu** ortaklaşa kullandığı sistemdir.

* **Nasıl Çalışır:** Kurumun 50 personeli var, ancak ISP'den sadece 10 tane Public IP satın alınmış. İnternete çıkmak isteyen ilk 10 personel, bu adresleri kapar ve dışarı çıkar. 11. personel internete girmek için birilerinin işini bitirip IP'yi havuza iade etmesini beklemek zorundadır.
* **Nerede Kullanılır:** Çok nadir kullanılır. Günümüzde IP adreslerinin tükenmesi nedeniyle pratik bir çözüm değildir.

---

### 3. PAT (Port Address Translation / NAT Overload)

İşte hepimizin evinde ve ofislerinde çalışan sihirbaz! **Milyarlarca cihazın internete bağlanabilmesini sağlayan, IPv4'ün tükenmesini yıllarca geciktiren ana kahramandır.**

PAT sayesinde tek bir Public IP adresi kullanılarak, içerideki binlerce cihaz (telefon, tablet, bilgisayar, TV) aynı anda internete çıkabilir.

#### ❓ Peki Router bu kadar cihazı nasıl birbirine karıştırmaz?

PAT, IP adreslerinin yanına geçici **Port Numaraları** (bir nevi kargo takip barkodu) ekleyerek cihazları birbirinden ayırt eder.

**Örnek Senaryo:**
Evdeki Public IP adresiniz: `88.22.33.44`

1. **Telefonun (`192.168.1.5`)** Instagram'a bağlanmak ister. Router bu isteği alır, paket üzerindeki iç IP'yi siler, kendi Public IP'sini yazar ve sonuna rastgele bir port ekler: `88.22.33.44:1001`
2. O sırada **Bilgisayarın (`192.168.1.6`)** YouTube'a bağlanır. Router aynı işlemi yapar ama farklı bir port verir: `88.22.33.44:1002`

İnternetten cevaplar geri geldiğinde Router kendi **NAT Tablosuna** bakar:
> *"Hmm, 1001 portuna gelen cevap Instagram'dan, bu telefonundu. 1002 portuna gelen cevap YouTube'dan, bu bilgisayarındı."* der ve paketleri evin içine doğru cihazlara dağıtır.

---

### ✅ NAT'ın Avantajları

- **IP Tasarrufu:** Tek Public IP ile onlarca cihaz internete çıkabilir.
- **Güvenlik:** İç ağ yapısı (private IP'ler) dışarıya gizlenir.

---

### 🚪 Port Yönlendirme (Port Forwarding)

NAT ve PAT varsayılan olarak **tek yönlüdür**. Yani iç ağdaki bir cihaz internete çıkabilir, ancak internetteki birisi dışarıdan kafasına göre iç ağınıza giremez. Router kapıyı yüzüne kapatır (bu aynı zamanda muazzam bir doğal güvenlik sağlar).

Ancak bazen dışarıdan içeriye erişmemiz *gerekir*. Örneğin evdeki bir güvenlik kamerasına iş yerinden bakmak veya kendi bilgisayarınızda bir Minecraft sunucusu kurup arkadaşlarınızı davet etmek isteyebilirsiniz.

İşte Router üzerinde açtığımız bu özel kapıya **Port Yönlendirme** denir.

* **Mantığı:** Router'a şu kural yazılır: *"Eğer internetten sana **8080** portunu arayarak bir istek gelirse, onu hiç sorgulamadan doğrudan içerideki `192.168.1.20` numaralı kameraya gönder."*
* Böylece dışarıdan Public IP'nizin 8080 portuna gelen herkes, aslında evinizin içindeki kameraya bağlanmış olur.

> ⚠️ **Güvenlik Uyarısı:** Port yönlendirme, dış dünyanın yerel ağınıza (LAN) doğrudan girmesi için bir delik açmak demektir. Kameranızın veya sunucunuzun şifresi zayıfsa, hackerlar bu açtığınız porttan içeri sızabilir.

---

## 📌 Kısa Özet

> 🔹 **Gateway** → Cihazın dış dünya kapısı (genellikle router)  
> 🔹 **Aynı ağ** → Doğrudan git (Gateway yok)  
> 🔹 **Farklı ağ** → Gateway'e ver, router yönlendirir  
> 🔹 **Routing Table** → Router'ın karar defteri  
> 🔹 **Static NAT** → Birebir IP eşleştirme (sunucular için)  
> 🔹 **Dynamic NAT** → IP havuzu paylaşımı (günümüzde nadir)  
> 🔹 **PAT** → Tek Public IP + port numarası ile binlerce cihaz (en yaygın)  
> 🔹 **Port Forwarding** → Dışarıdan içeriye kontrollü erişim kapısı  
> 🔹 **Routing ≠ NAT** → İkisi farklı iş yapar, ikisi de router'da çalışır

