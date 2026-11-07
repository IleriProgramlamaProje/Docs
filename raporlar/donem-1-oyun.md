# Dönem 1 · Oyun · Başkan: Kara · Yardımcı: Muhammed

> **TASLAK (7 Kasım).** Muhammed'in test, çalıştırma ve devir notlarıyla hazırlandı. `[DOLDUR: Kara]` yazan yerleri Kara tamamlar; raporu pazar günü Kara atar.

## Ne yapıldı (dosya yollarıyla)

Depo: [Game](https://github.com/IleriProgramlamaProje/Game) · Godot 4.7.2 .NET + C# (`net10.0`). Oyunun adı **BUYRUK** (`kararlar.md`, 7 Kasım). Dosya yolları `game/` altındadır.

- **Kurulum ve plan** (26 Eki, Muhammed): Godot projesi ve C# ortamı, `docs/oyun_gelistirme_plani.md`, ilk sahne iskeleti testi.
- **H1 · 1.8–1.13** (1 Kas, Kara, `kara` dalı): oyun durumu ve göstergeler (`Betikler/Oyun/OyunDurumu.cs`, `Betikler/Arayuz/Gostergeler.cs`), yerel yedek deste (`Betikler/Kartlar/YedekDeste.cs`), kart görünümü (`KartGorunumu.cs`), kaydırma (`KaydirmaKontrolu.cs`), açılış (`AcilisEkrani.cs`), oyun akışı (`OyunYoneticisi`, `OyunDurumu.cs` içinde).
- **H2 · 2.5–2.7, 2.9** (2 Kas, Muhammed): sonuç ekranı, sekiz son (`Betikler/Cekirdek/SonKontrolu.cs`), yıl sayacı (`Betikler/Cekirdek/YilSayaci.cs`), H1 ile birleşme. Assets paketiyle ortak tema (`Assets/ui/krallik_tema.tres`, Git LFS).
- **BUYRUK arayüzü** (6 Kas, Kara): ana menü ve alt ekranlar (`Sahneler/AnaMenu.tscn`, `YeniOyun`, `KayitliOyunlar`, `Ayarlar`, `Credits`; `MenuSahnesi.cs`), gösterge bileşenleri (`GostergeBileseni.cs`), sürüklemeli deste kartı. Not: `docs/buyruk_arayuz_ve_kart_guncellemeleri.md`.
- **Birleşme** (7 Kas, Muhammed, `main` `657dbf4`): `kara` + Assets teması. Çıkış animasyonunun karar kaybettirdiği hata, deste kartlarının `AddChild` hatası, kart yüksekliği ve dar ekran menü taşması düzeltildi. Klavyeyle karar (← → Enter), kalıcı ses/tam ekran ayarı, `MenuTesti` eklendi.
- **2.8 · altın set destesi** (7 Kas, Muhammed, `muhammed` dalı `39f7883`, PR bekliyor): oyun altın setten seçilen 600 kartla açılır (`Veri/yedek_deste.json`). Üretici: `araclar/deste_olustur.py`. 2.9 bu desteyle uçtan uca test edildi.
- **G0 · Android denemesi** (7 Kas, Muhammed, `muhammed` dalı, PR bekliyor): debug APK gerçek telefonda (POCO X5 Pro 5G, Android 14, arm64) kuruldu; üç tam oyun dokunarak, modelsiz oynandı. Sekiz sorun bulundu, düzeltildi ve testlere eklendi. Başlıcaları: Android'de C# derlenmiyordu (C# 13); oyun yatay açılıyordu (artık **dikey**, 360×640); dokunmayla ses kaydırıcısı ve sayfa kaydırma çalışmıyordu; geri tuşu uygulamayı kapatıyordu; dikeyde oyun ekranı sığmıyordu; kamera deliği sayacın üstüne denk geliyordu. Not: Game `docs/android_g0.md`.

**Devir paketi** (yol haritası 3.2): "Yedek desteyle baştan sona oynanabilen oyun (açılış, kaydırma, sonuç ekranı, 8 son)": var; masaüstünde ve Android telefonda. 2.8/G0 PR'ı birleşince `main`'de altın set destesiyle oynanır.

`[DOLDUR: Kara — kendi değerlendirmen, eklemek istediklerin]`

## Ne yarım kaldı, neden

- **İnceleme:** H1–H2 ve 7 Kasım birleşmesi doğrudan `main`'e alındı; bağımsız PR incelemesi yapılmadı. Plan kutuları (1.7–2.9) bu yüzden işaretsiz. 2.8 ve G0, `muhammed` → `main` PR'ı ile Kara tarafından incelenecek.
- **İkinci bilgisayar (1.7):** "İki geliştiricinin bilgisayarında açılır" şartı. `[DOLDUR: Kara — main kendi bilgisayarında açıldı ve testler geçti mi?]`
- **G0 Android denemesi:** H1'de yapılacaktı, dönemin son günü (7 Kasım) yapıldı; gecikmesi nedeniyle Android'de C# derlenmediği ancak şimdi görüldü. Release çıktısı (imza anahtarı ekip kararı) ve ikinci telefon 3.10'a kaldı.
- **Sonraki dönemin işleri (yarım değil, plan gereği):** kayıt (3.9; "Kayıtlı Oyun" ekranı şimdilik boş), kazanma/rekor (3.8; `hedef_yil` hâlâ `null`), rol–konu seçimi (3.7), ses (4.8; ayar hazır, ses dosyası yok), sonlara özel görseller (4.7; şimdilik ortak taç).

## Nasıl çalıştırılır

Ayrıntı: Game `README.md`. Game repo kökünden:

```sh
git lfs pull                                  # PNG görselleri
dotnet build game/Game.csproj                 # 0 uyarı / 0 hata beklenir
<godot-net> --path game                       # oyun (ana sahne AnaMenu.tscn)
for t in game/Testler/*.tscn; do <godot-net> --headless --path game "res://Testler/$(basename "$t")" || echo "BAŞARISIZ: $t"; done
python3 araclar/deste_olustur.py              # altın set güncellenince desteyi yenile
```

`<godot-net>`: Godot 4.7.2 **.NET** çalıştırılabilir dosyası (Steam/standart sürüm C# içermez). Kontroller: sürükle-bırak; klavyede ← → önizler, Enter onaylar, Esc vazgeçer.

Telefon (Android): `<godot-net> --headless --path game --export-debug "Android" ../exports/buyruk.apk` ve `adb install -r exports/buyruk.apk`. SDK/JDK ayarı, Xiaomi'deki "USB üzerinden yükle" izni ve denetim listesi: Game `docs/android_g0.md`.

## Büyük dosyalar nerede (Drive / Hugging Face)

- Arayüz PNG'leri Game deposunda **Git LFS** ile (104 dosya, ~25 MB). Klonladıktan sonra `git lfs pull`.
- Oyun Drive/Hugging Face kullanmaz; deste ve tema `game/Veri/` içinde paketlenir. APK'lar Git dışında tutulur.

## Bilinen sorunlar

- **Kart sırası:** Deste dosya sırasıyla dolaşır; her yeni oyun aynı kartlarla başlar. 3.7 kart seçici ile ele alınacak.
- **Denge (ilk gözlem):** Altın set destesiyle hep sağı seçen oyun 9, hep solu seçen 19 kararda bitiyor (benzetim). Telefonda oynanan üç farklı oyunun üçü de "Para İsyanı" ile bitti; hazine çok hızlı tükeniyor. 4.9 denge testine girdi.
- **Kural farkı:** Oyun ve `kart_formati.md` kart metnini 20–50, kararı 2–5 kelime kabul ediyor; YZ filtresi (`yz_gorevleri.md`) 12–50 ve 1–6 diyor. Bu yüzden 1.448 altın set kartının 103'ü oyuna giremedi. İki ekip tek kurala bağlamalı.
- **Android:** Debug APK ~124 MB (.NET çalışma zamanı + görseller); release ve kırpma 3.10'da ölçülecek. Android derlemesi `net9.0`/C# 13 ile yapılır; `Game.csproj` dil sürümünü 13'e sabitler. Tek telefonda denendi.
- **Oyun ortasında çıkış yok:** Geri tuşu ve "Ana Menüye Dön" yalnız hükümdar seçiminde ve sonda çalışır; onaylı çıkış kayıtla (3.9) birlikte düşünülmeli.

## Sayılar

- Test sahnesi: 10/10 başarılı, motor hatası yok. Başsız: H1 727, H2 1076, Menü 198 kontrol. Xvfb grafik: H1 763, H2 1127, Menü 226 kontrol (7 Kasım, `muhammed` dalı, G0 düzeltmeleriyle).
- Yedek deste: 600 kart (altın set 1.448 → oyuna uygun 1.345), 23 rolün hepsi, rol başına 26–27, hepsi 20–35 kelime.
- Ekran boyutları (test): 1152×648, 360×640, 360×800 (dikey telefonun mantıksal ekranı), 640×360.
- Android (G0): soğuk açılış ~5 sn, bellek ~270 MB, debug APK ~124 MB; tam oyun hep sağa 9 kararda bitti (masaüstü benzetimiyle aynı).

## Yeni gelen için ilk 3 adım (Mert, Dönem 2 oyun yardımcısı)

1. Game `README.md`: Godot 4.7.2 .NET ve .NET SDK 10 kur, `git lfs pull`, oyunu aç ve bir el oyna.
2. Tüm testleri çalıştır (yukarıdaki döngü); 10/10 geçmeli.
3. H3 (3.7–3.10): G0 yapıldı (Game `docs/android_g0.md`; APK'yı kendi telefonunda da kur). Sonra 3.9 kayıt, 3.8 kazanma ve 3.10 için release APK. Muhammed pazartesiden itibaren devri anlatır.
