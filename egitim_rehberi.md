# Model eğitimi rehberi · 1M / 10M / 30M

*26 Kasım 2026 · Eğitimi yapacak ekip için (YZ dönem 3: Kara + Muhammet). Karar noktası ~2 Aralık (`kararlar.md`, 11 Kasım).*

Veri, tokenizer ve eğitim kodu hazır. Kod yazmadan, Colab'da defteri çalıştırarak eğitim yapılır. Bu belge: veri nerede, nasıl eğitilir, hangi denemeler yapılacak, sonuçlar nasıl karşılaştırılacak.

---

## 1. Hazır olanlar

| Ne | Nerede |
|---|---|
| Eğitim defteri (Colab + Kaggle) | `AI/ai/egitim/egitim.ipynb` |
| Eğitim kodu | `AI/ai/egitim/egit.py`, model: `AI/ai/model/model.py` |
| Model boyutları | `AI/ai/model/boyutlar/1m.yaml`, `10m.yaml`, `30m.yaml` |
| Örnek üretme + kart geçerlilik oranı | `AI/ai/ornekleme/ornek_uret.py` |
| Dondurulmuş tokenizer (8000 parça) | `AI/data/uretilen/egitim/tokenizer.json` |
| Üç eğitim verisi | `AI/data/uretilen/egitim/duz/`, `istedigi/`, `kelimesiz/` |

**Tokenizer donduruldu (26 Kasım), değiştirilmez.** Bütün modeller aynı tokenizer'ı kullanır. Değişirse `train.bin`'deki numaraların anlamı değişir ve eğitilmiş modeller çöpe gider. Yeni bir etiket gerekirse tokenizer yeniden eğitilmez: `tokenizer.json`'daki 20 boş `<yedek_N>` etiketinden biri yeniden adlandırılır (`AI/ai/tokenizer/README.md`).

---

## 2. Üç veri seti

Üçü de aynı ham veriden (147.794 Gemma 4 12B kaydı) ve aynı tokenizer'la üretildi. Karışım: hikâye ~%65 · kart ~%23 · BİLGEM ~%10 · edebiyat ~%1,6.

| Klasör | Ne farklı | train.bin | val.bin |
|---|---|---:|---:|
| `duz/` | Temel. Hikâyede verilen 3 kelimenin 3'ü de geçmeli (kelime kuralı açık) | 15,36 M token | 0,89 M |
| `istedigi/` | `duz` ile aynı belgeler; saray kartlarının durum satırına danışmanın istediği karar eklendi: `<istiyor:sol>` / `<istiyor:sag>` / `<istiyor:belirsiz>` | 15,36 M token | 0,90 M |
| `kelimesiz/` | Hikâyede kelime kuralı **kapalı**: kelimeyi kullanmadığı için elenen ~19 bin hikâye de giriyor (hikâye %72,5 → %91,3 geçiyor) | 17,20 M token | 1,04 M |

`istedigi` etiket sayıları: Sol 10.417 · Sağ 3.466 · Belirsiz 1.399. **Sol ağırlığı var (~%70).** Model "danışman hep solu ister" diye öğrenebilir; sonuçta buna bakın.

Etiketli bir kart örneği:
```
<yonetim:75> <halk:10> <para:5> <ordu:5> <konu:çırak_yetiştirme> <konuşan:sinir_beyi> <istiyor:sag>
<kart> Sınır boyu geçitleri korumak için çırak yetiştirmeliyiz. …
<sol> Dostunu göreve ata <yonetim++> <ordu-->
<sonuc> …
<sag> … 
<sonuc> …
</kart>
```

---

## 3. Bir kez yapılacak hazırlık

1. **Depoyu çek.** Ham veri (~800 MB, Git LFS) eğitim için gerekmez, indirmemek için:
   ```sh
   GIT_LFS_SKIP_SMUDGE=1 git pull
   ```
2. **Drive'a yükle.** `AI/data/uretilen/egitim/` altındaki üç klasörü Drive'a şu yapıyla koy (her klasörde `train.bin`, `val.bin`, `tokenizer.json`):
   ```
   Drive'ım/kaydir_veri/egitim/duz/
   Drive'ım/kaydir_veri/egitim/istedigi/
   Drive'ım/kaydir_veri/egitim/kelimesiz/
   ```
   ⚠️ **Klasör adlarında Türkçe harf olmasın:** `egitim`, `duz` (✗ `eğitim`, `düz`). Yoksa defter "train.bin yok" hatası verir.

---

## 4. Bir eğitim nasıl çalıştırılır (Colab)

1. Colab → *Dosya → Not defteri yükle* → `AI/ai/egitim/egitim.ipynb`.
2. *Çalışma zamanı → Çalışma zamanı türünü değiştir → **T4 GPU***.
3. **"1 · Ayar"** hücresinde iki satırı değiştir, diğerlerine dokunma:
   ```python
   BOYUT = '1m'        # '1m' · '10m' · '30m'
   VERI_ADI = 'duz'    # 'duz' · 'istedigi' · 'kelimesiz'
   ```
