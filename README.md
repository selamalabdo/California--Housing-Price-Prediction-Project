# California--Housing-Price-Prediction-Project



## ⚙️ Veri Ön İşleme ve Özellik Mühendisliği
- **Eksik Veri:** `total_bedrooms` sütunundaki eksik değerler medyan ile dolduruldu.
- **Aykırı Değerler:** IQR yöntemi ile tespit edilip, silinmek yerine **baskılama (capping)** uygulandı.
- **Dönüşümler:** Çarpık dağılıma sahip değişkenlere (`total_rooms`, `population` vb.) **log dönüşümü** uygulandı.
- **Yeni Özellikler:** `bedrooms_per_room`, `distance_to_LA`, `avg_distance_to_cities` gibi yeni değişkenler türetildi.
- **Kodlama ve Ölçekleme:** `ocean_proximity` kategorik değişkeni One-Hot Encoding ile kodlandı, tüm sayısal veriler `StandardScaler` ile ölçeklendi.

## 🤖 Modeller ve Performans
En az 6 farklı algoritma kullanıldı ve her biri `GridSearchCV` ile hiperparametre optimizasyonundan geçirildi. Performans karşılaştırması:

| Model | R² (Test) | RMSE (USD) | MAE (USD) | MAPE (%) |
| :--- | :--- | :--- | :--- | :--- |
| **Stacking (Ensemble)** | **0.8390** | **45,934.78** | **29,743.92** | **16.60** |
| XGBoost | 0.8374 | 46,155.37 | 29,964.68 | 16.85 |
| Gradient Boosting | 0.8203 | 48,528.23 | 31,942.78 | 18.05 |
| Random Forest | 0.8192 | 48,668.32 | 31,161.48 | 17.31 |
| K-Nearest Neighbors | 0.7629 | 55,735.08 | 37,013.34 | 19.87 |
| Decision Tree | 0.7374 | 58,665.44 | 39,261.42 | 21.74 |
| Doğrusal Modeller (Ridge, Lasso, Linear) | ~0.6395 | ~68,730 | ~49,922 | ~29.63 |



## 📈 Temel Bulgular ve Sonuç
1.  **En İyi Performans:** En iyi bireysel model **XGBoost** oldu. En iyi genel performans ise, XGBoost, Gradient Boosting ve Random Forest modellerini birleştiren **Stacking Ensemble** modeli tarafından elde edildi.
2.  **Ensemble Üstünlüğü:** Ensemble yöntemleri (XGBoost, GBM, RF), geleneksel doğrusal modellere kıyasla belirgin şekilde daha yüksek R² ve daha düşük hata değerleri sağladı.
3.  **Kritik Özellikler:** `median_income`, konut fiyatını tahmin etmede açık ara en önemli özellik olarak öne çıktı. Bunu `housing_median_age` ve coğrafi konum değişkenleri izledi.
4.  **Gerçekçi Tahmin:** En iyi model (Stacking), Kaliforniya'daki bir konutun değerini ortalama **~30,000 USD (MAE)** veya **%16.6 (MAPE)** hata payı ile tahmin edebilmektedir.

