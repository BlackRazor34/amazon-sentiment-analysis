<p align="center">
  <img width="300" height="200" src="amazon_logo.png">
</p>

# Amazon Yorumları için Duygu Analizi ve Sınıflandırma Modeli

Bu proje, bir e-ticaret platformundaki ürün yorumlarını analiz ederek duygu analizi (sentiment analysis) yapmayı ve bu analiz sonuçlarına göre bir sınıflandırma modeli geliştirmeyi amaçlamaktadır. Proje, ev tekstili ve günlük giyim ürünleri satan "Kozmos" adlı bir marka için örnek bir iş problemi üzerinden geliştirilmiştir.

## 🚀 Projenin Amacı

Amazon üzerinden satış yapan Kozmos markasının temel hedefi, ürünlerine gelen yorumları analiz ederek müşteri memnuniyetini ve şikayetlerini anlamaktır. Bu doğrultuda;
* Ürün özelliklerini müşteri geri bildirimlerine göre iyileştirmek.
* Yorumlara duygu analizi uygulayarak pozitif (`pos`) ve negatif (`neg`) olarak etiketlemek.
* Etiketlenmiş veriyi kullanarak, yeni gelen bir yorumun duygu durumunu tahmin edebilecek bir makine öğrenmesi modeli oluşturmak.

## 📁 Veri Seti

Kullanılan veri seti (`amazon.xlsx`), bir ürün grubuna ait yorumları içermektedir. Veri setindeki sütunlar:

* **Star**: Ürüne 1-5 arasında verilen yıldız sayısı.
* **HelpFul**: Yorumu faydalı bulan kişi sayısı.
* **Title**: Yorum başlığı.
* **Review**: Ürüne yapılan detaylı yorum metni.

## 🔧 Proje Aşamaları

Proje aşağıdaki adımlardan oluşmaktadır:

**1. Metin Ön İşleme (Text Preprocessing):**
* Tüm metinler küçük harfe çevrildi.
* Noktalama işaretleri ve rakamlar metinden çıkarıldı.
* İngilizce için genel "stopwords" (etkisiz kelimeler) temizlendi.
* Metinlerde anlamsal kökleri bulmak için **Lemmatization** işlemi uygulandı.

**2. Veri Görselleştirme (Text Visualization):**
* Ön işleme sonrası kalan kelimelerin frekansları (Term Frequency) hesaplandı ve en sık geçen kelimeler bir bar grafiği ile görselleştirildi.
* Yorum metinlerindeki en popüler kelimeleri bir bütün olarak görmek için bir **WordCloud** (Kelime Bulutu) oluşturuldu.

**3. Kural Tabanlı Duygu Analizi (Sentiment Analysis):**
* NLTK kütüphanesinin `SentimentIntensityAnalyzer` aracı kullanılarak her bir yorum için bir "compound" (bileşik) duygu skoru hesaplandı.
* Bu skor 0'dan büyükse yorum **"pozitif" (pos)**, değilse **"negatif" (neg)** olarak etiketlendi ve bu bilgi `Sentiment_Analysis` adında yeni bir sütun olarak veri setine eklendi.

**4. Makine Öğrenmesi için Hazırlık:**
* `Review` sütunu bağımsız değişken (X), yeni oluşturulan `Sentiment_Analysis` sütunu ise bağımlı değişken (y) olarak belirlendi.
* Veri seti, eğitim (%75) ve test (%25) olarak ikiye ayrıldı.
* Metin verilerini sayısal vektörlere dönüştürmek için **TF-IDF (Term Frequency-Inverse Document Frequency)** tekniği kullanıldı.

**5. Modelleme ve Değerlendirme:**

İki farklı sınıflandırma modeli eğitildi ve karşılaştırıldı:

* **Lojistik Regresyon (Logistic Regression):**
    * Çapraz doğrulama (cross-validation) ile elde edilen ortalama doğruluk (accuracy) değeri: **%85.4**

* **Random Forest:**
    * Çapraz doğrulama ile elde edilen ortalama doğruluk değeri: **%88.7**

Sonuç olarak, Random Forest modelinin bu veri seti üzerinde Lojistik Regresyon'a göre daha başarılı bir performans sergilediği gözlemlenmiştir.
