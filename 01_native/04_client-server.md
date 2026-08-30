# 🤝 İstemci — Sunucu Modeli (Client-Server)

Ağ üzerindeki her iletişim bir soru-cevap ilişkisidir. Bu ilişkide her zaman iki taraf vardır: **isteyen** ve **veren**.

> 💡 **Benzetme:** Bir restorana gittiğinizde siz müşteri (client), garson ise sunucu (server) rolündedir. Siz menü istersiniz (request), garson getirir (response). Siz tekrar istersiniz, garson tekrar getirir. Garson kendi isteğiyle masanıza yemek getirmez.

Bu yapıya **İstemci-Sunucu Modeli** denir ve ağ dünyasındaki hemen her iletişim bu mantıkla çalışır.

---

## İstemci (Client) Nedir?

İstek başlatan taraftır. Genellikle son kullanıcının cihazıdır.

- Tarayıcınız `google.com` açmak istediğinde **istemcidir**
- Telefonunuz DHCP'den IP adresi istediğinde **istemcidir**
- DNS sorgusu gönderen bilgisayar **istemcidir**

## Sunucu (Server) Nedir?

Gelen isteği karşılayan, yanıtlayan taraftır. Her zaman bekler, asla kendiliğinden konuşmaya başlamaz.

- `google.com`'un içeriğini barındıran makine **sunucudur**
- IP adresi dağıtan DHCP sunucusu **sunucudur**
- Alan adlarını çözen DNS sunucusu **sunucudur**

---

## Request — Response Döngüsü

```
İstemci                            Sunucu
   │                                  │
   │  ──── Request (İstek) ────►      │
   │       "google.com'u ver"         │
   │                                  │
   │  ◄─── Response (Yanıt) ────      │
   │       HTML, CSS, resimler        │
   │                                  │
```

Her iletişim bu döngüden oluşur:
1. İstemci bir **Request** gönderir
2. Sunucu isteği işler
3. Sunucu bir **Response** döndürür
4. Bağlantı tamamlanır

---

## Aynı Cihaz Hem Client Hem Server Olabilir

Roller sabite bağlı değildir; bağlama göre değişir.

```
Bilgisayarınız bir web sitesi açıyor  →  Client
Bilgisayarınızda yerel sunucu çalışıyor  →  Server
Bilgisayarınız DNS sorgusu yapıyor  →  Client
DNS sunucusu başka bir sunucuya soruyor  →  Hem Client hem Server
```

---

## Neden Bu Kadar Önemli?

Kitap boyunca göreceğiniz her protokol bu modelin üstüne kuruludur:

| Protokol | Client | Server |
|:---|:---|:---|
| **HTTP/HTTPS** | Tarayıcı | Web sunucusu |
| **DNS** | Bilgisayar | DNS sunucusu |
| **DHCP** | Ağa yeni bağlanan cihaz | DHCP sunucusu |
| **SSH** | Terminal uygulaması | Uzak makine |

> ⚠️ **Not:** Bu model tek yönlüdür — istek her zaman client'tan gelir. Sunucu, client sormadan veri göndermez. (Bu kuralın modern istisnaları vardır: WebSocket, push bildirimleri gibi — ama temel model böyle çalışır.)

---

## Özet

```
Client  →  İsteyen taraf, konuşmayı başlatır
Server  →  Yanıtlayan taraf, bekler ve hizmet eder
Request →  Client'ın gönderdiği istek
Response→  Server'ın verdiği yanıt
```
