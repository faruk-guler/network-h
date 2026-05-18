# 🌍-🌎-🌏 İnternet Nasıl Çalışır?

> *1969'da iki üniversite bilgisayarı arasında ilk mesaj gönderildi. Mesaj "LOGIN" kelimesiydi. Sistem ikinci harfte çöktü. Karşı tarafa yalnızca "LO" ulaştı. İnternet böyle başladı — mütevazı, hatalı ve insani.*

---

Hepimiz her gün "internete giriyoruz" ama çoğu insan interneti havada asılı duran sihirli bir "bulut" olarak hayal eder. Oysa gerçekte internet; okyanusların altından geçen kablolar, devasa veri merkezleri ve birbirine bağlı milyonlarca yönlendiriciden oluşan **fiziksel bir altyapıdır.**

Ve bu altyapının sahibi tek bir şirket, tek bir hükümet ya da tek bir ülke değildir. İnternet, **birbirine bağlı binlerce ağın oluşturduğu bir ağdır.** Merkezi yoktur. Kapatılabilecek tek bir noktası yoktur.

---

## 1. İnternet "Bulut" Değil, Kablodur

Telefonunla 5G üzerinden ya da evde Wi-Fi ile bağlansanız da sinyalin havada yalnızca birkaç metre yol alır. En yakındaki baz istasyonuna veya evindeki modeme ulaştığı an **fiber optik kablolara** girer.

Kıtalar arası iletişim uydularla değil, okyanusların tabanına döşenmiş **denizaltı kabloları** (Submarine Cables) ile sağlanır. Türkiye'den Amerika'daki bir web sitesine bağlandığında gönderdiğin paket, Atlantik Okyanusu'nun derinliklerindeki fiziksel bir cam kablodan geçerek hedefe ulaşır.

Bu kablolar parmak kalınlığında olabilir. Ama içlerinden geçen ışık sinyalleri saniyede terabitlerce veri taşır. Bugün itibarıyla 400'den fazla sualtı kablosu dünya okyanuslarının dibini örümcek ağı gibi kaplamış durumda.

---

## 2. İnternetin Sahipleri: Servis Sağlayıcılar (ISP)

İnternetin tek bir sahibi yoktur. Onu ayakta tutan, birbirine bağlanan binlerce farklı ağdır. Bu ağları işleten şirketlere **ISP (Internet Service Provider)** denir ve üç kademede çalışırlar:

- **Tier 3 — Yerel ISP'ler:** Seni bulunduğun ülkedeki ana santrallere bağlayan tanıdık şirketler. (Türk Telekom, Superonline gibi.) Sana kablo çekerler ama küresel ağa doğrudan erişimleri yoktur.
- **Tier 2 — Bölgesel ISP'ler:** Bir ya da birkaç ülkeyi kapsayan ağ operatörleri. Hem Tier 1'den bant genişliği satın alırlar hem de birbirleriyle peering (karşılıklı anlaşma) yaparlar.
- **Tier 1 — Küresel ISP'ler:** Adını pek duymadığın ama internetin omurgasını oluşturan devasa uluslararası şirketler. (Telia, Lumen/Level3 gibi.) Kıtaları okyanus altı kablolarla birbirine bağlarlar. Yerel servis sağlayıcın, bu şirketlere para ödeyerek seni küresel ağa çıkarır.

---

## 3. Web Siteleri Nerede Yaşıyor? — Veri Merkezleri ve CDN

Bir web sitesine girmek, aslında dünyanın başka bir yerindeki bilgisayara bağlanıp ondan dosya istemektir.

Google, Netflix veya Instagram gibi platformlar ev bilgisayarlarına sığmaz. Futbol sahası büyüklüğünde, içinde on binlerce güçlü sunucunun bulunduğu, 7/24 soğutma sistemleriyle çalışan ve asla elektriği kesilmeyen dev binalarda barınırlar. Bu binalara **Veri Merkezi (Data Center)** denir.

Ama burada önemli bir nokta var: Netflix'ten bir dizi açtığında, o video okyanusları aşıp Amerika'daki bir sabit diskten gelmez. Çünkü Netflix gibi büyük platformlar içeriklerini dünya genelinde stratejik noktalara önceden kopyalar. İstanbul'daysan büyük ihtimalle İstanbul'daki ya da Frankfurt'taki bir sunucudan gelir.

Bu sisteme **CDN (Content Delivery Network — İçerik Dağıtım Ağı)** denir. Amacı içeriği kullanıcıya olabildiğince yakın tutmaktır. Hem gecikme (latency) azalır hem de ana sunucunun üzerindeki yük hafifler.

