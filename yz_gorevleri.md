# YZ görevleri · Mert + Sokul · 2–8 Kasım

1. haftadan kalan görevler (1.1, 1.5) bu haftanın görevleriyle (2.1–2.4) birleştirildi.

## Hazır olanlar (bugün kart üretimi başlıyor)

- **Veri seti:** 1500 kelime, karakterler, torbalar, hikâye ve kart promptları, 8 örnek kart, `tema.json`.
- **Üretim kodu:**
  - türe göre kelime: hikâyede isim + fiil + sıfat, kartta isim + sıfat;
  - her istekte farklı bir örnek kart;
  - 12B'yi T4'e sığdıran 4-bit ve 8-bit motorlar;
  - kaldığı yerden devam ve süre sınırı;
  - `uretim.ipynb`: Colab ve Kaggle, önce kart sonra hikâye.

Üretim `ham/` klasörüne yazar. Aşağıdaki görevler bittikçe bu ham veri filtreden geçer, eğitim metnine ve altın sete dönüşür.

**Kural:** Her görev ayrı bir dalda yapılır (`mert/s2-donusturucu`, `sokul/s1-filtre` gibi) ve PR'la gelir. Mert'in PR'ını Sokul, Sokul'unkini Mert onaylar. Her görevin testi kendi PR'ında olur.

## Özet

| # | Görev | Kim | Dosya | Ne zamana | Bağlı olduğu |
|---|---|---|---|---|---|
| O2 | Her akşam üretim + altın set okuma | İkisi | `uretim.ipynb`, altın set sitesi | **bugünden itibaren** | — |
| S1 | Filtre (1.5) | Sokul | `ai/filtre/filtre.py` | Çar | — |
| S2 | Kart biçimi dönüştürücüsü (1.1) | Mert | `ai/ortak/kart_bicimi.py` | Çar | — |
| S3 | Hazır veriler (2.2) | Sokul | `data/edebiyat/`, `data/README.md` | Per–Cum | — |
| M5 | Tokenizer (2.3) | Mert | `ai/tokenizer/` | Per–Cmt | ilk temiz veri (S1) |
| O1 | Veri hazırlama (2.4) | İkisi | `ai/veri_hazirlama/hazirla.py` | Cum–Cmt | S1, S2, M5 |
| O3 | Dönem 1 raporu | Mert (Sokul katkı) | `donem-1-yapay-zeka.md` | Paz | — |

---

## O2 · Her akşam üretim + altın set (ikisi, bugünden itibaren)

**Üretim (~10 dk kurulum):**
1. **Colab:** `uretim.ipynb`'yi aç → Çalışma zamanı **T4 GPU** → 1. hücrede `KISI` = kendi adın → Tümünü çalıştır. Drive'a yazar, koparsa yeniden çalıştırınca kaldığı yerden devam eder.
2. **Kaggle:** Aynı defter → **GPU T4 x2**, **Internet On** → Add-ons → Secrets → `HF_TOKEN` → **Save & Run All**. Gece arka planda çalışır. Sabah Output'tan `kaydir_veri.zip`'i indir.
3. **Rapor:** Gruba ekranda yazan "saatte ~X kart" satırını at.

Sadece kart üretmek için 1. hücrede `KART_PAYI = 1.0` yap.

**Altın set:**
- Her gün ikiniz de ham kartlardan okursunuz. İyi kartları düzeltip altın set sitesine eklersiniz, kötülerin neden kötü olduğunu not edersiniz.
- Bu notlar filtrenin (S1) kurallarına girer.
- Okuma sırası: Mert Sokul'un kartlarını, Sokul Mert'in kartlarını okur.

## Sokul

### S1 · Filtre (1.5)
**Neden:** 12B'nin çıktısında bozuk kelimeler oluyor, özellikle 4-bit'te ünlü uyumu bozuluyor ("taşleri", "halkınin"). Ayrıca kurala uymayan kartlar ve tekrarlar çıkıyor. Bunlar eğitim verisine girmemeli.