4. *Tümünü çalıştır* (Ctrl+F9), Drive iznini ver.

Defter depoyu GitHub'dan kendisi indirir, eğitir, sonunda kayıp grafiğini ve örnekleri gösterir.

**Çıktı Drive'a kendiliğinden kaydedilir:** `Drive'ım/kaydir_veri/modeller/<boyut>_<veri>/` (ör. `1m_duz/`)

| Dosya | Ne |
|---|---|
| `en_iyi.pt` | Val kaybı en düşük model: **asıl kullanılacak** |
| `son.pt` | En son durum (koparsa buradan devam eder) |
| `kayip.csv` | Her ölçümün train/val kaybı |
| `ornek_kartlar.jsonl` | Sondaki 100 örnek kart |

Her 250 adımda kaydeder. **Oturum koparsa ya da iptal edersen:** aynı ayarlarla yeniden *Tümünü çalıştır*, `son.pt'den devam: adım …` yazar ve kaldığı yerden sürer. Bitince çalışma zamanını hemen silme, Drive'ın yazması için bir dakika bekle.

**Kaggle'da:** klasörü bir Kaggle *Dataset*'i olarak yükle, *Add Input* ile ekle, ayarlarda **GPU T4 ×2** ve **Internet on**. Çıktı `/kaggle/working/modeller/`'a gider ve **kendiliğinden kaydedilmez**: oturum sonunda *Output*'tan indir. Ayrıntı defterin ilk hücresinde.

---

## 5. Ekranda neye bakılır

- Her 250 adımda bir satır: `adım … · train … · val …`. İkisi de **~9'dan başlayıp düşmeli** (rastgele model 8000 parçadan birini tahmin eder: ln 8000 ≈ 9). Yanında `*en iyi` yazan satırda `en_iyi.pt` güncellenir.
- **Val 6 ölçüm iyileşmezse eğitim kendisi durur.** Hata değil: model ezberlemeye başlamış demektir, en iyi nokta zaten kayıtlı.
- **Grafik:** iki çizgi birlikte iniyorsa iyi. Train iniyor ama val yükseliyorsa ezber.
- **Örnek kartlar:** sonda 100 kart üretilir ve **kaçının biçimce geçerli olduğu** yazılır (`metinden_karta` okuyabiliyor mu: etiketler tam, etki işaretleri doğru, `</kart>` var). Karar noktasının ana sayısı bu.

---

## 6. Deney planı

Adım sayısı yaml'daki `tur: 4`'ten hesaplanır (veri 4 kez okunur). Süreler T4 için kabadır; doğru adım sayısını defter ilk satırda yazar.

### Aşama 1 · 1M, üç veri (hat çalışıyor mu + hangi veri iyi)

| # | BOYUT | VERI_ADI | ~adım | ~süre |
|---|---|---|---:|---|
| 1 | `1m` | `duz` | 3.750 | < 1 saat |
| 2 | `1m` | `istedigi` | 3.750 | < 1 saat |
| 3 | `1m` | `kelimesiz` | 4.200 | < 1 saat |

Üçü ayrı hesaplarda aynı anda çalışabilir.

**Cevaplanacak sorular:**
- **Kelime kuralı (`duz` ↔ `kelimesiz`):** ~19 bin hikâye fazlası (kelimeyi kullanmamış ama metni düzgün) modeli iyileştiriyor mu, yoksa fark yok mu?
- **istedigi (`duz` ↔ `istedigi`):** etiket kartların biçimini bozuyor mu? Model etiketi kullanabiliyor mu? (bkz. 7. bölüm, şu an ayrıca ölçülmüyor)

### Aşama 2 · 10M
Aşama 1'de en iyi çıkan veriyle `10m`. ~3.750–4.200 adım, birkaç saat. 15–17 M token 10M model için "idare eder": val kaybı yükselmeye başlayınca erken durur, bu beklenen bir şey.

Zaman ve hesap varsa iki aday veriyi 10M'de de karşılaştırın; küçük modelde görünmeyen fark büyükte çıkabilir.

### Aşama 3 · 30M
En iyi veriyle `30m`. ~7.500+ adım, yarım gün ve üstü; Kaggle'da 12 saat sınırı için `SURE_SAAT` ve devam (`ONCEKI`) ayarı defterde. 30M için veri azdır (ideali ~150 M+ token): ezber riski yüksek, dropout bu yüzden 0,2.

### Karar noktası (~2 Aralık)
1M / 10M / 30M sonuç tablosuna bakılır: **30M yeterli mi, 10M mi kullanılır, yoksa B planı mı** (hazır bir Türkçe modele LoRA ile ince ayar; `yol_haritasi.md` 5. hafta).

---

