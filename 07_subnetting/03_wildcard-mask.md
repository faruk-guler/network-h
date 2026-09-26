# 🎭 Wildcard Mask (Ters Maske)

Wildcard mask, subnet mask'in tam tersidir ve **"bu bitlere bakma, geç"** anlamına gelir.

> 💡 **Benzetme:** Bir kapı görevlisinin elindeki listeyi düşünün. Subnet mask "şu bitlerin tam eşleşmesi lazım" derken, wildcard mask "şu bitlere hiç bakma, kim olursa olsun geç" der.

---

## Subnet Mask → Wildcard Mask Dönüşümü

Wildcard mask, subnet mask'taki her bitin **NOT** (tersi) alınmasıyla elde edilir:

- Subnet mask'taki `1` → Wildcard mask'ta `0` (ağ bitine bak)
- Subnet mask'taki `0` → Wildcard mask'ta `1` (host bitini yoksay)

### 🔢 Kolay Hesaplama Yöntemi

Her oktet için: **255 − Subnet Mask Okteti = Wildcard Okteti**

```text
Subnet Mask  →  255.255.255.0
              ─────────────────
255 - 255  =  0
255 - 255  =  0
255 - 255  =  0
255 - 0    =  255

Wildcard Mask:  0.0.0.255
```

### Yaygın Örnekler

| CIDR | Subnet Mask | Wildcard Mask |
|:---:|:---|:---|
| /8 | 255.0.0.0 | 0.255.255.255 |
| /16 | 255.255.0.0 | 0.0.255.255 |
| /24 | 255.255.255.0 | 0.0.0.255 |
| /25 | 255.255.255.128 | 0.0.0.127 |
| /26 | 255.255.255.192 | 0.0.0.63 |
| /27 | 255.255.255.224 | 0.0.0.31 |
| /28 | 255.255.255.240 | 0.0.0.15 |
| /29 | 255.255.255.248 | 0.0.0.7 |
| /30 | 255.255.255.252 | 0.0.0.3 |
| /32 | 255.255.255.255 | 0.0.0.0 |

> 💡 IPv4 subnet tablosunda zaten "Ters Maske (Wildcard)" sütunu yer almaktadır — hızlı referans için bakabilirsiniz.

---

## Wildcard Mask Nerede Kullanılır?

Wildcard mask ağırlıklı olarak **ACL (Access Control List)** ve **OSPF** yapılandırmalarında kullanılır.

### 1. ACL (Erişim Kontrol Listesi)

Bir ağdaki IP aralığını tanımlarken hangi bitlerin "önemli" olduğunu belirtmek için kullanılır.

```text
Senaryo: Yalnızca 192.168.10.0/24 ağından gelen trafiğe izin ver

access-list 10 permit 192.168.10.0 0.0.0.255
                       ─────────── ───────────
                       Ağ adresi   Wildcard mask
                                   (son oktet → herkese izin)
```

- `0.0.0.255` → "İlk üç oktete bak, son okteti önemseme" = /24 ağındaki herkes

### 2. OSPF Ağ Bildirimi

OSPF hangi arayüzlerin sürece dahil edileceğini wildcard mask ile tanımlar:

```text
router ospf 1
 network 10.5.0.0 0.0.255.255 area 0
```

- `0.0.255.255` → "10.5.x.x ağındaki tüm arayüzleri dahil et" (/16 kapsamı)

---

## Özel Wildcard Mask Değerleri

| Wildcard | Anlamı | Kullanım |
|:---|:---|:---|
| `0.0.0.0` | Tam eşleşme (tek IP) | Bir IP'yi tam olarak belirt |
| `255.255.255.255` | Herkesi kapsıyor (any) | "Tümüne izin ver" kuralı |
| `0.0.0.255` | Son oktet serbest | /24 ağındaki tüm hostlar |
| `0.0.3.255` | 2. ve son oktet kısmen serbest | /22 ağı |

### 📌 Tek Bir IP İçin Wildcard

```text
Senaryo: Yalnızca 192.168.1.5 IP'sine izin ver

access-list 10 permit host 192.168.1.5
                         ──── eşdeğeri ────
access-list 10 permit 192.168.1.5 0.0.0.0
                                   ───────
                                   Hiçbir bite dokunma = tek IP
```

### 📌 Tüm IP'ler İçin Wildcard

```text
Senaryo: Herkese izin ver (any)

access-list 10 permit any
                     ──── eşdeğeri ────
access-list 10 permit 0.0.0.0 255.255.255.255
```

---

## Subnet Mask ile Farkı Nedir?

| | Subnet Mask | Wildcard Mask |
|:---|:---|:---|
| **Kullanım amacı** | IP adresinin hangi kısımda ağ, hangisinde host olduğunu belirtir | Eşleşmede hangi bitlerin "önemli" olduğunu belirtir |
| **"1" biti anlamı** | Bu bit ağ kısmına ait | Bu bite bakma / önemseme |
| **"0" biti anlamı** | Bu bit host kısmına ait | Bu bite bak / eşleş |
| **Kullanıldığı yer** | IP yapılandırması, routing | ACL, OSPF, BGP |

---

## Kısa Özet

```text
Wildcard Mask = 255.255.255.255 − Subnet Mask

"0" biti → "Bu bitle ilgilen, eşleşmeli"
"1" biti → "Bu biti yoksay, kim olursa olsun"

Kullanım yerleri: ACL kuralları, OSPF network komutu
```