**Girdi:** `ham/*.jsonl`. Her satırda `malzeme` (karakter, kelimeler, durum…) ve `cikti` (modelin yazdığı metin) var.
- Kart metni şu satırlardan oluşur: `Metin: …` / `Sol: …` / `Sol sonuç: …` / `Sol etki: Halk ++, Para -` / `Sağ: …` / `Sağ sonuç: …` / `Sağ etki: …`
- Üretilemeyen istekte `cikti` `[BOŞ ÇIKTI]` olur, bunu ele.

**Çıktı:**
- Geçenler `temiz/*.jsonl` dosyasına gider. Kart, S2'nin kullanacağı biçimde ayrıştırılmış olarak yazılır: `{"metin", "sol": {"karar", "sonuc", "etki": {"halk": 10}}, "sag": {…}}` (S2 oyun JSON'unda `karar`ı `etiket` yapar).
- **Rapor:** hangi kuraldan kaç kayıt atıldı. Prompt bu sayılara bakılarak düzeltilir, bu yüzden en önemli çıktı rapor.

**Hikâye kuralları:**
- Uzunluk: 100–150 kelime hedef, filtre biraz geniş tutsun (örneğin 70–200).
- Üç kelimenin üçü de geçmeli. Ek almış olabilir ("kervan" → "kervanı"), fiil çekimlenmiş olabilir ("kaçmak" → "kaçtı", "beklemek" → "bekliyordu"). Kelimeyi kök olarak kelime başında ara.
- Modern kelime yok (`tema.json` → `yasak_kelimeler`). Kısa kelimeyi tam kelime olarak ara, "bakan" gibi kelimeler yanlışlıkla elenmesin.
- Başlık veya açıklama satırı varsa sil ("Başlık: …", "# …").

**Kart kuralları** (`kart_formati.md` 4. bölüm):
- 7 satırın hepsi var. Model bazen satır başına `**`, `-`, `1.` koyuyor, bunları tolere et.
- Metin 12–50 kelime, karar 1–6 kelime, evet/hayır kararı yok.
- Her seçenek 1–3 göstergeyi etkiler, iki seçenek de en az birini düşürür.
- Sadece dört gösterge adı var, etkide sayı yok (`Halk ++` doğru, `Halk +10` yanlış).
- `{hitap}` dışında hitap yok ("Beyim", "hünkârım" yazılmaz).
- İki kelimeden en az biri geçiyor.

**İkisi için ortak:**
- **Bozuk kelime:** Çoğul ekinin ünlü uyumu (`taş` + `leri` ✗) ve ekin kendi içindeki uyumsuzluk (`halkınin` ✗) atılır.
  - Alıntı kelimelere dikkat, bunlar doğru: saatler, harpler, valinin, gazinin.
  - "arkadaşinin" gibi bazı hatalar yazılışı doğru kelimelerle aynı olduğu için yakalanamaz. Bunu kabul et.
- **Tekrar:** Aynı metin ikinci kez gelirse atılır.

**Bitti sayılır:** `test_filtre.py` hazır. İçinde doğru metinlerin geçtiği ve bozuk metinlerin elendiği örnekler var. Gerçek üretimden 30 kayıt filtreden geçirildi ve sonucu elle kontrol edildi.

### S3 · Hazır veriler (2.2)
- BİLGEM'in basit Türkçe hikâyelerini indir, `data/edebiyat/` altına koy.
- Telif süresi dolmuş, lisansı temiz edebiyat metinlerini de aynı yere koy.
- Her kaynağın adını, adresini, lisansını ve kelime sayısını `data/README.md`'ye yaz. Lisansı belirsiz olanı alma.
- Büyük dosyaları Git'e değil Drive'a koy, README'ye bağlantısını yaz.

**Bitti sayılır:** Kaynaklar indirildi, her birinin lisansı ve kelime sayısı `data/README.md`'de.

## Mert

### S2 · Kart biçimi dönüştürücüsü (1.1)
**Neden:** Öğretmen satırlı yazıyor. Model ise `kart_formati.md` 2. bölümdeki etiketli metinle eğitilecek, oyun ve altın set sitesi 3. bölümdeki JSON'u okuyacak.

