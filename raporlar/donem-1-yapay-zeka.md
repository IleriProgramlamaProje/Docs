# Dönem 1 · Yapay Zekâ · Başkan: Mert · Yardımcı: Sokul

> **TASLAK (7 Kasım).** `[DOLDUR]` yazan yerler ekipten gelecek bilgiyle pazar günü tamamlanacak.

## Ne yapıldı (dosya yollarıyla)
- **Üretim hattı:** `ai/veri_uretimi/` (`uretici.py`, `uretim.ipynb`, `uretim_gemini.ipynb`). Colab, Kaggle ve Gemini ile çalışır, kaldığı yerden devam eder. Üretim kodu ve veri seti Claude yardımıyla hazırlandı.
- **Veri seti:** `data/torbalar/` (1500 kelime, karakterler, konular, olaylar), promptlar, 8 örnek kart, `tema.json`.
- **Altın set sayfası:** `ai/altin_set/`. Kart ve hikâye üretir, kuralları otomatik kontrol eder. Kartlar `data/altin_set/ham/` altında.
- **Temizlik:** `ai/filtre/duzenle.py`, test `ai/testler/test_duzenle.py`. Elenen her kaydın sebebi `silindi/` altına yazılır.
- **Kart biçimi dönüştürücüsü (S2):** `ai/ortak/kart_bicimi.py`, test `ai/testler/test_kart_bicimi.py`. Mert, Claude yardımıyla.
- **Tokenizer (M5):** `ai/tokenizer/`. BPE, 8000 kelime, kart etiketleri tek token, `incele.ipynb`'de 20 örnek cümlenin bölünüşü var. Mert, Claude yardımıyla.
- **Token dosyası (O1'in tokenizer kısmı):** `ai/tokenizer/kodla.py`.
- **Filtre (S1):** `ai/filtre/filtre.py` `[DOLDUR: Sokul]`
- **Hazır veriler (S3):** `data/edebiyat/` `[DOLDUR: Sokul]`
- **Veri hazırlama (O1):** `ai/veri_hazirlama/hazirla.py` `[DOLDUR: Sokul]`

## Ne yarım kaldı, neden
7 Kasım itibarıyla:
- **Tokenizer'ın Hugging Face'e yüklenmesi:** kod hazır (`--hf-depo`), depo ve token belirlenmedi.
- **`train.bin` / `val.bin`:** `hazirla.py` bekleniyor.
- **Üretim hedefi:** hikâye 12.264 / 20.000, kart 8.472 / 10.000 (ham).
- **Hazır veriler ve S1 filtresi:** depoda henüz yok.

`[DOLDUR: pazar günü son durum]`

## Nasıl çalıştırılır (komutlar, Colab defterleri)
- Üretim: `Docs/yz_gorevleri.md` O2 bölümü, adım adım.
- Temizlik: `python ai/filtre/duzenle.py <veri klasörü>` (`ham/` ve `altin/` okur, `temiz/` ve `silindi/` yazar).
- Temiz kartları eğitim metnine çevirme: `python -m ai.ortak.kart_bicimi temiz/model_ciktilari.jsonl temiz/model_kart_egitim.txt`
- Tokenizer: `ai/tokenizer/README.md`.
- Altın set sayfası: `python -m ai.altin_set.sayfa_olustur`, sonra claude.ai'ye yayınla.
- Testler: `uv run --with pytest --with pyyaml --with openpyxl --with tokenizers --with numpy python -m pytest ai/testler -q`

## Büyük dosyalar nerede (Drive / Hugging Face)
- Ham ve temiz üretim: Drive `kaydir_veri/` `[DOLDUR: bağlantı]`
- Tokenizer: Hugging Face `[DOLDUR: depo]`
- `train.bin` / `val.bin`: `[DOLDUR]`

## Bilinen sorunlar
- 5 Kasım'da Colab aynı tohumla baştan başladı ve eski malzemeleri yeniden üretti. Colab artık günlük dosya ve tohum kullanıyor, tekrarlar ham dosyadan çıkarıldı (`kararlar.md` 7 Kasım).
- Kaggle'da 8-bit yavaş (saatte ~324 kart).
- Sınırlar iki yerde farklı: `yz_gorevleri.md` kart metni 12–50, karar 1–6, hikâye 70–200 kelime diyor; `duzenle.py`, oyun ve `kart_formati.md` kartta 20–50 ve 2–5 kullanıyor, `duzenle.py` hikâyede 90–150. Bu yüzden altın setin 1.448 kartından 103'ü oyuna giremiyor. `[DOLDUR: toplantı kararı]`

## Sayılar (7 Kasım, yalnız Mert'in Gemma üretimi)
| | Ham | Temiz | Hafta sonu hedefi (ham) |
| --- | --- | --- | --- |
| Hikâye | 12.264 | 11.539 | ~20.000 |
| Kart (Gemma) | 8.472 | 7.995 | ~10.000 |
| Altın set kartı | | 1.542 (1.448 + 94) | |

- Tokenizer son eğitim: 21.076 belge, 2,58 milyon token. Dağılım: hikâye %64,0 · kart %29,6 · altın set %6,3 (BİLGEM ve edebiyat henüz yok).
- Testler: 62 geçti.
- Sokul'un üretimi: `[DOLDUR: Sokul]`

## Yeni gelen için ilk 3 adım
1. `Docs/yz_gorevleri.md` ve bu raporu oku.
2. `ai/testler` testlerini çalıştır, sonra `ai/veri_uretimi/README.md` ile üretimi tanı.
3. `[DOLDUR: Dönem 2 ilk iş]`
