# Ağda Haberleşme Türleri

Bir ağda 3 tür haberleşme vardır: **Unicast**, **Multicast** ve **Broadcast**.

---

## 1) Unicast

Bir cihazdan **sadece bir** cihaza yapılan iletim.

Gönderici ile alıcı arasında bire bir iletişim kurulur. Veri paketi yalnızca hedef cihaza ulaşır, ağdaki diğer cihazlar bu iletimi görmez.

**Gerçek hayattan örnekler:**

- Tarayıcınızdan bir web sitesine istek göndermek (HTTP/HTTPS)
- WhatsApp'ta birine mesaj atmak
- Bir sunucuya SSH bağlantısı açmak
- E-posta göndermek (SMTP)
- VoIP ile bire bir sesli arama yapmak

---

## 2) Multicast

Bir cihazdan **belirli bir gruba** üye cihazlara yapılan iletim.

Veri paketi, ilgili gruba kayıtlı olan cihazlara iletilir. Gruba üye olmayan cihazlar bu veriyi almaz. Böylece bant genişliği verimli kullanılır.

**Gerçek hayattan örnekler:**

- Canlı yayın platformlarında video akışı (IPTV, online konser)
- Kurumsal ağlarda videokonferans (sadece toplantıya katılanlar alır)
- Borsa veri akışları (abone olan kullanıcılara anlık fiyat gönderimi)
- Yönlendiriciler arasındaki routing protokolleri (OSPF, RIP v2)
- Online oyunlarda aynı sunucudaki oyunculara konum güncellemesi

---

## 3) Broadcast

Bir cihazdan **ağdaki tüm** cihazlara yapılan iletim.

Veri paketi, ağdaki her cihaza gönderilir. Cihazlar paketi dinlemek zorunda olsun ya da olmasın, tümü bu iletiyi alır. Ağın son host IP adresi (`.255`) broadcast için kullanılır.

**Gerçek hayattan örnekler:**

- DHCP: Bilgisayarın ağa bağlandığında IP adresi istemesi (`192.168.1.255`)
- ARP: Bir cihazın MAC adresini öğrenmek için tüm ağa sorması
- Ağdaki yazıcıları veya paylaşılan kaynakları keşfetme (NetBIOS)
- Yönlendiricinin ağ yapılandırmasını duyurması
- Wake-on-LAN: Ağdaki bir cihazı uzaktan uyandırma paketi

---

## Karşılaştırma

| Özellik | Unicast | Multicast | Broadcast |
|---|---|---|---|
| Hedef | Tek cihaz | Belirli grup | Tüm cihazlar |
| Bant genişliği | Düşük | Orta | Yüksek |
| Ölçeklenebilirlik | Yüksek | Orta | Düşük |
| Kullanım amacı | Bireysel iletişim | Grup yayını | Ağ keşfi, duyuru |
| Örnek IP | `192.168.1.5` | `224.0.0.1` | `192.168.1.255` |
