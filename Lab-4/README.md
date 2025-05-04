Linear Regression Model Optimization - YZM212 Bahar 2024-2025
Genel Bakış
Bu laboratuvar çalışmasında Linear Regression (Doğrusal Regresyon) model optimizasyonu yapılacaktır. İki farklı yöntem kullanılacaktır: En Küçük Kareler Tahmini (Least Squares Estimation - LSE) ve Scikit-learn Linear Regression. Amaç, her iki yöntemle de model eğitmek ve performanslarını Mean Squared Error (MSE), Mean Absolute Error (MAE) ve R-squared (R²) gibi metriklerle karşılaştırmaktır.

Eğitim için kullanılan veri seti, öğrenci performansını, çalışma alışkanlıklarını, ekstrakuriküler aktiviteleri ve uyku saatlerini temsil eden çeşitli özellikler içermektedir.

Gereksinimler
En Küçük Kareler Tahmini (LSE): NumPy kullanarak, En Küçük Kareler yöntemiyle özel bir doğrusal regresyon modeli uygulanacaktır.

Scikit-learn Regresyon Modeli: Aynı veri seti kullanılarak, Scikit-learn kütüphanesindeki doğrusal regresyon modeli eğitilecektir.

Model Karşılaştırması: Eğitilen her iki model, aşağıdaki metriklerle karşılaştırılacaktır:

Mean Squared Error (MSE) - Ortalama Kare Hatası

Mean Absolute Error (MAE) - Ortalama Mutlak Hata

R-squared (R²) - Belirleme Katsayısı

Eğitim Süresi

GitHub Deposu: Bu çalışma bir GitHub deposunda takip edilecek ve projeye ait açıklamalar, kodlar ve sonuçlar burada yer alacaktır.

Veri Açıklaması
Modelin eğitilmesi için kullanılan veri seti, öğrencilerin çalışma alışkanlıkları, performansları ve ekstrakuriküler aktiviteleri ile ilgili bilgileri içermektedir. Veri setindeki sütunlar şunlardır:

Sütun Adı	Açıklama
Hours Studied	Öğrencinin çalıştığı saat sayısı
Previous Scores	Öğrencinin önceki sınav puanları
Extracurricular Activities	Öğrencinin ekstrakuriküler aktivitelere katılımı (Evet/Hayır)
Sleep Hours	Öğrencinin gece başına ortalama uyku süresi
Sample Question Papers Practiced	Öğrencinin çözdüğü deneme sınavı sayısı
Performance Index	Öğrencinin genel performansı

Örnek veri seti (5 örnek):

Hours Studied	Previous Scores	Extracurricular Activities	Sleep Hours	Sample Question Papers Practiced	Performance Index
7	99	Yes	9	1	91.0
4	82	No	4	2	65.0
8	51	Yes	7	2	45.0
5	52	Yes	5	2	36.0
7	75	No	8	5	66.0

Yöntemler
En Küçük Kareler Tahmini (LSE) ile Özel Doğrusal Regresyon:
Bu model, En Küçük Kareler Yöntemi kullanılarak sıfırdan oluşturulacaktır. Modelin amacı, doğrusal denklemdeki optimal katsayıları (
𝜃
0
θ 
0
​
 , 
𝜃
1
θ 
1
​
 ) bulmaktır:

𝑌
=
𝜃
0
+
𝜃
1
𝑋
Y=θ 
0
​
 +θ 
1
​
 X
Modelin amacı, Ortalama Kare Hatasını (MSE) minimize etmektir.

Scikit-learn ile Doğrusal Regresyon Modeli:
Aynı veri seti kullanılarak, Scikit-learn kütüphanesindeki doğrusal regresyon modeli ile eğitim yapılacaktır. Modelin amacı, veri setine en uygun doğrusal denklemi bulmaktır.

Performans Karşılaştırması
Her iki modelin performansı, MSE (Ortalama Kare Hatası), MAE (Ortalama Mutlak Hata), R² (Belirleme Katsayısı) ve Eğitim Süresi metrikleriyle karşılaştırılmıştır. Aşağıdaki tabloda, her iki modelin bu metriklere göre sonuçları verilmiştir:

Model	MSE (Ortalama Kare Hatası)	MAE (Ortalama Mutlak Hata)	R² (Belirleme Katsayısı)	Eğitim Süresi
En Küçük Kareler Yöntemi	262.22981	3.49070	0.92136	0.000858 sn
Scikit-learn Modeli	262.22981	3.49070	0.92136	0.001406 sn

Metrik Karşılaştırması ve Çıkarımlar
1. MSE (Ortalama Kare Hatası) ve MAE (Ortalama Mutlak Hata):
Her iki model de benzer MSE ve MAE değerleri elde etmiştir. Bu, her iki modelin tahminlerindeki genel hata oranlarının benzer olduğunu gösterir. MSE ve MAE arasındaki farklar küçük olmasına rağmen, MSE hata karelerini kullandığı için büyük hatalar üzerinde daha fazla etki yaratacaktır, ancak genel olarak modelin doğruluğu açısından benzer sonuçlar elde edilmiştir.

2. R² (Belirleme Katsayısı):
Her iki modelin R² değeri 0.92136'dır, bu da her iki modelin veriyi açıklama başarısının %92.14 olduğunu gösterir. Bu yüksek R² değeri, her iki modelin de öğrenci performansını açıklamada oldukça etkili olduğunu gösterir.

3. Eğitim Süresi:
Eğitim süreleri arasında belirgin bir fark bulunmaktadır. En Küçük Kareler Yöntemi, daha düşük bir eğitim süresine sahiptir (0.000858 sn), bu da işlemci gücü ve bellek açısından daha hafif olduğu anlamına gelir. Scikit-learn Modeli ise bir miktar daha fazla zaman almıştır (0.001406 sn). Bu fark, kullanılan algoritmaların farklı yapılarından kaynaklanmaktadır. Ancak, her iki yöntem de pratikte çok hızlıdır ve büyük veri setlerinde daha verimli hale gelebilirler.

Sonuçlar ve Yorumlar
En Küçük Kareler Yöntemi: Bu yöntem, modelin parametrelerini analitik olarak çözerek bulur. Küçük veri setlerinde oldukça hızlıdır, ancak daha büyük veri setlerinde işlem süresi artabilir. Yine de, küçük veri setleriyle çalışırken oldukça verimlidir.

Scikit-learn Modeli: Bu model, optimize edilmiş bir kütüphane fonksiyonu kullanarak hızlı ve etkili sonuçlar verir. Özellikle büyük veri setlerinde daha verimli olabilir. Eğitim süresi açısından biraz daha uzun olsa da, modelin genel doğruluğu ve stabilitesi açısından avantajlıdır.

Her iki model de aynı veri setiyle benzer doğruluk sonuçları verirken, Scikit-learn modeli eğitim süresi açısından daha hızlıdır.

