# Hazırlık Haftası · Kaydır & Karar Ver

*21–25 Ekim 2026 · Son güncelleme: 25 Ekim · Hazırlık bitti*

> Bu hafta oyun ya da model kodu yazılmıyor (hikâye üretici hariç). Kurulum + veri hazırlığı yapılıyor. **26 Ekim pazartesi düzenli çalışma başlıyor**, ayrıntısı `yol_haritasi.md`'de.
>
> Yanındaki **`Torba_Listesi.xlsx`**'i hep birlikte dolduruyoruz (bkz. 2. bölüm).

---

## 0. Bu hafta değişen büyük kararlar

| Konu | Eski | Yeni |
| --- | --- | --- |
| **Tema** | Orta Çağ Türk beyliği | **Türk tarzı krallık.** "Kral" denir; göstergeler **Yönetim**, Halk, Para, Ordu, dünya Türk-İslam kültüründe kalır |
| **Oynanış** | 4 mekanik adayı | **Düz kart + kaydırma.** Açılış → kart → sonuç ekranı → … → son |
| **Hitap** | "Beyim" yok | Oyuncu cinsiyet seçer → **"Beyim" / "Hatunum"**. Model `{hitap}` yazar, gerektiğinde |
| **Kart başlığı** | — | Konuşanın unvanı + ismi ("Defterdar Yakup"), oyun kodu koyar |
| **Sonuç cümlesi** | Yok | Model her seçenek için bir sonuç cümlesi yazar |
| **Etkiler** | 2 kademe (±10, ±20) | **3 kademe: ±5 · ±10 · ±15** |
| **Sonlar** | 8 son | 8 son + **kazanma sonu** (hedef süreye ulaşınca; isterse rekor için devam) |
| **Görseller** | — | Karakter başına portre + açılış + sonlar ≈ 25 resim, görsel üreticiyle |
| **Ekip** | 2 + 2 sabit | **2 haftalık dönemler, rol rotasyonu** · koordinatör: Mert |
| **Repo** | `kaydir-karar-ver` | **`ileri-programlama`** |

---

## 1. Bu haftanın işleri

| # | İş | Kim | Not |
| --- | --- | --- | --- |
| 1 | **Kurulum** | Herkes | Git, Unity, Python, Colab (`kurulum.md`) |
| 2 | **`ileri-programlama` deposu** | Bir kişi | `ileri-programlama.zip`'teki iskelet yüklenir |
| 3 | **Kelime torbası** | Herkes | ~2000 kelime, isim / fiil / sıfat |
| 4 | **Diğer torbalar** | Herkes | Olay, özellik, üslup, konu, yer, zaman, ruh hâli, ikilem |
| 5 | **Öğretmen model hız ölçümü + seçim** | Mert | Gemma 4 ve Qwen 3.5, Colab'da |
| 6 | **Hikâye üretici kodu** | Mert | Torba → prompt → öğretmen → dosya |

✅ **Yapıldı:** Öğretmen model kalite denemesi (LM Studio, 2 tur). Trendyol elendi, **Gemma 4 (4B) 1. aday, Qwen 3.5 (9B) 2. aday.** Ayrıntı: `docs/raporlar/ogretmen_secimi.md`.

---

## 2. Torbalar

### Torba nedir, neden var?

Modelimizi eğitmek için öğretmen modele yüz binlerce kısa hikâye ve kart yazdıracağız. Hep "bir hikâye yaz" dersek hep birbirine benzeyen hikâyeler yazar, model de tek tip yazmayı öğrenir.

Bunun için **torbalar** hazırlıyoruz. Her hikâye ya da kart için otomasyon her torbadan rastgele bir şey çeker ve öğretmen modele tek bir istek olarak verir:

> *"**Çoban** hakkında, **yaylada** geçen, **kötü biten** bir hikâye yaz. Hikâyede **kervan, kaçmak, yorgun** kelimeleri geçsin."*

Bu, TinyStories makalesindeki yöntemin aynısı (bkz. 8. bölüm).

### Ekibin hazırlayacağı torbalar (10)

| # | Torba | Ne içerir | Örnek | Önerilen hedef |
| --- | --- | --- | --- | --- |
| 1 | **Kelimeler** | isim / fiil / sıfat | kervan, kaçmak, yorgun | **~2000** ✅ |
| 2 | **Karakterler** | Rol (isim değil unvan) | Kadı, Vezir, Defterdar | **15** ✅ (son hâli 1. hafta) |
| 3 | **Olaylar** | Ne oluyor | kuraklık, düğün, sınırda baskın | ~100 |
| 4 | **Özellikler** | Hikâyenin bir niteliği | kötü bitsin, diyalog olsun | 30–40 |
| 5 | **Üsluplar** | Nasıl anlatılsın | Dede Korkut gibi, masal gibi | 20–30 |
| 6 | **Konular** | Kartın derdi | maaş, vergi, salgın | ~80 |
| 7 | **Yer** | Nerede geçiyor | han, kale, pazar | ~50 |
| 8 | **Zaman / mevsim** | Ne zaman | kış ortası, hasat vakti | ~40 |
| 9 | **Ruh hâli** | Konuşan nasıl hissediyor | öfkeli, korkmuş | ~40 |
| 10 | **İkilem** | Ne neye karşı tartılıyor | adalet ↔ merhamet | ~50 |

