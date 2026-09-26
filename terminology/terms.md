# 📖 Ağ Terminolojisi Sözlüğü

> **Kaynaklar:**
>
> - https://www.farukguler.com  
> - https://gelecegiyazanlar.turkcell.com.tr/konu/egitim/temel-network-egitimi/terimler-sozlugu

---

## Bit

Bir 1 veya 0 olan ikili sayı. Sekiz bit, bir **byte** yapar.

## BGP (Border Gateway Protocol)

İnternetin sistemler arası (AS'ler arası) yönlendirme protokolüdür; omurga trafiğinin yolunu belirler. Tier-1 operatörler birbirleriyle BGP konuşur; Anycast dağıtımları da BGP üzerine kuruludur.

## Byte
Byte (bayt), dijital sistemlerde veri depolama ve işleme için kullanılan temel birimlerden biridir. Günümüzde standart olarak 1 byte = 8 bit kabul edilir.

## Network Adresi

Bir IP ağı için belirtilen ilk IP adresidir. Tüm host bitleri 0 olarak ayarlanmıştır. Örn: `192.168.1.0/24` ağının network adresi `192.168.1.0`'dır. Cihaza atanamaz.

## Octet

IP adresinin bir bölümünü tanımlayan 8 bitlik değer. Her oktet 0-255 arasında bir değer alır. Ayrıca **byte** olarak da bilinir.

## Hextet

16 bitten oluşan grup; IPv6 adreslerinin yazım birimidir (0000–FFFF). Bir IPv6 adresi 8 hextet'ten oluşur ve hextetler hexadecimal ile yazılır.

## Nibble

4 bitlik veri grubu (bir byte'ın yarısı). Her hexadecimal rakam tam olarak bir nibble'a karşılık geldiği için binary↔hex dönüşümünün yapı taşıdır.

## Broadcast Adresi

Bir ağdaki tüm cihazlara gönderilen mesajların ulaştırıldığı adrestir. Örneğin, /24 subnet maskesi ile `192.168.1.0` IP ağı için broadcast adresi `192.168.1.255`'tir.

---

## ACL (Access Control List)

Ağ trafiğini filtrelemek ve güvenliği sağlamak için router veya switch üzerinde tanımlanan kurallar listesidir. İzin verilen veya engellenen IP adreslerini, portları ve protokolleri belirler.

## Alt Ağ (Subnet)

Geniş bir IP ağının daha küçük parçalara bölünmesiyle oluşan ağdır. Bir subnet adresi tarafından tanımlanır. Ağ yöneticisi, güvenlik ve performans için ağı segmentlere ayırır.

## Alt Ağ Maskesi (Subnet Mask)

IP adresinin ağ kısmını ve host kısmını belirlemek için kullanılan değerdir. Örneğin, `/24` subnet maskesi (`255.255.255.0`) IP adresinin ilk 24 bitinin ağ kısmını, son 8 bitinin host kısmını belirtir.

## Ağ Geçidi (Gateway)

Farklı ağları birbirine bağlayan, veri taşımasını sağlayan, yönlendirme işlemlerini gerçekleştiren bir cihaz veya yazılım bileşenidir. Genellikle ofisinizin/evinizin router'ıdır (Örn: `192.168.1.1`).

## ARP (Address Resolution Protocol)

RFC 826 ile tanımlanan, IP adresinden MAC adresini bulan protokoldür.

## APIPA (Automatic Private IP Addressing)

DHCP sunucusuna ulaşılamadığında işletim sisteminin cihaza otomatik atadığı geçici adres (Link-Local) aralığıdır: `169.254.x.x`. Yalnızca yerel ağda iletişim kurulabilir, internete çıkılamaz (RFC 3927).

## Asimetrik Şifreleme

Şifreleme ve şifre çözme işlemleri için farklı anahtarların (Public ve Private Key) kullanıldığı şifreleme yöntemidir. SSL/TLS ve SSH bu yöntemi kullanır.

## Atlama Sayısı (Hop Count)

Yoldaki router'ların sayısına bağlı olarak kaynak ve hedef arasındaki uzaklığı hesaplayan bir routing metriği. **RIP** protokolü tek metriği olarak hop sayısını kullanır (maksimum 15).

## Bant Genişliği (Bandwidth)

Ağ sinyalleri arasında kullanılan en yüksek ve en düşük frekanslar arasındaki aralık. Yaygın olarak, bir ağ protokolü veya ortamının ölçülen throughput (yapılan iş) kapasitesine işaret eder. "Belirli bir sürede taşınabilecek maksimum veri miktarı"

## Binary (İkili)

Birleri ve sıfırları kullanan, iki karakterli bir numaralama yöntemi. İkili numaralama sistemi, bilgilerin tamamen dijital gösterimi temeline dayanır.

## Bridge (Köprü)

Bir ağdaki iki segmenti bağlamak ve aralarında paketleri aktarmak için kullanılan cihaz. OSI referans modelinin **2. katmanı** (Veri Hattı) üzerinde çalışır. Bridge'in amacı, gelen bir frame'i MAC adresine bağlı olarak filtrelemek, göndermek ve yaymaktır.

## BPDU (Bridge Protocol Data Unit)

STP'de switch'lerin birbirine gönderdiği kontrol mesajı. Bu mesajlarla Root Bridge seçilir ve döngüyü kesecek portlar belirlenir.

## Yayın Alanı (Broadcast Domain)

Gruptaki herhangi bir cihazdan başlatılan broadcast frame'lerini alan cihazların grubudur. Router'lar broadcast frame'lerini **iletmezler**, bu nedenle broadcast domain'leri router sınırlarında biter.

## CIDR (Classless Inter-Domain Routing)

IP adreslerinin ve subnet maskelerinin esnek bir şekilde yönetilmesini sağlayan bir sistemdir ve bir sayı ile belirtilir (Örn: `/24`). Bir IP ağ grubunun, diğer ağlara birleşik olarak daha geniş görünmesine izin verir.

## A Kaydı (Address)

Domain adını IPv4 adresine eşleyen DNS kaydı. Bir web sitesinin arkasında genellikle bu kayıt vardır (örn. `google.com → 142.250.185.78`).

## AAAA Kaydı

Domain adını IPv6 adresine eşleyen DNS kaydı (A kaydının IPv6 karşılığı).

## CNAME Kaydı (Canonical Name)

Bir domain'in takma adıdır; sorguyu başka bir domain'e yönlendirir (örn. `www.siteadi.com → siteadi.com`).

## MX Kaydı (Mail Exchanger)

Domain'e gelen e-postayı teslim alacak sunucuyu ve öncelik değerini tutar.

## NS Kaydı (Name Server)

Bir zone'un (bölgenin) hangi yetkili DNS sunucularında barındığını belirtir.

## PTR (Pointer) Kaydı

Bir IP adresini bir alan adına eşleyen DNS kaydı (Ters DNS).

## QoS (Quality of Service)

Ağ trafiğini önceliklendirme teknolojisidir. Ses ve video gibi gecikmeye duyarlı trafiğin, dosya indirme gibi az öncelikli trafikten önce iletilmesini sağlar.

## MTU (Maximum Transmission Unit)

Bir ağ arayüzünün tek seferde taşıyabileceği maksimum paket boyutudur. Ethernet için genellikle 1500 byte.

## MSS (Maximum Segment Size)

TCP’nin tek segmentte taşıyabileceği maksimum veri miktarıdır.

## PoE (Power over Ethernet)

Ethernet kablosu üzerinden hem veri hem elektrik taşınmasını sağlayan teknolojidir. IP kamera ve Access Point’lerde yaygındır.

## RADIUS

Merkezi kimlik doğrulama (AAA) protokolüdür. VPN, Wi-Fi ve kurumsal erişimlerde kullanılır.

## Access Point (AP)

Kablosuz istemcilerin ağa bağlanmasını sağlayan cihazdır.

## Access Port

Yalnızca tek bir VLAN'a atanmış switch portudur; son kullanıcı cihazları (PC, yazıcı, IP kamera) bu porta bağlanır. Cihaz VLAN etiketinden haberdar değildir; etiketleme switch tarafından yapılır.

## SNMP (Simple Network Management Protocol)

Ağ cihazlarını izlemek ve yönetmek için kullanılan protokoldür. Port: UDP 161/162.

## NTP (Network Time Protocol)

Ağ cihazlarının saat senkronizasyonunu sağlayan protokoldür. Port: UDP 123.

## CDN (Content Delivery Network)

İçeriği kullanıcıya en yakın sunucudan dağıtan sistemdir. Web performansını artırır.

## Overlay Network

Fiziksel ağ üzerinde mantıksal olarak oluşturulan sanal ağ yapısıdır.

## Underlay Network

Overlay ağın üzerinde çalıştığı fiziksel IP ağıdır.

## Jumbo Frame

Standart Ethernet frame’inden daha büyük frame yapısıdır. Genellikle MTU > 1500.

## SDN (Software Defined Networking)

Ağın kontrol düzleminin (control plane) veri düzleminden (data plane) ayrıldığı ve yazılım ile merkezi olarak yönetildiği modern ağ mimarisidir.

## Collision (Çarpışma)

Ethernet'te aynı anda aktarım gönderen iki düğümün etkisi. Fiziksel ortamda karşılaştıklarında frame'ler çarpışır ve hasar görür.

## CIA Üçlüsü (Confidentiality, Integrity, Availability)

Bilgi güvenliğinin temel modelidir: Gizlilik (Yetkisiz erişimi önleme), Bütünlük (Veri bozulmasını önleme) ve Erişilebilirlik (Sistemin çalışır durumda olması).

## Collision Domain

Çarpışan frame'lerin tespit edildiği Ethernet'teki ağ alanı. Collision'lar hub ve repeater'lar ile yayılır, fakat LAN switch ve router'larla yayılmaz.

## DNS Cache

İşletim sistemi veya DNS sunucusunun daha önce çözümlenmiş domain → IP eşleşmelerini geçici olarak saklamasıdır. Sorgu hızını artırır.

## FQDN (Fully Qualified Domain Name)

Bir cihazın veya servisin tam alan adıdır. Örnek: www.google.com.

## Connection-Oriented (Bağlantı Odaklı)

Herhangi bir veri transfer edilmeden önce sanal bir devre oluşturan veri transfer yöntemi. Güvenli veri transferi için onay ve akış kontrolü kullanır. **TCP** bu yöntemi kullanır.

## Connectionless (Bağlantısız)

Bir sanal devre yaratmaksızın olan veri transferidir. Düşük ek yüke sahiptir ve hızlıdır; ancak teslim garantisi yoktur (best-effort delivery). **UDP** bu yöntemi kullanır.

## Crossover Kablo

Bir switch'i switch'e, PC'yi PC'ye, hub'ı hub'a bağlayan Ethernet kablo çeşididir. Bir uç T568A, diğer uç T568B standardıyla sonlandırılır.

## Dekapsülleme (De-encapsulation)

Bir katmanın, alt katmandan gelen PDU'daki (Protocol Data Unit) başlık bilgisini sildiği teknik.

## DHCP (Dynamic Host Configuration Protocol)

Ağdaki cihazlara dinamik olarak IP adresi ve diğer ağ yapılandırma bilgilerini dağıtan bir protokoldür. **Port:** UDP 67 (Server) / UDP 68 (Client).

## DORA

DHCP'nin 4 adımlı çalışma süreci: **D**iscover → **O**ffer → **R**equest → **A**cknowledge. Cihazın henüz IP'si olmadığı için Discover ve Request adımları broadcast olarak gönderilir.

## Lease Time (Kiralama Süresi)

DHCP'nin atadığı IP adresinin "kiralanma" süresidir. Sürenin %50'sinde cihaz yenileme (Renew/T1), %87,5'inde herhangi bir DHCP sunucusuyla kurtarma (Rebind/T2) dener; süre dolunca IP serbest kalır.

## DMZ (Demilitarized Zone)

Bir organizasyonun iç ağı ile dış ağı (internet) arasında yer alan, dışarıya açık servislerin (web, mail vb.) bulunduğu tampon bölgedir. İç ağı dış dünyadan izole ederek güvenliği artırır.

## DoS / DDoS (Denial of Service)

Bir sistemi veya ağı, meşru kullanıcıların erişemeyeceği şekilde kaynaklarını tüketerek devre dışı bırakma saldırısıdır. DDoS, bu saldırının dağıtık (çoklu kaynak) yapılmasıdır.

## DNS (Domain Name System)

Host isimlerini IP adreslerine çözmek için kullanılır. Örneğin `google.com` → `142.250.185.78`. **Port:** UDP/TCP 53.

## Dual-Stack

Bir cihazın veya ağ altyapısının IPv4 ve IPv6'yı aynı anda taşımasıdır; hedef hangiyse uygun protokol otomatik seçilir. Geçiş döneminin en yaygın yöntemidir.

## Ethernet

IEEE 802.3 standardına dayanan, CSMA/CD kullanan LAN teknolojisidir. Günümüzde en yaygın kullanılan yerel ağ standardıdır.

## Fast Ethernet

100 Mbps hızında Ethernet düzenlemesidir. IEEE 802.3u standardına dayanır. 10BaseT'den 10 kat daha hızlıdır.

## Fiber Optik

Veriyi elektrik değil **ışık** sinyalleriyle taşıyan kablo türü. Manyetik parazitlerden tamamen etkilenmez ve kilometrelerce mesafeye veri taşır. İki temel türü: **Single-Mode** (tek mod, uzun mesafe) ve **Multi-Mode** (çok mod, bina içi kısa mesafe).

## Fiziksel Katman (Physical Layer)

OSI referans modelinin **1. katmanı**. Bitleri elektrik sinyaline (veya ışık/radyo dalgasına) dönüştürmekten sorumludur. Kablo, konnektör ve sinyalleşme standartlarını tanımlar.

## Frame (Çerçeve)

Data Link katmanı tarafından gönderilen bilginin mantıksal bir birimi. Kaynak MAC, hedef MAC, veri ve hata kontrolü (FCS) içerir.

## FCS (Frame Check Sequence)

Frame'in sonundaki hata tespit alanı (CRC). Store-and-forward çalışan bir switch, FCS ile frame'in yolda bozulup bozulmadığını anlar; hatalı frame düşürülür.

## FTP (File Transfer Protocol)

Ağ düğümleri arasında dosya aktarılması için kullanılan bir TCP/IP protokolüdür. **Port:** TCP 20 (Data) / TCP 21 (Kontrol). RFC 959 ile tanımlıdır.

## Güvenlik Duvarı (Firewall)

Ağ trafiğini izleyen ve belirlenen güvenlik kurallarına göre gelen/giden paketleri engelleyen veya izin veren güvenlik sistemidir. Donanım veya yazılım tabanlı olabilir.

## Goodput

Uygulama katmanına ulaşan, yani protokol başlıkları ve hatalı paketler çıkarıldıktan sonra kalan **gerçek yararlı veri** hızıdır.

## Loopback Address

Bir cihazın kendi ağ kartını ve TCP/IP yığınını test etmek için kullandığı özel adrestir. IPv4 için 127.0.0.1, IPv6 için ::1/128 olarak tanımlanır.

## Handshake

Senkronize operasyonlardan emin olmak için ağdaki bir veya daha fazla cihaz arasında gidip gelen aktarımların serisi. Örnek: TCP 3-way handshake (SYN → SYN-ACK → ACK).

## Host

Ağdaki bir IP adresine sahip olan herhangi bir cihaz (bilgisayar, sunucu, telefon vb.).

## Hexadecimal (Onaltılık)

Tabanı 16 olan sayı sistemi; 0-9 ve A-F olmak üzere 16 sembol kullanır. Her hex rakamı tam 4 bit (1 nibble) eder. Ağ dünyasında MAC adresleri, IPv6 ve renk kodlarında kullanılır.

## Hub

Gerçekte sadece çok portlu repeater olan **fiziksel katman** cihazıdır. Bir porttan gelen sinyali, gönderildiği port hariç **tüm portlara** iletir. Günümüzde artık kullanılmamaktadır; yerini **switch** almıştır.

## IEEE (Institute of Electrical and Electronics Engineers)

Ağ kurulumu ve haberleşmeyi de içeren birçok alanın standartlarını tanımlayan profesyonel organizasyondur. IEEE standartları (802.3 = Ethernet, 802.11 = Wi-Fi) endüstride en yaygın kullanılan LAN standartlarıdır.

## ICMP (Internet Control Message Protocol)

Ağda hata bildirme ve teşhis amaçlı protokol. Ping (Echo Request/Reply) ve traceroute (Time Exceeded) ICMP ile çalışır. IP protokol numarası **1**'dir; port kullanmaz, IP paketinin içinde taşınır.

## Internet

Evrensel ağların ağıdır. TCP/IP protokol ailesi üzerine kuruludur ve farklı bilgisayar platformlarını birbirine bağlar.

## ISP (Internet Service Provider — ISS)

Abonelerine internet erişimi sağlayan operatörler (Türk Telekom, Superonline vb.). Kademeli yapıda çalışırlar: Tier 3 (yerel) → Tier 2 (bölgesel) → Tier 1 (küresel omurga).

## IXP (Internet Exchange Point)

Farklı ISP'lerin trafik takas etmek için fiziksel olarak buluştuğu noktalardır (İstanbul'da TR-IX, Frankfurt'ta DE-CIX). Yerel trafiği yerelde tutarak gecikmeyi ve maliyeti düşürür.

## Hybrid Cloud (Hibrit Bulut)

Yerel veri merkezi (On-Premise) ile genel bulut (Public Cloud) altyapısının birlikte çalıştığı entegre bilgi işlem ortamı.

## Region (Bölge)

Bulut sağlayıcılarının (AWS, Azure, GCP) coğrafi olarak ayrılmış, birden fazla veri merkezini (Availability Zone) içeren fiziksel konumlarıdır.

## IP Adresi

İnternet Protokolü adresidir ve ağdaki her cihazın benzersiz tanımlayıcısıdır. **IPv4** (32 bit, örn: `192.168.1.1`) ve **IPv6** (128 bit, örn: `2001:db8::1`) olmak üzere iki ana sürümü vardır.

## IP (Internet Protocol)

RFC 791'de tanımlı, TCP/IP yığınının parçası ve bağlantısız servis sunan **Ağ katmanı** protokolüdür. Adresleme ve parçalama (fragmentation) sağlar; güvenilirlik ve güvenlik üst katmanların (TCP, IPsec) işidir.

## IP Multicast

Bir kaynaktan çeşitli uç noktalara IP trafiğinin çoğaltılmasını mümkün kılan routing tekniği. Tek bir paket, multicast grup adresine gönderilir.

## IPv6

IPv4'ün yerine geçmek üzere geliştirilmiş yeni nesil IP adresleme sistemidir. 128 bit uzunluğunda, hexadecimal tabanlı adresler kullanır. Adres tükenmesi sorununu çözer.

## Private IP Adresleri

Yalnızca yerel ağlarda kullanılan, internette yönlendirilemeyen adresler (RFC 1918): `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`. İnternete çıkışları NAT ile public adrese çevrilerek olur.

## Public IP Adresleri

Dünya genelinde benzersiz, internette yönlendirilebilir adresler. IANA → RIR (RIPE NCC, ARIN vb.) → ISP zinciriyle dağıtılır. IPv4 public adresleri 2011'de fiilen tükendi; geçiş IPv6 ile sürmektedir.

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

## Unicast

Bir kaynaktan yalnızca tek bir hedef cihaza yapılan iletimdir (1→1). Ağdaki en yaygın trafik türüdür: web, SSH, dosya transferi.

## Anycast

Aynı IP adresinin birden fazla sunucuya atanmasıdır; paket, yönlendirme (BGP) sayesinde en yakın sunucuya ulaşır. Google DNS (`8.8.8.8`) ve CDN altyapıları bu yöntemi kullanır.

## NAT (Network Address Translation)

Ağdaki özel (private) IP adreslerini genel (public) IP adreslerine dönüştüren bir yöntemdir. Birden fazla cihazın aynı genel IP adresini kullanabilmesini sağlar.

## Native VLAN

Cisco switch'lerde varsayılan olarak **VLAN 1**'dir. Trunk portlarda tag'siz trafiğin ait olan VLAN'dır. Güvenlik için farklı bir VLAN'a değiştirilmesi önerilir.

## OSI (Open Systems Interconnection)

ISO ve ITU-T tarafından geliştirilen, farklı üretici ekipmanlarının birlikte çalışabilirliğini sağlayan 7 katmanlı ağ iletişim standardıdır.

## OSPF (Open Shortest Path First)

Açık standart (RFC 2328) iç gateway yönlendirme protokolü. Her router tüm ağın haritasını çıkarır ve Dijkstra ile en kısa yolu hesaplar; metrik olarak bant genişliğini kullanır. Kurumsal ağların fiili standardıdır.

## OUI (Organizationally Unique Identifier)

IEEE tarafından NIC üreticilerine tahsis edilen 3 byte (24 bit) uzunluğunda koddur. MAC adresinin ilk 3 byte'ını oluşturur.

## Octal (Sekizlik)

Tabanı 8 olan sayı sistemi; yalnızca 0-7 rakamları kullanılır. Her octal rakam 3 bitlik gruba karşılık gelir. Linux dosya izinlerinde yaygındır (`chmod 755`).

## Paket (Packet)

Veri iletişiminde transfer edilen bilginin temel mantıksal birimi. Başlık bilgileri (kaynak/hedef adres vb.) ve payload (taşınan veri) içerir. **OSI Layer 3**'ün PDU'sudur.

## Paket Kaybı (Packet Loss)

Ağ üzerinden gönderilen bir veya daha fazla paketin hedefe ulaşamaması durumudur. Genellikle ağ yoğunluğu, donanım hataları veya sinyal kalitesizliğinden kaynaklanır.

## Paket Anahtarlama (Packet Switching)

Veriyi paketlere bölerek aktarım yapan ağ teknolojisidir. Birden fazla cihazın aynı iletişim kanalını paylaşmasını mümkün kılar.

## PAT (Port Address Translation / NAT Overload)

En yaygın NAT türü: içerideki tüm private adresler, tek bir public IP üzerinde **farklı port numaralarıyla** dışarı çıkar (`88.22.33.44:1001` gibi). IPv4 tükenmesini onlarca yıl geciktiren teknolojidir.

## PDU (Protocol Data Unit)

OSI modelinde her katmanda verinin aldığı isim: Veri (Katman 7), Segment (Katman 4), Paket (Katman 3), Frame (Katman 2), Bit (Katman 1).

## Port

Bir işletim sisteminde çalışan belirli bir uygulamaya veya servise (HTTP, FTP vb.) veri iletmek için kullanılan sanal uç noktadır. 0 ile 65535 arasında numaralandırılır (Örn: Web 80, SSH 22).

## Port Yönlendirme (Port Forwarding)

Dış ağdan (İnternet) gelen belirli bir porttaki trafiğin, iç ağdaki (LAN) belirli bir cihaza ve porta yönlendirilmesi işlemidir. Genellikle modem/router üzerinden yapılır.

## Proxy (Vekil Sunucu)

İstemci ile sunucu arasında duran ve istemci adına istek yapan sunucudur. Güvenlik, hızlandırma (cache) veya içerik filtreleme amacıyla kullanılır.

## Protokol (Protocol)

Ağ üzerindeki cihazların birbirleriyle iletişim kurabilmesi için belirlenmiş kurallar ve standartlar bütünüdür. Ortak bir dil gibidir (Örn: TCP/IP).

## Root Bridge

STP (Spanning Tree Protocol) topolojisinde referans noktası olarak seçilen ve tüm yolların hesaplandığı ana switch'tir. En düşük Bridge ID'ye sahip switch Root Bridge seçilir.

## Router (Yönlendirici)

Ağ trafiğinin aktarımında en iyi yola karar veren **Network katmanı** (Layer 3) cihazıdır. IP adreslerine bakarak farklı ağlar arasında paket yönlendirir.

## RIP (Routing Information Protocol)

En eski dinamik yönlendirme protokolü. Metrik olarak hop sayısı kullanır ve 15 hop sınırı vardır; her 30 saniyede bir tablo komşulara gönderilir. Bugün yerini OSPF'ye bırakmıştır.

## Yönlendirme (Routing)

IP paketlerinin ağlar arasında yönlendirilmesi ve iletilmesi işlemidir.

## Statik ve Dinamik Routing

Statik routing: rotaların yönetici tarafından elle girilmesi (küçük ağ, öngörülebilir, arıza toleransı yok). Dinamik routing: router'ların RIP/OSPF/BGP gibi protokollerle rotaları birbirinden öğrenmesi (büyük ağ, otomatik toparlanma).

## Sequencing (Sıralama)

Sanal devrelerde segment'leri numaralayarak doğru sırayla yeniden birleştirmeyi sağlayan mekanizma. TCP bu özelliği kullanır.

## Subnetting (Alt Ağlara Bölme)

Büyük bir IP bloğunu, host bitlerinden borçlanarak daha küçük ve yönetilebilir alt ağlara bölme işlemidir. Broadcast trafiğini azaltır, güvenliği ve adres verimliliğini artırır.

## Supernetting (Route Summarization)

Subnetting'in tersi: yan yana küçük ağların tek büyük bir önekte (prefix) birleştirilmesi (4 × /24 → /22). Yönlendirme tablolarını küçük ve hızlı tutmak için kullanılır.

## SLAAC (Stateless Address Autoconfiguration)

IPv6'da cihazın, router'dan gelen reklam (RA) mesajıyla kendi adresini **kendiliğinden** oluşturmasıdır. Sunucu gerektirmez; IPv6'nın neden standart /64 alt ağ kullandığının sebebidir.

## SSID (Service Set Identifier)

Kablosuz ağın yayın addır; cihazların Wi-Fi listesinde gördüğü isimdir.

## STP (Spanning Tree Protocol)

Ethernet ağlarında sonsuz döngüleri (Loop) engellemek için geliştirilmiş Layer 2 protokolüdür (IEEE 802.1D). Yedekli yolları geçici olarak kapatarak ağın çökmesini önler.

> ⚠️ **Karışıklık uyarısı:** Kablolama bölümündeki **STP (Shielded Twisted Pair)** —koruma zıhlı bakır kablo— tamamen farklı bir kavramdır; bağlama göre okunmalıdır.

## RSTP (Rapid Spanning Tree Protocol)

STP'nin hızlı yakınsayan güncel sürümü (IEEE 802.1w). Port rol değişimlerini eşleşmeli (proposal/agreement) yaparak 30-50 saniye yerine 1-6 saniyede forwarding'e geçer.

## SD-WAN (Software-Defined WAN)

WAN bağlantılarını (MPLS, LTE, Fiber vb.) yazılım tabanlı olarak yöneten ve optimize eden teknolojidir. Trafiği anlık duruma göre en iyi hattan gönderir.

## Sunucu (Server)

Ağ üzerindeki istemcilere (clients) veri, dosya veya uygulama hizmeti sunan güçlü bilgisayar veya yazılımdır. Örnek: Web sunucusu, veritabanı sunucusu.

## Switch

Ağ kurulumunda frame filtreleme, yönlendirme ve gönderme gibi fonksiyonlardan sorumlu **Layer 2** cihazdır. MAC adres tablosuna bakarak frame'leri doğru porta iletir.

## TCP (Transmission Control Protocol)

En yaygın kullanılan transport protokolüdür. **Bağlantı odaklı** ve **güvenilirdir**. Bir paketin tamamı teslim edilmezse, paket kaynaktan tekrar talep edilir. 3-way handshake ile bağlantı kurar.

## TCP/IP Modeli

İnternetin üzerinde çalıştığı, 4 katmanlı pratik ağ modelidir: Uygulama, Taşıma, İnternet, Ağ Erişimi. OSI'nin sadeleştirilmiş halidir; OSI'nin 5, 6 ve 7. katmanları tek "Uygulama" katmanında birleşir.

## Telnet

TCP/IP protokol ailesinde standart terminal emülasyon protokolüdür. Uzak sunuculara bağlantı sağlar ancak **şifresiz** olduğu için güvenli değildir. **Port:** TCP 23. SSH ile değiştirilmiştir.

## TFTP (Trivial File Transfer Protocol)

FTP'nin basitleştirilmiş versiyonudur. Sadece dosya alıp gönderebilir, directory listeleme gibi özellikler yoktur. **Port:** UDP 69.

## Ağ Topolojisi

Ağdaki cihazların fiziksel veya mantıksal dizilimi: Bus (veri yolu), Star (yıldız), Ring (halka), Mesh (örgü) ve Hibrit. Topoloji; dayanıklılık, maliyet ve yönetimi doğrudan belirler.

## Trunk Port

Birden fazla VLAN'a ait trafiği taşıyabilen switch portudur. Genellikle switch'ler arası bağlantıda kullanılır ve 802.1Q etiketleme (tagging) yapar.

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

IEEE 802.11 standardına dayanan kablosuz yerel ağ teknolojisidir. **Wi-Fi 4** (802.11n), **Wi-Fi 5** (802.11ac), **Wi-Fi 6/6E** (802.11ax) ve **Wi-Fi 7** (802.11be) en bilinen sürümleridir.

## WPA2 / WPA3 (Wi-Fi Protected Access)

Wi-Fi şifreleme güvenlik standartları. WEP ve ilk WPA güvensiz sayılır; günümüzde en az WPA2, yeni kurulumlarda WPA3 tercih edilmelidir.

## Wildcard Mask (Ters Maske)

Subnet mask'in (alt ağ maskesinin) bit bazında tam tersidir. İkili sistemdeki 1'lerin 0, 0'ların 1 yapılmasıyla elde edilir. Access Control List (ACL) ve OSPF konfigürasyonlarında kullanılır. Subnet mask `255.255.255.0` ise wildcard mask `0.0.0.255` olur.

## WWW (World Wide Web)

İnternetin üzerinde HTTP protokolü ve tarayıcılarla çalışan bir bilgi hizmetidir. "İnternet" ile karıştırılır; web sadece internetin uygulamalarından biridir — e-posta ve VPN de internet üzerinde çalışır ama web değildir.
