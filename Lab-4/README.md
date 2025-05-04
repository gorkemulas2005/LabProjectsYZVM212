# Linear Regression Model Optimization - YZM212 Bahar 2024-2025

## Genel Bakış
Bu laboratuvar çalışmasında **Linear Regression (Doğrusal Regresyon)** model optimizasyonu yapılacaktır. İki farklı yöntem kullanılacaktır: **En Küçük Kareler Tahmini (Least Squares Estimation - LSE)** ve **Scikit-learn Linear Regression**. Amaç, her iki yöntemle de model eğitmek ve performanslarını **Mean Squared Error (MSE)**, **Mean Absolute Error (MAE)** ve **R-squared (R²)** gibi metriklerle karşılaştırmaktır.

Eğitim için kullanılan veri seti, öğrenci performansını, çalışma alışkanlıklarını, ekstrakuriküler aktiviteleri ve uyku saatlerini temsil eden çeşitli özellikler içermektedir.

## Veri Açıklaması
Modelin eğitilmesi için kullanılan veri seti, öğrencilerin çalışma alışkanlıkları, performansları ve ekstrakuriküler aktiviteleri ile ilgili bilgileri içermektedir. Veri setindeki sütunlar şunlardır:

| **Sütun Adı**                 | **Açıklama**                                              |
|-------------------------------|-----------------------------------------------------------|
| `Hours Studied`                | Öğrencinin çalıştığı saat sayısı                          |
| `Previous Scores`              | Öğrencinin önceki sınav puanları                          |
| `Extracurricular Activities`   | Öğrencinin ekstrakuriküler aktivitelere katılımı (Evet/Hayır)|
| `Sleep Hours`                  | Öğrencinin gece başına ortalama uyku süresi               |
| `Sample Question Papers Practiced` | Öğrencinin çözdüğü deneme sınavı sayısı                 |
| `Performance Index`            | Öğrencinin genel performansı                              |

### Veri Seti Örnekleri

**Veri Seti 1 - Öğrenci Performansı**

| **Hours Studied** | **Previous Scores** | **Extracurricular Activities** | **Sleep Hours** | **Sample Question Papers Practiced** | **Performance Index** |
|-------------------|---------------------|--------------------------------|-----------------|---------------------------------------|-----------------------|
| 7                 | 99                  | Yes                            | 9               | 1                                     | 91.0                  |
| 4                 | 82                  | No                             | 4               | 2                                     | 65.0                  |
| 8                 | 51                  | Yes                            | 7               | 2                                     | 45.0                  |
| 5                 | 52                  | Yes                            | 5               | 2                                     | 36.0                  |
| 7                 | 75                  | No                             | 8               | 5                                     | 66.0                  |

https://www.kaggle.com/datasets/nikhil7280/student-performance-multiple-linear-regression?resource=download

**Veri Seti 2 - X ve Y Değerleri (Düz Regresyon)**

| **X** | **Y**        |
|-------|--------------|
| 1     | 3.888889     |
| 2     | 4.555556     |
| 3     | 5.222222     |
| 4     | 5.888889     |
| 5     | 6.555556     |

https://www.kaggle.com/datasets/tanuprabhu/linear-regression-dataset

## Performans Karşılaştırması: İki Veri Seti

### Veri Seti 1 - Öğrenci Performansı

| **Model**                         | **MSE (Ortalama Kare Hatası)** | **MAE (Ortalama Mutlak Hata)** | **R² (Belirleme Katsayısı)**   | **Eğitim Süresi**  |
|-----------------------------------|-------------------------------|--------------------------------|--------------------------------|--------------------|
| **Scikit-learn Linear Regression**| 4.082628398521853             | -                              | 0.9889832909573145            | 0.017103 saniye    |
| **Custom Linear Regression (NumPy)** | 8.441550059672113e-27        | -                              | 1.0                            | 0.001140 saniye    |

### Veri Seti 2 - X ve Y Değerleri (Düz Regresyon)

