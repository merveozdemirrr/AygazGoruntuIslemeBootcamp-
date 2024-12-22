# Aygaz Görüntü İşleme Bootcamp 🚀

## 📌 Projenin Amacı:
Bu proje, görüntü işleme ve derin öğrenme tekniklerini kullanarak hayvan görüntülerinden sınıflandırma yapmayı ve model performansını analiz etmeyi amaçlamaktadır. Modelin doğruluğunu etkileyen faktörler (örneğin, görüntü manipülasyonu veya renk sabitliği) incelenmiştir.

---

## 1) Kütüphanelerin Yüklenmesi 📦
Proje kapsamında kullanılan temel kütüphaneler:
- **Sistem ve Dosya İşlemleri:** `os`, `zipfile`
- **Veri Manipülasyonu:** `numpy`, `cv2`, `sklearn`
- **Model Eğitim:** `tensorflow.keras`
- **Görselleştirme:** `matplotlib`

### Not:
Gerekli bağımlılıkların yüklenmesi ve Kaggle API anahtarının kullanımı için `kaggle` kütüphanesi entegre edilmiştir.

---

## 2) Veri Setinin Hazırlanması ve Dengelenmesi 🖼️
Veri seti Kaggle'dan indirilmiş ve belirli sınıflara filtrelenmiştir. Projede aşağıdaki hayvan sınıfları kullanılmıştır:

- **Sınıflar:** collie, dolphin, elephant, fox, moose, rabbit, sheep, squirrel, giant panda, polar bear
- **Her Sınıf İçin Görüntü Sayısı:** 650

Görüntüler, OpenCV kullanılarak seçilmiş ve normalize edilmiştir.

---

## 3) Boyutlandırma ve Normalizasyon 📏
Görüntüler 128x128 boyutuna küçültülmüş ve piksel değerleri [0,1] aralığında normalize edilmiştir.

---

## 4) Veriyi Eğitim ve Test Seti Olarak Bölme 🧪
Veri seti, %70 eğitim ve %30 test oranında bölünmüştür. Ayrıca, sınıflandırma etiketleri `LabelEncoder` ile dönüştürülmüş ve kategorik formata (`to_categorical`) çevrilmiştir.

---

## 5) Veri Artırma (Data Augmentation) 🔄
Eğitim setindeki çeşitliliği artırmak için veri artırma teknikleri uygulanmıştır:
- Döndürme: `rotation_range=20`
- Kaydırma: `width_shift_range` ve `height_shift_range`
- Yakınlaştırma: `zoom_range=0.2`
- Yatay Çevirme: `horizontal_flip=True`

---

## 6) CNN Modeli 🧠
Kullanılan model, temel bir Convolutional Neural Network (CNN) mimarisine sahiptir:
- **Katmanlar:**
  - Giriş Katmanı: (128x128x3)
  - Convolution ve MaxPooling
  - Flatten
  - Tam Bağlantılı (Dense) Katmanlar
  - Çıkış Katmanı: Softmax (10 sınıf için)

---

## 7) CNN Modeli Derleme ve Eğitim Süreci ⚙️

### 1. Modeli Derleme
Model, aşağıdaki parametrelerle derlenmiştir:
- **Optimizasyon Algoritması:** Adam (Öğrenme oranı: 0.001)
- **Kayıp Fonksiyonu:** Categorical Crossentropy
- **Değerlendirme Metrikleri:** Accuracy

### 2. Eğitim Verisinin Çeşitlendirilmesi
Data Augmentation jeneratörleri kullanılarak modelin aşırı öğrenmesini önlemek hedeflenmiştir.

### 3. Eğitim Süreci
Model, 20 epoch boyunca eğitim almış ve `steps_per_epoch` ile doğrulama adımları ayarlanmıştır.

---

## 8) Modelin Eğitilmesi ve Performansı 📊

### 1. Modelin Eğitilmesi
Model başarıyla eğitilmiş ve doğrulama doğruluğu gözlemlenmiştir.

### 2. Performans Grafiği
Eğitim ve doğrulama doğruluklarının epoch bazlı grafiği çizilmiştir. Model performansı eğri üzerinde görselleştirilmiştir.

### 3. Grafiğin Yorumlanması
- Eğitimin başında doğruluk düşükken, her epoch ile birlikte iyileşmiştir.
- Doğrulama doğruluğu belirli bir noktada stabilize olmuştur.

---

## 9) Görüntü Manipülasyonu ve Model Performansı 🎭

### 1. Görüntü Manipülasyonu
Manipülasyon, parlaklık ve kontrast değerlerini değiştirerek yapılmıştır.

### 2. Model Performansının Değerlendirilmesi
Manipüle edilmiş görüntüler üzerinde modelin doğruluğu hesaplanmıştır.

---

## 10) Manipüle Edilmiş Test Seti ile Model Performansı 🔍

### Amaç:
Manipüle edilmiş görüntülerin modele etkisini incelemek.

Sonuç olarak:
- Manipüle edilmiş görüntülerde model doğruluğu düşmüştür.

---

## 11) Renk Sabitliği Algoritması Uygulama 🎨

### 1. Renk Sabitliği Uygulanmış Test Seti
Gray World algoritması kullanılarak manipüle edilmiş görüntülere renk sabitliği uygulanmıştır.

### 2. Model Doğruluk Sonuçlarının Karşılaştırılması
- Orijinal Test Seti Doğruluğu
- Manipüle Edilmiş Test Seti Doğruluğu
- Renk Sabitliği Uygulanmış Test Seti Doğruluğu

Sonuçlar, renk sabitliğinin manipüle edilmiş görüntülerdeki doğruluğu artırdığını göstermektedir.

---

## 12) Modelin Test Edilmesi ✅
Model, farklı koşullar altında test edilmiş ve aşağıdaki sonuçlar karşılaştırılmıştır:
- **Orijinal Test Seti:** Model en yüksek doğruluğa ulaşmıştır.
- **Manipüle Edilmiş Test Seti:** Doğruluk önemli ölçüde azalmıştır.
- **Renk Sabitliği Uygulanmış Test Seti:** Manipülasyona göre daha iyi doğruluk elde edilmiştir.

---

## Önemli Notlar:
- Modelin manipüle edilmiş görüntüler üzerindeki performans düşüşü, modelin eğitim sırasında daha fazla çeşitlilik gerektirdiğini göstermektedir.
- Renk sabitliği gibi yöntemler, gerçek dünya uygulamalarında modelin güvenilirliğini artırabilir.

---

## Projenin Sonucu 🎯
Bu proje, görüntü manipülasyonu ve renk sabitliği gibi faktörlerin derin öğrenme modelleri üzerindeki etkisini anlamak için kapsamlı bir çalışma sunmuştur. Elde edilen bulgular, görüntü işleme projelerinde veri hazırlamanın önemini bir kez daha ortaya koymaktadır.
