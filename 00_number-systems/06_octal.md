# 8️⃣ Octal (Sekizlik) Sayı Sistemi

0'dan 7'ye kadar **8 sembol** kullanan sayı sistemidir. Her 3 binary bit, tam olarak 1 octal rakama karşılık gelir.

## Decimal → Octal

Sayıyı sürekli 8'e böl, kalanları ters sırayla yaz:

```
255 ÷ 8 = 31  kalan 7
 31 ÷ 8 =  3  kalan 7
  3 ÷ 8 =  0  kalan 3

Kalanlar (alttan yukarı): 3 → 7 → 7
✅ 255 = 377 (Octal)
```

---

## Binary → Octal

Binary sayıyı **3'erli grupla**, tablodan oku:

```
000 = 0    100 = 4
001 = 1    101 = 5
010 = 2    110 = 6
011 = 3    111 = 7
```

```
Binary:  11 000 000
Octal:    3   0   0
✅ 11000000 = 300 (Octal) = 192 (Decimal)
```

---

## 🐧 Gerçek Hayat: chmod 755

Linux'ta dosya izinleri octal ile gösterilir. `chmod 755 dosya.sh` komutunda `755` şu anlama gelir:

| Octal | Binary | İzin | Kim? |
|:---:|:---:|:---|:---|
| **7** | 111 | rwx — okuma + yazma + çalıştırma | Dosya sahibi |
| **5** | 101 | r-x — okuma + çalıştırma | Grup |
| **5** | 101 | r-x — okuma + çalıştırma | Diğerleri |
