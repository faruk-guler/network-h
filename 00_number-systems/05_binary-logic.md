# ⚙️ Binary Mantık İşlemleri

Ağ dünyasında üç temel binary mantık işlemi kullanılır: **AND**, **OR** ve **NOT**.

---

## AND — Her İkisi de 1 ise 1

> 💡 Subnet mask ile AND işlemi yapılarak bir IP'nin hangi ağa ait olduğu bulunur.

```text
IP Adresi :  172.16.1.1   = 10101100.00010000.00000001.00000001
Subnet    :  255.255.0.0  = 11111111.11111111.00000000.00000000
                             ↓        AND        ↓
Network   :  172.16.0.0   = 10101100.00010000.00000000.00000000
```

Mask'taki `1` bitleri IP'yi **olduğu gibi bırakır**, `0` bitleri **sıfırlar**.

---

## OR — En Az Biri 1 ise 1

> 💡 Network adresi ile Wildcard mask'ın OR'u alınarak Broadcast adresi bulunur.

```text
Network   :  172.16.0.0   = 10101100.00010000.00000000.00000000
Wildcard  :  0.0.255.255  = 00000000.00000000.11111111.11111111
                             ↓        OR         ↓
Broadcast :  172.16.255.255= 10101100.00010000.11111111.11111111
```

Wildcard'daki `1` bitleri karşılık gelen bitleri **1 yapar** → Host bitlerinin tamamı 1 → Broadcast adresi.

---

## NOT — Biti Tersine Çevir (0 ↔ 1)

> 💡 Subnet mask'ın NOT'u alınarak Wildcard mask elde edilir.

```text
Subnet Mask :  255.255.255.0  = 11111111.11111111.11111111.00000000
                                 ↓        NOT        ↓
Wildcard    :  0.0.0.255      = 00000000.00000000.00000000.11111111
```

---

## Özet

| İşlem | Kural | Ağda Kullanım |
|---|---|---|
| **AND** | Her ikisi de `1` ise `1` | IP + Subnet Mask → Network adresi |
| **OR** | En az biri `1` ise `1` | Network + Wildcard → Broadcast adresi |
| **NOT** | Biti tersine çevirir (`0↔1`) | Subnet Mask → Wildcard mask |
