# Acil Servis Hasta Yoğunluğu Tahmini

Sentetik veri ve çoklu makine öğrenmesi algoritmaları kullanarak acil servis hasta yoğunluğunu 4 saat önceden tahmin eden kapsamlı bir makine öğrenmesi projesi.

## Proje Yapısı

```
er-patient-prediction/
├── er_patient_prediction.ipynb    # Tam analiz içeren ana Jupyter notebook
├── er_prediction_script.py        # Python script versiyonu (bağımsız)
├── setup_and_run.sh              # Otomatik kurulum scripti
├── requirements.txt               # Proje bağımlılıkları
└── README.md                     # Bu dosya
```

## Hedef Metrikler

- **MAE (Ortalama Mutlak Hata)**: < 3 hasta
- **MAPE (Ortalama Mutlak Yüzde Hatası)**: < %20
- **R² (Belirleme Katsayısı)**: > 0.70

## Özellikler

Model, hasta yoğunluğunu tahmin etmek için çeşitli özellikler kullanır:

### Zaman Tabanlı Özellikler
- Günün saati (döngüsel kodlama)
- Haftanın günü (döngüsel kodlama)
- Ay (döngüsel kodlama)
- Tatil göstergeleri
- Hafta sonu göstergeleri
- Mesai saatleri, gece vakti, yoğun saatler

### Geçmiş Veriler
- Gecikme özellikleri (1s, 2s, 4s, 6s, 12s, 24s, 48s, 168s)
- Farklı pencereler üzerinden hareketli istatistikler (ortalama, std sapma, max, min)

### Hava Durumu Özellikleri
- Sıcaklık
- Yağış göstergeleri
- Yağış miktarı
- Hava durumu etkileşim özellikleri

## Uygulanan Modeller

1. **Doğrusal Regresyon**: Özellik ölçeklendirmeli temel model
2. **Random Forest**: Ağaç tabanlı topluluk yöntemi
3. **XGBoost**: Gradyan artırma algoritması

## Hızlı Başlangıç

### Seçenek 1: Otomatik Kurulum (Önerilen)
Tüm bağımlılıkları kuracak ve kurulumu doğrulayacak kurulum scriptini çalıştırın:
```bash
./setup_and_run.sh
```

### Seçenek 2: Manuel Kurulum
1. Gerekli paketleri kurun:
```bash
pip3 install --user pandas numpy matplotlib seaborn scikit-learn xgboost jupyter ipykernel
```

2. Jupyter notebook'u çalıştırın:
```bash
jupyter notebook er_patient_prediction.ipynb
```

VEYA bağımsız scripti çalıştırın:
```bash
python3 er_prediction_script.py
```

## Veri Üretimi

Proje, gerçekçi kalıplarla sentetik acil servis verisi üretir:

- **Saatlik kalıplar**: Gündüz yüksek, gece düşük yoğunluk
- **Haftalık kalıplar**: Hafta sonları artan yoğunluk
- **Mevsimsel kalıplar**: Kışın grip sezonu etkileri
- **Hava durumu etkisi**: Aşırı sıcaklıklar ve yağmur hasta yoğunluğunu artırır
- **Tatil etkileri**: Tatillerde yüksek yoğunluk

## Görselleştirmeler

Proje çeşitli görselleştirmeler üretir:

1. **Saatlik Eğilimler**: Saat, haftanın günü, ay ve gün tipine göre hasta sayısı kalıpları
2. **Hava Durumu Etkisi**: Sıcaklık ve yağış etkilerinin analizi
3. **Model Tahminleri**: Tahmin edilen ve gerçek değerleri gösteren dağılım grafikleri
4. **Zaman Serileri**: Hata analiziyle 7 günlük tahmin görselleştirmesi

## Sonuçlar

Modeller çoklu metriklerle değerlendirilir ve görselleştirmeler şunları gösterir:
- Özellik önem analizi
- Zaman içinde tahmin doğruluğu
- Hata dağılım analizi
- Model performans karşılaştırması

## Kullanım Notları

- Sentetik veri gerçekçi acil servis kalıplarını taklit eder
- Zaman tabanlı eğitim/test bölümü zamansal bütünlüğü korur
- Özellik mühendisliği gecikme değişkenleri ve hareketli istatistikleri içerir
- Modeller çoklu değerlendirme metriklerinde karşılaştırılır
- Görselleştirmeler veri kalıpları ve model performansı hakkında içgörüler sağlar