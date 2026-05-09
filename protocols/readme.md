# Ağ Protokolleri

Bilgisayar ağlarında iletişim, rastgele gerçekleşen bir veri akışı değil, belirli kurallar çerçevesinde yönetilen bir süreçtir. Bu kurallar bütününe **Protokol** adı verilir. Protokoller, verinin nasıl paketleneceğini, nasıl adresleneceğini, nasıl iletileceğini ve hata durumunda ne yapılacağını tanımlar.

## Protokol Nedir?
Bir ağ protokolü, ağ üzerindeki iki veya daha fazla cihazın birbirini anlamasını sağlayan ortak dildir. Tıpkı insanların iletişim kurarken kullandığı dil bilgisi kuralları gibi, makineler de veri alışverişi yaparken protokol standartlarına uymak zorundadır.

## OSI Modeli ve Katmanlı Yapı
Protokoller genellikle OSI (Open Systems Interconnection) modelindeki yedi katmana göre sınıflandırılır. Her katman, bir üst katmana hizmet sunar ve kendine özgü protokollere sahiptir.

| Katman No | Katman Adı | Fonksiyon | Önemli Protokoller |
| :--- | :--- | :--- | :--- |
| 7 | Uygulama (Application) | Kullanıcı arayüzü ve ağ servisleri | HTTP, FTP, DNS, SSH, SMTP |
| 4 | İletim (Transport) | Veri akış kontrolü ve hata denetimi | TCP, UDP |
| 3 | Ağ (Network) | Yönlendirme ve mantıksal adresleme | IP (IPv4/IPv6), ICMP, ARP |
| 2 | Veri Bağı (Data Link) | Fiziksel adresleme (MAC) | Ethernet, Switch protokolleri |

## En Yaygın Ağ Protokolleri

### Uygulama Katmanı Protokolleri
* **HTTP/HTTPS (HyperText Transfer Protocol):** Web sayfalarının tarayıcılara iletilmesini sağlar. HTTPS, veriyi TLS/SSL ile şifreleyerek güvenli hale getirir.
* **DNS (Domain Name System):** Alan adlarını (google.com) IP adreslerine (142.250.185.78) dönüştürür.
* **SSH (Secure Shell):** Uzaktaki bir sunucuya güvenli ve şifreli komut satırı erişimi sağlar.
* **DHCP (Dynamic Host Configuration Protocol):** Ağdaki cihazlara otomatik olarak IP adresi, alt ağ maskesi ve ağ geçidi atar.

### İletim Katmanı Protokolleri
İletişimin karakterini belirleyen iki ana protokol vardır:
1.  **TCP (Transmission Control Protocol):** Bağlantı temellidir. Verinin tam ve sıralı ulaştığını garanti eder. (Örn: Web tarama, E-posta)
2.  **UDP (User Datagram Protocol):** Bağlantısızdır. Hız önceliklidir, veri kaybını denetlemez. (Örn: Video konferans, Online oyunlar)

### Ağ Katmanı Protokolleri
* **IP (Internet Protocol):** Veri paketlerinin kaynaktan hedefe yönlendirilmesini sağlar. IPv4 32-bit (Octet bazlı), IPv6 ise 128-bit (Hextet bazlı) adresleme kullanır.
* **ICMP (Internet Control Message Protocol):** Ağdaki hata raporlama ve teşhis işlemlerinde kullanılır (Ping komutu gibi).

## Özet Tablo: Protokoller ve Portlar

| Protokol | Varsayılan Port | Kullanım Amacı |
| :--- | :--- | :--- |
| SSH | 22 | Güvenli Uzak Bağlantı |
| DNS | 53 | Alan Adı Çözümleme |
| HTTP | 80 | Web İçeriği İletimi |
| HTTPS | 443 | Güvenli Web İçeriği |
| RDP | 3389 | Uzak Masaüstü Bağlantısı |

---
> **Not:** Ağ dünyası yalnızca yukarıda bahsedilen birkaç protokolden ibaret değildir. Dosya aktarımı (*FTP*), uzaktan güvenli bağlantı (*SSH*), otomatik IP dağıtımı (*DHCP*), e-posta iletimi (*SMTP*) veya karmaşık cihaz yönlendirmeleri (*BGP, OSPF*) gibi çok çeşitli ihtiyaçlar için tasarlanmış **yüzlerce farklı protokol bulunmaktadır**.
