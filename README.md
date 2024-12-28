# VERİ SETİ 

Bu veri seti, 2019 yılına ait Airbnb evlerinin bilgilerini içerir. 

<span style="color: yellow;"> Veri seti bir CSV dosyasında yer alır. (dataset/clean_market_analysis_2019.csv) </span>

### CSV Dosyasındaki Sütunlar ve Anlamları

* unified_id: Airbnb mülkünün benzersiz bir kimliğini belirtir.
* month: Verilerin ait olduğu ayı belirtir.
* zipcode: Airbnb mülkünün bulunduğu posta kodunu içerir.
* city: Airbnb mülkünün bulunduğu şehri belirtir.
* host_type: Ev sahibinin mülk tipini belirtir (örneğin, ev, daire, villa gibi).
* bedrooms: Airbnb mülkünde bulunan yatak odası sayısını belirtir.
* bathrooms: Airbnb mülkünde bulunan banyo sayısını belirtir.
* guests: Mülkte konaklayabilecek maksimum misafir sayısını belirtir.
* revenue: Belirli bir dönemde mülkten elde edilen geliri belirtir.
* openness: Mülkün ne kadar sıklıkla kullanıldığını veya ne kadar süreyle kullanılamaz olduğunu belirten bir oran.
* occupancy: Mülkün doluluk oranını belirtir.
* nightly_rate: Günlük kira ücretini belirtir.
* lead_time: Rezervasyon yapıldığı tarih ile konaklama başlangıç ​​tarihi arasındaki süreyi belirtir.
* length_stay: Ortalama konaklama süresini belirtir.


# PROJE 

Bu veri seti, üzerinde veri analizi yapılarak bir makine öğrenmesi modeline gönderilmesi için uygun hale getirilecek.

## PROJE AŞAMALARI

## 1) **KÜTÜPHANELERİN IMPORT EDİLMESİ**

- **numpy**: Sayısal hesaplamalar için kullanılır, özellikle çok boyutlu diziler ve matris işlemleri için kullanılır.
- **pandas**: Veri manipülasyonu ve veri analizi için kullanılır, tablo veri yapılarını destekler ve veri setlerini kolayca işlemek için kullanılır. 
- **re**: Python'da düzenli ifadelerle (regular expressions) metin işleme yapmak için kullanılır, metinlerde desenleri bulmak, değiştirmek veya ayıklamak için kullanılır.
- **seaborn**: Veri görselleştirmesi için kullanılır, matplotlib'e dayanır ancak daha estetik ve kullanıcı dostu grafikler oluşturmayı sağlar.
- **matplotlib**: Grafik oluşturmak için kullanılır, çizgi grafikleri, dağılım grafikleri, histogramlar, görselleştirmeler ve diğer türde grafikler oluşturmak için kullanılır.
- **warnings**: Python programlarında çalışma zamanında oluşabilecek uyarı mesajlarını tanımlamak, yönetmek ve kontrol etmek için kullanılır.


## 2) **VERİ SETİNİN ELDE EDİLMESİ**
* CSV dosyasından veri seti okunarak bir DataFrame'e atanır.
* Veri setinde bazı sütun isimlerinde boşluklar bulunur. Bu boşluklar "_" ile doldurulur. Bunun nedeni sütun isimlerini "df.sütun_ismi" şeklinde kullanınca hatalar ile karşılaşılmasını önlemektir.


## 3) **KEŞİFSEL VERİ ANALİZİ (EDA - EXPLORATORY DATA ANALYSIS)**

* EDA görsel veya nümerik yöntemlerle, veriyi bir özet üzerinden yorumlama yaklaşımıdır. Veriyi ön işleme noktasında atılması gereken adımlardan çıkarım yapmak için kullanılacak metod ve modele kadar pek çok konuda fikir sahibi olunmasını sağlar.

