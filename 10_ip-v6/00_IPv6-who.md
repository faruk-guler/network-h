# 📶 Geleceğin İnternet Adresi: IPv6

## Neden IPv6'ya İhtiyaç Var?

IPv4 adresleri 32 bitten oluşur ve toplamda yaklaşık **4.3 milyar** farklı adres üretilebilir. Kulağa çok gibi gelse de günümüzde milyarlarca telefon, bilgisayar ve akıllı cihaz internete bağlanmaktadır. Bu nedenle IPv4 adresleri **2011 yılında fiilen tükendi.**

IPv6 bu sorunu çözmek için geliştirildi. 128 bit uzunluğundaki yapısıyla pratik olarak **sınırsız sayıda** adres üretilebilir.

> 💡 **Gerçek:** IPv6 ile dünyadaki her kum tanesine bir IP adresi versek bile adresler bitmez!

---

## IPv6 Adresi Nasıl Görünür?

IPv4'te adresler **nokta** ile ayrılmış 4 sayı grubundan oluşur:

```
192.168.1.1
```

IPv6'da ise adresler **iki nokta üst üste** ile ayrılmış 8 gruptan oluşur ve her grup **onaltılık (hexadecimal)** sayılarla yazılır:

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

| Özellik | IPv4 | IPv6 |
|---------|------|------|
| Bit uzunluğu | 32 bit | 128 bit |
| Format | Onluk (0-9) | Onaltılık (0-9, A-F) |
| Ayırıcı | Nokta (.) | İki nokta (:) |
| Örnek | 192.168.1.1 | 2001:db8::1 |

---

## IPv6 Adresi Nasıl Kısaltılır?

IPv6 adresleri çok uzun göründüğünden iki kısaltma kuralı kullanılır.

### Kural 1: Başındaki Sıfırları Sil

Her gruptaki **baştaki sıfırlar** silinebilir.

```
Uzun hali:  2001:0db8:0000:0042:0000:8a2e:0370:7334
Kısa hali:  2001:db8:0:42:0:8a2e:370:7334
```

### Kural 2: Ardışık Sıfır Gruplarını "::" ile Göster

Yan yana sıfır grupları **"::"** ile kısaltılabilir. Ancak bu kısaltma **yalnızca bir kez** kullanılabilir.

```
Uzun hali:  2001:0db8:0000:0000:0000:0000:0000:0001
Kısa hali:  2001:db8::1
```

⚠️ **Dikkat:** "::" iki kez kullanılırsa adresin hangi kısmının kaç sıfırdan oluştuğu bilinemez, bu yüzden hatalıdır.

```
❌ Yanlış: 2001::db8::1
✅ Doğru:  2001:db8::1
```

---

## IPv6 Adres Türleri

IPv6'da üç temel adres türü vardır:

### 1. Unicast (Tekil) — Tek Bir Cihaza

Bir cihaza özgü adrestir. En yaygın kullanılan türdür.

- **Global Unicast:** İnternette kullanılan genel adresler. IPv4'teki public IP'ye karşılık gelir. `2001:...` ile başlar.
- **Link-Local:** Yalnızca aynı ağ segmentinde geçerlidir, dışarı çıkamaz. Her cihazda otomatik oluşur. `fe80::` ile başlar.
- **Unique Local:** Özel ağlarda kullanılır. IPv4'teki `192.168.x.x` adreslerine karşılık gelir. `fd00::` ile başlar.

### 2. Multicast (Çoğul) — Bir Gruba

Bir paketi aynı anda birden fazla cihaza gönderir. IPv4'teki broadcast'in yerini almıştır.

> ⚠️ **Not:** IPv6'da broadcast **yoktur**, bunun yerine multicast kullanılır.

### 3. Anycast (Herhangi Birine) — En Yakın Cihaza

Aynı adres birden fazla cihaza atanır. Paket bu cihazların **en yakınına** iletilir. Genellikle DNS sunucularında kullanılır.

---

## IPv4'ten IPv6'ya Geçiş

İnternet bir anda IPv6'ya geçemez. Bu nedenle geçiş döneminde her iki protokol bir arada kullanılır.

**Dual-Stack (Çift Yığın):** Bir cihazda hem IPv4 hem de IPv6 adresi aynı anda bulunur. Hedefe göre uygun protokol otomatik seçilir. Günümüzdeki modern cihazların büyük çoğunluğu bu yöntemi kullanır.

```
Bir cihazın iki adresi olabilir:
IPv4: 192.168.1.10
IPv6: 2001:db8:acad:1::10
```

---

## Özet

| Konu | Özet |
|------|------|
| Neden çıktı? | IPv4 adresleri tükendi |
| Kaç bit? | 128 bit |
| Format | Onaltılık, iki nokta ile ayrılır |
| Kısaltma | Baştaki sıfırlar silinir, ardışık sıfırlar "::" olur |
| Broadcast | Yoktur, multicast kullanılır |
| Geçiş | Dual-Stack ile IPv4 ve IPv6 birlikte çalışır |