Atasözü torbası düşünüldü, alınmadı. Torba boyutları (3–10) öneri; neden az yettiği: 15 karakter × 100 olay × 50 yer zaten 75.000 farklı başlangıç eder.

**Kodun ürettiği:** Gösterge durumu (Yönetim, Halk, Para, Ordu için rastgele değerler). Model, kartı o anki duruma uygun yazmayı böyle öğrenir.

### Torbalar nasıl kullanılır?
- **Hikâyelerde:** Birkaç torba her zaman (karakter + olay + 3 kelime), diğerlerinden rastgele 1–2 tanesi. İstek kısa kalır, öğretmen model şaşırmaz.
- **Kartlarda:** Oyunda modele hangi bilgiler gidecekse, eğitimdeki kartlarda da çoğunlukla bulunmalı. Düz kart seçildiği için hangi durum etiketlerinin gideceği **1. haftada kart biçimiyle birlikte** kesinleşir.

### `Torba_Listesi.xlsx` nasıl doldurulur?
- Her torbanın kendi sekmesi var. Boş satıra yaz, **"Ekleyen"**e adını koy.
- Kelimelerde **"Tür"** açılır liste. Aynı kelime iki kez yazılırsa hücre turuncu olur.
- **"Özet"** sekmesi kendiliğinden sayar. **"Durum"** sütunu isteğe bağlı.
- Her torbada **ilk 30 madde Claude'dan** (Ekleyen = Claude). Beğenmediğinizi silin.
- Drive'a yükleyip Google E-Tablolar ile açarsak herkes aynı anda yazabilir.

### Yazarken dikkat
- **Sade Türkçe,** modern kelime yok (bütçe, reform, memur, bakan, vali, depo, politika…).
- **Basit, günlük kelimeler.** Nadir ve süslü kelimeler küçük modelin işini zorlaştırır.
- **Kelimeler yalın hâliyle:** "evlerimizden" değil "ev".
- **Benzer maddeler yazmayın.** "Yangın" ve "ambar yangını" tek madde sayılır.
- **Krallık:** "beylik / bey" yerine "krallık / kral" (ör. "komşu beyliğe haraç" → "komşu krallığa haraç").

---

## 3. Karakterler ve isimler

- **23 rol** (unvan), 4 grup: Yönetim 7 · Ordu 4 · Halk 6 · Para 6. Her rolün kimlik kartı var: ton, görev, örnek cümle, sık kullandığı sözler, asla yapmadığı, benzerinden farkı (`data/torbalar/karakterler.csv`). "Çift" cinsiyetli roller oyunda erkek de kadın da olabilir.
- **İsimler oyun kodunda rastgele atanır**, her yeni oyunda bir kez. Model isim görmez.
- **Kart içinde başka karakterden sadece unvanla bahsedilir:** "Defterdar dün hazineyi saydı…"
- **Karakter–konu uyumu:** Dert, konuşanın işine uygun olsun. Kadı ordu işi getirmez, vergiyi Defterdar getirir. Oyun kodu kartı "rol–konu tablosuna" göre seçer (3. hafta).

---

## 4. Kart kuralları (güncel)