| **Model**                         | **MSE (Ortalama Kare Hatası)** | **MAE (Ortalama Mutlak Hata)** | **R² (Belirleme Katsayısı)**   | **Eğitim Süresi**  |
|-----------------------------------|-------------------------------|--------------------------------|--------------------------------|--------------------|
| **Scikit-learn Linear Regression**| 262.22981                     | 3.49070                        | 0.92136                        | 0.001406 saniye    |
| **Custom Linear Regression (NumPy)** | 262.22981                    | 3.49070                        | 0.92136                        | 0.000858 saniye    |

## Sonuçlar ve Yorumlar

### Veri Seti 1: Öğrenci Performansı

- **Scikit-learn Linear Regression**: Model, oldukça yüksek bir **R²** (0.988) ile mükemmel bir uyum sağlamaktadır. **MSE** değeri çok düşük olup modelin tahminleri çok iyi bir şekilde gerçek değerlerle örtüşmektedir. Eğitim süresi ise 0.017 saniye ile oldukça hızlıdır.
- **Custom Linear Regression (NumPy)**: Modelin **R²** değeri 1.0 olup, mükemmel uyum sağlamakta. Ancak, çok küçük bir **MSE** değeri (yaklaşık sıfır) gözlemlenmiştir. Bu, modelin çok yüksek doğrulukla çalıştığını ancak bazı sayıların yuvarlanmasından kaynaklanmış olabilir. Eğitim süresi ise 0.001 saniye ile oldukça hızlıdır.

### Veri Seti 2: X ve Y Değerleri (Düz Regresyon)

- **Scikit-learn Linear Regression**: Modelin **R²** değeri 0.92136 ile oldukça iyi bir uyum göstermektedir. **MSE** ve **MAE** değerleri de modelin doğruluğunu desteklemektedir. Eğitim süresi 0.001406 saniye ile hızlıdır.
- **Custom Linear Regression (NumPy)**: Bu modelin de **R²** değeri 0.92136'dır, yani Scikit-learn modeli ile aynı doğruluğa sahiptir. **MSE** ve **MAE** değerleri de birbirine eşittir, ancak NumPy versiyonunun eğitim süresi 0.000858 saniye ile biraz daha hızlıdır.

## Çıkarımlar

- **Model Performansı**: Her iki model de farklı veri setlerinde benzer sonuçlar vermektedir. Ancak, **Custom Linear Regression (NumPy)** modelinin eğitim süresi daha kısa olmasına rağmen, sonuçlar açısından **Scikit-learn** ile eşdeğerdir.
- **Eğitim Süresi**: **NumPy** tabanlı özel model, eğitim süresi açısından çok daha hızlıdır. Bu, özellikle büyük veri setlerinde önemli bir avantaj sağlayabilir.
- **Hata Değerleri**: İlk veri seti için **Scikit-learn** ve **Custom Linear Regression** arasında büyük farklar yoktur, ancak **Custom** modelde **MSE** değeri çok düşük olmuştur. Bu durum, sayısal hassasiyet farklarından kaynaklanabilir.

## Performans Ölçüm Metrikleri

- **Mean Squared Error (MSE)**: Ortalama kare hatası, modelin tahminleri ile gerçek değerler arasındaki farkların karelerinin ortalamasıdır. Küçük MSE değeri, modelin iyi bir doğrulukla çalıştığını gösterir.
- **Mean Absolute Error (MAE)**: Ortalama mutlak hata, tahminlerin gerçek değerlerden ne kadar uzaklaştığını gösteren bir metriktir. MAE'nin düşük olması, modelin tahminlerinin gerçek verilere yakın olduğunu gösterir.
- **R-squared (R²)**: Belirleme katsayısı, modelin veri setindeki varyansı ne kadar açıkladığını gösterir. 1'e yakın bir R² değeri, modelin veriye çok iyi uyduğunu belirtir.
- **Eğitim Süresi**: Modelin eğitim süresi, modelin eğitim sırasında ne kadar zaman harcadığını ölçer. Düşük eğitim süresi, modelin hızlı ve verimli olduğunu gösterir.
