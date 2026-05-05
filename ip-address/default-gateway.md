# Default Gateway (Varsayılan Ağ Geçidi)

**Default Gateway**, bir cihazın kendi yerel ağı (subnet) dışına çıkmak istediğinde trafiği gönderdiği ilk router (yönlendirici) adresidir. 

Basit bir ifadeyle: **Cihazın "dış dünya kapısı"** veya **"varsayılan çıkış noktası"** dır.

---

## Temel Mantık

Bir cihaz veri gönderirken şu kararı verir:
- 🎯 **Hedef aynı ağdaysa** → Doğrudan gönderir (gateway kullanmaz)
- 🌍 **Hedef farklı ağdaysa** → Default Gateway'e gönderir

> **Örnek:** Evinizdeki bir bilgisayar Google'a (8.8.8.8) bağlanmak istiyorsa, önce bu paketi modeminize (default gateway) gönderir. Modem de sıradaki adıma iletir. Sıradaki adımda standart ev kullanıcıları için ISP Router olur.

---

## Görsel Örnek

Aşağıdaki şemada **default gateway** kavramını iki farklı seviyede görebilirsiniz:

                  INTERNET
                     │
                     │
          ┌──────────▼─────┐
          │   ISP Router   │ ← Default Gateway (Modem için)
          │                │
          └───────┬────────┘
                  │
                  │
    ┌─────────────|─────────────┐
    │          EV |             │
    │             |             │
    │    ┌────────|─────┐       │
    │    │ ADSL/Kablo   │       │
    │    │    MODEM     │ ← Default Gateway (Bilgisayar için)
    │    └──────────────┘       │
    │         │  │ │            │
    │  ┌──────┘  │ └──┐         │
    │  │         │    │         │
    │ Laptop    PC   Telefon    │
    │                           │
    └───────────────────────────┘