| Kural | Değer |
| --- | --- |
| **Göstergeler** | **Yönetim** · Halk · Para · Ordu (0–100, 50'den başlar) |
| **Uzunluk** | 20–35 kelime, en fazla 50 |
| **Hitap** | `{hitap}` → oyun kodu "Beyim" / "Hatunum" yapar. Her kartta değil, gerektiğinde |
| **Seçenek yazısı** | Kartın derdine verilen bir **karar**: emir ya da eylem cümlesi ("Kanalı kazdır", "Beklesinler, hazine boş"). Soyut başlık yok |
| **Sonuç cümlesi** | Her seçenekten sonra bir cümle. Aynı kartın kapanışı, sonraki karta bağlanmaz |
| **Etkiler** | `+` ±5 · `++` ±10 · `+++` ±15. Kartın hikâyesine göre mantıklı olsun |
| **Gösterge sınırı** | Seçenek başına 1–3 gösterge |
| **Altın kural** | İki seçenek de en az bir göstergeyi düşürür |
| **Bağlantı** | Kartlar birbirinden bağımsız |
| **Kelime seçimi** | Yumuşak sınır: öğretmene "basit kelimeler kullan" denir, filtre aşırı nadir kelimeli olanları ayıklar |

**Oyuncu ne görür:** Kaydırırken seçenek yazısı + sadece ok (Para ▼ Halk ▲). Bırakınca sonuç ekranında sonuç cümlesi + sayı (Para −10, Halk +5).

**Örnek:**

> **Akıncı Beyi Tolga** *(başlık: unvan + isim, oyun kodu koyar)*
> "Beyim, askerler üç aydır maaş alamadı. Kışlada söylenmeler başladı; ödenmezse kaçanlar olacak."
>
> ⬅️ **Maaşları hazineden öde** → Para ▼ · Ordu ▲ → *"Askerler sevindi, ama hazine iyice eridi."* (Para −10, Ordu +10)
> ➡️ **Beklesinler, hazine boş** → Ordu ▼ · Halk ▼ → *"Kışlada homurtular büyüdü, birkaç asker gece kaçtı."* (Ordu −10, Halk −5)

Modelin yazdığı biçim: `docs/kart_formati.md`.

---

## 5. Altın set

- Hedef **2.500 iyi kart**: ~2.300 ince ayar · 200 sınav (model hiç görmez) · en iyi 600 yedek deste.
- **Herkesin her hafta görevi.** Eşit hız: haftada ~310, **kişi başı günde ~11 iyi kart.**
- Sohbet ekranından (Claude, Gemini, ChatGPT) elle üretilir. **Okuma sırası:** Mert → Sokul'un, Sokul → Kara'nın, Kara → Muhammet'in, Muhammet → Mert'in kartlarını okur.
- İnce ayar 5. haftada eldeki kartlarla, 7. haftada bütün kartlarla.
- ⚠️ Altın Set sayfası eski kuralları kullanıyor. **1. haftada yeni kurallara göre güncellenir**, sonra paylaşılır.

---

## 6. Doğrulayıcının kontrol listesi

1. **Biçim:** `<kart>`, `<sol>`, `<sonuc>`, `<sag>`, `<sonuc>`, `</kart>` yerinde mi?
2. **Uzunluk:** 20–35 kelime, en fazla 50
3. **Altın kural:** İki seçenek de en az bir göstergeyi düşürüyor mu?
4. **Gösterge sınırı:** Seçenek başına 1–3; işaretler sadece `+ ++ +++ - -- ---`
5. **İsim yok:** Sadece unvan
6. **Hitap:** "Beyim/Hatunum" elle yazılmamış, sadece `{hitap}`
7. **Modern kelime yok:** `tema.json`'daki yasak kelimeler
8. **Sonuç cümlesi** var mı, boş değil mi?

"Kart mantıklı mı, güzel mi?" sorusunu doğrulayıcı değil, **ölçüm aşaması** cevaplar.

---

## 7. Öğretmen model

- **Kalite denemesi yapıldı** (LM Studio, 2 tur): Trendyol elendi · **Gemma 4 (4B) 1. aday** (kurallara en çok uyan, ~37 tok/s) · **Qwen 3.5 (9B) 2. aday** (Türkçesi iyi ama "Beyim" dedi, ~24 tok/s).
- **Sıradaki:** Colab'da hız ölçümü (saatte kaç hikâye) → seçim.
- Denemeden öğrenilen: Kart promptuna unvan listesi, karakter–konu uyumu, karar cümlesi, "sadece +/-", yasak kelime örnekleri ve "açıklama yazma" eklenince sonuçlar belirgin iyileşti.

---

## 8. TinyStories makalesinden notlar

*Eldan & Li, 2023 · arxiv.org/abs/2305.07759*

- **Ne yaptılar?** 3–4 yaşındaki bir çocuğun bildiği ~1500 kelimeyle GPT-3.5/4'e kısa hikâyeler yazdırdılar. Her hikâyede rastgele 3 kelime (isim + fiil + sıfat) ve rastgele özellikler istediler.
- **Asıl ders:** Küçük modele küçük ve dar bir dünya verilirse, 10M parametrenin altında bile tutarlı hikâye yazabiliyor.
- **Torba yöntemimiz** makaledekinin aynısı. **Kart biçimimiz** makaledeki "talimatlı" sürümün karşılığı.
- **30M hedefimiz yerinde:** Makalede 28M civarı modeller tutarlı.
- **Beklenti:** Önce dilbilgisi, sonra tutarlılık, en son yaratıcılık gelir.
- **Bizim için zor kısımlar:** Türkçe eklemeli dil (biraz daha fazla veri ya da biraz daha büyük model gerekebilir); öğretmenimiz GPT-4 değil (filtre ve öğretmen seçimi önemli).
- **Ölçüm fikirleri:** Öğretmen-puanlama, ezber testi. **Sunum:** Küçük modelin içi okunabiliyor.

---

## 9. Sonraya kalanlar

| Konu | Ne zaman |
| --- | --- |
| ~~Karakterlerin son hâli~~ ✅ 23 rol, kimlik kartlarıyla (25 Ekim) | — |
| Kart biçiminin son hâli, durum etiketleri | 1. hafta |
| Teslim sorumlusu (kura) | 1. hafta toplantısı |
| Kelimelerin isim / fiil / sıfat dağılımı · torba boyutlarının onayı | 1. hafta |
| Hedef veri miktarı | Hız ölçümünden sonra |
| Türkçe ve tokenizer | 2. hafta |
| Model derinliği (çok sığ olmamalı) | 3. hafta |
| Hedef süre, kaç kartta bir yıl, oyunun adı | 4. hafta (denge testi) |
| Kısıtlı üretim ("bekçi"), bkz. `fikir_notlari.md` | 6. hafta |
| Sıfırdan mı, hazır modele ince ayar mı? (Mert en sona bıraktı) | 5. hafta karar noktası |
