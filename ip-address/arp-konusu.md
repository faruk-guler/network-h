# ARP – Adres Çözümleme Protokolü
RFC 826 ile tanımlanan, IP adresinden MAC adresini bulan protokoldür.

> **"IP adresini biliyorum, ama kapıyı çalmak için isim lazım."**

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
Linux:
arp -a

Windows:
arp -a

```

---
