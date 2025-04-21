Logistic Regression Model Performansı Karşılaştırması
Giriş
Bu proje, iki farklı Logistic Regression modelinin performansını karşılaştırmayı amaçlamaktadır. Birinci model, Scikit-learn Logistic Regression kullanarak eğitim ve tahmin yaparken, ikinci model, gradient descent (Gradyan İnişi) yöntemiyle elle yazılmış Logistic Regression modelini kullanmaktadır. Her iki modelin doğruluk, eğitim süresi, tahmin süresi ve confusion matrix sonuçları karşılaştırılacaktır.

Kullanılan Yöntemler
1. Scikit-learn Logistic Regression:
Scikit-learn kütüphanesindeki Logistic Regression modelini kullanarak veri setini eğittik. Modelin performansını accuracy ve confusion matrix gibi metriklerle değerlendirdik.

2. Elle Yazılmış Logistic Regression (Gradient Descent):
Bu modelde, logistic regression modelinin parametreleri (katsayıları) için gradient descent (gradyan inişi) yöntemiyle optimizasyon yapıldı. Burada sigmoid fonksiyonu kullanılarak tahminler yapılır ve maximum likelihood estimation (MLE) prensipleriyle parametreler güncellenir. Bu, her iterasyonda parametrelerin hata fonksiyonunu minimize etmek için güncellenmesi anlamına gelir.

Veri Seti
Veri seti, çeşitli istatistiksel özellikler içeren (örneğin, variance, skewness, curtosis, entropy) dört özelliğe ve class etiketine sahip örneklerden oluşmaktadır. Veriler eğitim ve test olarak ikiye ayrılmıştır. (https://www.kaggle.com/datasets/davorbudimir/data-banknote-authentication)

Örnek Veri Seti:
variance	skewness	curtosis	entropy	class
3.62160	8.6661	-2.8073	-0.44699	0
4.54590	8.1674	-2.4586	-1.46210	0
3.86600	-2.6383	1.9242	0.10645	0
3.45660	9.5228	-4.0112	-3.59440	0
0.32924	-4.4552	4.5718	-0.98880	0
Veri, scaled formda aşağıdaki gibi dönüştürülmüştür:

variance	skewness	curtosis	entropy
-0.6392	1.8056	-0.1884	-3.051
0.8219	0.8524	-0.5941	0.6035
-1.6570	-1.6333	2.3839	-0.3424
1.7289	0.3286	-0.7481	1.0844
0.1140	0.2060	0.3251	0.5347
Model Performansları
1. Scikit-learn Logistic Regression Performansı:
Accuracy: 0.9690

Recall: 0.9843

Precision: 0.9239

F1-Score: 0.9766

2. Elle Yazılmış Logistic Regression Performansı:
Accuracy: 0.9239

Recall: 0.7944

Precision: 0.8543

F1-Score: 0.8543

Eğitim ve Tahmin Süreleri:
Scikit-learn Logistic Regression:
Eğitim süresi: 0.0050 saniye

Tahmin süresi: 0.0024 saniye

Elle Yazılmış Logistic Regression:
Eğitim süresi: 0.0100 saniye

Tahmin süresi: 0.0040 saniye

Confusion Matrix:
Scikit-learn Logistic Regression:
lua
Kopyala
Düzenle
[[180   3]
 [  2  75]]
Elle Yazılmış Logistic Regression:
lua
Kopyala
Düzenle
[[174   9]
 [  7  70]]
 
Metrikler ve Değerlendirme

1. Accuracy (Doğruluk):
Accuracy, modelin doğru tahminlerinin, tüm tahminlerin oranını temsil eder. Yani, doğru sınıflandırılan örneklerin tüm örneklere oranıdır.
Scikit-learn modelinin doğruluğu 0.9690'dır.
Elle yazılmış model ise 0.9239 doğruluğa sahiptir.

2. Precision (Kesinlik):
Precision, doğru şekilde pozitif sınıflandırılan örneklerin, model tarafından pozitif olarak sınıflandırılan tüm örneklere oranıdır. Yani, modelin pozitif tahminlerinin ne kadar doğru olduğuna bakar.
Scikit-learn modelinde precision değeri 0.9239'dur.
Elle yazılmış modelde ise precision değeri 0.8543'tür.

3. Recall (Duyarlılık):
Recall, gerçek pozitiflerin doğru şekilde sınıflandırılan örneklere oranıdır. Yani, modelin tüm gerçek pozitifleri yakalama başarısını gösterir.
Scikit-learn modelinde recall değeri 0.9843'tür.
Elle yazılmış modelde recall değeri 0.7944'tür.

4. F1-Score:
F1-Score, precision ve recall değerlerinin harmonik ortalamasıdır ve her iki metriği dengeleyerek modelin genel başarısını ölçer.
Scikit-learn modelinde F1-Score değeri 0.9766'dır.
Elle yazılmış modelde F1-Score değeri 0.8543'tür.

5. Confusion Matrix (Karışıklık Matrisi):
Confusion matrix, modelin tahminlerinin doğruluğunu daha ayrıntılı bir şekilde görmek için kullanılır. Her satır, gerçek sınıfları, her sütun ise modelin tahmin ettiği sınıfları gösterir.

Scikit-learn modelinin confusion matrix'i:

[[180   3]
 [  2  75]]
Bu, 180 doğru negatif, 75 doğru pozitif, 3 yanlış pozitif ve 2 yanlış negatif tahmin olduğunu gösterir.

Elle yazılmış modelin confusion matrix'i:

[[174   9]
 [  7  70]]
Bu, 174 doğru negatif, 70 doğru pozitif, 9 yanlış pozitif ve 7 yanlış negatif tahmin olduğunu gösterir.

6. Estimation (Tahmin):
Bu projede kullanılan estimation, modelin doğru parametreleri (ağırlıkları) öğrenme sürecine işaret eder. Maximum likelihood estimation (MLE) yaklaşımını kullanarak, modelin parametrelerini gradient descent yöntemiyle iteratif olarak güncelledik. Bu, her iterasyonda modelin doğruluğunu artırmaya yönelik bir optimizasyon sürecidir.

Elle yazılmış Logistic Regression modeli, gradyan inişi ile likelihood fonksiyonunu en yüksek yapacak parametreleri bulmak için çalışır. Her güncelleme, parametrelerin daha doğru bir tahmin yapmasını sağlar.

Sonuçlar
Scikit-learn Logistic Regression modelinin doğruluğu daha yüksek (accuracy = 0.9690) ve recall ile precision değerleri de daha iyi.

Elle yazılmış model biraz daha düşük performans gösteriyor. Bunun nedeni, gradient descent algoritmasının daha fazla iterasyona ihtiyaç duyması ve parametrelerin tam olarak optimum çözüme ulaşamaması olabilir.

Eğitim süresi açısından, Scikit-learn modeli çok daha hızlı çalışırken, elle yazılmış modelde biraz daha uzun süreler alınmıştır.
