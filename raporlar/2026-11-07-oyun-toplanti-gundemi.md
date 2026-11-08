# Oyun ekibinden toplantı gündemi · 7 Kasım 2026

Muhammed'in G0 Android denemesinden çıkan konular. Deneme POCO X5 Pro 5G'de (Android 14) yapıldı; altın set destesiyle üç tam oyun dokunarak oynandı.

- Ayrıntılar ve denetim listesi: Game [`docs/android_g0.md`](https://github.com/IleriProgramlamaProje/Game/blob/main/docs/android_g0.md)
- Kod: Game [PR #1](https://github.com/IleriProgramlamaProje/Game/pull/1), 7 Kasım'da `main`'e alındı; Kara inceleyip yorum yazabilir.

Onaylanan maddeler `kararlar.md`'ye yazılır.

## Duyuru

1. **Oyun dikey.** Muhammed 7 Kasım'da karar verdi:
   - Telefonda ekran dikeye kilitli. Temel boyut 360×640, telefonda ekran yaklaşık 360×800 birim.
   - Masaüstü pencere 450×800 açılır ve büyütülebilir.
   - Neden: yatay telefonda kartın altı ekrandan taşıyordu.

## Konuşulacaklar

2. ✅ **8 Kasım'da çözüldü:** Kara'nın kayıt sistemi birleşince geri tuşu oyun ortasında "Kaydet ve Ana Menüye Dön" ile aynı işi yapıyor; ilerleme kaybolmuyor. Aşağıdaki not tarihçe için duruyor.

   **Oyun ortasında geri tuşu.** Kart ve sonuç ekranında Android geri tuşu bilerek hiçbir şey yapmıyor; ilerleme kazara kaybolmasın diye. Ekrandaki "Ana Menüye Dön" de yalnız oyun sonunda açık.
   - Onaylı bir çıkış ("Oyundan çıkılsın mı?") istenirse kayıt özelliğiyle (3.9) birlikte konuşulmalı.
   - Diğer ekranlarda geri tuşu ana menüye döner; ana menüde uygulamadan çıkar.
3. **Denge.** Telefonda oynanan üç oyunun üçü de "Para İsyanı" ile bitti: 9, 13 ve 18 kararda. Hazine çok hızlı tükeniyor.
   - ~~Ayrıca her oyun aynı kartla başlıyor~~ — 8 Kasım'da çözüldü: her hükümdarlık destenin rastgele bir olayından başlıyor. 8 Kasım'daki ikinci oyun "Halk İsyanı" ile bitti, yani sonlar çeşitleniyor; denge yine de ölçülmeli.
   - İlgili görevler: 4.9 denge testi ve 3.7 kart seçici.
4. **Release APK için imza anahtarı.** Şimdilik yalnız debug APK var. 3.10'dan önce karar verilmeli:
   - anahtarı kim üretecek;
   - nerede saklanacak;
   - parolayı kim bilecek.

   Anahtar ve parola Git'e girmez.
5. **Kart kuralı farkı.** İki ekip farklı kural uyguluyor:

   | | Metin | Karar |
   |---|---|---|
   | Oyun ve `kart_formati.md` | 20–50 kelime | 2–5 kelime |
   | YZ filtresi (`yz_gorevleri.md`) | 12–50 kelime | 1–6 kelime |

   Bu fark yüzünden altın setteki 1.448 kartın 103'ü oyuna giremedi. İki ekip tek kurala bağlanmalı. `kart_formati.md` iki ekibin ortak dili olduğu için birlikte değiştirilir; Python ve C# doğrulayıcıları da aynı anda güncellenir.

## Muhammed'e kalanlar

6. Kendi altın set kart üretimi.
7. Karakter kör tahmin testi.
8. Bu sayfadaki maddelerin toplantıda onaylanması.
