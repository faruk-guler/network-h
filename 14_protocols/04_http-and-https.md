# 🔒 HTTP ve HTTPS — Web'in Dili

Telefonunuz `google.com`'un IP'sini buldu (DNS), TCP bağlantısı kuruldu (3-way handshake). Sırada asıl konuşma var: tarayıcı ile web sunucusunun anlaştığı dil — **HTTP**. Web'de gördüğünüz her sayfa, her resim, her "404" bu dille gelir.

> 💡 **Hatırlayın:** İstemci sorar, sunucu cevaplar. HTTP bu soru-cevapların **yazım kurallarıdır**: isteğin ve yanıtın nasıl görüneceği baştan bellidir.

---

## Bir İstek (Request) Gerçekten Ne Der?

`google.com` yazıp Enter'a bastığınızda tarayıcının gönderdiği ham metin şudur:

```text
GET / HTTP/1.1          ← "Başlangıç sayfasını VER (GET)"
Host: google.com        ← Hangi adrese ait olduğunu soruyorum
User-Agent: Chrome/126  ← Ben kimim
Accept-Language: tr     ← Türkçe içeriğe açığım

```

Kural basittir: **ilk satır eylem + yol + sürüm**, ardından bilgi başlıkları (header), sonra boş satır. Eylemler (method) dört tanesiyle hayatınızın tamamını anlatır:

| Method | Anlamı | Örnek |
|:---:|:---|:---|
| **GET** | "Ver, bana göster" | Sayfa açmak, resim indirmek |
| **POST** | "Al, bunu kaydet" | Form göndermek, giriş yapmak |
| **PUT / DELETE** | "Değiştir / Sil" | API işlemleri |

## Sunucu Neyle Cevap Verir?

```text
HTTP/1.1 200 OK         ← Satır 1: sürüm + SONUÇ KODU
Content-Type: text/html ← Yanıtın cinsi
Content-Length: 45210   ← Gövdede kaç byte var

<!DOCTYPE html> ...     ← Gövde (body): asıl sayfalar/veri burada
```

İlk satırdaki sayı, cevabın **özetidir** — kodları ve sınıflarını bilmek, arıza anlamayı kolaylaştırır:

| Sınıf | Anlamı | Sık gördükleriniz |
|:---:|:---|:---|
| **2xx** | Başarılı | `200 OK`, `201 Created` |
| **3xx** | Yönlendir | `301` (taşındı), `304` (değişmemiş, önbellekten oku) |
| **4xx** | **Senin hatan** — istek bozuk/erişim yok | `404 Not Found`, `403 Forbidden` |
| **5xx** | **Sunucunun hatası** | `500 Internal Server Error`, `502 Bad Gateway` |

> 💡 `404` gördüğünüzde internet değil **o yol** yoktur; `5xx` gördüğünde suç sizde değil sunucudadır. Hangi tarafı suçlayacağınızı ilk rakam söyler.

---

## HTTP Çıplaktır: HTTPS Nasıl Giydirir?

HTTP'nin sırrı aynı zamanda zaafıdır: yukarıdaki her satır **düz metindir**. Aynı Wi-Fi'daki biri paketınızı yakalasa, gönderdiğiniz şifreyi kitap gibi okur.

**HTTPS, yeni bir protokol değildir** — aynı HTTP'nin **TLS** denen bir zarfa sarılmış hâlidir:

```text
HTTP  → [ TLS ZARI: her şey şifreli gider gelir ] → TCP → IP
```

Zarın kapatılma anı (TLS handshake), üç soruyu cevaplar:

1. **"Kimsin?"** — Sunucu **sertifikasını** gösterir: bir Sertifika Otoritesi (CA) tarafından imzalanmış kimlik belgesi. Tarayıcı, işletim sisteminde güvenilen CA listesiyle bunu doğrular; sahte kimlik yakayı ele verir.
2. **"Anahtarı nasıl paylaşacağız?"** — Taraflar, dinleyen üçüncü kişilerin hesabına karşı **ortak bir oturum anahtarı** pazarlık eder (anahtarın kendisi ağda dolaşmaz; sadece üretiminin malzemesi dolaşır).
3. **"Tamam, bundan sonra mühürlü."** — El sıkışma bitince tüm HTTP istek/yanıtları bu anahtarla şifreli akar.

Port ayrımı bunun yansımasıdır: HTTP **80**, HTTPS **443/TCP**. Tarayıcıdaki 🔒 simgesi "zar kapalı" demektir.

> ⚠️ **Şehir efsanesi uyarısı:** HTTPS "güvenli site" demek **değildir** — yalnızca "yolda kimse okuyamaz" demektir. Bugün zararlı sitelerin çoğu https kullanıyor; kilit simgesi sitenin dürüstlüğüne değil, tünelin sağlamlığına kefil olur.

---

## Hızlıca Günümüz

- **HTTP/2:** Aynı bağlantıda çoklu istek (sayfa kaynakları sıraya girip beklemiyor).
- **HTTP/3 (QUIC):** HTTP'nin TCP yerine **UDP** üzerine kurulmuş yeni hâli — kayıpsız ama daha çevik. "UDP hızlıdır" kuralının web'e uygulanmış son hâli.

---

## Özet

```text
HTTP = tarayıcı ile sunucunun ortak dili: "GET /" sorar, "200 OK" cevap verir
İlk satırdaki sınıf suçu söyler: 4xx = istekte sorun, 5xx = sunucuda sorun
HTTPS = HTTP + TLS zarı: sertifika (kimlik) + oturum anahtarı (şifre) + mühürlü trafik
443/TCP, 🔒 = tünel sağlam; ama bu sitenin iyi ve güvenli olduğu anlamına gelmez
```
