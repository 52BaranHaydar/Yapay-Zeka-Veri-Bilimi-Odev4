# Yapay Zeka ve Veri Bilimi Proje Raporu

**Ders / Program:** Social Office — Yapay Zeka Mesleki Gelişim Programı  
**Proje Konusu:** Günlük Hayatta Karşılaşılan Problemlerin Yapay Zeka ile Çözümü  
**Proje Adı:** Akıllı Şehir İçi Trafik ve Toplu Taşıma Optimize Sistemi (AI-Trafik)  
**Hazırlayan:** Yapay Zeka ve Veri Bilimi Katılımcısı  
**Tarih:** Ağustos 2026  

---

## 1. Giriş ve Problem Tanımı

### 1.1. Problemin Tanımı
Günümüz büyükşehirlerinde yaşanan en büyük günlük sorunlardan biri şehir içi trafik sıkışıklığıdır. Mevcut sinyalizasyon sistemleri sabit zaman aralıklarına göre (örneğin her yöne 45 saniye) çalıştığı için, bir şeritte hiç araç yokken diğer şeritte kilometrelerce araç kuyruğu oluşabilmektedir. Bu durum sürücüler için ciddi zaman kaybı ve stres yaratmaktadır.

### 1.2. Etkilenen Kitle ve Etkileri
Bu sorun her gün işe ve okula gitmek zorunda olan milyonlarca sürücüyü, toplu taşıma yolcularını, lojistik firmalarını ve acil durum araçlarını (ambulans, itfaiye) doğrudan etkilemektedir.

### 1.3. Problemin Temel Nedenleri
* Sabit zamanlı trafik lambalarının anlık araç yoğunluğunu ölçememesi.
* Beklenmeyen kaza veya yol çalışmaları durumunda sinyal sürelerinin otomatik güncellenememesi.
* Şehirlerdeki araç sayısının altyapı kapasitesinden daha hızlı artması.

### 1.4. Çözümün Önemi
Trafik sıkışıklığının azaltılması sadece bireysel bekleme sürelerini düşürmekle kalmaz; gereksiz rölanti çalışmayı engelleyerek yakıt tasarrufu sağlar ve şehirdeki karbon salınımını belirgin şekilde azaltır.

### 1.5. Kısa ve Uzun Vadeli Etkiler
* **Kısa Vadede:** Sürücülerin yolda geçirdiği süre azalır, günlük stres seviyesi düşer ve kavşaklardaki gereksiz kuyruklar engellenir.
* **Uzun Vadede:** Şehir içi hava kalitesi artar, yakıt ithalatı ve ekonomik kayıplar azalır, toplu taşıma kullanımı teşvik edilmiş olur.

### 1.6. Çözülmemesi Durumunda Ortaya Çıkacak Riskler
Trafik sorunu çözülmediği takdirde şehir içi hava kirliliği kritik seviyelere ulaşacak, ekonomik verimlilik kaybı artacak ve acil müdahale araçlarının olay yerine ulaşma süreleri uzayarak can güvenliği riski yaratacaktır.

### 1.7. Coğrafi ve Demografik Boyut
Problem özellikle nüfusu 500 binin üzerinde olan büyükşehirlerde ve ana arter kavşaklarında yoğunlaşmaktadır. Sabit mesai saatlerinde (07:30 - 09:30 ve 17:30 - 19:30) pik noktaya ulaşmaktadır.

### 1.8. Var Olan Çözümler ve Yetersizlikleri
Mevcut mobil navigasyon uygulamaları (Yandex, Google Maps) alternatif rotalar sunabilse de kavşaklardaki trafik lambası sürelerini değiştiremezler. Manuel trafik polis kontrolü ise her kavşak için sürdürülebilir değildir.

---

## 2. Veri ve Analiz

### 2.1. İhtiyaç Duyulan Veriler
* **Trafik Kamera Görüntüleri:** Kavşaklardaki anlık araç sayıları ve araç tipleri (otomobil, otobüs, kamyon).
* **Anlık Bekleme Süreleri:** Araçların kırmızı ışıkta ortalama bekleme süresi.
* **Geçmiş Yoğunluk Verileri:** Günün saatlerine ve haftanın günlerine göre geçmiş trafik oranları.
* **Toplu Taşıma Konum Verileri:** Otobüslerin anlık konum ve doluluk oranları.

### 2.2. Veri Kaynakları
Veriler belediye ulaşım yönetim merkezleri (UKM) kameralarından, açık veri portallarından ve araç içi GPS sinyallerinden anonim olarak elde edilecektir.

### 2.3. Teknik ve Lojistik Zorluklar
Şiddetli yağmur, sis veya gece karanlığında kamera görüntülerinin kalitesinin düşmesi ve sensör arızaları en büyük teknik zorluklardır.

### 2.4. Veri Gizliliği, Güvenliği ve Etik Kullanımı
Kamera görüntülerindeki araç plakaları ve sürücü yüzleri yapay zeka tarafından işlendiği anda otomatik olarak bulanıklaştırılacak (`anonymization`), hiçbir kişisel veri kaydedilmeyecektir (KVKK uyumlu).

### 2.5. Toplanan Verilerin Sağladığı İçgörüler
Veriler sayesinde hangi kavşağın günün hangi saatinde ne kadar kapasiteye ihtiyaç duyduğu ve hangi yönün önceliklendirilmesi gerektiği net olarak ortaya konulacaktır.

