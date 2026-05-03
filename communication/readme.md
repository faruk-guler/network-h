# Haberleşme Türleri

Bir ağda cihazlar birbirleriyle üç farklı şekilde haberleşir: **Unicast**, **Multicast** ve **Broadcast**.

## 1) Unicast — Bire Bir İletim

Bir cihazdan **tek bir** cihaza yapılan iletimdir.

Veri paketi yalnızca hedef cihaza ulaşır. Ağdaki diğer cihazlar bu iletimden haberdar olmaz.

**Örnekler:**

- Bir web sitesine bağlanmak
- E-posta göndermek
- WhatsApp'ta mesaj atmak

---

## 2) Multicast — Gruba İletim

Bir cihazdan **belirli bir gruba** üye cihazlara yapılan iletimdir.

Veri paketi yalnızca o gruba kayıtlı cihazlara ulaşır. Gruba dahil olmayan cihazlar bu veriyi almaz.

**Örnekler:**

- IPTV ile canlı yayın izlemek
- Kurumsal ağda video konferans
- Online oyunlarda oyunculara konum güncellemesi göndermek

---

## 3) Broadcast — Herkese İletim

Bir cihazdan **ağdaki tüm** cihazlara yapılan iletimdir.

Veri paketi, ağdaki her cihaza ulaşır. İstemeseler de tüm cihazlar bu iletiyi alır. Ağın son host IP adresi olan `.255` adresi broadcast için kullanılır.

**Örnekler:**

- Bilgisayarın ağa bağlandığında IP adresi istemesi (DHCP)
- Bir cihazın MAC adresini öğrenmek için ağa soru sorması (ARP)
- Ağdaki yazıcı veya paylaşılan kaynakları keşfetmek

---

## Özet Tablo

| | Unicast | Multicast | Broadcast |
|---|---|---|---|
| **Hedef** | Tek cihaz | Belirli grup | Tüm cihazlar |
| **Örnek IP** | `192.168.1.5` | `224.0.0.1` | `192.168.1.255` |
| **Kullanım** | Web, e-posta | IPTV, konferans | DHCP, ARP |
