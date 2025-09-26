# deep-learning-project

Bu doküman, Convolutional Neural Network (CNN) mimarisine dayanan bir görüntü sınıflandırma projesini detaylandırmaktadır.
Proje, katılımcılara derin öğrenme, veri analizi, model geliştirme, değerlendirme ve yorumlama konularında pratik deneyim kazandırmayı amaçlamaktadır.

---

## 1. Projenin Amacı ve Kapsamı

Projenin temel amacı, karmaşık görüntü verilerini işleyerek kedi ve köpek resimlerini yüksek doğrulukla sınıflandırabilen bir derin öğrenme modeli geliştirmektir. Proje, model geliştirme sürecini adım adım takip ederek, elde edilen sonuçları bilimsel metriklerle analiz etmeyi ve modelin performansını yorumlamayı kapsamaktadır.

---

## 2. Veri Seti Hakkında Bilgi

Projede kullanılan veri seti, Kaggle üzerinde yer alan popüler bir ikili sınıflandırma (binary classification) veri seti olan **Dogs vs. Cats**'tir.
**Boyut:** Veri seti, yaklaşık **25.000 eğitim görüntüsü** ve **12.500 test görüntüsü** içermektedir.
**Yapısal Zorluk:** Veri setinin ham hali, `ImageDataGenerator`'ın ihtiyaç duyduğu sınıf bazlı alt klasörlere sahip değildir. Bu nedenle, projenin ilk aşamasında tüm resimler `cat` ve `dog` adında iki ayrı klasöre manuel olarak taşınmıştır.

---

## 3. Kullanılan Yöntemler ve Model Mimarisi

Model geliştirme süreci, proje adımları doğrultusunda titizlikle uygulanmıştır.

### A) Veri Ön İşleme ve Veri Çoğaltma (Data Augmentation)
Modelin daha sağlam ve genellenebilir tahminler yapabilmesi için veri çoğaltma yöntemleri kullanılmıştır.
* `ImageDataGenerator` sınıfı ile resimler 0-1 aralığına normalize edilmiştir.
* Modelin resimlerin konumuna ve açısına karşı daha dayanıklı olması için **döndürme**, **kaydırma**, **yakınlaştırma** ve **yatay çevirme** gibi dönüşümler uygulanmıştır.

### B) CNN Model Mimarisi
Görüntü sınıflandırma için Evrişimli Sinir Ağı (CNN) mimarisi kullanılmıştır. Model, temel derin öğrenme katmanlarından oluşmaktadır:
**Evrişim Katmanları (`Conv2D`):** Görüntülerdeki temel özellikleri (kenarlar, dokular) öğrenmek için kullanılmıştır.
**Havuzlama Katmanları (`MaxPooling2D`):** Görüntü boyutunu küçülterek en önemli özellikleri korumuştur.
**Dropout Katmanı:** Modelin aşırı uydurma (overfitting) yapmasını engellemek için eğitim sırasında rastgele nöronları devre dışı bırakmıştır.
**Tam Bağlantılı Katmanlar (`Dense Layers`):** Öğrenilen özelliklere dayanarak nihai sınıflandırma kararını vermiştir.

---

## 4. Elde Edilen Sonuçlar ve Analiz

Model, 15 epok boyunca eğitildikten sonra aşağıdaki sonuçlar elde edilmiştir:

### A) Eğitim ve Doğrulama Grafikleri
Modelin eğitimi sırasında, **eğitim kaybı** azalmaya devam ederken, **doğrulama kaybı** bir noktadan sonra artış göstermiştir. Bu durum, modelin sadece eğitim verisini ezberlediğini ve aşırı uydurma (overfitting) yaptığını açıkça göstermektedir.

### B) Değerlendirme Raporları
* **Accuracy (Doğruluk):** Test verisi üzerinde modelin genel doğruluk skoru **%50** olarak hesaplanmıştır.
* **Confusion Matrix ve Classification Report:** Raporlar, modelin kedi ve köpek sınıfları arasında tahmin yapmakta zorlandığını ortaya koymuştur. Her iki sınıf için de **Precision**, **Recall** ve **F1-Score** değerleri yaklaşık %50 seviyesindedir.

### Sonuç ve Yorum
Elde edilen sonuçlar, modelin performansının iyileştirilmesi gerektiğini göstermektedir.Projenin sonraki aşamalarında, **hiperparametre optimizasyonu** yapılarak modelin daha yüksek bir doğruluk skoruna ulaşması hedeflenmelidir.

---
## 4. Karşılaşılan Zorluklar ve Öğrenim Süreci

Bu projeyi geliştirirken, Kaggle'ın çalışma ortamından kaynaklanan teknik sorunlarla karşılaştım. Özellikle, `FileNotFoundError` gibi tekrar eden sorunlar, dosya düzenleme ve veri ön işleme adımlarının tek bir kod bloğunda birleştirilmesini gerektirmiştir. Bu zorluklar, sadece doğru kodu yazmanın değil, aynı zamanda verimli bir iş akışı oluşturmanın ve platform kısıtlamalarına adapte olmanın önemini anlamamı sağlayan değerli bir öğrenim süreci olmuştur.Notebook'ta görebileceğiniz bazı hata mesajlarını kasıtlı olarak silmedim; çünkü bunlar, problem çözme ve hata ayıklama aynı zamanda proje sürecimin birer parçasıdır.

---
### Kaggle Notebook Linki
Projenin tüm kodlarına, çıktılarına aşağıdaki Kaggle notebook linkinden ulaşabilirsiniz:

https://www.kaggle.com/code/fadimeocal/dog-and-cat