### 2.6. Eksik veya Kalitesiz Veri Yönetimi
Kamera arızası veya hava muhalefeti durumunda yapay zeka modeli geçmiş verileri ve komşu kavşakların yoğunluğunu kullanarak eksik verileri tahmin (`imputation`) edecektir.

### 2.7. Çelişkili Verilerin Yönetimi
Farklı kaynaklardan gelen veriler arasında çelişki olması durumunda doğrudan kavşak kamerasından alınan anlık görüntü verisine öncelik verilecektir.

---

## 3. Çözüm Önerileri Geliştirme

### 3.1. Çözüm Önerimiz (AI-Trafik)
Geliştirilecek **AI-Trafik** sistemi, kavşaklardaki kameralardan alınan canlı görüntüleri işleyerek şeritlerdeki araç sayısını anlık tespit eder. Yoğun olan şeride yeşil ışık süresini otomatik olarak uzatır, boş olan şeridin kırmızı ışık süresini kısaltır.

### 3.2. Uygulanabilirlik ve Maliyet Gereksinimleri
Şehirdeki mevcut altyapı ve kameralar kullanılacağı için donanım maliyeti düşüktür. Ana maliyet yapay zeka yazılımı ve merkezi sunucu entegrasyonudur.

### 3.3. Avantajlar ve Olası Dezavantajlar
* **Avantajlar:** Ortalama bekleme süresinde %25-30 azalma, yakıt tasarrufu, düşük emisyon.
* **Dezavantajlar:** İlk kurulum aşamasında yazılım entegrasyonu ve test süreci gerektirir.

### 3.4. Başarı Metrikleri
* **Kavşak Bekleme Süresindeki Düşüş (%):** Hedeflanan en az %20 azalma.
* **Ortalama Araç Hızı:** Pik saatlerde ortalama hızın 15 km/s'den 25 km/s'ye çıkarılması.
* **Karbon Emisyonu Azalması:** Rölanti süresinin kısalmasıyla %10 emisyon tasarrufu.

### 3.5. Test Yöntemleri
Sistem ilk aşamada belirlenen 2 pilot kavşakta bilgisayar simülasyonu ile test edilecek, ardından 30 günlük saha denemesi ile doğrulanacaktır.

### 3.6. Sürdürülebilirlik Planı
Sistem sürekli öğrenen yapay zeka modelleriyle desteklenecek, yeni açılan yollar ve değişen şehir yapısına göre kendini güncelleyecektir.

---

## 4. Yapay Zeka Entegrasyonu

### 4.1. Yapay Zekanın Rolü
Yapay zeka, kameradan gelen görüntü içerisindeki araçları tespit eder, sayar ve en uygun yeşil ışık süresini hesaplayarak trafik sinyalizasyon kutusuna anlık komut gönderir.

### 4.2. Kullanılan Yapay Zeka Yöntemleri
* **Bilgisayarlı Görü (Computer Vision / YOLO):** Görüntüden araç tespiti ve sınıflandırılması.
* **Pekiştirmeli Öğrenme (Reinforcement Learning):** En uygun ışık süresini deneme-yanılma ve ödül mekanizmasıyla öğrenen algoritmalar.

### 4.3. Hız ve Verimlilik Katkısı
Geleneksel sistemler değişen trafiğe tepki veremezken, yapay zeka sistemi her 5 saniyede bir durumu değerlendirerek anında karar alır.

### 4.4. Karşılaşılabilecek Zorluklar
Gece görüşü, aşırı parlak ışık yansımaları veya nesne engellemeleri modelin doğruluğunu etkileyebilir.

### 4.5. Gerçek Zamanlı Çalışma
Sistem 50 milisaniye tepki süresi ile tam gerçek zamanlı (`real-time`) olarak çalışır.

### 4.6. Manuel Yöntemlere Göre Avantajları
İnsan operatörlerin tüm şehirdeki yüzlerce kavşağı aynı anda izlemesi imkansızdır. AI sistemi 7/24 kesintisiz ve hatasız analiz yapar.

### 4.7. Ölçeklenebilirlik
Yazılım altyapısı modüler olduğu için küçük bir beldeden 15 milyonluk bir metropolün tamamına kadar ölçeklenebilir.

---

## 5. Sonuç ve Öneriler

### 5.1. Bireysel ve Toplumsal Faydalar
Sürücüler günde ortalama 20-30 dakika zaman kazanacak, şehir içi hava kirliliği düşecek ve ambulans gibi acil araçlar olay yerine daha hızlı ulaşacaktır.

### 5.2. Mesleki ve Bireysel Katkılar
Bu proje, şehir planlamacıları ve belediye yöneticileri için veriye dayalı karar alma imkanı sunar.

### 5.3. Sürdürülebilirlik ve Uzun Vadeli Etkiler
Akıllı şehir vizyonunun temel bir parçası olarak daha yaşanabilir ve çevreci şehirler oluşmasına katkı sağlayacaktır.

### 5.4. Geliştirme Önerileri
İlerleyen aşamalarda toplu taşıma otobüslerine yaklaştıklarında otomatik yeşil ışık önceliği veren akıllı geçiş modülü eklenmelidir.
