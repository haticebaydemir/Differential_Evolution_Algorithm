Projenin kodlarına [buraya tıklayarak](https://colab.research.google.com/drive/1wl3IkTDNqjwMwuyzyO4LR-QgT3ZbBOhe#revisionId=0B2nNk3QINWyYa08rMDAvdU9jZmZPR1lCVUdjdzBIcFh3eUw4PQ) ulaşabilirsiniz.
# Differential_Evolution_Algorithm

`import numpy as np  #NumPy kütüphanesini içe aktarıyoruz, sayısal hesaplamalar için kullanacağız.`

### Problem parametreleri
```
DIMENSIONS = 2  # Problem boyutu (x ve y)
POPULATION_SIZE = 5  # Popülasyon büyüklüğü (çıktıları daha kolay takip edebilmek için küçülttüm)
GENERATIONS = 4  # Nesil sayısı (çıktıları daha kolay takip edebilmek için küçülttüm)
F = 0.8  # Mutasyon faktörü, diferansiyel vektörün ölçekleme faktörüdür.
CR = 0.9  # Çaprazlama oranı(pc), yeni bireyin mevcut bireyden ne kadar farklı olacağını belirtir.
```

### Fitness fonksiyonu: f(x, y) = x^2 + y^2
```
def fitness(position):
    return np.sum(position**2)  # Verilen pozisyonun fitness değerini hesaplar, karelerin toplamını hesaplıyor. Hedef minimum.
```

### Rastgele popülasyon oluşturma
```
def create_population(size, dimensions):
    return np.random.uniform(0, 10, (size, dimensions))  # Popülasyon büyüklüğünde ve verilen boyutta rastgele pozisyonlar oluşturur.Bu fonksiyon, 0 ile 10 arasında rastgele değerlerle dolu bir matris oluşturur.
```

### Diferansiyel Gelişim algoritması
```
def differential_evolution():
    population = create_population(POPULATION_SIZE, DIMENSIONS)  # Başlangıç popülasyonunu oluşturur
    best_idx = np.argmin([fitness(ind) for ind in population])  # Popülasyondaki en iyi bireyin indeksini bulur
    best = population[best_idx]  # En iyi bireyin pozisyonunu belirler

    print("Initial Population:")  # Başlangıç popülasyonunu yazdırır
    for i, ind in enumerate(population):
        print(f"Individual {i}: {ind}, Fitness: {fitness(ind)}")

    for generation in range(GENERATIONS):  # Belirtilen nesil sayısı boyunca algoritmayı çalıştırır
        print(f"\nGeneration {generation + 1}:")
        new_population = []  # Yeni popülasyon listesi
        for i in range(POPULATION_SIZE):  # Popülasyondaki her birey için döngü
            print(f"\nProcessing Individual {i}...")
            # Üç rastgele birey seç
            indices = list(range(POPULATION_SIZE))  # Mevcut popülasyonun indekslerini alır
            indices.remove(i)  # Mevcut bireyin indeksini listeden çıkarır
            a, b, c = population[np.random.choice(indices, 3, replace=False)]  # Üç rastgele birey seçer
            print(f"Selected for Mutation: a={a}, b={b}, c={c}")

            # Mutant vektörü oluşturur ve pozisyonu -10 ile 10 arasında sınırlar
            mutant = np.clip(a + F * (b - c), -10, 10) #donör vektör de denilebilir. V1 diyebiliriz.
            print(f"Mutant Vector: {mutant}")

            # Rastgele çaprazlama noktaları oluşturur
            cross_points = np.random.rand(DIMENSIONS) < CR
            if not np.any(cross_points):  # Eğer hiçbir çaprazlama noktası seçilmemişse, en az birini seçmek için
                cross_points[np.random.randint(0, DIMENSIONS)] = True  # Rastgele bir çaprazlama noktası seçer
            # Çaprazlama sonucu deneme vektörü oluşturur
            trial = np.where(cross_points, mutant, population[i])
            print(f"Trial Vector: {trial}")

            # Deneme vektörünün uygunluk değeri mevcut bireyden daha iyiyse
            if fitness(trial) < fitness(population[i]):
                print(f"Trial is better: {fitness(trial)} < {fitness(population[i])}")
                new_population.append(trial)  # Yeni popülasyona deneme vektörünü ekler
            else:
                print(f"Current is better: {fitness(population[i])} <= {fitness(trial)}")
                new_population.append(population[i])  # Aksi takdirde mevcut bireyi korur

        population = np.array(new_population)  # Yeni popülasyon mevcut popülasyon olur
        best_idx = np.argmin([fitness(ind) for ind in population])  # Yeni popülasyondaki en iyi bireyi bulur
        best = population[best_idx]  # En iyi bireyi günceller

        print("\nUpdated Population:")  # Güncellenmiş popülasyonu yazdırır
        for i, ind in enumerate(population):
            print(f"Individual {i}: {ind}, Fitness: {fitness(ind)}")
        print(f"Best Fitness in Generation {generation + 1}: {fitness(best)}")  # Nesil içindeki en iyi fitness değerini yazdırır

    return best, fitness(best)  # En iyi çözümü ve fitness değerini döndürür.
```

### Diferansiyel Gelişim algoritmasını çalıştırma
```
best_solution, best_fitness = differential_evolution()
print(f"\nBest Solution: {best_solution}, Best Fitness: {best_fitness}")  # En iyi çözümü ve fitness değerini yazdırır.
```