* "review_dataset" adlı bir fonksiyon oluşturulur. Bu fonksiyona girdi olarak veri setinin yolu verilir ve ekrana veri seti ile ilgili aşağıdaki bilgileri yazdırır:
    - Veri Seti İsmi: market_analysis_2019.csv

    - Veriseti Boyutu: (29928, 14) / Satır Sayısı: 29928 / Sütun Sayısı: 14

    - Veriseti Sütunlar: ***"columns"*** metodu ile veri setindeki sütun isimleri elde edilir.
        Index(['unified_id', 'month', 'zipcode', 'city', 'host_type', 'bedrooms',
            'bathrooms', 'guests', 'revenue', 'openness', 'occupancy',
            'nightly rate', 'lead time', 'length stay'],
            dtype='object')

    - Veriseti Veri Tipleri: ***"dtypes"*** metodu ile veri seti sütunlarındaki verilerin veri tipleri belirlenir.
    
    - Veriseti Hakkında özet Bilgi: ***"info()"*** metodu ile veri seti hakkında özet bilgi çıkarılmıştır.

    - Veriseti İlk 3 Satır: ***"head(3)"*** metodu ile veri setinin ilk 3 satırı ekrana yazdırılır.

    - Veriseti Sütunlarında Eksik Veri Kontrolü: ***"isnull().sum()"*** metodu ile veri setinin sütunlarındaki eksik veriler kontrol edilir.

* ***"describe()"*** metodu ile sadece sayısal sütunlar için bilgiler elde edilir.
    - count: veri sayısı 
    - mean: ortalaması
    - std: standart sapması
    - min: minimum değeri
    - max: maksimum değeri 

* ### **Tip Dönüşümleri**

Veri setinde bazı object tipine sahip değişkenler sayısal bir anlam içermektedir. Bu yüzden bunları int veya float tiplerine dönüştürmek gerekir.
* Aşağıdaki gibi veri tipleri dönüştürülmeli:
    - ***"bathrooms"*** float olarak kalması görünüm için daha iyi
    - ***"guests"*** object fakat sayısal bir değer taşır o yüzden int tipine dönüştüeülmeli. Ayrıca '15+' ifadelerini '16' olarak değiştirilir.
    - ***"revenue"*** object fakat sayısal bir değer taşır o yüzden float tipine dönüştüeülmeli. 
    - ***"occupancy"*** object fakat sayısal bir değer taşır o yüzden float tipine dönüştüeülmeli. 
    - ***"nightly_rate"*** object fakat sayısal bir değer taşır o yüzden float tipine dönüştüeülmeli.
    - ***"lead_time"*** object fakat sayısal bir değer taşır o yüzden float tipine dönüştüeülmeli.
    - ***"length_stay"*** object fakat sayısal bir değer taşır o yüzden float tipine dönüştüeülmeli.

* ### **Kategorik, Kardinal, Sayısal Sütunların Belirlenmesi**


- **Kategorik:** Kategorik değişkenler genellikle "object" türündedirler, birbirinden ayrı kategorilere ait farklı grupları temsil eder. Bu gruplar genellikle belirli bir sınıflandırmaya göre ayrılır ve sütun içindeki her bir değer bir kategoriye aittir. Örneğin, cinsiyet, şehir, posta kodları, ürün tipi gibi değişkenler kategoriktir.

- **Kardinal:** Kardinal değişkenler genellikle "object" türündedirler, bir sütun içindeki benzersiz değerlerin sayısını ifade eder. Yüksek kardinaliteye sahip bir değişken, birçok farklı değere sahip olabilirken, düşük kardinaliteye sahip bir değişken, az sayıda farklı değere sahip olacaktır. Örneğin, müşteri kimlik numarası gibi benzersiz tanımlayıcılar kardinal değişkenlerdir.

- **Sayısal (Numerik):** Sayısal değişkenler genellikle "int64" veya "float64" türündedirler, sayısal değerlerin temsil edildiği değişkenlerdir. Bu değişkenler üzerinde matematiksel işlemler yapılarak analizler gerçekleştirilir. Örneğin, yaş, gelir, sıcaklık gibi değişkenler sayısal değişkenlerdir ve gerçek sayıları temsil ederler.

* Sütunlaradaki eşsiz değerler ve bu eşsiz değerlerin sayısı belirlenir. Bu sayede kategorik ve kardinal verileri ayırabilmek için ***"column_detection"*** adlı fonksiyonda parametre olarak kullanılacak eşik değerler belirlenir.

    - cat_th: Bir sütunun kategorik olarak kabul edilmesi için eşik değeri. 
    - car_th: Bir sütunun kategorik ancak kardinal (yüksek kardinaliteye sahip) olarak kabul edilmesi için eşik değeri. 


## 4) **VERİ TEMİZLEME VE ÖN İŞLEME**

* Bu aşamada veri setinin sütunlarındaki eksik veriler doldurulur ve aykırı değerler yok edilir.

