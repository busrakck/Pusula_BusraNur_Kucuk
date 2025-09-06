
# EDA & Veri Ön İşleme Raporu

**Ad Soyad:** [Büşra Nur Küçük]  
**E-posta:** [busranurrkucuk@gmail.com]  

## 1. Keşifsel Veri Analizi (EDA)

### Eksik Değerler
- Bazı sütunlarda eksik değerler bulundu.
- `TedaviSuresi` ve `UygulamaSuresi` sütunları sayısal değerler yerine metin içeriyordu (örn. "5 Seans", "10 dk"). Bu nedenle regex ile sayılar ayıklandı.

### Sayısal Değişkenler
- **Yaş (Yas):** Daha çok genç bireylerde yoğunlaşma var.
- **Tedavi Süresi (TedaviSuresi):** Çoğunluk kısa süreli tedavi görmüş, az sayıda uzun tedavi vakası mevcut.
- **Uygulama Süresi (UygulamaSuresi):** Düşük değerlerde yoğunlaşma gözlendi.

### Korelasyon
- `TedaviSuresi` ile `UygulamaSuresi` arasında pozitif korelasyon bulundu.
- `Yas` ile diğer değişkenler arasında güçlü ilişki yok.

### Kategorik Değişkenler
- **Cinsiyet:** Dağılım eşit değil.
- **Kan Grubu:** 8 farklı tip standardize edildi.
- **Uyruk:** Çoğunluk Türk vatandaşlarından oluşuyor.
- **Bölüm:** Bazı bölümlerde yoğunluk var.
- **Tedavi Adı:** Belirli tedaviler öne çıkıyor.

### Çok-Değerli Değişkenler
- `KronikHastalik`, `Alerji`, `Tanilar`, `UygulamaYerleri` birden fazla değer içerebilir.
- En sık görülenler: Astım, Diyabet (KronikHastalık), Toz Alerjisi (Alerji).

---

## 2. Veri Ön İşleme (Preprocessing)

### Sayısal Dönüşümler
- `TedaviSuresi` ve `UygulamaSuresi` → regex ile sayılar çıkarıldı.
- Eksik değerler median ile dolduruldu.
- StandardScaler ile normalizasyon yapıldı.

### Kategorik Dönüşümler
- **Tek-değerli kategorikler** → One-Hot Encoding  
  *Neden?* Sıralı anlamları yok, model bunları bağımsız kategoriler olarak görmeli.  
- **Çok-değerli kategorikler** → Multi-hot Encoding  
  *Neden?* Bir satırda birden fazla değer olabiliyor. Multi-hot encoding sayesinde her olasılık ayrı bir sütun olarak işaretlendi (0/1).  

### Eksik Veri Doldurma
- Sayısal → median  
- Kategorik → en sık görülen değer  

### Pipeline
- Tüm adımlar sklearn Pipeline içine alındı.
- Yeni gelen veri için aynı dönüşümler kolayca uygulanabilir.

### Çıktılar
- `dataset_model_ready.csv` → işlenmiş veri seti  
- `model_ready_preprocess.joblib` → pipeline objesi  

---

## 3. Özet
- Veri başlangıçta eksik ve metinsel sayılar içeriyordu.  
- EDA ile dağılımlar, korelasyonlar ve kategorik yoğunluklar incelendi.  
- Ön işleme süreci ile veri temizlendi, encode edildi ve modellemeye hazır hale getirildi.  
