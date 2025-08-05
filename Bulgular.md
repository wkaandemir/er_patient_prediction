# Acil Servis Hasta Hacmi Tahmini - Proje Bulguları

## 📊 Veri Seti Özeti

- **Toplam Kayıt Sayısı**: 17,517 saatlik veri
- **Zaman Aralığı**: 1 Ocak 2022 - 1 Ocak 2024 (2 yıl)
- **Oluşturulan Özellik Sayısı**: 46
- **Eğitim Seti**: 14,013 örnek
- **Test Seti**: 3,504 örnek

## 🎯 Hedef Metrikler ve Başarı Durumu

| Metrik | Hedef Değer | Elde Edilen (Linear Regression) | Durum |
|--------|-------------|----------------------------------|-------|
| MAE    | < 3.0       | 2.97                            | ✅ Başarılı |
| MAPE   | < 20%       | 35.8%                           | ❌ Başarısız |
| R²     | > 0.70      | 0.589                           | ❌ Başarısız |

**Genel Başarı Durumu**: KISMI - Bazı hedefler için daha fazla model iyileştirmesi gerekiyor.

## 🏆 Model Performans Karşılaştırması

### Test Seti Performansları (MAE'ye göre sıralı):

1. **Linear Regression**
   - MAE: 2.97
   - RMSE: 3.82
   - R²: 0.589
   - MAPE: 35.8%

2. **Random Forest**
   - MAE: 2.98
   - RMSE: 3.87
   - R²: 0.577
   - MAPE: 35.5%

3. **XGBoost**
   - MAE: 3.10
   - RMSE: 3.99
   - R²: 0.551
   - MAPE: 36.7%

## 📈 Önemli Bulgular

### 1. Temporal (Zamansal) Desenler
- **Saatlik Desenler**: Hasta yoğunluğu gün içinde belirgin bir desen gösteriyor
  - En yoğun saatler: Gündüz saatleri (özellikle 10:00-20:00 arası)
  - En az yoğun saatler: Gece saatleri (22:00-06:00 arası)
- **Haftalık Desenler**: Hafta sonu günlerinde ortalama %30 daha fazla hasta gelişi
- **Mevsimsel Desenler**: Kış aylarında (grip sezonu) belirgin artış

### 2. Hava Durumu Etkisi
- **Sıcaklık**: Aşırı sıcak veya soğuk havalarda hasta sayısında artış
  - Optimal sıcaklık: 22°C civarı
  - Sıcaklıkla hasta sayısı arasında U-şekilli ilişki
- **Yağış**: Yağışlı günlerde ortalama %20 daha fazla hasta
  - Muhtemel sebep: Kaza ve yaralanmalarda artış

### 3. Özel Günler Etkisi
- **Tatil Günleri**: Tatillerde %50'ye varan artış
- **Hafta Sonları**: Hafta sonlarında %30 artış

### 4. En Önemli Özellikler (Random Forest Model)
1. patient_count_lag_4h (4 saat önceki hasta sayısı)
2. patient_count_rolling_mean_24h (24 saatlik ortalama)
3. patient_count_lag_1h (1 saat önceki hasta sayısı)
4. patient_count_lag_2h (2 saat önceki hasta sayısı)
5. patient_count_rolling_mean_6h (6 saatlik ortalama)

### 5. Model Performans Analizi
- **En İyi Model**: Linear Regression (En düşük MAE)
- **Tahmin Doğruluğu**: Ortalama %64.2 doğruluk oranı
- **Hata Dağılımı**: 
  - Tahminlerin %50'si ±2 hasta içinde
  - Tahminlerin %70'i ±3 hasta içinde
  - Ortalama hata: 2.97 hasta

## 🔍 Zayıf Noktalar ve Geliştirme Alanları

1. **MAPE Değeri Yüksek**: %35.8 ile hedefin (%20) oldukça üzerinde
   - Özellikle düşük hasta sayılarında yüzdesel hata yüksek
   
2. **R² Değeri Düşük**: 0.589 ile hedefin (0.70) altında
   - Modelin varyansın sadece %58.9'unu açıklayabilmesi

3. **Overfitting Problemi**: Random Forest'ta train/test performansı arasında büyük fark
   - Train R²: 0.944
   - Test R²: 0.577

## 💡 Öneriler

### Kısa Vadeli İyileştirmeler:
1. **Feature Engineering**:
   - Daha fazla lag özelliği (12h, 36h)
   - Haftanın günü ve saat etkileşimi
   - Özel günler takvimi genişletme

2. **Model Optimizasyonu**:
   - Hyperparameter tuning
   - Ensemble yöntemler (model birleştirme)
   - Regularization teknikleri

### Uzun Vadeli İyileştirmeler:
1. **Veri Kalitesi**:
   - Gerçek hastane verileri kullanımı
   - Daha detaylı hava durumu verileri
   - Yerel etkinlik takvimi entegrasyonu

2. **Model Mimarisi**:
   - LSTM/GRU gibi zaman serisi özel modeller
   - Prophet gibi mevsimsel decomposition modeller
   - Hybrid yaklaşımlar

3. **Üretim Ortamı**:
   - Gerçek zamanlı veri pipeline
   - Model performance monitoring
   - Otomatik re-training sistemi
   - Güven aralıkları ile tahmin

## 📊 Sonuç

Proje, acil servis hasta yoğunluğunu 4 saat önceden tahmin etmede kısmi başarı sağlamıştır. MAE hedefi yakalanmış olsa da, MAPE ve R² değerleri hedeflerin altında kalmıştır. Model, ortalama olarak ±3 hasta hassasiyetinde tahmin yapabilmektedir ki bu operasyonel planlama için kullanılabilir bir seviyedir. Ancak, daha güvenilir tahminler için yukarıda belirtilen iyileştirmelerin yapılması önerilmektedir.