### **Eksik Verilerin Doldurulması** 

* ***"isnull().sum()"*** metodu ile sütunlardaki eksik veriler kontrol edilir. 

    * Orjinal veri setinin, **"revenue"** sütununda **16**, **"nightly_rate"** sütununda **6442**, **"lead_time"** sütununda **8031**, **"length_stay"** sütununda **8031** tane veri eksiktir.

    

- **"revenue"** sütununda eksik değer sayısı çok az olduğu için o değerler silinir.
- **"nightly_rate"** sütunundaki eksik değerler, o sütunun ortalamasıyla doldurulur.
- **"lead_time"** sütunundaki eksik değerler, o sütunun ortalamasıyla doldurulur.
- **"length_stay"** sütunundaki eksik değerler, o sütunun ortalamasıyla doldurulur.


### **Aykırı Verilerin Temizlenmesi**

- IQR (Interquartile Range) yöntemi kullanılarak veri setindeki değerlerin çeyrekliklerine dayanarak aykırı değerler tespit edile bu değerler veri setinden temizlenir.
- Genellikle sayısal sütunlar için uygulanan bir yöntemdir, çünkü temel olarak verilerin dağılımını hesaplamak için istatistiksel kavramlara dayanır.

Aaşağıdaki sütunlar için bu işlemi yapmanın daha mantıklı olacağını düşündüm çünkü farklı değere sahip veri sayısı çok ve aykırı değer olması ihtimal.
* revenue: 21833 
* nightly rate: 20651
* lead time: 4677
* length stay: 671

    - Öncelikle sütunun kutu grafiği çizdirilir.
    - ![Revenue Kutu Grafiği](images/revenue_kutu_grafigi.PNG)

    - "revenue" sütununa ait bu kutu grafiğinde IQR, kutunun alt ve üst sınırlarını belirleyen Q1 ve Q3 değerleri arasındaki uzaklığı temsil eder. daireler aykırı değerleri ifade eder. Grafikteki daireler aykırı değerleri ifade eder.

    - Sonrasında dataframe'de ilgili sütundaki aykırı verilerin temizlenmesi için ***"outliers_remove_with_iqr"*** adlı bir fonksiyon oluşturulur.

    - Bu fonksiyona sütun ismi ve dataframe girdi olarak verilir çıktı olarak ise iligli sütundaki aykırı değerlerin yok edildiği yeni dataframe döndürülür.

    - Seçilen sütunlar için bu fonksiyon kullanılarak veri setinin tamamından aykırı değerler silimiş olur.

</br>
Veri setinde yapılan bu işlemlerden dolayı veri setinin boyutu küçülmüştür.
Veri seti boyutu:  (23597, 14)


## 5) **TEMEL İSTATİSTİKSEL ANALİZLER**

* Veri setinin sayısal sütunları için histogram grafikleri çıkarılmış ve aşağıdaki istatistiksel değerler hesaplanmıştır. Ayrıca grafiklerin ve istatistiksel değerlerin analizleri yapılmıştır.

    - ***"Mod:"*** Bir veri kümesinde en sık tekrar eden değerdir. Mod, veri setinin en yaygın olan noktasını belirtir.

    - ***"Ortalama (Mean):"*** Bir veri kümesindeki tüm değerlerin toplamının veri kümesinin eleman sayısına bölünmesiyle elde edilir. Ortalama, veri setinin merkezini temsil eder.

    - ***"Medyan:"*** Bir veri kümesindeki değerlerin küçükten büyüğe sıralandığında ortadaki değerdir. Eğer veri setinde tek sayıda eleman varsa, medyan tek bir değerdir; ancak çift sayıda eleman varsa, medyan iki ortanca değerin ortalamasıdır. Medyan, veri setinin merkezindeki değeri belirtir.

    - ***"Standart Sapma:"*** Bir veri kümesindeki değerlerin ortalama etrafındaki yayılımını ölçer. Küçük standart sapma, veri noktalarının ortalama etrafında yoğunlaştığını, büyük standart sapma ise veri noktalarının ortalama etrafında daha da yayıldığını gösterir. Standart sapma, veri setinin dağılımını ölçer.

* Analizler için **"statistical_analysis"** adlı bir fonksiyon oluşturulmuştur. Girdi olarak dataframe ve sütun ismini alır çıktı olarak yukarıdaki istatistiksel değerleri hesaplayarak ekrana yazdırır.

