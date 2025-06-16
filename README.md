# Yapay_Zeka_Destekli_Yuz_Tespiti_Giris_Cikis_Sistemi

# 🧠 Yapay Zeka Destekli Yüz Tanıma ile Giriş-Çıkış Tespit Sistemi

Bu proje, gerçek zamanlı olarak çalışan, yapay zeka tabanlı bir **yüz tanıma, takip ve giriş-çıkış tespit sistemidir**. Sistem; kamera ya da video kaynağı üzerinden insan yüzlerini tespit eder, kimlik doğrulaması yapar, kişileri takip eder ve giriş/çıkış gibi olayları kayıt altına alır. Tek kamera veya çift kamera senaryolarında çalışacak şekilde optimize edilmiştir.

---

## 🚀 Özellikler

- 🔍 **Yüz Tespiti:** YOLOv8 ile gerçek zamanlı yüz algılama
- 🧬 **Yüz Tanıma:** `face_recognition` ile kimlik eşleştirme
- 👁️‍🗨️ **Takip:** DeepSORT algoritması ile kişi bazlı takip
- 🔄 **Giriş/Çıkış Tespiti:** Sanal çizgi ile etkileşime dayalı giriş-çıkış olayları
- 📝 **Loglama:** Kişi ismi, ID, tarih, saat, içeride kalma süresi gibi bilgilerin kaydı
- 🧪 **Model Optimizasyonu:** ONNX ve TensorRT ile hızlandırma
- 🎯 **Gerçek dünya senaryosuna uygunluk:** Market, bina girişi gibi durumlarda uygulanabilir yapı

---

## 🧰 Kullanılan Teknolojiler

| Alan | Teknoloji |
|------|-----------|
| **Yüz Tespiti** | YOLOv8n (Ultralytics) |
| **Yüz Tanıma** | `face_recognition`, OpenCV |
| **Takip** | DeepSORT (Multi-Object Tracking) |
| **Programlama Dili** | Python 3.11.9 |
| **Kütüphaneler** | PyTorch, Torch-TensorRT, ONNX, Numpy, Pickle, OS |
| **Donanım** | Nvidia RTX 3050 GPU |
| **Geliştirme Ortamı** | Google Colab, VSCode, PyCharm |

---

## 🛠️ Sistem Mimarisi

1. **YOLOv8 Tabanlı Yüz Tespiti:**
   - `face-det-fwsp` veri setiyle YOLOv8n modeli eğitildi.
   - Tespit edilen yüzler kırpılarak tanıma sistemine gönderilir.

2. **Yüz Tanıma:**
   - `face_recognition` ile tespit edilen yüzler veri tabanındaki kayıtlı yüzlerle karşılaştırılır.
   - Eşleşme varsa kişi adı ile tanımlanır, yoksa otomatik olarak yeni bir kişi (örneğin `kisi4`) atanır.

3. **DeepSORT ile Takip:**
   - Tanınan kişiye benzersiz bir takip ID’si atanır.
   - ID ataması sonrası kişi, yüzü görünmese bile takip edilebilir.
   - Takip edilen kişinin en alt orta noktası (mor nokta) kullanılarak çizgi temas kontrolü yapılır.

4. **Giriş-Çıkış Tespiti:**
   - Video üzerine yerleştirilen sanal çizgiler (yeşil=giriş, kırmızı=çıkış) ile kişi çerçevesinin teması kontrol edilir.
   - Giriş yapıp çıkmayan kişilere özel uyarı sistemi vardır (120 frame boyunca görünmezse sistemden silinir).

5. **Loglama Sistemi:**
   - `loglama.txt` dosyasına kişi adı, takip ID’si, tarih/saat, içeride kalma süresi gibi bilgiler kayıt edilir.
   - Terminal üzerinden de canlı olarak kullanıcı bilgilendirmesi yapılır.
