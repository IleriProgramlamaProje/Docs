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

Üretim `ham/` klasörüne yazar. Aşağıdaki görevler bittikçe bu ham veri filtreden geçer, eğitim metnine dönüşür.

**Kural:** Her görev ayrı bir dalda yapılır (`mert/s2-donusturucu`, `sokul/s1-filtre` gibi) ve PR'la gelir. Mert'in PR'ını Sokul, Sokul'unkini Mert onaylar. Her görevin testi kendi PR'ında olur.

## Özet

| # | Görev | Kim | Dosya | Ne zamana | Bağlı olduğu |
|---|---|---|---|---|---|
| O2 | Her akşam üretim + altın set | İkisi | `uretim.ipynb`, altın set sitesi | **bugünden itibaren** | — |
| S1 | Filtre (1.5) | Sokul | `ai/filtre/filtre.py` | Çar | — |
| S2 | Kart biçimi dönüştürücüsü (1.1) | Mert | `ai/ortak/kart_bicimi.py` | Çar | — |
| S3 | Hazır veriler (2.2) | Sokul | `data/edebiyat/`, `data/README.md` | Per–Cum | — |
| M5 | Tokenizer (2.3) | Mert | `ai/tokenizer/` | Per–Cmt | ilk temiz veri (S1) |
| O1 | Veri hazırlama (2.4) | İkisi | `ai/veri_hazirlama/hazirla.py` | Cum–Cmt | S1, S2, M5 |
| O3 | Dönem 1 raporu | Mert (Sokul katkı) | `donem-1-yapay-zeka.md` | Paz | — |

---

## O2 · Her akşam üretim + altın set (ikisi, bugünden itibaren)

Öğretmen olarak Gemma 4 12B (Colab + Kaggle) ve Gemini kullanılır (2 Kasım kararı).

### Hazırlık (bir kere)
1. huggingface.co'da hesap aç / giriş yap. `google/gemma-4-12B-it` Apache 2.0, onay kutusu yok.
2. Profil → **Access Tokens** (huggingface.co/settings/tokens) → **Create new token** → tür **Read** → oluştur, `hf_...` değerini bir yere kaydet (bir daha gösterilmez).
3. Kaggle için: kaggle.com → profil → **Settings** → **Phone Verification** (yoksa Internet açılmaz).

