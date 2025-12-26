# SmartRoute OSRM + ORTools

## 🧭 Genel Tanım

**SmartRoute**, depo merkezli teslimat operasyonlarını **otomatik rota optimizasyonu** ile yöneten Django tabanlı bir sistemdir.  
Bu modül, **OSRM (Open Source Routing Machine)** ve **Google OR-Tools** birleşimiyle günlük siparişlerin en verimli dağıtım güzergâhını hesaplar.

Amaç:  
> Depo yönetiminin manuel rota planlama sürecini ortadan kaldırarak, araç kapasitesi, konum mesafesi ve zaman kısıtlarına göre en optimal teslimat rotalarını otomatik olarak oluşturmak.

---

## ⚙️ Sistem Mimarisi

### Kullanıcı Rolleri
| Rol | Yetki Düzeyi | Açıklama |
|------|---------------|-----------|
| **Superuser** | Tam erişim | Tüm sistem ayarları ve kullanıcı yönetimi |
| **Yönetici (Admin)** | Rota oluşturma & planlama yetkisi | Siparişleri toplar, rota hesaplar ve personele atar |
| **Eleman (Staff)** | Görüntüleme yetkisi | Kendisine atanan rotaları harita üzerinde görebilir |

### Çalışma Mantığı
1. Gün sonunda (örneğin saat 17:00) sistem yeni siparişleri toplar.  
2. Adresler geocode edilir → koordinatlar çıkarılır.  
3. OSRM servisi üzerinden nokta çiftleri arasındaki sürüş mesafesi/süresi matrisi oluşturulur.  
4. OR-Tools algoritması bu matrise dayanarak her araç için en kısa/optimal rotayı hesaplar.  
5. Oluşturulan rotalar veritabanına kaydedilir ve personel panelinde görsel olarak sunulur.

---

## 🧩 Teknoloji Yığını

| Katman | Teknoloji / Servis | Görev |
|---------|---------------------|--------|
| Backend Framework | **Django (Python son sürüm)** | Uygulama mantığı, kullanıcı yönetimi, veri akışı |
| Veritabanı | **PostgreSQL (Railway)** + `PostGIS` eklentisi önerilir | Coğrafi sorgular & veri depolama |
| Harita Servisi / Routing Motoru | **OSRM Server** (OpenStreetMap tabanlı) | Gerçek yol verisine dayalı mesafe/süre hesaplaması |
| Optimizasyon Motoru | **Google OR-Tools** (`ortools.constraint_solver`) | Rota sıralama ve araç ataması |
| Arka Plan Görevleri | **Celery + Redis** veya Django `crontab` modülü | Gün sonu otomatik rota tetikleme işlemi |
| Depolama Alanı / Medya Servisi | **AWS S3 Bucket** | Rota raporları veya çıktı dosyalarının saklanması |
| Görselleştirme Katmanı | **Leaflet.js / Folium** harita kütüphanesi | Rotanın personel arayüzünde gösterilmesi |

---

## 🏗️ Kurulum Adımları

### 1️⃣ Ortam Hazırlığı
```bash
git clone https://github.com/<username>/SmartRoute.git
cd SmartRoute
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
