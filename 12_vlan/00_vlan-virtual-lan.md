# 🏢 VLAN (Virtual LAN — Sanal Yerel Ağ)

Fiziksel olarak aynı switch'e bağlı cihazları **mantıksal olarak farklı ağlara ayırma** teknolojisidir.

> 💡 **Benzetme:** Büyük bir ofis katı düşünün. Fiziksel bölme duvarı olmasa da HR, IT ve Muhasebe çalışanları ayrı gruplar hâlinde çalışır. VLAN, switch'te bu sanal duvarları oluşturur — kablolar aynı switch'e gitmeye devam eder ama trafik birbirini görmez.

---

## Neden VLAN'a İhtiyaç Var?

VLAN olmadan, aynı switch'e bağlı **tüm cihazlar aynı broadcast domain**'dedir. Bu şu anlama gelir:

- Birinin gönderdiği broadcast (ARP, DHCP isteği vb.) **herkese** ulaşır.
- Muhasebe'nin trafiğini IT de görebilir — güvenlik açığı.
- Ağ büyüdükçe broadcast fırtınaları performansı düşürür.

**VLAN ile:**

- Ağ, mantıksal segmentlere ayrılır.
- Broadcast trafiği her VLAN'ın kendi içinde hapsolur.
- Farklı VLAN'lar birbirinden tamamen izole edilir.

---

## Gerçek Dünya Örneği

Bir şirketin tek katta 3 departmanı var, hepsi aynı switch'e bağlı:

```
                        [Switch]
                    /      |      \
           VLAN 10    VLAN 20    VLAN 30
           (IT)       (HR)      (Muhasebe)
          PC-1,2,3   PC-4,5,6   PC-7,8,9
```

- IT departmanı yalnızca kendi içinde haberleşebilir.
- HR, Muhasebe'nin trafiğini göremez.
- Departmanlar arası tam ağ izolasyonu sağlanır.

---

## Özet Tablo

| Kavram | Açıklama |
|:---|:---|
| **VLAN** | Aynı switch'teki cihazları mantıksal olarak ayırma |
| **Access Port** | Tek VLAN'a bağlı son kullanıcı portu |
| **Trunk Port** | Birden fazla VLAN trafiğini taşıyan port (switch'ler arası) |
| **802.1Q** | VLAN etiketleme standardı (IEEE) |
| **Native VLAN** | Trunk portta etiketsiz trafiğin ait olduğu VLAN |

> 💡 **Kısa kural:** Aynı VLAN = aynı ağ = doğrudan haberleşir. Farklı VLAN = izole ağ = doğrudan haberleşemez.
