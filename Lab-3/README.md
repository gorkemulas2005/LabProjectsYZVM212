# Özdeğer ve Özvektör Hesaplama Karşılaştırması

Bu projede, farklı matris boyutları için özdeğer (eigenvalue) ve özvektör (eigenvector) hesaplamaları iki farklı yöntemle gerçekleştirilmiştir:

1. **Custom (Elle Kodlanan) Yöntem**
2. **NumPy Kütüphanesi Kullanılarak**

Ayrıca **zaman** ve **RAM kullanımı** açısından performans karşılaştırması yapılmış, küçük matrislerde özvektör yönleri görselleştirilmiştir.

---

##  Kullanılan Matrisler ve Yöntemler

### 1. Küçük Matris (2x2)

**A = [[4, 2], [1, 3]]**

| Yöntem      | Özdeğerler     | Süre (sn) | RAM (MB) |
|-------------|----------------|-----------|----------|
| Custom      | [5, 2]         | 0.0007    | 0.04     |
| NumPy       | [5, 2]         | 0.0010    | 0.30     |

Her iki yöntem de doğru sonuçlar vermektedir. Küçük boyutlu matrislerde `Custom` yöntemin zamanı daha kısa, RAM kullanımı daha düşüktür.

**Görselleştirme:**

Özvektörlerin yönleri iki yönteme göre matplotlib ile çizilmiştir. Vektörlerin doğrultusu benzer, yalnızca normalize edilme yönleri değişebilir.!!!

---

### 2. Büyük Matris (1000x1000)

`np.random.rand(1000, 1000)` ile oluşturulmuştur.

| Yöntem      | Özdeğerler     | Süre (sn) | RAM (MB) |
|-------------|----------------|-----------|----------|
| Custom      | ❌ Uygulanamaz | ❌        | ❌       |
| NumPy       | İlk 10 değer gösterildi | 3.50      | 19.39    |

---

##  Neden `Custom` Yöntem Büyük Matris İçin Uygun Değil?

`Custom` yöntemde elimizdeki formüller ve çözüm yaklaşımı yalnızca 2x2 matrisler için geçerlidir. Daha büyük matrisler için karakteristik polinomun el ile çıkarımı ve çözümü **yapısal olarak mümkün değildir**:

- Karakteristik denklemi çözülemez hâle gelir.
- Özvektör bulma işleminde `A - λI` boyut uyumsuzluğu oluşur.
- Python hata mesajı:  
  `operands could not be broadcast together with shapes (100,100) (2,2)`

Bu nedenle yalnızca **NumPy** gibi hazır algoritmalar büyük boyutlu matrislerde verimli ve güvenilir çözümler sunabilir.

---

##  RAM ve Zaman Karşılaştırması

| Matris Boyutu | Yöntem | Süre (sn) | RAM (MB) |
|---------------|--------|-----------|----------|
| 2x2           | Custom | 0.0007    | 0.04     |
| 2x2           | NumPy  | 0.0010    | 0.30     |
| 1000x1000     | NumPy  | 3.50      | 19.39    |

---

### 1. Yöntemler aynı sonuçları veriyor mu?

Evet, küçük matrislerde hem `Custom` hem de `NumPy` aynı özdeğerleri ve doğrultuda özvektörleri vermektedir.

### 2. Hangi yöntem daha verimli?

- Küçük matrislerde `Custom` yöntem daha hızlıdır.
- Büyük matrislerde ise yalnızca `NumPy` kullanılabilir.

### 3. Bellek (RAM) kullanımı nasıl değişiyor?

- Küçük matrislerde RAM kullanımı ihmal edilebilir düzeyde.
- Büyük matrislerde RAM kullanımı anlamlı şekilde artmaktadır (yaklaşık **20 MB**).

### 4. Hangi yöntem önerilir?

- 2x2 veya 3x3 gibi küçük matrislerde custom yöntem öğretici olabilir.
- Ancak 4x4 ve üstü matrislerde NumPy gibi optimize kütüphaneler zorunludur.

---

## `Custom` Yöntemde Kullanım Sınırlamaları

`Custom` yöntemde yalnızca **2x2 matrisler** için geçerli olan el ile çözüm uygulanmıştır. Bu yöntemin kullanılmaması gereken bazı durumlar ve nedenleri şunlardır:

###  Neden Daha Büyük Matrislerde Kullanılmamalı?

