# Dönem 1 · Oyun · Başkan: Kara (Ömer) · Yardımcı: Muhammed

**Dönem:** 26 Ekim–8 Kasım 2026 · **Durum tarihi:** 8 Kasım 2026 · Game `main` `fba6c30`

> Bu rapor iki raporun birleşimidir (8 Kasım): Kara'nın Game deposuna yazdığı dönem raporu (`docs/raporlar/donem-1-oyun.md`, `kara` `17c5030`) ve Muhammed'in buradaki taslağı. Son okumayı Kara yapar.

## Ne yapıldı (dosya yollarıyla)

Depo: [Game](https://github.com/IleriProgramlamaProje/Game) · Godot 4.7.2 .NET + C# (masaüstü `net10.0`, Android `net9.0`). Oyunun adı **BUYRUK** (`kararlar.md`, 7 Kasım). Dosya yolları `game/` altındadır.

**Kara'nın özeti:** BUYRUK, 600 Altın Set kartıyla açılıştan oyun sonuna kadar çevrimdışı oynanıyor. Muhammed'in 2.8–2.9 çalışması ve Android düzeltmesi temel alındı; Kara'nın kayıt/yükleme, rekor ve yerleşim çalışması bu temelin üzerine eklendi.

**Dönemin akışı**

- **Kurulum ve plan** (26 Eki, Muhammed): Godot projesi ve C# ortamı, `docs/oyun_gelistirme_plani.md`, ilk sahne iskeleti testi.
- **H1 · 1.8–1.13** (1 Kas, Kara): oyun durumu ve göstergeler (`Betikler/Oyun/OyunDurumu.cs`, `Betikler/Arayuz/Gostergeler.cs`), yerel yedek deste (`Betikler/Kartlar/YedekDeste.cs`), kart görünümü (`KartGorunumu.cs`), kaydırma (`KaydirmaKontrolu.cs`), açılış (`AcilisEkrani.cs`), oyun akışı (`OyunYoneticisi`, `OyunDurumu.cs` içinde).
- **BUYRUK arayüzü** (6 Kas, Kara): ana menü ve alt ekranlar (`Sahneler/AnaMenu.tscn`, `YeniOyun`, `KayitliOyunlar`, `Ayarlar`, `Credits`; `MenuSahnesi.cs`), gösterge bileşenleri (`GostergeBileseni.cs`), sürüklemeli deste kartı. Not: `docs/buyruk_arayuz_ve_kart_guncellemeleri.md`.
- **Birleşme 1** (7 Kas, Muhammed, `657dbf4`): `kara` + Assets teması. Düzeltilen hatalar:
  - çıkış animasyonu kararı kaybettiriyordu;
  - deste kartları `AddChild` hatası veriyordu;
  - kart yüksekliği yanlış hesaplanıyordu;
  - dar ekranda menü taşıyordu.

  Eklenenler: klavyeyle karar (← → Enter), kalıcı ses/tam ekran ayarı, `MenuTesti`.
- **G0 · Android denemesi** (7 Kas, Muhammed, PR #1): debug APK gerçek telefonda (POCO X5 Pro 5G, Android 14, arm64) kuruldu; üç tam oyun dokunarak, modelsiz oynandı. Sekiz sorun bulundu, düzeltildi ve testlere eklendi. Başlıcaları:
  - Android'de C# derlenmiyordu (C# 13).
  - Oyun yatay açılıyordu; artık **dikey**, 360×640.
  - Dokunmayla ses kaydırıcısı ve sayfa kaydırma çalışmıyordu.
  - Geri tuşu uygulamayı kapatıyordu.
  - Dikeyde oyun ekranı sığmıyordu.
  - Kamera deliği sayacın üstüne denk geliyordu.

  Not: Game `docs/android_g0.md`.
- **Kayıt, rekor, deste kimlikleri** (7 Kas, Kara, `kara` `17c5030`):
  - Her yeni hükümdarlık ayrı bir kayıt alır (`user://hukumdarliklar/`).
  - Kayıtlı Oyunlar ekranından bekleyen karta veya karar sonucuna dönülür.
  - Bozuk kayıt sağlam kayıtları engellemez.
  - Tamamlanan hükümdarlıklar geçmiş ve rekor bölümüne girer.
  - Kartlara kalıcı olay kimliği, isteğe bağlı olay grubu ve YZ kartı için yedekli kaynak eklendi.

  Dosyalar: `Betikler/Oyun/OyunKayitDeposu.cs`, `OyunAnligi.cs`, `HukumdarlikGecmisi.cs`, `Betikler/Arayuz/KayitliOyunlarEkrani.cs`, `Betikler/Kartlar/YedekliKartKaynagi.cs`, `Araclar/DesteDogrulama.tscn`, `Testler/OturumKaydiTesti.tscn`, `Testler/DengeTesti.tscn`. Ayrıntı: Game `docs/BUYRUK_DEVELOPMENT_REPORT.md`.
- **Birleşme 2** (8 Kas, Muhammed, PR #2, `fba6c30`): Kara'nın kayıt/rekor çalışması `main`'e alındı ve telefonda denendi. Üstüne eklenenler:
  - geri tuşu oyun ortasında kaydedip menüye döner;
  - her hükümdarlık destenin rastgele bir olayından başlar;
  - son ekranı rekoru gösterir.

  Not: Game `docs/android_g0.md`, 8 Kasım bölümü.

**H2 görevleri**

| Görev | Kim | Durum | Uygulama |
| --- | --- | --- | --- |
| **2.5 — Karar sonucu** | Muhammed (2 Kas) | Tamamlandı | Seçilen kararın sonucu ve gösterge etkileri gösteriliyor. **Devam Et** sonraki karta veya sona götürüyor; sınırda biten kararda önce sonuç gösteriliyor. `Sahneler/Oyun.tscn`, `Betikler/Arayuz/OyunEkranlari.cs` |
| **2.6 — Sekiz son ve yeniden oynama** | Muhammed (2 Kas) | Tamamlandı | Dört göstergenin 0 ve 100 değerleri sekiz sona karşılık geliyor; aynı kararda birden çok sınır tetiklenirse hepsi gösteriliyor. **Tekrar Oyna** temiz hükümdar seçimine dönüyor. `Betikler/Cekirdek/SonKontrolu.cs`, `Veri/tema.json` |
| **2.7 — Yıl sayacı** | Muhammed (2 Kas) | Tamamlandı | 5 kabul edilmiş karar 1 yıl; önizleme ve **Devam Et** karar sayılmıyor. `Betikler/Cekirdek/YilSayaci.cs` |
| **2.8 — Altın Set yedek destesi** | Muhammed (7 Kas) | Tamamlandı | 600 kart varsayılan deste (`Veri/yedek_deste.json`); 23 rolün hepsi var; `kaynak: altin_set`, `lisans: sadece_ders` korunuyor. Üretici: `araclar/deste_olustur.py` |
| **2.9 — Modelsiz tam oyun** | Muhammed (7 Kas) | Tamamlandı | Varsayılan desteyle açılış, karar, sonuç, son ve yeniden başlama; masaüstünde ve telefonda. `Testler/SahneIskeletiTesti.tscn` |

**Altın Set kaynağı:** AI deposunun `22a71a2` revizyonundaki `data/altin_set/ham/altin_set.json`. 1.448 kartın 1.345'i oyun doğrulamasını geçti. `deste_olustur.py`, 600 kartı hedef metin uzunluğu ve rol dengesiyle seçiyor. 2 Kasım kararıyla kartlar çapraz okuma yerine otomatik kontrolle kabul ediliyor. Eski 10 örnek kart regresyon testleri için `Testler/Veri/ornek_deste.json` altında.

**Devir paketi** (yol haritası 3.2): "Yedek desteyle baştan sona oynanabilen oyun (açılış, kaydırma, sonuç ekranı, 8 son)" var. Masaüstünde ve Android telefonda, `main`'de altın set destesiyle oynanıyor; kayıt ve rekor da hazır.

## Ne yarım kaldı, neden

- **İnceleme:** PR #1 ve PR #2, Kara'nın incelemesinden önce `main`'e alındı. Daha önceki H1–H2 ve 7 Kasım birleşmesi de doğrudan `main`'e girmişti. Kara, PR #2'de inceleyici; PR'lar birleşmiş olsa da yorum yazılabilir. Plan kutuları (1.7–2.9, G0) inceleme gelene kadar işaretsiz.
- **İkinci bilgisayar (1.7):** "İki geliştiricinin bilgisayarında açılır" şartı. Kara'nın Windows bilgisayarında 7 Kasım'da kendi birleşik sürümü derlendi (0 uyarı, 0 hata) ve 12 başsız testin 12'si geçti; Muhammed'in Linux bilgisayarında `main` geçiyor. Güncel `main`'in (`fba6c30`) Windows'ta bir kez daha denenmesi iyi olur.
- **G0 Android denemesi:** H1'de yapılacaktı; dönemin son günlerinde (7–8 Kasım) yapıldı. Bu gecikme yüzünden Android'de C# derlenmediği de ancak o zaman görüldü. Release çıktısı (imza anahtarı ekip kararı) ve ikinci telefon 3.10'a kaldı.
- **Sonraki dönemin işleri** (yarım değil, plan gereği):
  - Kazanma kuralı (3.8): kayıt ve rekor hazır, `hedef_yil` hâlâ `null`. Kara'nın geliştirme raporunda iki seçenek var: açık uçlu rekor ya da süreli "Altın Çağ".
  - Rol–konu seçimi (3.7).
  - Ses (4.8): ayar hazır, ses dosyası yok.
  - Sonlara özel görseller (4.7): şimdilik ortak taç.

## Nasıl çalıştırılır

Ayrıntı: Game `README.md`. Game repo kökünden:

```sh
git lfs pull                                  # PNG görselleri
dotnet build game/Game.csproj                 # 0 uyarı / 0 hata beklenir
<godot-net> --headless --path game --editor --import   # ilk açılışta içe aktarma
<godot-net> --path game                       # oyun (ana sahne AnaMenu.tscn)
for t in game/Testler/*.tscn; do <godot-net> --headless --path game "res://Testler/$(basename "$t")" || echo "BAŞARISIZ: $t"; done
<godot-net> --headless --path game res://Araclar/DesteDogrulama.tscn -- res://Veri/yedek_deste.json 600
python3 araclar/deste_olustur.py              # altın set güncellenince desteyi yenile
```

`<godot-net>`: Godot 4.7.2 **.NET** çalıştırılabilir dosyası (Steam/standart sürüm C# içermez). Oynama yolu **Yeni Oyun → Başla → Beyim/Hatunum**. Kontroller: sürükle-bırak; klavyede ← → önizler, Enter onaylar, Esc vazgeçer; telefonda geri tuşu ekrandaki düğmelerle aynı işi yapar. İlerleme otomatik kaydedilir, **Kayıtlı Oyun**'dan sürdürülür.

Telefon (Android): `<godot-net> --headless --path game --export-debug "Android" ../exports/buyruk.apk` ve `adb install -r exports/buyruk.apk`. SDK/JDK ayarı, Xiaomi'deki "USB üzerinden yükle" izni ve denetim listesi: Game `docs/android_g0.md`.

## Büyük dosyalar nerede (Drive / Hugging Face)

- Arayüz PNG'leri Game deposunda **Git LFS** ile (104 dosya, ~25 MB), `game/Assets/ui/` altında. Klonladıktan sonra `git lfs pull`.
- Oyun Drive/Hugging Face kullanmaz. Deste ve tema `game/Veri/` içinde paketlenir; oynamak için model ağırlığı veya ağ bağlantısı gerekmez. APK'lar Git dışında tutulur.

## Bilinen sorunlar

- **Denge (ilk gözlem):** Telefonda oynanan beş oyunun dördü "Para İsyanı", biri "Halk İsyanı" ile bitti (9–35 karar); hazine çok hızlı tükeniyor. Altın set destesinde benzetimle hep sağ 9, hep sol 19 kararda bitiyor. Kara'nın 10 kartlık örnek destedeki ölçümü (1.000 rastgele koşu: medyan 13, %90 yüzdeliği 22 karar) gerçek deste için temsilî değil. 4.9 denge testine girdi.
- **Kural farkı:** Oyun ve `kart_formati.md` kart metnini 20–50, kararı 2–5 kelime kabul ediyor; YZ filtresi (`yz_gorevleri.md`) 12–50 ve 1–6 diyor. Bu yüzden 1.448 altın set kartının 103'ü oyuna giremedi. İki ekip tek kurala bağlamalı.
- **Android:** Debug APK ~124 MB (.NET çalışma zamanı + görseller); release ve kırpma 3.10'da ölçülecek. Tek telefonda denendi.
- **Aralıklı grafik test hatası:** Kara'nın ilk Windows grafik turunda H1'de bir kart kararı zamanında tamamlanmadı (sol ok önizlemesi). Tekrarda görülmedi, Linux'ta hiç görülmedi; nedeni kesinleşmedi.
- **Kayıt maliyeti:** Her kararda karar geçmişinin tamamı yazılıyor. Çok uzun oturumlarda yazma süresi ve beklenmedik güç kaybı cihazda ölçülmeli.

## Sayılar

- **Test sahnesi:** 12/12 başarılı, motor hatası yok (8 Kasım, `main` `fba6c30`, Linux):
  - başsız: H1 915, H2 1076, Menü 199, Oturum 28 kontrol;
  - Xvfb grafik: H1 960, H2 1127, Menü 227, Oturum 28 kontrol.
- **Kara'nın Windows çalıştırması** (7 Kasım, kendi birleşik sürümü): 12/12; H1 652, H2 1076, Menü 132, Oturum 14 kontrol.
- **Yedek deste:** 600 kart, 600 olay grubu (altın set 1.448 → oyuna uygun 1.345); 23 rolün hepsi var, rol başına 26–27 kart, hepsi 20–35 kelime.
- **Ekran boyutları (test):** 1152×648, 923×520, 360×640, 360×800 (dikey telefonun mantıksal ekranı), 640×360.
- **Android (G0):**
  - Soğuk açılış ~5 sn, bellek ~270 MB, debug APK ~124 MB.
  - Telefonda beş tam oyun: 7 Kasım'da 9, 13 ve 18 karar; 8 Kasım'da 35 ve 16 karar.
  - Kayıttan dönüş piksel piksel aynı.

## Yeni gelen için ilk 3 adım (Mert, Dönem 2 oyun yardımcısı)

1. **Kur ve oyna:** Game `README.md`'ye göre Godot 4.7.2 .NET ve .NET SDK 10'u kur, `git lfs pull` yap. `main`'i açıp varsayılan desteyle bir oyunu baştan sona oyna, tüm testleri çalıştır (yukarıdaki döngü); 12/12 geçmeli.
2. **Kaydı dene:** Bir karardan sonra oyunu kapat. **Kayıtlı Oyun**'dan aynı kart, sonuç ve göstergelerle devam edildiğini doğrula. Android telefonun varsa APK'yı kur (`docs/android_g0.md`).
3. **H3 (3.7–3.10):** Kazanma kuralını (3.8) ve rol–konu eşleşmelerini (3.7) ekipçe karara bağla, 3.10 için release APK'yı hazırla. Muhammed pazartesiden itibaren devri anlatır.
