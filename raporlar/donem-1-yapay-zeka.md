# Dönem 1 · Yapay Zekâ · Başkan: Mert · Yardımcı: Sokul

> **TASLAK (5 Kasım).** Sayılar 5 Kasım sabahının. `[DOLDUR]` yazan yerler pazar günü tamamlanacak.

## Ne yapıldı (dosya yollarıyla)
- **Üretim hattı:** `ai/veri_uretimi/` (`uretici.py`, `uretim.ipynb`, `uretim_gemini.ipynb`). Colab, Kaggle ve Gemini ile çalışır, kaldığı yerden devam eder. Üretim kodu ve veri seti Claude yardımıyla hazırlandı.
- **Veri seti:** `data/torbalar/` (1500 kelime, karakterler, konular, olaylar), promptlar, 8 örnek kart, `tema.json`.
- **Altın set sayfası:** `ai/altin_set/`. Kart ve hikâye üretir, kuralları otomatik kontrol eder.
- **Kart biçimi dönüştürücüsü (S2):** `ai/ortak/kart_bicimi.py`, test `ai/testler/test_kart_bicimi.py`. Mert, Claude yardımıyla.
- **Tokenizer (M5):** `ai/tokenizer/`. BPE, 8000 kelime, kart etiketleri tek token. Mert, Claude yardımıyla.
- **Filtre (S1):** `ai/filtre/` `[DOLDUR: Sokul]`
- **Hazır veriler (S3):** `data/edebiyat/` `[DOLDUR: Sokul]`
- **Veri hazırlama (O1):** `ai/veri_hazirlama/hazirla.py` `[DOLDUR]`

## Ne yarım kaldı, neden
`[DOLDUR]`

## Nasıl çalıştırılır (komutlar, Colab defterleri)
- Üretim: `Docs/yz_gorevleri.md` O2 bölümü, adım adım.
- Altın set sayfası: `python -m ai.altin_set.sayfa_olustur`, sonra claude.ai'ye yayınla.
- Tokenizer: `ai/tokenizer/README.md`.
- Testler: `uv run --with pytest --with pyyaml --with openpyxl --with tokenizers --with numpy python -m pytest ai/testler -q`

## Büyük dosyalar nerede (Drive / Hugging Face)
- Ham ve temiz üretim: Drive `kaydir_veri/` `[DOLDUR: bağlantı]`
- Tokenizer: Hugging Face `[DOLDUR: depo]`
- `train.bin` / `val.bin`: `[DOLDUR]`

## Bilinen sorunlar
- 5 Kasım'da Colab aynı tohumla baştan başladı: 3.276 kaydın hepsi eski malzemelerin tekrarı çıktı, 2.795'i "aynı prompt" diye elendi. Düzeltildi, Colab artık günlük dosya ve tohum kullanıyor.
- Kaggle'da 8-bit yavaş (saatte ~324 kart).
- Filtre kuralları iki yerde farklı: `yz_gorevleri.md` kart metni 12–50 kelime, karar 1–6 kelime, hikâye 70–200 kelime diyor; temizleme betiği `duzenle.py` 20–50, 2–5 ve 90–150 kullanıyor. `[DOLDUR: hangisi kaldı]`

## Sayılar (5 Kasım sabahı, yalnız Mert'in üretimi)
| | Ham | Temiz | Hafta sonu hedefi (ham) |
| --- | --- | --- | --- |
| Hikâye | 12.104 | 9.702 | ~20.000 |
| Kart (Gemma) | 8.304 | 6.728 | ~10.000 |
| Altın set kartı | | 1.542 (1.448 + 94) | |

- Tokenizer ilk eğitim: 17.972 belge, 2,2 milyon token. Dağılım: hikâye %63,3 · kart %29,3 · altın set %7,4 (BİLGEM ve edebiyat henüz yok).
- Testler: 61 geçti.
- Sokul'un üretimi: `[DOLDUR]`

## Yeni gelen için ilk 3 adım
1. `Docs/yz_gorevleri.md` ve bu raporu oku.
2. `ai/testler` testlerini çalıştır.
3. `[DOLDUR: Dönem 2 ilk iş]`
