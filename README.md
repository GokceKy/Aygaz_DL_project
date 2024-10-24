# Balık Görüntü Sınıflandırması ile ANN ve Hiperparametre Optimizasyonu

## Proje Açıklaması

Bu proje, büyük ölçekli bir balık veri setini kullanarak farklı balık türlerini sınıflandırmayı hedeflemektedir. Proje, görüntü verilerini işlemek için aktivasyon fonksiyonları, dropout katmanları ve optimizasyon için hiperparametre ayarı içeren bir Yapay Sinir Ağı (ANN) kullanmaktadır. Amaç, doğruluğu maksimize etmek ve aşırı öğrenmeyi azaltarak genel performansı artırmaktır.

Veri seti, farklı türde balıkların görüntülerini içermektedir ve proje, modelin eğitimini, test edilmesini ve performansını artırmak için optimizasyon yapılmasını kapsamaktadır.

## Veri Seti

Veri seti, farklı balık türlerinin görüntülerini içermekte olup eğitim ve test setlerine ayrılmıştır. Her görüntü, ilgili balık kategorisi ile etiketlenmiştir.

- **Veri Seti Yolu**: `/kaggle/input/a-large-scale-fish-dataset/Fish_Dataset/Fish_Dataset`
- **Eğitim Seti Boyutu**: Veri setinin %80'i
- **Test Seti Boyutu**: Veri setinin %20'si

Her balık görüntüsü, kategorisine göre etiketlenmiştir ve amaç, bu görüntüleri bir ANN kullanarak sınıflandırmaktır.

---

Model Mimarisi
Model, aşağıdaki temel bileşenlere sahip bir ardışık ANN'e dayanmaktadır:

Flatten Katmanı: Görüntüyü 1D diziye dönüştürmek için.
Dense Katmanlar: Çeşitli birim sayısına sahip tamamen bağlı katmanlar.
Dropout Katmanları: Aşırı öğrenmeyi azaltmak için düzenleme tekniği.
Aktivasyon Fonksiyonları: Gizli katmanlar için ReLU, çıktı katmanı için Softmax.
Başlangıç Model Yapısı:
Girdi Şekli: (128, 128, 3) (yeniden boyutlandırılmış görüntüler)
Dense Katmanlar:
Gizli katmanlar: 128 ve 64 birim
Dropout: 0.3
Çıktı Katmanı: Sınıf sayısı kadar birim, softmax aktivasyon ile.

Model Özeti:


Layer (type)               Output Shape         Param #     
=================================================================
flatten_1 (Flatten)         (None, 49152)        0           
_________________________________________________________________
dense_1 (Dense)             (None, 128)          6291584     
_________________________________________________________________
dropout_1 (Dropout)         (None, 128)          0           
_________________________________________________________________
dense_2 (Dense)             (None, 64)           8256        
_________________________________________________________________
dropout_2 (Dropout)         (None, 64)           0           
_________________________________________________________________
output_layer (Dense)        (None, 5)            325         
=================================================================
Toplam parametre: 6,299,165
Eğitilebilir parametreler: 6,299,165
Eğitilmeyen parametreler: 0
Modelin Eğitilmesi
Eğitim Epoch Sayısı: 20
Optimizasyon Yöntemi: Adam
Kayıp Fonksiyonu: Kategorik Çapraz Entropi
Metriği: Doğruluk
Modeli eğitmek, veri setini eğitim ve test setlerine ayırmayı ve yukarıdaki yapılandırma ile veriye uyum sağlamak için modeli eğitmeyi içerir.

Hiperparametre Optimizasyonu
KerasTuner kullanarak aşağıdaki hiperparametrelerin optimizasyonu yapıldı:

Gizli katman sayısı (1 ile 3 katman)
Katman başına düğüm sayısı (64 ile 512 birim)
Dropout oranı (0.1 ile 0.5)
Optimizasyon Yöntemi (adam, sgd, rmsprop)
Hiperparametre Ayarlama Sonuçları:
Bulunan en iyi hiperparametreler:

Katman Sayısı: 2
Katman Başına Birimler:
İlk Katman: 256
İkinci Katman: 128
Dropout Oranları:
İlk Katman: 0.3
İkinci Katman: 0.2
Optimizasyon Yöntemi: Adam
En iyi performansı gösteren model, doğrulama setinde %92.5 doğruluk elde etmiştir.

Sonuçlar
Nihai Model Performansı
En iyi hiperparametrelerle eğitim tamamlandıktan sonra modelin elde ettiği performans metrikleri:

Eğitim Doğruluğu: %94.3
Doğrulama Doğruluğu: %92.5
Eğitim Kaybı: 0.18
Doğrulama Kaybı: 0.22
Eğitim ve Doğrulama Doğruluğu/Kayıp:
Aşağıda doğruluk ve kayıp metriklerinin görselleştirilmesi bulunmaktadır:


# Sınıflandırma Raporu
Bu proje, büyük ölçekli bir veri setini kullanarak balık türlerini sınıflandırmak için bir Yapay Sinir Ağı uygulamasını göstermektedir. Hiperparametre ayarlaması ve dropout düzenlemesi uygulanarak modelin performansı önemli ölçüde artırılmıştır.