- **Karakteristik Denklem Karmaşıklığı:** 3x3 ve üstü matrislerde determinant üzerinden elde edilen denklemlerin çözümü analitik olarak zorlaşır.
- **Boyut Uyumsuzluğu:** `A - λI` işlemi sırasında `broadcast` hatası oluşabilir. Örnek hata mesajı:  


  ```python
  operands could not be broadcast together with shapes (100,100) (2,2)


##  Ödevde Cevaplanması İstenen Sorular


 Özdeğer ve Özvektör Hesaplaması: Teori, NumPy ve El ile Uygulama
Bu proje, makine öğrenmesi bağlamında özdeğer (eigenvalue) ve özvektör (eigenvector) kavramlarını anlamak, bu kavramların matrislerle ilişkisini keşfetmek, NumPy kütüphanesi üzerinden özdeğer-özvektör hesaplamasını gerçekleştirmek ve bu işlemleri el ile gerçekleştiren özelleştirilmiş bir fonksiyonla karşılaştırmak amacıyla hazırlanmıştır.

 1. Özdeğerler, Özvektörler ve Makine Öğrenmesi ile İlişkisi
 Tanımlar;
Matris: Sayılardan oluşan iki boyutlu bir dizidir. Makine öğrenmesinde veri, genellikle matris formunda temsil edilir.

Özdeğer (Eigenvalue): Bir matrisin etkisi altında yalnızca ölçeklenen, yönü değişmeyen vektörlerin o matris tarafından ne kadar ölçeklendiğini gösteren skalarlardır.

Özvektör (Eigenvector): Bir matrisle çarpıldığında yalnızca boyu değişen, yönü sabit kalan vektörlerdir. 
𝐴𝑣=𝜆𝑣
Av=λv

 2. Makine Öğrenmesinde Kullanım Alanları
Özdeğer ve özvektör kavramları aşağıdaki yöntemlerde kritik rol oynar:

PCA (Principal Component Analysis): Boyut indirgeme. Verideki maksimum varyansı temsil eden yönleri bulmak için kullanılır.

Covariance Matrix Decomposition: Korelasyon matrislerinin özdeğer ayrışımıyla analiz edilmesi.

Markov Zincirleri / Hidden Markov Models (HMM): Geçiş olasılık matrislerinin istasyoner dağılımları özdeğer ile belirlenir.

Spektral Kümeleme (Spectral Clustering): Grafın Laplasyeni üzerinden özvektör hesaplanarak kümeler oluşturulur.

Doğrusal Dinamik Sistemler: Sistem kararlılığı özdeğerlerle incelenir.

 Kaynaklar
ChatGpt' nin konu hakkındaki açıklamaları
https://www.geeksforgeeks.org/applications-of-eigenvalues-and-eigenvectors/

 2. NumPy ile Özdeğer ve Özvektör Hesaplama
 numpy.linalg.eig Fonksiyonu
NumPy’nın linalg (linear algebra) modülündeki eig fonksiyonu, bir karesel matrisin özdeğerlerini ve özvektörlerini hesaplar.

Kullanımı:
python
eigvals, eigvecs = np.linalg.eig(A)
eigvals: Özdeğerleri içeren 1D array.

eigvecs: Sütunları özvektör olan 2D array. Her eigvecs[:, i] vektörü, eigvals[i] özdeğeriyle eşleşir.

Kaynak Kod İncelemesi:
https://www.geeksforgeeks.org/applications-of-eigenvalues-and-eigenvectors/
https://www.geeksforgeeks.org/applications-of-eigenvalues-and-eigenvectors/

İlgili Dosyalar:

linalg.py → üst seviye API

lapack_lite.c → düşük seviye LAPACK çağrıları

NumPy aslında LAPACK kütüphanelerini kullanır (örneğin dgeev, zgeev) ve Python üzerinden sarmalayıp çağırır.

Adımlar:
Matrisin boyutu kontrol edilir.

LAPACK fonksiyonları çağrılarak (örn. dgeev) özdeğer ve özvektör ayrıştırması yapılır.

Karmaşık/gerçek sayılar ayrılır.

Sonuç Python array’lerine dönüştürülerek döndürülür.

 3. El ile Özdeğer ve Özvektör Hesaplaması (custom_eigen_2x2)
Bu projede, yalnızca 2x2 matrisler için geçerli özel bir fonksiyon tanımlanmıştır. Bu fonksiyon:

Matrisin izini (trace) ve determinantını (det) hesaplar.

Karakök içinde negatif çıkarsa hata verir.

Klasik çözüm formülüyle özdeğerleri bulur.

λ= [Tr(A)± (Tr(A) ^2 −4⋅det(A))^1/2]/2
​(𝐴−𝜆𝐼)𝑣=0 denklemi çözülerek özvektör bulunur.
