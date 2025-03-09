# naivebayesML
Bu proje, **YZM212 Makine Öğrenmesi** dersinin ilk laboratuvar ödevi olarak yapılmıştır. Ödevde **Naive Bayes** algoritması ile ikili sınıflandırma yapılmıştır. Gaussian, Bernoulli ve Multinomial naive bayes modellerinin elimizdeki veri setine uygunluğunu test etmek için karışıklık matrislerinin ve çalışma sürelerinin hesabı yapılmıştır.

# Naive Bayes ile Müzik Beğeni Tahmini

Bu proje, bir müzik veri seti kullanarak bir şarkının beğenilip beğenilmeyeceğini tahmin etmek için **Naive Bayes** algoritmalarını uygular. **Gaussian, Multinomial ve Bernoulli Naive Bayes** modelleri karşılaştırılmış, performans ölçümleri yapılmış ve karmaşıklık matrisleri görselleştirilmiştir.


## Veri Seti
Kullanılan veri seti, şarkılara ait **tempo, danceability, energy, acousticness, valence, speechiness** gibi özelliklerden oluşmaktadır. "liked" sütunu, şarkının beğenilip beğenilmediğini gösterir (1: Beğenildi, 0: Beğenilmedi).

Örnek veri:
| danceability | energy | tempo | acousticness | valence | liked |
|-------------|--------|-------|--------------|---------|-------|
| 0.803       | 0.624  | 95.968| 0.451        | 0.628   | 0     |
| 0.762       | 0.703  | 151.33| 0.206        | 0.519   | 1     |
| 0.261       | 0.0149 | 75.296| 0.992        | 0.0382  | 0     |

## Kullanılan Modeller
### 1. Gaussian Naive Bayes
- **Sürekli veriler** için kullanılır.
- Özellikle normal dağılıma uygunluk gösteren özellikler için tercih edilir.

### 2. Multinomial Naive Bayes
- **Metin verileri** gibi **kategori sayımlarına** dayalı özellikler için uygundur.
- Bu veri setinde tam uygun olmamakla birlikte karşılaştırma amacıyla eklenmiştir.

### 3. Bernoulli Naive Bayes
- **İkili (0-1) veriler** için uygundur.
- Özellikle düşük veya yüksek değerlerle sınırlı özelliklerde daha iyi çalışabilir.

## Performans Değerlendirme
Modellerin doğruluk oranı şu şekildedir:

| Model                 | Doğruluk |
|----------------------|----------|
| Gaussian Naive Bayes | 0.82     |
| Multinomial Naive Bayes | 0.73 |
| Bernoulli Naive Bayes | 0.76 |

### Kullanılan Metrikler
- **Accuracy (Doğruluk Oranı):** Modelin tüm tahminlerinin doğruluk yüzdesidir.
- **Precision (Kesinlik):** Pozitif tahminlerin doğruluk oranını gösterir.
- **Recall (Duyarlılık):** Gerçek pozitiflerin model tarafından doğru tahmin edilme oranıdır.
- **F1-score:** Precision ve Recall’in dengeli bir birleşimidir, özellikle dengesiz veri setlerinde önemlidir.

## Karmaşıklık Matrisi ve Görselleştirme
Her model için **confusion matrix (karmaşıklık matrisi)** aşağıdaki gibidir:

### Gaussian Naive Bayes
```
[[13  6]
 [ 1 19]]
```
Precision, Recall ve F1-score değerleri:
- **0 sınıfı:** 0.93 precision, 0.68 recall, 0.79 F1-score
- **1 sınıfı:** 0.76 precision, 0.95 recall, 0.84 F1-score

### Multinomial Naive Bayes
```
[[22  6]
 [10 21]]
```
Precision, Recall ve F1-score değerleri:
- **0 sınıfı:** 0.69 precision, 0.79 recall, 0.73 F1-score
- **1 sınıfı:** 0.78 precision, 0.68 recall, 0.72 F1-score

### Bernoulli Naive Bayes
```
[[20  8]
 [ 6 25]]
```
Precision, Recall ve F1-score değerleri:
- **0 sınıfı:** 0.77 precision, 0.71 recall, 0.74 F1-score
- **1 sınıfı:** 0.76 precision, 0.81 recall, 0.78 F1-score

### Karmaşıklık Matrisi Grafikleri
Kod içerisinde **Seaborn ve Matplotlib** kullanılarak karmaşıklık matrisi ısı haritası şeklinde görselleştirilmiştir.

## Sonuç ve Tartışma
### Problem ve Sınıf Dağılımı, Değerlendirme Metriklerini Nasıl Etkiler?
- Eğer sınıf dağılımı **dengesiz** olsaydı (örneğin beğenilen şarkılar %90, beğenilmeyenler %10), **accuracy (doğruluk oranı) tek başına güvenilir bir ölçüt olmazdı**. Çünkü model, hep "beğenildi" diyerek yüksek doğruluk oranı elde edebilirdi.
- **Bu nedenle, dengesiz veri setlerinde F1-score gibi metrikler daha önemli hale gelir.**
- **Gaussian Naive Bayes** sürekli verilerle iyi çalıştığı için en yüksek doğruluk oranını sağladı.
- **Multinomial Naive Bayes** kategorik olmayan veriyle çalıştığı için daha düşük doğruluk oranı verdi.
- **Bernoulli Naive Bayes**, ikili veriler için tasarlandığından bu veri setiyle orta seviyede performans gösterdi.

### Hangi Model Seçilmelidir?
- Eğer özellikler **sürekli değerler içeriyorsa (tempo, energy gibi)**, Gaussian Naive Bayes daha iyi çalışır.
- Eğer özellikler **kategori bazlı (örn. kelime sayımları gibi)** olsaydı, Multinomial daha iyi olabilirdi.
- Eğer **bütün özellikler 0 ve 1 değerlerinden oluşsaydı**, Bernoulli daha uygun olurdu.

Bu projede **Gaussian Naive Bayes** en iyi sonucu verdiği için, tercih edilmesi önerilir. 🚀

