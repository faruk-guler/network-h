# 🔀 VLAN'lar Arası Routing

Farklı VLAN'lardaki cihazlar **birbirini göremez** — çünkü farklı ağlardalar. Birbirleriyle konuşmaları için paketlerin **Layer 3 (IP) seviyesinde yönlendirilmesi** gerekir.

> 💡 **Kural:** Aynı VLAN = aynı ağ = switch yeterli. Farklı VLAN = farklı ağ = mutlaka router veya Layer 3 switch gerekir.

---

## Neden Router Gerekir?

Switch, VLAN'ları birbirinden izole eder. Bu izolasyon güvenlik açısından iyidir; ama bazen farklı departmanların birbirleriyle konuşması da gerekir. Örneğin HR departmanının yazıcısına IT ekibinin de erişmesi gerekebilir.

Bu durumda paket, bir VLAN'dan çıkıp Layer 3'e (router'a) çıkmalı, oradan hedef VLAN'a inmelidir:

```
IT (VLAN 10)  →  Router  →  HR (VLAN 20)
```

Router, her VLAN'ı ayrı bir ağ olarak görür ve aralarında yönlendirme yapar.

---

## Yöntem 1: Router Üzerinden (Router-on-a-Stick)

Switch, router'a tek bir kablo üzerinden **trunk** olarak bağlanır. Router bu bağlantı üzerinde her VLAN için ayrı bir sanal arayüz çalıştırır ve her VLAN'ın **gateway**'i olur.

```
                    [Router]
                    (Her VLAN için ayrı gateway)
                        │  (Trunk bağlantı)
                    [Switch]
                   /    |    \
             VLAN 10  VLAN 20  VLAN 30
              (IT)     (HR)   (Muhasebe)
```

**Nasıl çalışır?**

1. IT'deki bir bilgisayar, Muhasebe'deki bir bilgisayara paket göndermek ister.
2. Farklı ağda olduğu için paketi kendi gateway'ine (router'a) gönderir.
3. Router paketi alır, hedef IP'ye bakar, Muhasebe VLAN'ına yönlendirir.
4. Switch paketi alır ve Muhasebe'deki hedef cihaza iletir.

**Ne zaman kullanılır?** Küçük ağlarda, az sayıda VLAN varsa.

---

## Yöntem 2: Layer 3 Switch (Daha Yaygın)

Modern kurumsal switch'ler **hem switch hem router** gibi çalışabilir. Harici bir router'a gerek kalmadan, VLAN'lar arası yönlendirmeyi kendi içinde yapar.

```
                [Layer 3 Switch]
            (Switch + Router bir arada)
               /       |        \
         VLAN 10     VLAN 20   VLAN 30
          (IT)        (HR)    (Muhasebe)
```

Her VLAN için switch üzerinde bir sanal gateway tanımlanır. Paket aynı cihaz içinde VLAN'lar arasında geçiş yapar — dış kablo ve router gerekmez.

**Ne zaman kullanılır?** Orta ve büyük kurumsal ağlarda, çok sayıda VLAN varsa.

---

## Karşılaştırma

| | Router-on-a-Stick | Layer 3 Switch |
|:---|:---|:---|
| **Ek donanım** | Router gerekli | Tek cihaz yeterli |
| **Performans** | Orta | Yüksek |
| **Maliyet** | Düşük | Daha yüksek |
| **Kullanım** | Küçük ağ, lab ortamı | Kurumsal, kampüs ağı |

> 💡 **Özet:** Farklı VLAN = farklı ağ. Aralarında konuşmak için mutlaka bir Layer 3 cihaz (router veya Layer 3 switch) gerekir.