* Histogram grafiği için **"his_grap"** adlı bir fonksiyon oluşturulmuştur. Girdi olarak dataframe ve sütun ismini alır çıktı olarak ise o sütuna ait histogram grafiğini çizdirir.


## 6) **VERİ GÖRSELLEŞTİRME**

Oluşturulan grafikler ipynb dosyasında yer almaktadır.

- Şehirlere göre günlük kira ücreti hesaplanır ve sütun grafiği oluşturulur.
    -  Grafiğe göre en fazla gecelik kira ücretinin "Big Bear Lake" şehrinde en azı ise "Joshua Tree" şehrilde olduğu görülür.

- Ev tipi bazında elde edilen gelir incelenir ve sütun grafiği oluşturulur.
    - Grafiğe göre en çok geliri "2-5 Units" ev tipi elde etmektedir.

- Şehir bazında elde edilen gelir incelenir.
    - Grafiğe göre en çok geliri "Yucca Valley" şehri elde etmektedir.

- Ay bazında elde edilen gelir incelenir
    - Grafiğe göre en çok geliri "2019-12" ay elde etmektedir.

- Yatak odası sayısına göre ortalama gecelik kira ücreti hesaplanır ve sütun grafiği oluşturulur.
    - Grafiğe göre 5 tane yatak odasına sahip evlerin gecelik kira ücretinin diğer şehirlerden fazla olduğu görülür. 
    - Oda sayısı arttıkça gecelik kira ücreti de artmaktadır. 

- Şehirler bazında günlük kira ücreti ve doluluk oranını incelenir ve FacetGrid 
    - Grafiğe göre en fazla doluluk oranının "Big Bear Lake" şehrinde, en az doluluk oranın ise "Yucca Valley" şehrinde olduğu görülmektedir.
    - Doluluk oranı arttıkça gecelik kira ücretinin her şehirde azaldığı görülür. 
    - Her şehirde gecelik kira ücreti 100-300 civarında yoğunlaşmıştır.

- Şehirler ve ev tiplerine göre ortalama günlük kira ücretini incelenir ve pivot tablosu oluşturulur.
    - Tabloya göre en yüksek ortalam gecelik kira ücreti "Big Bear Lake" şehrindeki "Professionals" ev tipine sahip airnbnblere ait olduğu görülür.
    - Tabloya göre en yüksek ortalam gecelik kira ücretinin ise "Joshua Tree" şehrindeki "Single Owners" ev tipine sahip airnbnblere ait olduğu görülür.

- Şehir bazında airbnb mülk sayısının heasplanır ve pasta grafiği oluşturulur.
    - Grafiğe göre en çok airnbn sayısı "Big Bear Lake" şehrinde, en az ise "Yucca Valley" şehrinde olduğu görülmektedir.


<span style="color: yellow;">
Bu zaman kadar kullanılan ve temizlenmiş verilerin bulunduğu dataframe, "clean_market_analysis_201" adlı bir CSV dosyasında kaydedilir. Bunun nedeni veriler üzerinde yapılacak değişiklerde yapılan hatalar yüzünden diğer bütün işlemleri tekrarlamamak.
</span>


## 6) **ÖZELLİK MÜHENDİSLİĞİ (FEATURE ENGINEERING)**

Var olan özellikler kullanılarak yeni özellikler oluşturulur. 

"clean_market_analysis_201.csv" dosayası okunarak temizlenmiş veri elde edilir.

* "month" sütunu bugünden çıkarılarak kaç aydır airbnb mülkünün verisetinde yer aldığı bulunur ve *"months_difference"* adlı yeni sütuna bu değerler eklenir.
* Aylara göre doluluk oranlarını hesaplanır ve *"monthly_avg_occupancy"* adlı yeni sütuna bu değerler eklenir.
* Aylık kira ücretinin hesaplanması ve *"monthly_rate"* adlı yeni sütuna bu değerler eklenir.

## 8) **DEĞİŞKENLER ARASINDAKİ İLİŞKİLERİN ANALİZİ**

### One-Hot Encoding

One-hot encoding, kategorik değişkenlerin sayısal formatta temsil edilmesi için kullanılan bir yöntemdir ve değişkenler arasındaki ilişkilerin daha iyi analiz edilebilmesi için bu kategorik değişkenlerin dönüştürülmesi gerekir.

