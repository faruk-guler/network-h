# 📖 Ağ Terminolojisi Sözlüğü

> **Kaynak:** [www.farukguler.com](https://www.farukguler.com)

---

## Alt Ağ (Subnet)

Geniş bir IP ağının daha küçük parçalara bölünmesiyle oluşan ağdır. Bir subnet adresi tarafından tanımlanır. Ağ yöneticisi, güvenlik ve performans için ağı segmentlere ayırır.

## Alt Ağ Maskesi (Subnet Mask)

IP adresinin ağ kısmını ve host kısmını belirlemek için kullanılan değerdir. Örneğin, `/24` subnet maskesi (`255.255.255.0`) IP adresinin ilk 24 bitinin ağ kısmını, son 8 bitinin host kısmını belirtir.

## Ağ Geçidi (Gateway)

Farklı ağları birbirine bağlayan, veri taşımasını sağlayan, yönlendirme işlemlerini gerçekleştiren bir cihaz veya yazılım bileşenidir. Genellikle ofisinizin/evinizin router'ıdır (Örn: `192.168.1.1`).

## ARP (Address Resolution Protocol)

RFC 826 ile tanımlanan, IP adresinden MAC adresini bulan protokoldür.

## Atlama Sayısı (Hop Count)

Yoldaki router'ların sayısına bağlı olarak kaynak ve hedef arasındaki uzaklığı hesaplayan bir routing metriği. **RIP** protokolü tek metriği olarak hop sayısını kullanır (maksimum 15).

## Bant Genişliği (Bandwidth)

Ağ sinyalleri arasında kullanılan en yüksek ve en düşük frekanslar arasındaki aralık. Yaygın olarak, bir ağ protokolü veya ortamının ölçülen throughput (yapılan iş) kapasitesine işaret eder.

## Binary (İkili)

Birleri ve sıfırları kullanan, iki karakterli bir numaralama yöntemi. İkili numaralama sistemi, bilgilerin tamamen dijital gösterimi temeline dayanır.

## Bit

Bir 1 veya 0 olan ikili sayı. Sekiz bit, bir **byte** yapar.

## Bridge (Köprü)

Bir ağdaki iki segmenti bağlamak ve aralarında paketleri aktarmak için kullanılan cihaz. OSI referans modelinin **2. katmanı** (Veri Hattı) üzerinde çalışır. Bridge'in amacı, gelen bir frame'i MAC adresine bağlı olarak filtrelemek, göndermek ve yaymaktır.

## Broadcast Adresi

Bir ağdaki tüm cihazlara gönderilen mesajların ulaştırıldığı adrestir. Örneğin, /24 subnet maskesi ile `192.168.1.0` IP ağı için broadcast adresi `192.168.1.255`'tir.

## Yayın Alanı (Broadcast Domain)

Gruptaki herhangi bir cihazdan başlatılan broadcast frame'lerini alan cihazların grubudur. Router'lar broadcast frame'lerini **iletmezler**, bu nedenle broadcast domain'leri router sınırlarında biter.

## CIDR (Classless Inter-Domain Routing)

IP adreslerinin ve subnet maskelerinin esnek bir şekilde yönetilmesini sağlayan bir sistemdir.## PTR (Pointer) Kaydı

Bir IP adresini bir alan adına eşleyen DNS kaydı (Ters DNS).

## QoS (Quality of Service)

Ağ trafiğini önceliklendirme teknolojisidir. Ses ve video gibi gecikmeye duyarlı trafiğin, dosya indirme gibi az öncelikli trafikten önce iletilmesini sağlar.

## SDN (Software Defined Networking)

Ağın kontrol düzleminin (control plane) veri düzleminden (data plane) ayrıldığı ve yazılım ile merkezi olarak yönetildiği modern ağ mimarisidir.
 ve bir sayı ile belirtilir (örneğin, `/24`). Bir IP ağ grubunun, diğer ağlara birleşik olarak daha geniş görünmesine izin verir.

## Collision (Çarpışma)

Ethernet'te aynı anda aktarım gönderen iki düğümün etkisi. Fiziksel ortamda karşılaştıklarında frame'ler çarpışır ve hasar görür.

## CIA Üçlüsü (Confidentiality, Integrity, Availability)

Bilgi güvenliğinin temel modelidir: Gizlilik (Yetkisiz erişimi önleme), Bütünlük (Veri bozulmasını önleme) ve Erişilebilirlik (Sistemin çalışır durumda olması).

## Collision Domain

Çarpışan frame'lerin tespit edildiği Ethernet'teki ağ alanı. Collision'lar hub ve repeater'lar ile yayılır, fakat LAN switch ve router'larla yayılmaz.

## Connection-Oriented (Bağlantı Odaklı)

Herhangi bir veri transfer edilmeden önce sanal bir devre oluşturan veri transfer yöntemi. Güvenli veri transferi için onay ve akış kontrolü kullanır. **TCP** bu yöntemi kullanır.

## Connectionless (Bağlantısız)

Bir sanal devre yaratmaksızın olan veri transferidir. Düşük ek yüke sahiptir, en güçlü taşımayı kullanır ancak güvenli değildir. **UDP** bu yöntemi kullanır.

## Crossover Kablo

Bir switch'i switch'e, PC'yi PC'ye, hub'ı hub'a bağlayan Ethernet kablo çeşididir. Bir uç T568A, diğer uç T568B standardıyla sonlandırılır.

## Dekapsülleme (De-encapsulation)

Bir katmanın, alt katmandan gelen PDU'daki (Protocol Data Unit) başlık bilgisini sildiği teknik.

## DHCP (Dynamic Host Configuration Protocol)

Ağdaki cihazlara dinamik olarak IP adresi ve diğer ağ yapılandırma bilgilerini dağıtan bir protokoldir. **Port:** UDP 67 (Server) / UDP 68 (Client).

## DMZ (Demilitarized Zone)

Bir organizasyonun iç ağı ile dış ağı (internet) arasında yer alan, dışarıya açık servislerin (web, mail vb.) bulunduğu tampon bölgedir. İç ağı dış dünyadan izole ederek güvenliği artırır.

## DoS / DDoS (Denial of Service)

Bir sistemi veya ağı, meşru kullanıcıların erişemeyeceği şekilde kaynaklarını tüketerek devre dışı bırakma saldırısıdır. DDoS, bu saldırının dağıtık (çoklu kaynak) yapılmasıdır.

## DNS (Domain Name System)

Host isimlerini IP adreslerine çözmek için kullanılır. Örneğin `google.com` → `142.250.185.78`. **Port:** UDP/TCP 53.

## Ethernet

IEEE 802.3 standardına dayanan, CSMA/CD kullanan LAN teknolojisidir. Günümüzde en yaygın kullanılan yerel ağ standardıdır.

## Fast Ethernet

100 Mbps hızında Ethernet düzenlemesidir. IEEE 802.3u standardına dayanır. 10BaseT'den 10 kat daha hızlıdır.

## Fiziksel Katman (Physical Layer)

OSI referans modelinin **1. katmanı**. Veri frame'lerini elektrik sinyaline (veya ışık/radyo) çevirmekten sorumludur. Kablo, konnektör ve sinyalleşme standartlarını tanımlar.

## Frame (Çerçeve)

Data Link katmanı tarafından gönderilen bilginin mantıksal bir birimi. Kaynak MAC, hedef MAC, veri ve hata kontrolü (FCS) içerir.

## FTP (File Transfer Protocol)

Ağ düğümleri arasında dosya aktarılması için kullanılan bir TCP/IP protokolüdür. **Port:** TCP 20 (Data) / TCP 21 (Kontrol). RFC 959 ile tanımlıdır.

## Güvenlik Duvarı (Firewall)

Ağ trafiğini izleyen ve belirlenen güvenlik kurallarına göre gelen/giden paketleri engelleyen veya izin veren güvenlik sistemidir. Donanım veya yazılım tabanlı olabilir.

## Goodput

Uygulama katmanına ulaşan, yani protokol başlıkları ve hatalı paketler çıkarıldıktan sonra kalan **gerçek yararlı veri** hızıdır.

## Handshake

Senkronize operasyonlardan emin olmak için ağdaki bir veya daha fazla cihaz arasında gidip gelen aktarımların serisi. Örnek: TCP 3-way handshake (SYN → SYN-ACK → ACK).

## Host

Ağdaki bir IP adresine sahip olan herhangi bir cihaz (bilgisayar, sunucu, telefon vb.).

## Hub

Gerçekte sadece çok portlu repeater olan **fiziksel katman** cihazıdır. Bir porttan gelen sinyali, gönderildiği port hariç **tüm portlara** iletir. Günümüzde artık kullanılmamaktadır; yerini **switch** almıştır.

## IEEE (Institute of Electrical and Electronics Engineers)

Ağ kurulumu ve haberleşmeyi de içeren birçok alanın standartlarını tanımlayan profesyonel organizasyondur. IEEE standartları (802.3 = Ethernet, 802.11 = Wi-Fi) endüstride en yaygın kullanılan LAN standartlarıdır.

## Internet

Evrensel ağların ağıdır. TCP/IP protokol ailesi üzerine kuruludur ve farklı bilgisayar platformlarını birbirine bağlar.

## Hybrid Cloud (Hibrit Bulut)

Yerel veri merkezi (On-Premise) ile genel bulut (Public Cloud) altyapısının birlikte çalıştığı entegre bilgi işlem ortamı.

## Region (Bölge)

Bulut sağlayıcılarının (AWS, Azure, GCP) coğrafi olarak ayrılmış, birden fazla veri merkezini (Availability Zone) içeren fiziksel konumlarıdır.

## IP Adresi

İnternet Protokolü adresidir ve ağdaki her cihazın benzersiz tanımlayıcısıdır. **IPv4** (32 bit, örn: `192.168.1.1`) ve **IPv6** (128 bit, örn: `2001:db8::1`) olmak üzere iki ana sürümü vardır.

## IP (Internet Protocol)

RFC 791'de tanımlı, TCP/IP yığınının parçası ve bağlantısız servis sunan **Ağ katmanı** protokolüdür. Adresleme, parçalama ve güvenlik özelliklerini sağlar.

## IP Multicast

Bir kaynaktan çeşitli uç noktalara IP trafiğinin çoğaltılmasını mümkün kılan routing tekniği. Tek bir paket, multicast grup adresine gönderilir.

## IPv6

IPv4'ün yerine geçmek üzere geliştirilmiş yeni nesil IP adresleme sistemidir. 128 bit uzunluğunda, hexadecimal tabanlı adresler kullanır. Adres tükenmesi sorununu çözer.

## İstemci (Client)

Ağ üzerindeki bir servisi (web, dosya, e-posta vb.) talep eden ve kullanan bilgisayar veya yazılımdır. Örneğin: Web tarayıcınız bir istemcidir.

## Kapsülleme (Encapsulation)

Bir katmanın, üst katmandan gelen PDU'ya başlık bilgisini eklediği teknik. Örneğin: IP başlığı + TCP başlığı + Uygulama verisi = Paket.

## Katman (Layer)

OSI modelinin nasıl çalıştığını hiyerarşik olarak belirtmek için kullanılan terim. Her katman belirli bir göreve odaklanır (7 katman).

## Latency (Gecikme)

Bir veri paketinin kaynaktan hedefe ulaşması için geçen süredir. Genellikle milisaniye (ms) cinsinden ölçülür.

## Load Balancing (Yük Dengeleme)

Gelen ağ trafiğinin birden fazla sunucuya dengeli bir şekilde dağıtılması işlemidir. Sistem performansını ve yedekliliğini artırır.

## Jitter (Gecikme Değişkenliği)

Paketlerin iletim süreleri arasındaki farktır. Yüksek jitter, özellikle ses ve video (VoIP) trafiğinde takılmalara ve kalite bozukluğuna neden olur.

## LAN (Local Area Network)

Limitli coğrafi bir alandaki (birkaç kilometreye kadar) cihazları birbirine bağlayan yüksek hızlı, düşük gecikmeli ağdır. Örnek: Ev veya ofis ağı.

## LAN Switch

MAC adres tabanlı trafiği doğru porta ileten, yüksek hızlı, çoklu interface'li **Layer 2** köprüleme mekanizmasıdır.

## MAC Adresi (Media Access Control Address)

Her ağ kartının fabrikada atanan **48 bit** uzunluğunda benzersiz fiziksel adresidir. Format: `AA:BB:CC:DD:EE:FF`. İlk 3 byte **OUI** (üretici kodu), son 3 byte benzersiz cihaz numarasıdır.

## MAC (Media Access Control)

Donanım adresleme, ortam erişimi ve frame'ler için hata tespitinden sorumlu, Data Link katmanının alt katmanı.

## Maksimum Hop Sayısı

RIP gibi protokollerde, bir paketin hedefe ulaşmak için geçebileceği en fazla router sayısı (15). Bu sayıyı aşan hedefler "ulaşılamaz" kabul edilir. TTL ile karıştırılmamalıdır.

## Modem (Modulator-Demodulator)

Dijital sinyalleri analog sinyallere (ve tersine) dönüştürerek telefon hatları veya kablo üzerinden internet erişimi sağlayan cihazdır.

## MPLS (Multiprotocol Label Switching)

Verileri uzun ağ adresleri yerine kısa etiketlerle (labels) yönlendiren yüksek performanslı bir WAN teknolojisidir. IP yönlendirmeden daha hızlı ve güvenilirdir.

## Multicast

Tek bir verici ile çoklu alıcılar arasındaki bağlantıdır. Broadcast'in aksine, mesajlar sadece tanımlı bir grup adresine gönderilir.

## NAT (Network Address Translation)

Ağdaki özel (private) IP adreslerini genel (public) IP adreslerine dönüştüren bir yöntemdir. Birden fazla cihazın aynı genel IP adresini kullanabilmesini sağlar.

## Native VLAN

Cisco switch'lerde varsayılan olarak **VLAN 1**'dir. Trunk portlarda tag'siz trafiğin ait olan VLAN'dır. Güvenlik için farklı bir VLAN'a değiştirilmesi önerilir.

## Network Adresi

Bir IP ağı için belirtilen ilk IP adresidir. Tüm host bitleri 0 olarak ayarlanmıştır. Örn: `192.168.1.0/24` ağının network adresi `192.168.1.0`'dır. Cihaza atanamaz.

## Oktet

IP adresinin bir bölümünü tanımlayan 8 bitlik değer. Her oktet 0-255 arasında bir değer alır. Ayrıca **byte** olarak da bilinir.

## OSI (Open Systems Interconnection)

ISO ve ITU-T tarafından geliştirilen, farklı üretici ekipmanlarının birlikte çalışabilirliğini sağlayan 7 katmanlı ağ iletişim standardıdır.

## OUI (Organizationally Unique Identifier)

IEEE tarafından NIC üreticilerine tahsis edilen 3 byte (24 bit) uzunluğunda koddur. MAC adresinin ilk 3 byte'ını oluşturur.

## Paket (Packet)

Veri iletişiminde transfer edilen bilginin temel mantıksal birimi. Başlık bilgileri (kaynak/hedef adres vb.) ve payload (taşınan veri) içerir. **OSI Layer 3**'ün PDU'sudur.

## Paket Kaybı (Packet Loss)

Ağ üzerinden gönderilen bir veya daha fazla paketin hedefe ulaşamaması durumudur. Genellikle ağ yoğunluğu, donanım hataları veya sinyal kalitesizliğinden kaynaklanır.

## Paket Anahtarlama (Packet Switching)

Veriyi paketlere bölerek aktarım yapan ağ teknolojisidir. Birden fazla cihazın aynı iletişim kanalını paylaşmasını mümkün kılar.

## Port

Bir işletim sisteminde çalışan belirli bir uygulamaya veya servise (HTTP, FTP vb.) veri iletmek için kullanılan sanal uç noktadır. 0 ile 65535 arasında numaralandırılır (Örn: Web 80, SSH 22).

## Port Yönlendirme (Port Forwarding)

Dış ağdan (İnternet) gelen belirli bir porttaki trafiğin, iç ağdaki (LAN) belirli bir cihaza ve porta yönlendirilmesi işlemidir. Genellikle modem/router üzerinden yapılır.

## Proxy (Vekil Sunucu)

İstemci ile sunucu arasında duran ve istemci adına istek yapan sunucudur. Güvenlik, hızlandırma (cache) veya içerik filtreleme amacıyla kullanılır.

## Protokol (Protocol)

Ağ üzerindeki cihazların birbirleriyle iletişim kurabilmesi için belirlenmiş kurallar ve standartlar bütünüdür. Ortak bir dil gibidir (Örn: TCP/IP).

## Router (Yönlendirici)

Ağ trafiğinin aktarımında en iyi yola karar veren **Network katmanı** (Layer 3) cihazıdır. IP adreslerine bakarak farklı ağlar arasında paket yönlendirir.

## Yönlendirme (Routing)

IP paketlerinin ağlar arasında yönlendirilmesi ve iletilmesi işlemidir.

## Sequencing (Sıralama)

Sanal devrelerde segment'leri numaralayarak doğru sırayla yeniden birleştirmeyi sağlayan mekanizma. TCP bu özelliği kullanır.

## SD-WAN (Software-Defined WAN)

WAN bağlantılarını (MPLS, LTE, Fiber vb.) yazılım tabanlı olarak yöneten ve optimize eden teknolojidir. Trafiği anlık duruma göre en iyi hattan gönderir.

## Sunucu (Server)

Ağ üzerindeki istemcilere (clients) veri, dosya veya uygulama hizmeti sunan güçlü bilgisayar veya yazılımdır. Örnek: Web sunucusu, veritabanı sunucusu.

## Switch

Ağ kurulumunda frame filtreleme, yönlendirme ve gönderme gibi fonksiyonlardan sorumlu **Layer 2** cihazdır. MAC adres tablosuna bakarak frame'leri doğru porta iletir.

## TCP (Transmission Control Protocol)

En yaygın kullanılan transport protokolüdür. **Bağlantı odaklı** ve **güvenilirdir**. Bir paketin tamamı teslim edilmezse, paket kaynaktan tekrar talep edilir. 3-way handshake ile bağlantı kurar.

## Telnet

TCP/IP protokol ailesinde standart terminal emülasyon protokolüdür. Uzak sunuculara bağlantı sağlar ancak **şifresiz** olduğu için güvenli değildir. **Port:** TCP 23. SSH ile değiştirilmiştir.

## TFTP (Trivial File Transfer Protocol)

FTP'nin basitleştirilmiş versiyonudur. Sadece dosya alıp gönderebilir, directory listeleme gibi özellikler yoktur. **Port:** UDP 69.

## TTL (Time to Live)

Bir paketin geçerli olduğu süreyi/hop sayısını belirten IP başlığındaki alan. Her router'dan geçtiğinde 1 azalır, 0 olunca paket silinir. Sonsuz döngüyü önler.

## UDP (User Datagram Protocol)

Onay veya taşıma garantisi olmaksızın datagramların değiş tokuş edilmesine izin veren **bağlantısız** transport katmanı protokolüdür. Hızlıdır ancak güvenilir değildir. Ses, video ve DNS gibi uygulamalarda kullanılır. RFC 768'de tanımlıdır.

## UTP (Unshielded Twisted Pair)

Korumasız bükümlü çift kablo. Kullanıcı cihazlarını switch'e bağlamak için küçükten büyüğe ağlarda kullanılır. En yaygın ağ kablolama türüdür.

## Varsayılan Rota (Default Route)

Routing tablosunda bir sonraki hop'un belirtilmediği paketleri yöneltmek için kullanılan statik routing tablo girişi. Genellikle `0.0.0.0/0` olarak ifade edilir.

## Veri Bağlantı Katmanı (Data Link Layer)

OSI referans modelinin **2. katmanı**. Fiziksel bir hat üzerinde güvenli veri aktarımını sağlar. Fiziksel adresleme, hat disiplini, ağ topolojisi, hata uyarısı ve akış kontrolü sağlar. IEEE, bu katmanı **MAC** alt katmanı ve **LLC** alt katmanı olarak ikiye bölmüştür.

## VLAN (Virtual LAN)

Bir veya daha fazla mantıksal segmentlere ayrılmış LAN'daki cihazlar grubudur. Fiziksel konuma bağlı olmaksızın cihazları aynı ağ segmentinde gruplamayı sağlar. Güvenlik, performans ve esneklik için kullanılır.

## VPC (Virtual Private Cloud)

Genel bulut sağlayıcıları (AWS, Azure vb.) üzerinde oluşturulan, izole edilmiş sanal ağ. Kullanıcı kendi IP aralığını, alt ağlarını ve ağ geçitlerini tanımlayabilir.

## WAN (Wide Area Network)

Geniş coğrafi alanları kapsayan ağdır. Şehirler, ülkeler veya kıtalar arası bağlantıyı sağlar. İnternet, dünyanın en büyük WAN'ıdır.

## VPN (Virtual Private Network)

Halka açık bir ağ (internet) üzerinde şifreli ve güvenli bir tünel oluşturarak özel ağlara erişim sağlayan teknolojidir. Site-to-Site ve Remote Access türleri vardır.

## Wi-Fi (Wireless Fidelity)

IEEE 802.11 standardına dayanan kablosuz yerel ağ teknolojisidir. **Wi-Fi 4** (802.11n), **Wi-Fi 5** (802.11ac) ve **Wi-Fi 6** (802.11ax) yaygın sürümleridir.

## Wildcard Mask (Ters Maske)

Subnet mask'in tersidir. Access Control List (ACL) ve OSPF konfigürasyonlarında kullanılır. Subnet mask `255.255.255.0` ise wildcard mask `0.0.0.255` olur.

---

## Kaynaklar

- [Turkcell Gelecegi Yazanlar - Terimler Sözlüğü](https://gelecegiyazanlar.turkcell.com.tr/konu/egitim/temel-network-egitimi/terimler-sozlugu)

---

**Navigasyon:**

- [🏠 Ana Sayfa](./README.md)
