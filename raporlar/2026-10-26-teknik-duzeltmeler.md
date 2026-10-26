# Teknik düzeltmeler · 26 Ekim 2026

Mevcut yerel çalışmalar önce Docs `1276eed`, Game `65617d8` commit'leriyle GitHub'a gönderildi; AI o aşamada zaten günceldi.

## Düzeltmeler

- AI kardeş Docs deposunu bağlantı gerektirmeden bulur; özel dizin desteklenir.
- Kart konu dağılımı yaklaşık %15 serbest hedefini karşılar; öğretmen promptu etiketli kart gövdesi ister.
- Sabit tohumla devam önceki malzemeleri yeniden kullanmaz. Geçersiz grup boyutu, bozuk/uyumsuz JSONL, eski kayıt sürümü ve eksik/boş motor cevabı açık hata verir. Yeni kayıt sürümü 2; eski dosyalar korunup yeni dosyada üretime başlanır.
- Colab AI ve Docs depolarını ayrı klonlar; mevcut klasörü silmez, kimlik bilgilerini URL'ye yazmaz. Hız ölçümü yeni dosya kullanır.
- Güncel rehberler Godot ve üç depo düzenini anlatır. Önceki Unity kurulum araştırması arşivlenmiştir; geçmiş karar/deney raporları değiştirilmemiştir.

## Doğrulama

- AI: 11 test geçti; ayrıca temiz geçici AI + Docs yerleşiminde, sembolik bağlantı olmadan aynı 11 test geçti.
- İki notebook'un tüm kod hücrelerinin sözdizimi kontrol edildi; kayıtlı çıktılar temiz.
- Game C# derlemesi: 0 hata, 0 uyarı. Godot headless sahne testi: üç boyutta dört panel başarılı. Bu düzeltme turunda oyun kaynak kodu değiştirilmedi.
- `git diff --check`: üç depoda başarılı.

## Açık işler

Gerçek Colab/GPU üretimi ve paket sabitleme, gerçek dokunma/klavye etkileşimi, ikinci geliştirici kurulumu ve Android APK doğrulaması henüz yapılmadı. Model, filtre, kart dönüştürücü ve sunucu planlanan işlerdir. Rol/konu anahtarlarının normalizasyonu, aynı turda birden çok sonun önceliği ve hedef yıl gibi ürün kararları bu teknik düzeltmeyle kesinleştirilmedi.
