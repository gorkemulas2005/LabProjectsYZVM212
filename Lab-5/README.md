#  Customer Churn Prediction using Neural Networks

##  Proje Amacı
Bu proje, bir bankanın müşteri verileriyle müşteri kaybını (churn) tahmin etmeye yönelik bir sınıflandırma problemidir. Farklı aktivasyon fonksiyonlarıyla çalışan MLP modelleri (hem Scikit-learn tabanlı hem de custom sinir ağı mimarisi) karşılaştırılmıştır. Performans değerlendirmesi için şu metrikler kullanılmıştır:

- Accuracy
- Log Loss
- Precision
- Recall
- F1-Score
- Confusion Matrix

---

##  Veri Kümesi Özeti

- **Gözlem sayısı:** 10.000
- **Hedef değişken:** `Exited` (1: Ayrıldı, 0: Kaldı)

###  Sınıf Dağılımı:
- `Exited = 0 (Kalıcı)`: 7.963 (%79.63)
- `Exited = 1 (Ayrılan)`: 2.037 (%20.37)

> **Not:** Veri seti dengesiz olduğundan dolayı accuracy yerine recall, precision ve F1-score daha anlamlıdır.

###  Veri Kümesinin İlk 5 Satırı
- https://www.kaggle.com/datasets/shubh0799/churn-modelling

| RowNumber | CustomerId | Surname  | CreditScore | Geography | Gender | Age | Tenure | Balance   | NumOfProducts | HasCrCard | IsActiveMember | EstimatedSalary | Exited |
|-----------|------------|----------|-------------|-----------|--------|-----|--------|-----------|----------------|-----------|----------------|------------------|--------|
| 1         | 15634602   | Hargrave | 619         | France    | Female | 42  | 2      | 0.00      | 1              | 1         | 1              | 101348.88        | 1      |
| 2         | 15647311   | Hill     | 608         | Spain     | Female | 41  | 1      | 83807.86  | 1              | 0         | 1              | 112542.58        | 0      |
| 3         | 15619304   | Onio     | 502         | France    | Female | 42  | 8      | 159660.80 | 3              | 1         | 0              | 113931.57        | 1      |
| 4         | 15701354   | Boni     | 699         | France    | Female | 39  | 1      | 0.00      | 2              | 0         | 0              | 93826.63         | 0      |
| 5         | 15737888   | Mitchell | 850         | Spain     | Female | 43  | 2      | 125510.82 | 1              | 1         | 1              | 79084.10         | 0      |

---

##  Veri Ön İşleme Adımları

- `RowNumber`, `CustomerId`, `Surname` sütunları kaldırıldı.
- `Gender`, `Geography`: `LabelEncoder` ile sayısallaştırıldı.
- Sayısal sütunlar: `StandardScaler` ile normalize edildi.
- %80 / %20 eğitim/test ayrımı stratified olarak yapıldı.

---

##  1. Scikit-learn `MLPClassifier` Sonuçları

- **Model yapısı:** 2 gizli katman (64, 32)
- **Optimizasyon:** Adam, `max_iter=500`, `early_stopping=True`
- **Çıkış aktivasyonu:** `logistic` (sigmoid)

| Aktivasyon | Accuracy | F1-Score | Log Loss | Eğitim Süresi (sn) |
|------------|----------|----------|----------|---------------------|
| Tanh       | 0.8595   | 0.6003   | 0.3428   | 4.52                |
| Logistic   | 0.8590   | 0.5621   | 0.3440   | 14.68               |
| ReLU       | 0.8555   | 0.5601   | 0.3498   | 2.55                |

###  Gözlemler:

- Tanh ile en yüksek F1-score ve en düşük log loss elde edilmiştir.
- Eğitim süresi açısından ReLU çok hızlı ancak F1 düşüktür.
- Logistic iyi precision verse de recall düşüktür (müşteri kaybını kaçırabilir!).

