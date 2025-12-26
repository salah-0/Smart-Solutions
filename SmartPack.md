# SmartPack – Akıllı Palet Dizilim ve Hazırlama Rehberi Sistemi

## 🧭 Genel Tanım

**SmartPack**, depo operasyonlarında insan hatasını minimize etmek amacıyla geliştirilen akıllı palet hazırlama sistemidir.  
Sipariş alındığında, ürünlerin fiziksel özelliklerini (boyut, ağırlık, kırılganlık vb.) analiz eder; ardından algoritmik olarak en uygun dizilimi hesaplar.  
Sonuçta her sipariş için özel bir **Hazırlama Rehberi Listesi** oluşturur — personel bu listeyi takip ederek paleti doğru sırayla ve dengeli biçimde hazırlar.

Amaç:
> İnsan hatasını azaltmak, süreçleri standardize etmek ve palet hazırlama hızını artırmak.

---

## ⚙️ Sistem Mimarisi

### 🔹 Kullanıcı Rolleri
| Rol | Yetki Düzeyi | Açıklama |
|------|---------------|-----------|
| **Superuser** | Tam erişim | Sistem ayarları ve kullanıcı yönetimi |
| **Yönetici (Admin)** | Sipariş onayı & rehber üretimi yetkisi | Siparişi analiz eder, algoritmayı çalıştırır |
| **Eleman (Staff)** | Görüntüleme yetkisi | Hazırlama rehberini takip eder |

---

### 🔹 Süreç Akışı

```text
Sipariş Alındı →
Ürün Verileri Çekildi →
Algoritma Dizilim Planını Hesapladı →
Hazırlama Rehberi Listesi Oluşturuldu →
Personel Listenin çıktısı Takip Etti →
Palet Hazırlandı 🎯
