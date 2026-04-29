# ARP – Adres Çözümleme Protokolü

> **"IP adresini biliyorum, ama kapıyı çalmak için isim lazım."**

---

## Ne İşe Yarar?

Ağda bir cihaza veri göndermek için hem **IP adresi** hem de **MAC adresi** gerekir.

- IP adresi → elimizde var.
- MAC adresi → **bilmiyoruz.**

ARP, bu MAC adresini sormak için kullanılır.

---

## Nasıl Çalışır?

**1. Sor** → Ağdaki herkese yayın yap:
> *"192.168.1.10 IP'sine sahip olan var mı?"*

**2. Yanıtla** → Sadece o cihaz cevap verir:
> *"Benim! MAC adresim: AA:BB:CC:DD:EE:02"*

**3. Kaydet** → Öğrenilen bilgi ARP tablosuna yazılır, bir daha sorulmaz.

---

## ARP Tablosu

Öğrenilen IP-MAC eşleşmeleri saklanır. Görüntülemek için:

```bash
arp -a
```

---

## Özet

| | |
|---|---|
| **Ne yapar?** | IP → MAC adresini öğrenir |
| **Nerede çalışır?** | Yerel ağ (LAN) |
| **IPv6'daki karşılığı** | NDP |
