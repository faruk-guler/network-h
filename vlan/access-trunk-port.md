# 🔌 Access Port ve Trunk Port

VLAN trafiğini taşımak için switch portları iki farklı modda çalışır.

---

## Access Port (Erişim Portu)

Yalnızca **tek bir VLAN'a** ait trafiği taşır. Son kullanıcı cihazları (bilgisayar, telefon, yazıcı, IP kamera) buraya bağlanır.

```
[PC]      ──── Access Port (VLAN 10) ────┐
[Telefon] ──── Access Port (VLAN 20) ────┤ [Switch]
[Yazıcı]  ──── Access Port (VLAN 10) ────┘
```

- Port yalnızca **bir** VLAN'a atanır.
- Cihaz VLAN etiketinden haberdar değildir; paketi sıradan bir Ethernet frame'i olarak alır.
- Switch, frame'i alırken etiketi ekler; gönderirken söker — cihaz hiç fark etmez.

---

## Trunk Port

Birden fazla VLAN'a ait trafiği **aynı anda ve etiketli** olarak taşır. Switch'ler arası veya switch-router arası bağlantılarda kullanılır.

```
[Switch A] ──── Trunk Port ──── [Switch B]
                 (VLAN 10 + VLAN 20 + VLAN 30)
```

- Her frame, hangi VLAN'a ait olduğunu belirten **802.1Q etiketi** taşır.
- Bu etiket 4 byte'tır ve frame'in başına eklenir.
- Bir trunk port varsayılan olarak **tüm VLAN'ları** taşır; istenirse belirli VLAN'larla sınırlandırılabilir.

---

## 802.1Q Etiketleme (VLAN Tagging)

Trunk port üzerindeki frame'ler, VLAN ID'yi taşımak için etiketlenir:

```
Normal Ethernet Frame:
┌──────────┬──────────┬─────┬──────┬─────┐
│ Hedef MAC│ Kaynak MAC│ Tip │ Veri │ FCS │
└──────────┴──────────┴─────┴──────┴─────┘

802.1Q Etiketli Frame:
┌──────────┬──────────┬──────────────────┬─────┬──────┬─────┐
│ Hedef MAC│ Kaynak MAC│ 802.1Q TAG(4byte)│ Tip │ Veri │ FCS │
└──────────┴──────────┴────────┬─────────┴─────┴──────┴─────┘
                               │
                         VLAN ID (1–4094)
```

---

## Native VLAN

Trunk portta **etiketsiz (tag'siz)** gelen trafik, Native VLAN'a ait kabul edilir.

- Cisco switch'lerde varsayılan olarak **VLAN 1**'dir.
- Her iki taraftaki trunk portun Native VLAN'ı aynı olmalıdır; yoksa trafik yanlış VLAN'a düşer.

> ⚠️ **Güvenlik:** Native VLAN'ı VLAN 1'de bırakmak güvenlik açığı oluşturabilir (VLAN hopping saldırısı). Kullanılmayan ayrı bir VLAN numarasına (örn. VLAN 999) taşımak iyi bir uygulamadır.

---

## Karşılaştırma Tablosu

| Özellik | Access Port | Trunk Port |
|:---|:---|:---|
| **Taşıdığı VLAN** | Tek (1 adet) | Birden fazla |
| **Etiketleme** | Yok (cihaz görmez) | 802.1Q ile etiketli |
| **Kullanım Yeri** | Son kullanıcı cihazı | Switch-switch / switch-router |
| **Tipik Bağlantı** | PC, telefon, yazıcı | Uplink, inter-switch link |