## 7. Sonuçları karşılaştırma

⚠️ **Val kaybını yalnız aynı veri setindeki modeller arasında karşılaştırın** (ör. 1M_duz ↔ 10M_duz). `kelimesiz`'in val seti farklı belgelerden oluşuyor; `istedigi`'nin val'inde ek etiketler var. Veri setleri arasında karşılaştırırken asıl ölçü:

1. **Geçerli kart oranı** (100 karttan kaçı biçimce doğru). Defterin son hücresi yazar.
2. **Göz kontrolü:** her modelden 20 kart + 5 hikâye okuyun. Türkçe düzgün mü, kart konuşanına uygun mu, kararlar mantıklı mı, sonuç cümlesi karara uyuyor mu?

Adil olsun diye örnekleri aynı ayarla üretin (defterdeki gibi `--sicaklik 0.8`, varsayılan `--tohum 0`).

**istedigi'yi ölçmek:** `ornek_uret.py` modele `<istiyor:…>` vermiyor; şu anki sayı yalnız biçimi ölçer. Etiketin işe yarayıp yaramadığını görmek için `istedigi` modeline durum satırını elle `… <konuşan:vezir> <istiyor:sag>` diye verip kartlarda danışmanın gerçekten sağı isteyip istemediğine bakın. Gerekirse `ornek_uret.py`'ye `--istiyor` seçeneği eklenir.

### Sonuç tablosu (doldurun, `AI/ai/olcum/sonuclar/`'a koyun)

| Model | Veri | Adım (durduğu) | En iyi val | Geçerli kart /100 | Göz notu |
|---|---|---:|---:|---:|---|
| 1M | duz | | | | |
| 1M | istedigi | | | | |
| 1M | kelimesiz | | | | |
| 10M | | | | | |
| 30M | | | | | |

---

## 8. Sorun giderme

| Belirti | Çözüm |
|---|---|
| `AssertionError: …/egitim/duz/train.bin yok` | Drive'daki klasör adları Türkçe harfli (`eğitim`, `düz`). Yeniden adlandır, "2 · Hazırlık" hücresini tekrar çalıştır. Hâlâ yoksa `drive.mount('/content/drive', force_remount=True)` |
| `GPU: YOK` | Çalışma zamanı türü T4 GPU seçilmemiş |
| Oturum koptu / iptal edildi | Aynı ayarlarla yeniden çalıştır, `son.pt`'den devam eder |
| Devamda `torch.load` / `EOF` hatası | `son.pt` yazılırken kesilmiş. Drive'da `modeller/<boyut>_<veri>/` klasörünü **komple** sil (yalnız `son.pt`'yi değil, yoksa `kayip.csv` karışır), baştan başlat |
| `CUDA out of memory` (30M'de olabilir) | "3 · Eğit" hücresinde `komut` satırından sonra `komut += ['--yigin', '16', '--biriktir', '2']` ekle: yığın yarıya iner, iki adımda birikir, sonuç aynı |
| Kayıp hiç düşmüyor / `nan` | Ekran görüntüsüyle gruba yazın |

---

## 9. Veriyi yeniden üretmek (gerekirse)

Ham veri değişirse ya da kelime kuralı başka bir ayarla denenecekse (tokenizer **değişmez**):
```sh
cd AI
git lfs pull                                # ham veri (~800 MB)
mkdir -p data/uretilen/filtre_girdi/ham
ln -sfn ../../ham/ham_iliskili/hikaye.jsonl data/uretilen/filtre_girdi/ham/hikaye.jsonl
ln -sfn ../../ham/ham_iliskili/kart.jsonl   data/uretilen/filtre_girdi/ham/kart.jsonl

# duz + istedigi
python ai/filtre/filtre.py data/uretilen/filtre_girdi --cikti data/uretilen/filtre
python ai/veri_hazirlama/hazirla.py data/uretilen --temiz data/uretilen/filtre/temiz --cikti data/uretilen/egitim/duz --oran edebiyat=0.015
python ai/veri_hazirlama/hazirla.py data/uretilen --temiz data/uretilen/filtre/temiz --cikti data/uretilen/egitim/istedigi --oran edebiyat=0.015 --istedigi
# kelimesiz
python ai/filtre/filtre.py data/uretilen/filtre_girdi --kelimeye-bakma --cikti data/uretilen/filtre_kelimesiz
python ai/veri_hazirlama/hazirla.py data/uretilen --temiz data/uretilen/filtre_kelimesiz/temiz --cikti data/uretilen/egitim/kelimesiz --oran edebiyat=0.015
```
**Edebiyat oranı neden 0,015:** `hazirla.py` toplamı en kıt kaynağa göre kısar. Edebiyatın tamamı ~0,29 M token; varsayılan %5'le `train.bin` 5,5 M'de kalıyordu. %1,5'le edebiyatın tamamı yine giriyor, toplam ~3 katına çıkıyor.
