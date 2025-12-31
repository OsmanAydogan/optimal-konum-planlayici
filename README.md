# Optimal Konum Planlayıcı

[![Demo](https://img.shields.io/badge/Demo-Live-brightgreen)](https://optimal-konum-demo.onrender.com/)
[![Medium](https://img.shields.io/badge/Medium-Article-black)](https://medium.com/@aydoganosman17/optimal-konum-planlay%C4%B1c%C4%B1-1a513b99f61a)
[![License](https://img.shields.io/badge/License-Demo_Only-red.svg)](#)

![Algorithm Comparison](algorithm_comparison.png)

> **Not:** Bu repository sadece dokümantasyon içermektedir. Kaynak kodlar paylaşılmamıştır. Uygulama canlı demo olarak kullanılabilir: [https://optimal-konum-demo.onrender.com/](https://optimal-konum-demo.onrender.com/)

## Proje Hakkında

Optimal Konum Planlayıcı, p-Median optimizasyon problemini çözen bir web uygulamasıdır. Matematiksel programlama teknikleri kullanarak, tesis konumlarının optimal seçimini yapar ve toplam mesafeyi minimize eder.

### Önceki Versiyon ile Karşılaştırma

Bu proje, [önceki açık kaynak versiyonun](https://github.com/OsmanAydogan/istanbul_kahve_dukkanlari) geliştirilmiş halidir:

| Özellik | Önceki Versiyon | Bu Proje |
|---------|-----------------|----------|
| Kaynak Kodu | Açık kaynak | Kapalı kaynak (demo-only) |
| UI/UX | Basit arayüz | Modern, dark theme, responsive |
| Harita | Google Maps Embed | Leaflet.js (interaktif) |
| Konum Arama | Manuel girdi | Google Places Autocomplete |
| Mesafe Hesaplama | Kuş uçuşu (Haversine) | Gerçek yol mesafesi (Distance Matrix API) |
| Mobilite | Desktop only | Mobil uyumlu, responsive |
| Demo Senaryoları | Yok | Önceden hesaplanmış senaryolar |
| Sektör Desteği | Genel amaçlı | 6 farklı sektör terminolojisi |
| Deployment | Local | Cloud (Render.com) |

**Temel İyileştirmeler:**
- Gerçek yol mesafelerinin kullanımı (Google Maps Distance Matrix API)
- Modern kullanıcı arayüzü ve responsive tasarım
- Cloud deployment ve API quota yönetimi
- LRU cache ile performans optimizasyonu

## Özellikler

- **Matematiksel Garanti:** MILP (Mixed-Integer Linear Programming) ile optimal sonuç
- **Gerçek Mesafeler:** Google Maps API ile gerçek yol mesafeleri
- **İnteraktif Harita:** Leaflet.js tabanlı görsel arayüz
- **Demo Senaryoları:** API key gerektirmeyen hazır senaryolar
- **Çoklu Sektör Desteği:** Perakende, sağlık, lojistik, kamu, enerji

## Canlı Demo

**Demo URL:** [https://optimal-konum-demo.onrender.com/](https://optimal-konum-demo.onrender.com/)

Demo senaryoları API key gerektirmez ve önceden hesaplanmış sonuçları anında gösterir.

## Video Tanıtım

![Optimal Konum Planlayıcı](Optimal%20Konum%20Planlayıcı.mp4)

## Teknik Altyapı

### Teknolojiler

**Backend:**
- Python 3.8+
- Flask (Web Framework)
- PuLP (MILP Optimizasyon)
- Google Maps API (Distance Matrix, Places, Geocoding)

**Frontend:**
- HTML5, CSS3, JavaScript (ES6+)
- Leaflet.js (İnteraktif Haritalar)
- OpenStreetMap

**Deployment:**
- Render.com (Cloud Platform)
- Gunicorn (WSGI Server)

### Algoritma: p-Median Problemi

Uygulama, klasik p-Median Problemini çözer:

- **Girdi:** N adet aday konum, M adet talep noktası, P sayıda açılacak tesis
- **Amaç:** Toplam mesafeyi minimize eden P konumu seçmek
- **Çözücü:** CBC (COIN-OR Branch and Cut)
- **Yöntem:** Mixed-Integer Linear Programming (MILP)

**Matematiksel Model:**

```
Minimize: Σ Σ d_ij * y_ij

Kısıtlar:
- Σ y_ij = 1  (her talep bir tesise atanır)
- y_ij ≤ x_i  (atama sadece açık tesislere)
- Σ x_i = p   (p tesis açılır)
```

Burada:
- d_ij: i konumundan j talep noktasına gerçek yol mesafesi
- x_i: i konumunda tesis açılırsa 1, değilse 0
- y_ij: j talep noktası i tesisine atanırsa 1, değilse 0

## Performans

### MILP vs Brute Force

| Aday Sayısı | Seçim | Kombinasyon | Brute Force | MILP |
|-------------|-------|-------------|-------------|------|
| 10 | 3 | 120 | ~1 saniye | ~0.1 sn |
| 15 | 5 | 3,003 | ~10 saniye | ~0.2 sn |
| 20 | 5 | 15,504 | ~2 dakika | ~0.5 sn |
| 25 | 10 | 3,268,760 | ~2 saat | ~2 sn |
| 30 | 10 | 30,045,015 | ~1 gün | ~5 sn |

MILP, brute force yönteminden yaklaşık 1000 kat daha hızlıdır.

## Kullanım Alanları

- **Perakende:** Mağaza ve şube konumlarının optimizasyonu
- **Sağlık:** Hastane ve ambulans istasyonlarının stratejik yerleşimi
- **Lojistik:** Depo ve dağıtım merkezlerinin optimal konumlandırması
- **Kamu Hizmetleri:** Belediye hizmet noktalarının planlanması
- **Enerji:** Şarj istasyonlarının yerleşim optimizasyonu

## Akademik Referanslar

- **Hakimi, S. L. (1964).** Optimum Locations of Switching Centers and the Absolute Centers and Medians of a Graph
- **ReVelle, C. S., & Swain, R. W. (1970).** Central facilities location
- **Daskin, M. S. (1995).** Network and Discrete Location: Models, Algorithms, and Applications
- **Church, R. L., & Murray, A. T. (2009).** Business Site Selection, Location Analysis and GIS

## Dokümantasyon

- **[README.md](README.md)** - Proje genel tanıtımı (bu dosya)
- **[USER_GUIDE.md](USER_GUIDE.md)** - Kullanım kılavuzu

## Detaylı Teknik Açıklama

Projenin detaylı teknik açıklaması için Medium makalesini inceleyebilirsiniz:

[Medium Makalesi - Optimal Konum Planlayıcı](https://medium.com/@aydoganosman17/optimal-konum-planlay%C4%B1c%C4%B1-1a513b99f61a)

## Lisans

Copyright (c) 2024 Osman Aydoğan

Tüm hakları saklıdır. Bu proje kapalı kaynak kodludur. Kaynak kodlar paylaşılmamaktadır.

Uygulama sadece canlı demo olarak kullanıma açıktır:
- Demo URL: https://optimal-konum-demo.onrender.com/
- Ticari kullanım için iletişime geçiniz

## İletişim

- Medium: [@aydoganosman17](https://medium.com/@aydoganosman17)
- GitHub: [OsmanAydogan](https://github.com/OsmanAydogan)