###  Tanh Aktivasyonu Detayları:

- **Accuracy:** 0.8595
- **Precision:** 0.7128
- **Recall:** 0.5184
- **F1-Score:** 0.6003

#### Confusion Matrix:

[[1508 85]
[ 196 211]]


> **Yorum:** Pozitif sınıf (Exited) iyi yakalanmakta; yanlış negatif (196) hâlâ var ama genel F1 tatmin edici.

---

##  2. Custom Neural Network Sonuçları

- **Yapı:** 2 gizli katman
- **Epoch sayısı:** 500
- **Çıkış aktivasyonu:** Sigmoid, **threshold = 0.3** (`default = 0.5` yerine)

| Aktivasyon + Output | Accuracy | F1-Score | Eğitim Süresi (sn) | Final Loss |
|---------------------|----------|----------|---------------------|-------------|
| ReLU + Sigmoid      | 0.822    | 0.5870   | 1.74                | 0.3465      |
| Sigmoid + Sigmoid   | 0.718    | 0.4882   | 3.39                | 0.4363      |
| Tanh + Sigmoid      | 0.8355   | 0.4946   | 8.04                | 0.4071      |

###  Confusion Matrix (Tanh + Sigmoid, threshold = 0.3):

[[1510 97]
[ 232 161]]


###  Yorumlar:

- **ReLU + Sigmoid**, hem F1-skorda hem de final loss’ta en iyi sonucu verdi.
- **Sigmoid + Sigmoid**, en kötü performansa sahip model.
- **Tanh**, accuracy’de önde ama recall çok düşük → ayrılan müşterileri kaçırma riski.

---

##  Karşılaştırmalı Yorumlar ve Sonuç

| Model                  | Accuracy | Precision | Recall | F1-Score | Log Loss | Eğitim Süresi |
|------------------------|----------|-----------|--------|----------|----------|----------------|
| Scikit-learn (Tanh)    | 0.8595   | 0.7128    | 0.5184 | 0.6003   | 0.3428   | 4.52 s          |
| Scikit-learn (Logistic)| 0.8590   | 0.7637    | 0.4447 | 0.5621   | 0.3440   | 14.68 s         |
| Scikit-learn (ReLU)    | 0.8555   | 0.7360    | 0.4521 | 0.5601   | 0.3498   | 2.55 s          |
| Custom (ReLU+Sigmoid)  | 0.822    | 0.5394    | 0.6438 | 0.5870   | 0.3465   | 1.74 s          |

---

##  Genel Değerlendirme

- **Recall açısından** custom ReLU+Sigmoid modeli, Scikit-learn modellerini geride bırakıyor → müşteri kaybını yakalama açısından değerli.
- **Tanh (Scikit-learn)** modeli ise **dengeli performans** açısından en başarılı model.
- **Eğitim süresi** açısından custom modeller oldukça verimli, ancak **hassasiyet (precision)** ve doğrulukta bazı zayıflıkları var.

---

##  Threshold = 0.3 Seçimi ile:

- Pozitif sınıfın daha fazla yakalanması (recall ↑) sağlanıyor,
- Ancak yanlış pozitif (false positive) artabileceğinden precision düşebiliyor.

---

##  Sonuç ve Öneriler

İdeal model, kullanım amacına göre değişir:

- Eğer **müşteri kaybını önlemek öncelikliyse**, recall yüksek olan modeller (custom ReLU+Sigmoid) tercih edilebilir.
- Eğer **yanlış alarm maliyeti yüksekse**, precision yüksek modeller (Scikit-learn Logistic) daha uygundur.

###  Gelecek Geliştirme Önerileri:

- Veri dengesizliğini düzeltmek için:
  - SMOTE
  - `class_weights`
  - Focal Loss
- Eğitim süresi kritikse custom modeller tercih edilebilir; ancak model doğruluğu açısından scikit-learn MLP daha kararlı gözükmektedir.
