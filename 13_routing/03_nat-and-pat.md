# 🎭 NAT ve PAT (Ağ Adresi Çevirisi)

Private (Özel) IP adreslerinin internete doğrudan çıkamadığını öğrenmiştik. Akla hemen şu soru gelir: *"Benim bilgisayarımın IP'si 192.168.1.5 ise, ben şu an bu web sitesine nasıl bağlanıyorum?"*

İşte bu sorunun cevabı **NAT (Network Address Translation - Ağ Adresi Çevirisi)** protokolüdür. NAT, evinizdeki veya şirketinizdeki router'ın (modemin) kapısında duran bir çevirmendir. İç ağdaki özel adresleri, internette geçerli olan tek bir Public (Genel) adrese çevirir.

Ağ dünyasında bu çeviri işleminin üç farklı yöntemi vardır:

---

## 1. Static NAT (Birebir Eşleştirme)
İç ağdaki belirli bir cihazın, **her zaman** aynı Public IP adresi ile dışarı çıkmasını sağlayan sistemdir. Birebir (1:1) eşleştirme yapılır.

* **Nasıl Çalışır:** Şirketin bir Web Sunucusu (`192.168.1.10`) vardır. Router'a "Bu sunucu dışarı çıkarken veya dışarıdan biri bu sunucuya gelirken her zaman `88.22.33.44` Public IP'sini kullan" denir.
* **Nerede Kullanılır:** İnternetten sürekli ve sabit bir adresten erişilmesi gereken sunucularda (Web, Mail sunucuları) kullanılır.

---

## 2. Dynamic NAT (Havuz Mantığı)
İçerideki cihazların, dışarı çıkmak için ISP'den satın alınan Public IP **havuzunu** ortaklaşa kullandığı sistemdir.

* **Nasıl Çalışır:** Kurumun 50 personeli var, ancak ISP'den sadece 10 tane Public IP satın alınmış. İnternete çıkmak isteyen ilk 10 personel, bu adresleri kapar ve dışarı çıkar. 11. personel internete girmek için birilerinin işini bitirip IP'yi havuza iade etmesini beklemek zorundadır.
* **Nerede Kullanılır:** Çok nadir kullanılır. Günümüzde IP adreslerinin tükenmesi nedeniyle pratik bir çözüm değildir.

---

## 3. PAT (Port Address Translation / NAT Overload)
İşte hepimizin evinde ve ofislerinde çalışan sihirbaz! **Milyarlarca cihazın internete bağlanabilmesini sağlayan, IPv4'ün tükenmesini yıllarca geciktiren ana kahramandır.**

PAT sayesinde tek bir Public IP adresi kullanılarak, içerideki binlerce cihaz (telefon, tablet, bilgisayar, TV) aynı anda internete çıkabilir.

### ❓ Peki Router bu kadar cihazı nasıl birbirine karıştırmaz?
PAT, IP adreslerinin yanına geçici **Port Numaraları** (bir nevi kargo takip barkodu) ekleyerek cihazları birbirinden ayırt eder.

**Örnek Senaryo:**
Evdeki Public IP adresiniz: `88.22.33.44`

1. **Telefonun (`192.168.1.5`)** Instagram'a bağlanmak ister. Router bu isteği alır, paket üzerindeki iç IP'yi siler, kendi Public IP'sini yazar ve sonuna rastgele bir port ekler: `88.22.33.44:1001`
2. O sırada **Bilgisayarın (`192.168.1.6`)** YouTube'a bağlanır. Router aynı işlemi yapar ama farklı bir port verir: `88.22.33.44:1002`

İnternetten cevaplar geri geldiğinde Router kendi **NAT Tablosuna** bakar:
> *"Hmm, 1001 portuna gelen cevap Instagram'dan, bu telefonundu. 1002 portuna gelen cevap YouTube'dan, bu bilgisayarındı."* der ve paketleri evin içine doğru cihazlara dağıtır.

---

## 🚪 Port Yönlendirme (Port Forwarding)
NAT ve PAT varsayılan olarak **tek yönlüdür**. Yani iç ağdaki bir cihaz internete çıkabilir, ancak internetteki birisi dışarıdan kafasına göre iç ağınıza giremez. Router kapıyı yüzüne kapatır (bu aynı zamanda muazzam bir doğal güvenlik sağlar).

Ancak bazen dışarıdan içeriye erişmemiz *gerekir*. Örneğin evdeki bir güvenlik kamerasına iş yerinden bakmak veya kendi bilgisayarınızda bir Minecraft sunucusu kurup arkadaşlarınızı davet etmek isteyebilirsiniz.

İşte Router üzerinde açtığımız bu özel kapıya **Port Yönlendirme** denir.

* **Mantığı:** Router'a şu kural yazılır: *"Eğer internetten sana **8080** portunu arayarak bir istek gelirse, onu hiç sorgulamadan doğrudan içerideki `192.168.1.20` numaralı kameraya gönder."*
* Böylece dışarıdan Public IP'nizin 8080 portuna gelen herkes, aslında evinizin içindeki kameraya bağlanmış olur.

> ⚠️ **Güvenlik Uyarısı:** Port yönlendirme, dış dünyanın yerel ağınıza (LAN) doğrudan girmesi için bir delik açmak demektir. Kameranızın veya sunucunuzun şifresi zayıfsa, hackerlar bu açtığınız porttan içeri sızabilir.
