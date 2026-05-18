# EVE-NG: Kurulum ve Kullanım Kılavuzu

EVE-NG (Emulated Virtual Environment - Next Generation), tarayıcı tabanlı arayüzüyle ağ cihazlarını sanallaştırmak için kullanılan güçlü bir simülasyon platformudur. Bu bölümde EVE-NG'yi sıfırdan kurarak ilk laboratuvarınızı oluşturacaksınız.

---

## 1. Kurulum Seçenekleri

EVE-NG üç farklı biçimde kullanılabilir:

| Yöntem | Açıklama | Önerilen Kullanım |
|---|---|---|
| **Bare-metal** | Doğrudan fiziksel sunucuya kurulum | Üretim / kalıcı lab |
| **VMware / VirtualBox OVA** | Hazır sanal makine görüntüsü | Kişisel bilgisayar |
| **AWS / GCP bulut** | Bulut üzerinde EVE-NG | Uzaktan erişim |

Bu kitap boyunca **VMware üzerinde OVA kurulumu** temel alınacaktır; en hızlı ve taşınabilir yöntemdir.

---

## 2. Sistem Gereksinimleri

| Bileşen | Minimum | Önerilen |
|---|---|---|
| İşlemci | 4 çekirdek, VT-x/AMD-V destekli | 8+ çekirdek |
| RAM | 8 GB | 16–32 GB |
| Disk | 50 GB | 200 GB+ (SSD) |
| Sanallaştırma | VMware Workstation Pro 16+ | VMware ESXi 7+ |
| İşletim Sistemi (host) | Windows 10/11 veya Linux | — |

> **Önemli:** BIOS/UEFI ayarlarından `Intel VT-x` veya `AMD-V` sanallaştırma desteğinin etkinleştirildiğinden emin olun. Aksi hâlde iç içe sanallaştırma (nested virtualization) çalışmaz.

---

## 3. OVA ile Kurulum (VMware)

### 3.1 EVE-NG İndirme

