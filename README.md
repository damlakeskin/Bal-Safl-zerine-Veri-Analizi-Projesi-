# Bal Saflığı Üzerine Veri Analizi Projesi

## İçindekiler

- [Giriş](#giriş)
- [Veri Seti Açıklaması](#veri-seti-açıklaması)
- [Veri Hazırlama](#veri-hazırlama)
- [Eksik Veri Analizi](#eksik-veri-analizi)
- [Keşifsel Veri Analizi (EDA)](#keşifsel-veri-analizi-eda)
  - [Tanımlayıcı İstatistikler](#tanımlayıcı-istatistikler)
  - [Veri Görselleştirme](#veri-görselleştirme)
- [Korelasyon Analizi](#korelasyon-analizi)
- [Sonuç](#sonuç)
- [Gelecek Çalışmalar](#gelecek-çalışmalar)
- [Referanslar](#referanslar)

## Giriş

Bu projede, balın **saflığı** ve **fiyatını** etkileyen faktörleri anlamak amacıyla Kaggle'dan alınan bal veri seti üzerinde kapsamlı bir veri analizi gerçekleştirdim. Keşifsel veri analizi (EDA) ile balın çeşitli fizikokimyasal özellikleri arasındaki ilişkileri ve bu özelliklerin kalite ve piyasa değeri üzerindeki etkilerini inceledim.

**Amaçlarım:**

- Veri setini analiz ederek değişkenlerin dağılımını anlamak.
- Eksik verileri etkili bir şekilde ele almak.
- Farklı özellikler arasındaki ilişkileri keşfetmek.
- Balın saflığını ve fiyatını tahmin etmeye yardımcı olabilecek içgörüler sağlamak.

## Veri Seti Açıklaması

- **Veri Seti Adı:** Predict Purity and Price of Honey
- **Kaynak:** [Kaggle - Predict Purity and Price of Honey](https://www.kaggle.com/datasets/stealthtechnologies/predict-purity-and-price-of-honey)
- **Açıklama:** Bu veri seti, bal örneklerinin çeşitli özelliklerini içerir; kimyasal özellikler, polen analizi, saflık ve fiyat gibi. Balın kalitesini ve piyasa fiyatını etkileyen faktörleri keşfetmek için fırsat sunar.

### Özellikler:

- **CS (Renk Skoru):** 1.0 - 10.0 (düşük değerler açık renkli balı ifade eder)
- **Density (Yoğunluk):** 1.21 - 1.86 g/cm³
- **WC (Su İçeriği):** %12.0 - %25.0
- **pH:** 2.50 - 7.50
- **EC (Elektriksel İletkenlik):** 0.7 - 0.9 milliSiemens/cm
- **F (Fruktoz):** 20 - 50
- **G (Glukoz):** 20 - 45
- **Pollen_analysis (Polen Analizi):** 18 farklı polen kaynağı
- **Viscosity (Viskozite):** 1500 - 10000 centipoise
- **Purity (Saflık):** 0.01 - 1.00
- **Price (Fiyat):** 128.72 - 976.69

## Veri Hazırlama

### Eksik Verilerin Eklenmesi

Gerçek dünya senaryolarını simüle etmek amacıyla veri setine rastgele eksik veriler ekledim. %3'lük bir eksik veri oranı uyguladım. Bu, veri analizi ve modelleme sürecinde eksik verilerin nasıl ele alınacağını göstermeyi amaçladı.

### Eksik Verilerin Doldurulması

- **Sayısal Sütunlar:** Eksik değerleri, ilgili sütunların ortalaması ile doldurdum. Verilerin dağılımında büyük dalgalanmalar olmadığı için ortalama ile doldurmanın uygun olduğunu düşündüm.
- **Kategorik Sütun (Pollen_analysis):** Eksik değerleri mod (en sık görülen değer) ile doldurdum.

## Eksik Veri Analizi

Veri setindeki eksik değerlerin sayısını ve oranını hesapladım. Toplam 80.555 adet eksik gözlem olduğunu belirledim. Eksik değerlerin sütunlar arasındaki dağılımını ve eksik verilerin veri seti üzerindeki etkisini inceledim.

## Keşifsel Veri Analizi (EDA)

### Tanımlayıcı İstatistikler

Sütunların istatistiksel verilerini gözlemledim ve şu önemli noktaları belirledim:

- **CS (Renk Skoru):** Ortalama 5.5, hem açık hem koyu renkli bal türlerinin karışık olduğunu gösteriyor.
- **Density (Yoğunluk):** Ortalama yoğunluk 1.54 g/cm³, kabul edilebilir bir değerdedir.
- **WC (Su İçeriği):** Ortalama su içeriği %18.5, bu da kabul edilebilir sınırlar içinde yer alıyor.
- **pH:** Ortalama pH değeri 4.99, doğal bal için tipik bir değerdir.
- **EC (Elektriksel İletkenlik):** Ortalama iletkenlik 0.80 milliSiemens/cm, saf bal için tipik bir değer.
- **F (Fruktoz) ve G (Glukoz):** Dengeli bir şeker oranına işaret ediyor.
- **Viscosity (Viskozite):** Ortalama saflık değeri 0.82, bu da veri setindeki bal örneklerinin çoğunun saf olduğunu gösteriyor.

### Veri Görselleştirme

#### Fiyat Dağılımı

Genel olarak ilk baktığım grafik, **Fiyat** kategorisinin dağılımını ve sıklığını içeren grafikti. Grafik yorumlanacak olursa, ortalama olarak 600 birimlik fiyata sahip ürünlerde bir yığılma mevcuttur. Balların çoğunlukla pahalı olduğunu söyleyebiliriz.

#### Polen Analizine Göre Ortalama Fiyat

Fiyat ve polen türleri arasındaki ilişkiyi incelediğimde, 18 türden 9 tanesinin 700 birimden fazla fiyata sahip olduğunu gördüm. En yüksek fiyatlı polen ise **Manuka** polenidir. Ortalama fiyatın altında 4 polen türü bulunuyor: **Alfalfa**, **Wildflower**, **Orange Blossom** ve **Clover**.

#### Polen Analizine Göre Ortalama Saflık

Saflık ve polen türleri arasındaki ilişkiyi incelediğimde, değerlerin birbirine fazlasıyla yakın olduğunu gözlemledim. "Sunflower", "Heather", "Wildflower" polenlerinden elde edilen balın saflığının diğer ballara göre biraz daha fazla olduğu görülebilir, ancak genel olarak büyük bir fark bulunmamaktadır.

#### Fiyat Dağılımının Polen Türlerine Göre İncelenmesi

Her polen türü için fiyatlar arasında önemli farklılıklar bulunmaktadır. Premium olarak bilinen polen türleri (örneğin **Manuka**, **Heather**, **Avocado**) genel olarak daha yüksek fiyat segmentlerinde konumlanmıştır. Daha düşük fiyatlı polen türleri arasında **Clover**, **Orange Blossom** ve **Wildflower** bulunmaktadır.

#### Saflık ile Diğer Değişkenler Arasındaki İlişkiler

Saflık ile diğer özellikler (CS, Density, WC, pH, EC, F, G, Viscosity, Price) arasında belirgin bir doğrusal ilişki gözlemlemedim. Ancak bazı değişkenlerde kümelenmeler ve zayıf ilişkiler fark ettim.

### Manuka Balı Analizi

Manuka balının antibiyotik özelliği olduğunu ve bu nedenle pahalı olduğu bilindiği için, bu özellikleri etkileyen faktörleri inceledim:

- **Düşük Su İçeriği (WC)**
- **Düşük pH Seviyesi**
- **Yüksek Şeker Oranı (Fruktoz ve Glukoz dengesi)**
- **Düşük Elektriksel İletkenlik (EC)**

Yaptığım analizde, bu özelliklerin veri setindeki farklı bal türleri arasında benzer olduğunu ve Manuka balının antibiyotik özelliklerini açıklamak için bu değişkenlerin yeterli olmayabileceğini gözlemledim.

## Korelasyon Analizi

Değişkenler arasındaki ilişkileri incelemek için korelasyon analizini gerçekleştirdim. Önemli bulgular:

- **Viscosity ve Purity:** Orta düzeyde pozitif bir ilişki (0.42). Daha yüksek viskozite, daha yüksek saflıkla ilişkilidir.
- **Purity ve Price:** Orta düzeyde pozitif bir ilişki (0.42). Saflık arttıkça balın fiyatı da artmaktadır.
- **WC ve Purity:** Zayıf negatif ilişki (-0.22). Daha düşük su içeriği, daha saf balı işaret edebilir.
- **pH ve Purity:** Zayıf negatif ilişki (-0.22). Daha düşük pH seviyeleri, daha saf balları temsil edebilir.

**Sonuç:** Yüksek viskozite, balın saflığı ve fiyatı ile pozitif ilişkiye sahiptir. Bu, balın kalitesini ve piyasa değerini tahmin etmek için önemli bir göstergedir.

## Sonuç

Bu analiz sonucunda, **viskozite**nin balın **saflığı** ve **fiyatı** üzerinde önemli bir faktör olduğunu belirledim. Daha yüksek viskoziteye sahip ballar genellikle daha saf ve daha yüksek fiyatlıdır. Ayrıca, belirli polen türlerinin (örneğin Manuka) daha yüksek fiyatlandırıldığını, ancak fizikokimyasal özelliklerin genel olarak benzer olduğunu gözlemledim.

**Önemli Noktalar:**

- **Pazar Segmentasyonu:** Bal türleri, polen türü ve fiyatına göre farklı pazar kategorilerine ayrılabilir (premium, orta seviye, ekonomik).
- **Saflık Göstergeleri:** Viskozite, balın saflığının potansiyel bir göstergesi olarak kullanılabilir ve tahmin modellerinde önemli bir özelliktir.
- **Fiyat Belirleyicileri:** Saflık ve viskozite, balın fiyatını belirlemede önemli faktörlerdir.

## Gelecek Çalışmalar

Bu bulgulara dayanarak, bal fiyatlarını tahmin etmek için bir regresyon modeli oluşturmayı planlıyorum. Gelecekteki adımlar:

- **Model Oluşturma:** Viskozite, saflık ve polen türü gibi özellikleri kullanarak tahmin modelleri geliştirmek.
- **Model Değerlendirmesi:** Modelin performansını uygun metriklerle (örneğin RMSE, MAE) değerlendirmek.
- **Karşılaştırmalı Analiz:** Diğer makine öğrenimi modellerini (örneğin Random Forest, Gradient Boosting) araştırmak ve etkinliklerini karşılaştırmak.

## Referanslar

- **Veri Seti:** [Predict Purity and Price of Honey](https://www.kaggle.com/datasets/stealthtechnologies/predict-purity-and-price-of-honey)
- **Kaggle Notebook:** [Notebook](https://www.kaggle.com/code/ayemdamlakeskin/bal-safl-zerine-veri-analizi)