---

## 4. Ağlar Nerede Buluşuyor? — IXP

Farklı ISP'lerin ağları birbirleriyle nerede konuşur? **IXP (Internet Exchange Point — İnternet Değişim Noktası)** adı verilen fiziksel noktalarda.

Bu noktalar olmadan her ülkedeki trafik önce Amerika'ya gidip geri dönmek zorunda kalabilirdi. İstanbul'da bir IXP var (TR-IX). Frankfurt'ta Avrupa'nın en büyüklerinden biri çalışıyor (DE-CIX). Bu noktalar sayesinde yerel trafik yerel kalır, gecikme azalır, maliyet düşer.

---

## 5. İnternetin Trafik Polisi — BGP

Paketin Türkiye'den Japonya'ya giderken hangi ülkelerden, hangi yönlendiricilerden ve hangi kablolardan geçeceğine kim karar veriyor?

Bu devasa haritayı yöneten protokole **BGP (Border Gateway Protocol)** denir. BGP, internetteki tüm yolları bilen dev bir navigasyon sistemi gibidir. Bir ülkede fiber kablo koptuğunda BGP saniyeler içinde trafiği başka bir güzergaha yönlendirir ve internet çökmez.

Bu dayanıklılık tesadüf değil, tasarım gereği. İnternetin atası ARPANET, nükleer saldırıya karşı dayanıklı bir iletişim ağı olarak kurulmuştu. Merkezi bir nokta yoksa, o noktayı yok ederek sistemi çökertmek mümkün değildir.

---

## 6. İnterneti Kim Yönetiyor?

Kısa cevap: kimse. Ve herkes.

Birkaç kuruluş kritik parçaları koordine eder:

- **ICANN** — Alan adlarını ve IP adres bloklarını kim kullanacak koordine eder. `.com`, `.tr`, `.org` gibi uzantıları yönetir.
- **IETF** — İnternet protokollerinin standartlarını yazar. Kararlar "RFC" adı verilen açık belgelerle yayınlanır. Herkes katılabilir.
- **RIPE NCC** — Avrupa, Orta Doğu ve Türkiye dahil bölgedeki IP adreslerini dağıtan kuruluştur.

---

## 7. WWW ile İnternet Aynı Şey Değildir

Sık yapılan bir yanılgı: "internete girmek" ile "web'e girmek" aynı şey sanılır.

**İnternet** — altyapıdır. Kablolar, protokoller, yönlendiriciler.

**World Wide Web (WWW)** — bu altyapı üzerinde çalışan bir **hizmettir.** HTTP protokolü ve tarayıcılar aracılığıyla birbirine bağlı sayfalar topluluğu.

E-posta da interneti kullanır. WhatsApp mesajları da. Bir oyun sunucusuna bağlanmak da. Bunların hiçbiri web değildir ama hepsi internettir.

Web, Tim Berners-Lee tarafından 1991'de icat edildi — internetin kendisinden yaklaşık 20 yıl sonra.

---

## Büyük Resim

```
Senin Cihazın
     │
     │  Wi-Fi / 5G (birkaç metre)
     ▼
Modem / Router
     │
     │  Fiber / ADSL
     ▼
Yerel ISP (Tier 3)
     │
     │  Ulusal fiber hatlar
     ▼
IXP (TR-IX gibi)
     │
     ├──── Bölgesel ISP (Tier 2)
     │              │
     │        Tier 1 Omurga Ağı
     │              │
     │       Sualtı Kabloları
     │              │
     └──────────────┘
                    │
              Uzak Ülkedeki ISP
                    │
              CDN Sunucusu
                    │
              Hedef Veri Merkezi
```

---

## Özet Tablo

| Kavram | Ne işe yarar |
|---|---|
| Fiber Optik / Sualtı Kabloları | Verileri ışıkla fiziksel olarak taşır |
| ISP (Tier 1/2/3) | İnternete erişim kademelerini oluşturur |
| BGP | Paketleri en iyi güzergahtan yönlendirir |
| IXP | Farklı ağların fiziksel buluşma noktası |
| Veri Merkezi | Web sitelerinin ve servislerin yaşadığı binalar |
| CDN | İçeriği kullanıcıya yakın tutar |
| DNS | Alan adlarını IP adresine çevirir |
| WWW | İnternet üzerinde çalışan bir hizmet, internetin kendisi değil |

---
