Projenin kodlarına [buraya tıklayarak](https://colab.research.google.com/drive/1wl3IkTDNqjwMwuyzyO4LR-QgT3ZbBOhe#revisionId=0B2nNk3QINWyYa08rMDAvdU9jZmZPR1lCVUdjdzBIcFh3eUw4PQ) ulaşabilirsiniz.
# Diferansiyel Gelişim Algoritması

Bu proje, Diferansiyel Gelişim (Differential Evolution) algoritmasını kullanarak iki boyutlu bir optimizasyon problemi çözmeyi amaçlamaktadır. Projede, belirli bir fitness fonksiyonu altında en iyi çözümün bulunması hedeflenmektedir. 

## Proje İçeriği

### Kullanılan Teknolojiler
- **Python**: Projenin ana programlama dili.
- **NumPy**: Sayısal hesaplamalar ve matris işlemleri için kullanılmıştır.

### Problem Tanımı
Fitness fonksiyonu olarak belirlenen `f(x, y) = x^2 + y^2` kullanılarak, hedef minimum değeri (0,0) olan bir optimizasyon problemi çözülmüştür. Problemin boyutu 2 olarak belirlenmiştir, bu nedenle çözüm uzayı iki boyutlu bir düzlemde temsil edilmektedir.

### Parametreler
- **DIMENSIONS**: Problem boyutu (x ve y).
- **POPULATION_SIZE**: Popülasyon büyüklüğü (5 olarak belirlenmiştir).
- **GENERATIONS**: Algoritmanın çalışacağı nesil sayısı (4 olarak belirlenmiştir).
- **F**: Mutasyon faktörü (0.8).
- **CR**: Çaprazlama oranı (0.9).

### Algoritma Akışı
1. **Rastgele Popülasyon Oluşturma**: İlk popülasyon, belirlenen boyut ve aralıkta rastgele değerlerle oluşturulmuştur.
2. **Fitness Hesaplama**: Her bireyin fitness değeri hesaplanmıştır.
3. **Diferansiyel Gelişim**: Belirtilen nesil sayısı boyunca her birey için mutasyon, çaprazlama ve seçim adımları gerçekleştirilmiştir.
4. **Sonuçların Yazdırılması**: Her nesil sonrası güncellenmiş popülasyon ve en iyi fitness değeri yazdırılmıştır.

### Sonuç
Algoritma, belirli bir sayıda nesil boyunca çalışarak en iyi çözümü bulmayı hedeflemektedir. Sonuç olarak, en iyi çözüm ve fitness değeri elde edilmektedir.

## Kurulum
Bu projeyi çalıştırmak için Python ve NumPy kütüphanesinin yüklü olduğundan emin olun. Gerekli kütüphaneyi yüklemek için aşağıdaki komutu kullanabilirsiniz:

```bash
pip install numpy