### Colab (1 GPU, 4-bit)
1. Defteri doğrudan aç: https://colab.research.google.com/github/IleriProgramlamaProje/AI/blob/main/ai/veri_uretimi/uretim.ipynb
   (Colab'ın GitHub listesinde organizasyon görünmeyebilir; bu bağlantı yeterli, depo herkese açık.)
2. **Runtime → Change runtime type → T4 GPU → Save.**
3. Sol çubukta 🔑 **Secrets → Add new secret**: ad `HF_TOKEN`, değer token'ın, **Notebook access** açık.
4. 1. hücre: `KISI = 'mert'` / `'sokul'` (küçük harf, iki kişide farklı). Diğer ayarlar varsayılan kalır (`KART_PAYI = 0.4`: sürenin %40'ı kart, kalanı hikâye).
5. **Run all** → "Not authored by Google" uyarısında **Run anyway** → Drive iznini ver → Secrets erişimi sorarsa **Grant access**.
6. Model 5–10 dk'da açılır. "5 · Kart üret" hücresinde **saatte ~X kart** satırı çıkınca gruba at.
7. Dosyalar Drive'da `MyDrive/kaydir_veri/ham/`. Koparsa yine **Run all**: kaldığı yerden devam eder.
8. Bitince **Runtime → Disconnect and delete runtime** (birim harcamasın).
9. Ertesi gün: `KART_ADET`/`HIKAYE_ADET`'i artır (1500 → 3000), **Run all**. Not: GitHub'dan açılan defterde `KISI` kaydedilmez; her seferinde yeniden yaz ya da **Copy to Drive** ile kendi kopyanı kullan.

### Kaggle (2 GPU, 8-bit, gece arka planda)
1. **+ Create → New Notebook → File → Import Notebook** → GitHub adresi: `https://github.com/IleriProgramlamaProje/AI/blob/main/ai/veri_uretimi/uretim.ipynb`
2. Sağ panel: **Accelerator: GPU T4 x2**, **Internet: On**.
3. **Add-ons → Secrets → Add**: `HF_TOKEN`, deftere bağla (gece modunda zorunlu).
4. 1. hücre: `KISI` = kendi adın (Colab'la aynı ad olabilir; dosya adına ortam eklenir).
5. **Save Version → Save & Run All (Commit) → Save.** Sekmeyi kapatabilirsin; 10,5 saatte kendi durur.
6. Sabah: o sürümü aç → **Output** → `kaydir_veri.zip`'i indir (oturum kapanınca silinir), Drive'a `kaydir_veri/ham/` altına koy.

### Gemini
Gemini için ayrı defter var: `uretim_gemini.ipynb` (GPU gerekmez). Colab'da açmak için: https://colab.research.google.com/github/IleriProgramlamaProje/AI/blob/main/ai/veri_uretimi/uretim_gemini.ipynb
1. aistudio.google.com → **Get API key** → **Create API key** → anahtarı kopyala.
2. Colab'da 🔑 Secrets'a ya da Kaggle'da *Add-ons → Secrets*'a `GEMINI_API_KEY` adıyla ekle, **Notebook access** açık. (Colab'daki *Gemini API keys* düğmesiyle içe aktarılan `GOOGLE_API_KEY` de olur.)
3. 1. hücrede `KISI` = kendi adın (model: `GEMINI_MODEL`, varsayılan `gemini-flash-latest`). Colab'da çalışma zamanı CPU yeterli; Kaggle'da GPU seçmeye gerek yok, Internet açık olmalı.
4. **Run all** (Kaggle'da gece için *Save & Run All*). Dosyalar `kart_<ad>_<ortam>_<oturum>_gemini.jsonl` adıyla yazılır, Gemma dosyalarına karışmaz; filtre (S1) ikisini birden okur.
5. Ücretsiz kotada dakikalık/günlük sınır var: kota dolunca motor bekleyip yeniden dener, günlük sınır biterse defter durur, ertesi gün **Run all** kaldığı yerden devam eder.

### Altın set (her gün, kendi yapay zekânla)
1. Claude, Gemini ya da kullandığın başka bir yapay zekânın web sohbet ekranını aç.
2. `ai/veri_uretimi/promptlar/kart.txt` (veya `hikaye.txt`) promptunu ver; karakter, kelimeler ve gösterge durumunu kendin seç ya da torbalardan al.
3. Çıkan kartı `kart_formati.md` 4. bölümdeki kurallara göre elle düzelt (7 satır, etkiler, hitap…).
4. Altın set sitesine ekle; günün sonunda JSON'u indirip gruba at.
5. Ham kartlarda gördüğün hataları (bozuk kelime, kurala uymayan kart) not et: bu notlar filtrenin (S1) kurallarına girer.

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
| Sal 3 | Altın set (kendi yapay zekânla) · S2 | Altın set (kendi yapay zekânla) · S1 |
| Çar 4 | Toplantı: ilk günün sayıları · S2 bitir | Toplantı · S1 bitir |
| Per 5 | M5 tokenizer | İlk veriyi filtreden geçir, rapor · S3 |
| Cum 6 | M5 · O1'e tokenizer'ı bağla | S3 · O1 iskeleti |
| Cmt 7 | Tokenizer'ı yeniden eğit · `train.bin` | Filtre raporlarını topla: en sık eleme sebepleri |
| Paz 8 | 📄 Rapor | Rapora katkı |

**Her akşam ikiniz de:** Colab + Kaggle üretimi. **Her gün:** altın set (kendi yapay zekânla).

**Hedef:** Perşembe günü ilk günün hızına göre kesinleşir. Kaba tahmin hafta sonuna kadar **~10 bin ham kart + ~20 bin ham hikâye**. Filtreden yaklaşık 2/3'ü geçer.