1. [https://www.eve-ng.net](https://www.eve-ng.net) adresine gidin.
2. **Download → Community** sekmesinden ücretsiz **Community Edition OVA** dosyasını indirin.
3. İndirilen dosyanın adı `EVE-NG-Community-x.x.x.ova` biçiminde olacaktır.

### 3.2 OVA'yı VMware'e Aktarma

1. VMware Workstation'ı açın.
2. **File → Open** menüsünden indirilen `.ova` dosyasını seçin.
3. Sanal makineye bir isim verin (örn. `EVE-NG-Lab`) ve hedef klasörü belirleyin.
4. **Import** düğmesine tıklayın; içe aktarma birkaç dakika sürer.

### 3.3 Sanal Makine Ayarlarını Yapılandırma

İçe aktarma tamamlandıktan sonra sanal makineyi başlatmadan önce şu ayarları düzenleyin:

**VM Settings → Hardware:**

- **Memory:** En az 8 GB atayın (labın büyüklüğüne göre artırın).
- **Processors:** Çekirdek sayısını 4 veya üzerine çıkarın.
  - `Virtualize Intel VT-x/EPT or AMD-V/RVI` seçeneğini **etkinleştirin.**
- **Network Adapter:** `NAT` veya `Bridged` olarak bırakın.

### 3.4 İlk Açılış ve Temel Yapılandırma

Sanal makineyi başlatın. Konsol ekranında aşağıdaki adımları takip edin:

```
login: root
password: eve
```

Giriş sonrasında sistem otomatik olarak yapılandırma sihirbazını başlatır:

```
hostname: eve-ng          # Makineye bir isim verin
domain:   lab.local       # Alan adı (isteğe bağlı)
```

**Ağ Yapılandırması:**

```
Management interface: eth0
IP type: dhcp             # veya static (sabit IP önerilir)
```

Sabit IP kullanmak istiyorsanız:

```
IP address:    192.168.1.100
Subnet mask:   255.255.255.0
Gateway:       192.168.1.1
DNS:           8.8.8.8
```

Yapılandırma tamamlandıktan sonra sistem yeniden başlar.

### 3.5 Web Arayüzüne Erişim

Tarayıcınızda EVE-NG'nin IP adresine gidin:

```
http://192.168.1.100
```

Varsayılan giriş bilgileri:

| Alan | Değer |
|---|---|
| Kullanıcı adı | `admin` |
| Parola | `eve` |

> İlk girişten sonra parolayı değiştirmeniz önerilir: **System → User Management → admin → Edit**

---

## 4. İstemci Tarafı Hazırlık

EVE-NG, cihaz konsollarına erişmek için bilgisayarınıza istemci paketleri (client pack) kurulmasını gerektirir.

### 4.1 Windows İstemci Paketi

1. EVE-NG web arayüzünde **sağ üst köşedeki kullanıcı simgesine** tıklayın.
2. **Download → Windows Client Pack** seçeneğini indirin.
3. Kurulum sihirbazını çalıştırın; aşağıdaki bileşenler otomatik kurulur:

| Bileşen | Amaç |
|---|---|
| SecureCRT / PuTTY | Telnet/SSH konsol erişimi |
| UltraVNC | Grafik arayüzlü cihaz erişimi |
| Wireshark | Paket yakalama entegrasyonu |
| Uyumlu tarayıcı uzantısı | Protokol bağlantılarını yönetme |

### 4.2 Linux / macOS

Linux veya macOS kullanıyorsanız **EVE-NG HTML5 konsolu** ek yazılım gerektirmez; doğrudan tarayıcıdan çalışır. Bağlantı türü olarak **HTML5** seçin.

---

## 5. Görüntü (Image) Yükleme

EVE-NG, cihaz simülasyonu için üretici yazılımlarını (IOS, NX-OS, vb.) kullanır. Bu dosyalar telif hakkı nedeniyle EVE-NG ile birlikte gelmez; kendiniz temin etmeniz gerekir.

### 5.1 Desteklenen Görüntü Türleri

| Tür | Cihazlar |
|---|---|
| **Dynamips** | Cisco IOS (7200, 3725, 3640…) |
| **IOL/IOU** | Cisco IOS on Linux (L2/L3) |
| **QEMU** | Cisco XRv, NX-OSv, Juniper vMX, Arista vEOS, Fortinet, PaloAlto… |

### 5.2 Görüntü Yükleme (SCP/SFTP)

Görüntü dosyalarını SCP veya SFTP ile EVE-NG sunucusuna aktarın:

```bash
# Örnek: Dynamips görüntüsü yükleme
scp c7200-adventerprisek9-mz.152-4.S5.bin root@192.168.1.100:/opt/unetlab/addons/dynamips/

# Örnek: QEMU görüntüsü yükleme (klasör yapısı oluşturun)
# /opt/unetlab/addons/qemu/<cihaz-adı>-<versiyon>/
mkdir -p /opt/unetlab/addons/qemu/vios-15.8/
scp vios-adventerprisek9-m.vmdk root@192.168.1.100:/opt/unetlab/addons/qemu/vios-15.8/
```

### 5.3 İzinleri Düzeltme

Her görüntü yüklemesinin ardından izinleri güncelleyin:

```bash
ssh root@192.168.1.100
/opt/unetlab/wrappers/unl_wrapper -a fixpermissions
```

> Bu komut çalıştırılmazsa EVE-NG görüntüyü göremez.

---

## 6. İlk Laboratuvarı Oluşturma

### 6.1 Yeni Lab Açma

1. Web arayüzünde sol panelden **Add new lab** butonuna tıklayın.
2. Açılan formda:

| Alan | Açıklama |
|---|---|
| **Name** | Lab adı (örn. `OSPF-Lab-01`) |
| **Version** | Versiyon numarası |
| **Author** | Yazar adı |
| **Description** | Kısa açıklama |

3. **Save** ile kaydedin; boş tuvale yönlendirilirsiniz.

### 6.2 Node (Cihaz) Ekleme

Tuval üzerinde **sağ tıklayın → Add a new node:**

1. **Node type** listesinden cihaz türünü seçin (örn. `Cisco IOL`).
2. Yüklü görüntüleriniz otomatik listelenir; uygun olanı seçin.
3. Cihaz sayısını, RAM değerini ve diğer parametreleri ayarlayın.
4. **Save** ile tuvale ekleyin.

### 6.3 Cihazları Bağlama

İki cihaz arasında bağlantı kurmak için:

1. Kaynak cihazın üzerine gelin ve **sürükle** işlemini başlatın.
2. Hedef cihaza bırakın.
3. Karşılıklı arabirimleri seçin (örn. `e0/0 ↔ e0/0`).
4. Bağlantı tuvale çizgi olarak eklenir.

### 6.4 Ağ Nesneleri (Network) Ekleme

Sanal switch, bulut bağlantısı veya internet erişimi için:

- **Sağ tıklayın → Add a new network**
- `Bridge` → fiziksel ağa erişim
- `Management (Cloud)` → internet bağlantısı

### 6.5 Labı Başlatma

- Tüm cihazları seçin: **Ctrl+A**
- **Start selected** (yeşil üçgen) düğmesine tıklayın.
- Cihaz simgeleri yeşile döndüğünde hazırdır.

---

## 7. Konsol Erişimi

Çalışan bir cihaza erişmek için simgesine **çift tıklayın** ya da sağ tıklayıp **Console** seçin.

| Protokol | Ne Zaman Kullanılır |
|---|---|
| **Telnet** | Dynamips, IOL cihazları |
| **VNC** | Grafik arayüzlü sanal makineler |
| **SSH** | Destekleyen QEMU görüntüleri |
| **HTML5** | Ek yazılım gerektirmez; her platformda çalışır |

---

## 8. Faydalı EVE-NG Komutları

Sunucuya SSH ile bağlanıp yönetim işlemleri yapabilirsiniz:

```bash
# Servis durumunu kontrol etme
systemctl status eve-ng

# Servisyi yeniden başlatma
systemctl restart eve-ng

# İzinleri düzeltme (görüntü yüklemesinden sonra)
/opt/unetlab/wrappers/unl_wrapper -a fixpermissions

# Çalışan labları listeleme
ls /opt/unetlab/tmp/0/

# Disk kullanımı
df -h

# Görüntüleri listeleme
ls /opt/unetlab/addons/dynamips/
ls /opt/unetlab/addons/qemu/
```

---

## 9. Yaygın Sorunlar ve Çözümleri

| Sorun | Olası Neden | Çözüm |
|---|---|---|
| Cihaz başlamıyor | Görüntü bulunamıyor | `fixpermissions` komutunu çalıştırın |
| Konsol açılmıyor | İstemci paketi eksik | Windows Client Pack kurun veya HTML5 kullanın |
| Web arayüzüne erişilemiyor | IP yanlış yapılandırılmış | Konsoldan `ifconfig eth0` ile IP'yi doğrulayın |
| Yavaş performans | Yetersiz RAM | VM'e daha fazla RAM atayın; daha az cihaz çalıştırın |
| VT-x hatası | Nested virtualization kapalı | VMware → VM Settings → Processors → VT-x/EPT'yi etkinleştirin |

---

## 10. Community ve Pro Sürüm Farkları

| Özellik | Community | Pro |
|---|---|---|
| Eş zamanlı node | Sınırlı | Sınırsız |
| Multi-user desteği | — | ✓ |
| RBAC (rol tabanlı erişim) | — | ✓ |
| Resmi destek | — | ✓ |
| Fiyat | Ücretsiz | Ücretli lisans |

Bireysel öğrenim ve bu kitaptaki laboratuvarlar için **Community Edition** yeterlidir.

---

> **Sonraki Adım:** EVE-NG kurulumunuz hazır. Bir sonraki bölümde ilk Cisco IOL laboratuvarını oluşturarak temel yönlendirme senaryolarını simüle edeceğiz.