**Ne yapılacak** (`ai/ortak/kart_bicimi.py`):
- `egitim_metni(kart, malzeme)`: S1'in temiz kaydından etiketli metin üretir. Önce durum satırı: `<yonetim:50> <halk:50> <para:60> <ordu:35> <konu:…> <konuşan:…>`. Sonra `<kart> … </kart>`.
  - Etkileri hep aynı sırada yaz (yonetim, halk, para, ordu) ki model tutarlı öğrensin.
  - `malzeme.durum` anahtarları görünen adlardır (`Yönetim`, `Halk`…); etikette küçük harf ASCII kullan (`ayarlar.GOSTERGELER`).
- `oyun_json(kart, malzeme)`: 3. bölümdeki JSON. Altın set sitesine aktarmak için de bu kullanılır.
- `metinden_karta(metin)`: Etiketli metinden karta geri çevirir. Modelin çıktısını okurken bu kullanılacak, biçim bozuksa hata versin.
- **Konuşan anahtarı:** `tema.json` → `karakterler[].anahtar` (`akinci_beyi`).
- **Etki:** `++` → 10, `---` → -15 (`ayarlar.ETKI_KADEMELERI`).
- S1 bitmeden de başlanabilir: elle yazılmış birkaç temiz kayıtla test et.

**Bitti sayılır:** `test_kart_bicimi.py` geçiyor. Kart → metin → kart dönüşümünde aynı kart çıkıyor, JSON 3. bölümle aynı alanlara sahip.

### M5 · Tokenizer (2.3)
Yol haritasındaki gibi:
- `ai/tokenizer/egit_tokenizer.py`: ilk temiz hikâyelerle BPE eğit.
- `incele.ipynb`: Türkçe kelimelerin nasıl bölündüğüne bak.
- Kart etiketleri (`<kart>`, `<sol>`, `<halk++>` …) tek parça token olmalı.
- Cumartesi günü o güne kadarki veriyle yeniden eğit, sonra HF'ye yükle.

**Bitti sayılır:** Tokenizer HF'de. `incele.ipynb`'de 20 örnek cümlenin bölünüşü var, kart etiketleri tek token.

## İkisi

### O1 · Veri hazırlama (2.4) · Sokul iskeleti kurar, Mert tokenizer'ı bağlar
`ai/veri_hazirlama/hazirla.py` şunları yapar:
- Kaynakları okur: temiz hikâyeler, S2'den geçmiş kartlar ve hazır veriler.
- Karışım oranını uygular.
- %95 train, %5 val olarak ayırır.
- Tokenizer ile `train.bin` / `val.bin` dosyalarını üretir.
- Kaynak başına token sayısını raporlar.

**Bitti sayılır:** `train.bin` / `val.bin` Drive'da, kaynak başına token sayıları rapora yazıldı.

### O3 · Dönem 1 raporu
Pazar günü Mert yazar. Sokul 2.2'yi ve üretim sayılarını ekler. Raporda kodu kimin yazdığı ve yardım alınan yerler açıkça yazılır: üretim kodu ve veri seti Claude yardımıyla hazırlandı.

## Gün gün

| Gün | Mert | Sokul |
|---|---|---|
| Pzt 2 | PR'ı gönder · **Akşam üretim** (Colab + Kaggle) | PR'ı incele, birleştir · Kaggle hesabı (telefon onayı, `HF_TOKEN`) · **Akşam üretim** |
| Sal 3 | Ham kartlardan oku → altın set · S2 | Ham kartlardan oku → altın set · S1 |
| Çar 4 | Toplantı: ilk günün sayıları · S2 bitir | Toplantı · S1 bitir |
| Per 5 | M5 tokenizer | İlk veriyi filtreden geçir, rapor · S3 |
| Cum 6 | M5 · O1'e tokenizer'ı bağla | S3 · O1 iskeleti |
| Cmt 7 | Tokenizer'ı yeniden eğit · `train.bin` | Filtre raporlarını topla: en sık eleme sebepleri |
| Paz 8 | 📄 Rapor | Rapora katkı |

**Her akşam ikiniz de:** Colab + Kaggle üretimi. **Her gün:** altın set okuması.

**Hedef:** Perşembe günü ilk günün hızına göre kesinleşir. Kaba tahmin hafta sonuna kadar **~10 bin ham kart + ~20 bin ham hikâye**. Filtreden yaklaşık 2/3'ü geçer.
