# Yapay Zeka Destekli Yüz Tanıma ve Takip Sistemi

## Proje Özeti

Bu proje; derin öğrenme ve bilgisayar görüsü tekniklerini kullanarak gerçek zamanlı yüz tespiti, tanıma ve nesne takibi (tracking) gerçekleştiren entegre bir sistemdir. Sistem, özellikle güvenli alan giriş-çıkış senaryoları için tasarlanmış olup, kişilerin alanda kalma sürelerini otomatik olarak hesaplama ve loglama yeteneğine sahiptir.

## Proje Mimarisi

Sistem, yüksek performans ve doğruluk sağlamak amacıyla katmanlı bir mimari üzerine inşa edilmiştir:

1.  **Yüz Tespiti (Detection):** Görüntü akışındaki yüzleri belirlemek için **YOLOv8n** (Nano) modeli kullanılmaktadır.
2.  **Yüz Tanıma (Recognition):** Tespit edilen yüzlerin kimliklendirilmesi için **face\_recognition** kütüphanesi ve **Deep Learning** tabanlı algoritmalar entegre edilmiştir.
3.  **Nesne Takibi (Tracking):** Tanınan bireylerin hareketlerini izlemek ve benzersiz bir kimlik (Unique ID) atamak için **DeepSORT** algoritması kullanılmaktadır.
4.  **Hız Optimizasyonu:** Gerçek zamanlı performans için model, **ONNX** formatı üzerinden **NVIDIA TensorRT** motoruna dönüştürülmüştür.
5.  **Olay Yönetimi:** Giriş-çıkış olayları, zaman damgası ve içeride kalma süresi bilgileriyle birlikte log dosyasına kaydedilir.

## Temel Özellikler

  * **Gerçek Zamanlı İşleme:** TensorRT entegrasyonu ile düşük gecikmeli çıkarım (inference).
  * **Kesintisiz Takip:** Kişi arkasını dönse dahi DeepSORT ile sürekli takip ve ID yönetimi.
  * **Sanal Sınır Etkileşimi:** OpenCV ile tanımlanan sanal "giriş" ve "çıkış" çizgileri üzerinden olay tetikleme.
  * **Süre Analizi:** Bireylerin ilgili alanda geçirdiği sürenin otomatik hesaplanması.
  * **Hata Yönetimi:** Kayıtlı olmayan kişilerin çıkış işlemlerinde otomatik uyarı sistemi.

## Kullanılan Teknolojiler

| Kategori              | Teknolojiler                                    |
| :-------------------- | :---------------------------------------------- |
| **Dil**               | Python                                          |
| **AI Frameworks**     | PyTorch, TensorFlow/Keras, Ultralytics (YOLOv8) |
| **Bilgisayar Görüsü** | OpenCV, face\_recognition, DeepSORT             |
| **Optimizasyon**      | ONNX, NVIDIA TensorRT, CUDA, cuDNN              |
| **Veri Analizi**      | NumPy, Pickle                                   |

## Model Eğitim Bilgileri

  * **Eğitim:** 100 epoch.
  * **Performans Metrikleri:**
      * Doğruluk (Precision): %97.7
      * Duyarlılık (Recall): %96.6
      * mAP@50: %98.9

## Donanım Gereksinimleri

  * **GPU:** NVIDIA RTX 3050 veya üzeri (CUDA & TensorRT desteği için).
  * **İşlemci:** Yüksek performanslı hesaplama birimi.