Sayısal formatta olmayan one-hot encoding uygulanacak kategorik değikenler: ['month', 'city', 'host_type']

Sayısal formata çevirilecek değişkenler hedef değişken yani "revenue" ile ilişkili bir şekilde çevrilir.

### **Korelasyon Matrisi**

Bir veri setindeki sayısal değişkenler arasındaki ilişkileri gösteren bir matristir.

* 1'e yaklaşan bir korelasyon katsayısı, pozitif bir ilişkiyi gösterir. Yani, bir değişkenin değeri arttığında diğer değişkenin de artma eğiliminde olduğunu ifade eder.
* -1'e yaklaşan bir korelasyon katsayısı, negatif bir ilişkiyi gösterir. Yani, bir değişkenin değeri arttığında diğer değişkenin azalma eğiliminde olduğunu ifade eder.
* 0'a yaklaşan bir korelasyon katsayısı, değişkenler arasında bir ilişki olmadığını veya çok zayıf bir ilişki olduğunu gösterir.

***"corr_matrix"*** adlı fonksiyon kullanılarak veri setindeki sayısal sütunlara ait korelasyon matrisi elde edilir.

Elde edilen korelasyon matrisi:

![Korelasyon Matrisi](images/korelasyon_matrisi.png)

Korelasyon matrisindeki sütunlar arasındaki korelasyon değerlerinin 1'e ve -1'e yaklaşması, sütunlar arasında pozitif ve negatif ilişkinin yüksek olmasını gösterir.

- Her sütunun kendisi ile arasındali ilişki zaten 1'dir.

- "month" ile "monthly_avg_occupancy" arasında 0.84'lük bir pozitif ilişki vardır.
- "revenue" ile "occupancy" arasında 0.81'lik bir pozitif ilişki vardır.
- "quest" ile "bedrooms" arasında 0.60'lık bir pozitif ilişiki vardır.

- "city" ile "zipcode" arasında -0.65'lik bir negatif ilişki vardır.
- "revenue" ile "length_stay" arasında -0.38'lik bir negatif ilişki vardır.
- "length_stay" ile "occupancy" arasında -0.39'luk bir negatif ilişki vardır.


### **Özellik Seçimi (Feature Selection)**

Makine öğrenimi modeli oluştururken, belirli özelliklerin seçilmesi gereklidir. Sayısal olmayan ifadeler makine öğrenimi modellerinde genellikle yok sayılır. Ayrıca, sayısal ifadeler arasında da hedef değişkeni (bağımlı değişken) etkilemeyen değişkenler model başarısını olumsuz etkileyebilir.

Bu bağlamda, hedef değişken olarak elde edilen gelir miktarını ifade eden "revenue" sütunu seçilir. Diğer sütunlar ise bağımsız değişkenler olarak değerlendirilir. Ancak, bazı değişkenler "revenue" ile çok ilişkili değildir. En ilişkili değişkenleri belirlemek için korelasyon matrisine bakılır ve düşük ilişkiye sahip sütunlar veri setinden çıkarılarak makine öğrenimi modeli için uygun bir veri seti oluşturulur.

Korelasyon matrisine bakıldığında "revenue" sütunu ile 0.1'den büyük veya -0.1'den küçük korelasyona sahip olan değişkenler belirlenir. Bu değişkenler:

- **occupancy**: 0.81
- **length_stay**: -0.35
- **month**: 0.21
- **openness**: 0.20
- **monthly_avg_occupancy**: 0.18
- **nightly_rate**: 0.17
- **monthly_rate**: 0.17
- **guests**: 0.12

Bu özellikler, makine öğrenimi modeli için bağımlı değişkeni etkileyen bağımsız değişkenler olarak seçilebilir.

Özetle, "revenue" sütunu ile belirgin ilişkiye sahip olan yukarıdaki değişkenler, modelde kullanılacak özellikler olarak seçilir ve diğer özellikler veri setinden çıkarılır. Bu şekilde, model başarısını artıracak, daha anlamlı ve etkili bir veri seti elde edilir.

<span style="color: yellow;">
Seçilen özellikler ile yeni bir dataframe oluşturulur ve bu dataframe daha sonrasında makine öğrenimi modellerinde kullanmak için veri "market_analysis_2019_for_ML" adlı yeni bir CSV dosyasına kaydedilir.
</span>
