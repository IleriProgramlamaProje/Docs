# Repo Rehberi · Hangi dosya ne işe yarar?

*Depoda bir dosyayı açtığında "bu ne, içine ne yazılır, kim yazar" sorusunun cevabı burada.*
💡 = öneri (adlar ve biçimler 1. haftada değişebilir). **[H3]** = 3. haftada oluşturulur.

---

## Önce büyük resim

Depo dört ana klasörden oluşuyor. Her birinin tek bir işi var:

| Klasör | Tek cümleyle | Benzetme |
| --- | --- | --- |
| `docs/` | Kararlar ve planlar, yani **neyi neden yaptığımız** | Projenin defteri |
| `data/` | Elle hazırlanan **küçük veriler** (torbalar, altın set) | Mutfaktaki malzeme rafı |
| `ai/` | Modeli **yapan** Python kodu | Fırın ve tarifler |
| `unity/` | Oyunun **kendisi** (C#) | Lokantanın salonu |

İki ekip bu klasörler üzerinden buluşur:
- `docs/kart_formati.md` → İki ekibin **ortak dili.** Model kartı bu biçimde yazar, Unity bu biçimde okur.
- `data/altin_set/yedek_deste.json` → Model olmasa bile oyunun oynanmasını sağlayan kartlar.
- `docs/api.md` → Unity'nin Python'a "bana kart ver" deme kuralı.

**Altın kural:** Büyük dosyalar (model ağırlıkları, yüz binlerce hikâye) Git'e **girmez.** Drive ve Hugging Face'te durur (`.gitignore` bunları otomatik dışarıda bırakır).

---

## Kök dizin

| Dosya | Ne işe yarar | İçine ne yazılır |
| --- | --- | --- |
| `README.md` | Depoyu ilk açan kişinin okuduğu sayfa | Proje ne, klasörler, ilk kurulum komutları, çalışma kuralları özeti. Proje ilerledikçe "nasıl çalıştırılır" bölümü güncellenir (son hâli 8. hafta) |
| `.gitignore` | Git'e **girmemesi** gereken dosyaların listesi | Python önbellekleri, sanal ortam, model ağırlıkları (`*.bin`, `*.pt`), Unity'nin geçici klasörleri (`Library/`, `Temp/`). Biri yanlışlıkla 2 GB'lık dosya yüklemesin diye |
| `.gitattributes` | Git'in bazı dosyaları **nasıl** saklayacağı | Görsel/ses → Git LFS. Unity sahneleri → Unity'nin birleştirme aracı (iki kişi aynı sahneyi değiştirirse çakışma azalır) |

---

## `docs/` · Belgeler

> **Mantık:** Bir şey kararlaştırıldıysa burada yazılıdır. Sohbette kalan karar yoktur.

| Dosya | Ne işe yarar | İçine ne yazılır | Kim, ne zaman |
| --- | --- | --- | --- |
| `yol_haritasi.md` | 8 haftalık plan | Haftalar, görevler, kişi kişi plan, devir günleri | Koordinatör; her çarşamba gerekirse güncellenir |
| `hazirlik_haftasi.md` | İlk haftanın belgesi + torbaların mantığı | Torbalar, kart kuralları, TinyStories notları | Tamamlandı; arşiv olarak kalır |
| `kararlar.md` | **Karar günlüğü** | Her satır: tarih · karar · neden. Yeni karar en alta | Toplantı kararlarını koordinatör yazar |
| `ekip.md` | Kim kim, hangi dönem nerede | Dönemler, roller, altın set okuma sırası, teslim sorumlusu | Değişince güncellenir |
| `kurulum.md` | Ne kurulacak, nasıl | Adım adım kurulum + kontrol listesi | Unity sürümü 1. haftada yazılır |
| `kart_formati.md` | İki ekibin **ortak dili** | Modelin yazdığı biçim, Unity JSON'u, doğrulayıcı listesi | 1. haftada kesinleşir; sonra değişirse **iki ekip birlikte** değiştirir |
| `api.md` **[H5]** | Unity ↔ Python bağlantı kuralı | Adres (`localhost:8000/kart`), istek ve cevap örnekleri, hata durumları | YZ + Oyun birlikte |
| `tema.json` | Oyunun **sabit bilgileri** | Göstergeler, etki kademeleri, sonların metinleri, karakterler, hitaplar, yasak kelimeler | Kod (Python ve Unity) buradan okur. Unity'ye kopyası gider |
| `rol_konu.json` **[H3]** | Hangi rol hangi dertleri getirir | `"kadi": ["miras", "hırsızlık", "kadı kararı"…]` | Oyun ekibi; Kadı ordu işi getirmesin diye |
| `fikir_notlari.md` | İleride bakılacak fikirler | Karar değil, not (ör. kısıtlı üretim) | Herkes |
| `repo_rehberi.md` | Bu belge | — | Yeni dosya eklenince güncellenir |

### `docs/raporlar/`

| Dosya | Ne işe yarar | İçine ne yazılır |
| --- | --- | --- |
| `README.md` | Rapor şablonu | Dönem raporunun başlıkları |
| `ogretmen_secimi.md` | Öğretmen model neden seçildi | LM Studio denemesi (2 tur), promptlar, çıktılar, değerlendirme. Colab hız ölçümü sonuçları da eklenecek |
| `donem-N-yapay-zeka.md` / `donem-N-oyun.md` | **Devir belgesi** | Ne yapıldı, ne yarım, nasıl çalıştırılır, büyük dosyalar nerede, sayılar, yeni gelen için ilk 3 adım. Dönemin son pazarı giden başkan yazar |
| `denge_testi.md` **[H4]** | Oyun dengesi | Kaç oyun oynandı, ortalama kaç yıl dayanıldı, hangi gösterge çok hızlı bitiyor, belirlenen hedef süre |
| `oyun_testi.md` **[H7]** | Ekip dışı oyuncu testi | Kim oynadı, ne gözlendi, hangi sorunlar düzeltildi |

---

## `data/` · Küçük veriler

> **Mantık:** Elle hazırlanan, Git'te takip edilmesi gereken veriler burada. Kodun ürettiği büyük veriler burada **değil**, Drive/Hugging Face'te.

### `data/torbalar/`
| Dosya | İçine ne yazılır | Örnek |
| --- | --- | --- |
| `Torba_Listesi.xlsx` | **Asıl kaynak.** Herkes buraya yazar | — |
| `kelimeler.csv` | `kelime,tur,ekleyen` | `kervan,isim,Claude` |
| `karakterler.csv` | `rol,konusma_tonu` | `Kadı,"ağırbaşlı, kuralcı"` |
| `olaylar.txt`, `konular.txt`, `yer.txt`… | Her satırda bir madde | `kuraklık` |
| `ikilem.csv` | `taraf1,taraf2` | `adalet,merhamet` |

**Neden hem Excel hem metin dosyası?** Excel insanlar için rahat (açılır liste, tekrar uyarısı). Metin dosyaları kod için rahat (Python kolay okur, Git'te değişiklik satır satır görünür). Excel'den dışa aktarma bir betikle yapılır 💡.

### `data/altin_set/`
| Dosya | Ne | Biçim |
| --- | --- | --- |
| `ham/<isim>.jsonl` | Sohbet ekranından gelen, henüz okunmamış kartlar | Her satır bir kart (Unity JSON biçimi) |
| `iyi.jsonl` | Çapraz okumadan "iyi" alanlar | Aynı |
| `sinav.jsonl` **[H4]** | 200 kart. **Modele hiç gösterilmez**, sonunda ölçmek için | Aynı |
| `yedek_deste.json` **[H2]** | En iyi kartlar (hedef 600). Model hata verirse oyun bunlarla devam eder | Kart listesi |

**JSONL nedir?** Her satırı ayrı bir JSON olan dosya. Kart eklemek = dosyanın sonuna bir satır eklemek. Dört kişi aynı anda eklese bile Git'te çakışma azdır.

### Diğerleri
| Klasör | İçinde |
| --- | --- |
| `uretilen/ornekler/` | Öğretmen üretiminden okunmak için küçük örnekler (100–500 tane). Tamamı Drive'da |
| `edebiyat/` **[H2]** | Lisansı temiz metinler + her biri için kaynak/lisans notu |

---

## `ai/` · Yapay zekâ (Python)

> **Mantık:** Klasörler **akış sırasına** göre dizildi. Bir klasörün çıktısı bir sonrakinin girdisi:
>
> `veri_uretimi` → `filtre` → `tokenizer` → `veri_hazirlama` → `model` + `egitim` → `ornekleme` → `olcum` → `kart_uretici`
>
> Kod adım adım yazılır: **sor → küçük parça yazdır → çalıştır ve gör → not al.**

| Dosya | Ne işe yarar | Girdi → Çıktı |
| --- | --- | --- |
| `requirements.txt` | Gereken Python paketleri | `pip install -r` ile kurulur |

### `ai/ortak/` **[H1]** · Herkesin kullandığı parçalar
| Dosya | Ne yapar |
| --- | --- |
| `kart_bicimi.py` | Kartı üç biçim arasında çevirir: **model metni** (`<kart> … <sol> …`) ↔ **Python sözlüğü** ↔ **Unity JSON'u**. Etki işaretlerini sayıya çevirir (`++` → 10). Filtre, doğrulayıcı, ölçüm hepsi bunu kullanır; bir kez doğru yazılınca her yerde doğru olur |
| `ayarlar.py` | Sabitler tek yerde: dosya yolları, gösterge adları, etki kademeleri. Bir değer değişince sadece burası değişir |

### `ai/veri_uretimi/` **[Hz–H1]** · Öğretmenle veri üretmek
| Dosya | Ne yapar | Girdi → Çıktı |
| --- | --- | --- |
| `torbalar.py` | Torbaları okur, rastgele çeker | `data/torbalar/*` → `{"karakter": "Çoban", "olay": "kuraklık", "kelimeler": [...]}` |
| `istek_olusturucu.py` | Çekilenleri prompt şablonuna yerleştirir | torba seçimi + `promptlar/*.txt` → öğretmen için tam metin |
| `promptlar/hikaye.txt`, `kart.txt`, `uslup.txt` | Prompt **şablonları**. İçinde `{karakter}`, `{olay}` gibi boşluklar var | Kod boşlukları doldurur |
| `uretici.py` | Öğretmen modeli çalıştırır, cevabı dosyaya yazar | prompt → `uretilen/gece_XX.jsonl` (Drive) |
| `hiz_olcumu.ipynb` | Colab: öğretmen saatte kaç hikâye yazıyor | Öğretmen seçimi için sayı |
| `uretim.ipynb` | Colab: gece boyu toplu üretim | "Tümünü çalıştır" ile başlar, Drive'a yazar |

**Neden prompt ayrı bir `.txt`?** Prompt'u değiştirmek için kod değiştirmek gerekmesin. Oyun ekibindeki biri de prompt'u okuyup düzeltebilsin.

### `ai/filtre/` **[H1]** · Kötüleri ayıklamak
| Dosya | Ne yapar |
| --- | --- |
| `kurallar.py` | Her kural küçük bir fonksiyon: "çok kısa mı?", "yasak kelime var mı?", "aşırı nadir kelime çok mu?", "aynısı daha önce var mı?", "kart biçimi bozuk mu?" |
| `filtre.py` | Ham üretimi kurallardan geçirir. Geçenleri `temiz/`'e yazar, **kaç tanesinin hangi kuraldan atıldığını** raporlar (öğretmen promptunu düzeltmek için önemli) |

### `ai/tokenizer/` **[H2]** · Metni parçalara bölmek
**Mantık:** Model harfleri değil "parçaları" (token) okur. Tokenizer, Türkçe metni en sık geçen parçalara bölmeyi öğrenir (`evlerimizden` → `ev`, `ler`, `imiz`, `den` gibi).

| Dosya | Ne yapar |
| --- | --- |
| `egit_tokenizer.py` | Temiz veriden tokenizer eğitir; kart etiketlerini (`<kart>`, `<sol>`, `{hitap}`…) **bölünmez özel parça** olarak ekler; Hugging Face'e yükler |
| `incele.ipynb` | Türkçe kelimelerin nasıl bölündüğünü gösterir. Sunum için de güzel bir slayt |

### `ai/veri_hazirlama/` **[H2]** · Eğitime hazırlamak
| Dosya | Ne yapar |
| --- | --- |
| `hazirla.py` | Karışım oranlarına göre (hikâye %55–65, kart %15–20…) metinleri birleştirir, tokenizer'la sayılara çevirir, `train.bin` (eğitim) ve `val.bin` (doğrulama) dosyalarını yazar. Kaç token olduğunu raporlar |

### `ai/model/` **[H3–H4]** · Modelin kendisi
| Dosya | Ne yapar |
| --- | --- |
| `model.py` | Dil modelinin mimarisi (nanoGPT örnek alınarak). Her parçanın (gömme, dikkat, ileri besleme) ne yaptığı yorum satırlarında Türkçe açıklanır |
| `boyutlar/1m.yaml`, `10m.yaml`, `30m.yaml` | Modelin boyut ayarları (katman sayısı, genişlik, dikkat başı sayısı…). Kod aynı, sadece bu dosya değişir |

**Neden boyutlar ayrı dosyada?** 1M, 10M ve 30M aynı kodla eğitilir. Hangisinin eğitildiği sadece hangi `.yaml`'ın verildiğine bağlı.

### `ai/egitim/` · Eğitmek
| Dosya | Ne yapar |
| --- | --- |
| `egit.py` **[H3]** | Ön eğitim döngüsü: veriyi okur, modeli eğitir, kayıp grafiği çizer, belli aralıklarla kayıt noktası alır (Colab kopsa bile kaldığı yerden devam için) |
| `egitim.ipynb` **[H3]** | Colab defteri: Drive'ı bağlar, `egit.py`'yi seçilen boyutla çalıştırır |
| `ince_ayar.py` **[H5]** | Ön eğitimli modeli altın setle ince ayar yapar. 1. tur 5. haftada (~1.250 kart), 2. tur 7. haftada (~2.300 kart). Sınav kartları hariç |

### `ai/ornekleme/` **[H3]** · Modele yazdırmak
| Dosya | Ne yapar |
| --- | --- |
| `ornek_uret.py` | Eğitilmiş modelden metin üretir. Sıcaklık (ne kadar yaratıcı), uzunluk gibi ayarlar. "Model ne öğrendi?" sorusunun ilk cevabı |

### `ai/olcum/` **[H4]** · Model ne kadar iyi?
| Dosya | Ne ölçer |
| --- | --- |
| `sinav.py` | 200 sınav kartının durumlarıyla model kart yazar: biçim geçerli mi, doğrulayıcıdan geçiyor mu (%) |
| `ogretmen_puanlama.py` | Öğretmen model, modelin kartlarına Türkçe / tutarlılık / takas puanı verir (TinyStories yöntemi) |
| `ezber_testi.py` | Modelin yazdığı 4–5 kelimelik parçalar eğitim verisinde geçiyor mu? "Ezberlemiyor, yeni yazıyor" kanıtı |
| `ic_bakis.ipynb` **[H7]** | Modelin içine bakış: hangi dikkat başı neye bakıyor. Sunum slaytı |
| `sonuclar/` | Tablolar ve grafikler (1M / 10M / 30M karşılaştırması burada) |

### `ai/kart_uretici/` **[H5–H6]** · Oyuna kart vermek
| Dosya | Ne yapar |
| --- | --- |
| `sahte_sunucu.py` **[H5]** | Model yokken yedek desteden rastgele kart döner. Oyun ekibi, model hazır olmadan bağlantıyı deneyebilsin diye |
| `uretici.py` **[H6]** | Oyunun gönderdiği durumdan (göstergeler, konu, konuşan) modelin ilk satırını kurar, kartı yazdırır |
| `dogrulayici.py` **[H6]** | Kartı 8 maddelik listeden geçirir (`kart_formati.md` 4. bölüm). Geçmezse yeniden yazdırılır |
| `kisitli_uretim.py` **[H6]** | "Bekçi": model yazarken biçimin dışına çıkmasını engeller (`fikir_notlari.md`) |
| `sunucu.py` **[H6]** | Dizüstünde çalışan yerel sunucu. Unity `POST /kart` der, bu dosya `uretici` + `dogrulayici`'yı çalıştırıp JSON döner |

### `ai/disa_aktarma/` **[H7, zaman kalırsa]**
Modeli ONNX'e çevirip Unity Sentis ile telefonun içinde çalıştırma denemesi.

### `ai/testler/`
| Dosya | Neyi test eder |
| --- | --- |
| `test_kart_bicimi.py` **[H1]** | Dönüşümler doğru mu (`++` gerçekten 10 mu, bozuk kart hata veriyor mu) |
| `test_filtre.py` **[H1]** | Her kural doğru kartı atıyor mu |
| `test_dogrulayici.py` **[H6]** | 8 kontrolün her biri için doğru ve yanlış örnek |

**Neden test?** Rol değişince yeni gelen kişi bir şeyi bozduğunu `pytest ai/testler` ile hemen görür. Devir teslimi kolaylaştırır.

---

## `unity/` · Oyun (C#)

> **Mantık:** Kod **dört katman**a ayrıldı. Her katman sadece kendi işini yapar:
> - **Cekirdek** = oyunun kuralları (sayılar, sonlar). Ekranı bilmez.
> - **Kartlar** = kart nereden gelir, nasıl hazırlanır. Ekranı bilmez.
> - **Arayuz** = ekranda ne görünür. Kuralları bilmez, Cekirdek'e sorar.
> - **Ag** = Python'la konuşmak.
>
> Böylece mesela kartın yedek desteden mi modelden mi geldiği değişince ekran kodu hiç değişmez.

### `Assets/Scenes/`
| Dosya | Ne |
| --- | --- |
| `Oyun.unity` **[H1]** | Tek sahne. Açılış, kart, sonuç ve son ekranları aynı sahnede **paneller** olarak durur, sırayla açılıp kapanır. Tek sahne = daha az çakışma, daha kolay akış |

### `Assets/Scripts/Cekirdek/` · Oyunun kuralları
| Dosya | Ne yapar |
| --- | --- |
| `OyunYoneticisi.cs` **[H1]** | **Orkestra şefi.** Akışı yönetir: açılış → kart iste → kaydırma bekle → etkiyi uygula → sonuç ekranı → son mu? → sonraki kart |
| `OyunDurumu.cs` **[H1]** | Oyunun o anki hâli: 4 gösterge, yıl, kaçıncı kart, cinsiyet, bu oyunda atanan isimler |
| `Gostergeler.cs` **[H1]** | Etkiyi uygular (`para -10`), değerleri 0–100 arasında tutar, sınıra değince haber verir |
| `SonKontrolu.cs` **[H2]** | Hangi son geldi? (8 son + kazanma sonu) |
| `YilSayaci.cs` **[H2]** | Her N kartta bir yıl ilerletir (N, denge testinde belirlenir) |
| `KayitSistemi.cs` **[H3]** | Oyunu kaydeder (devam et) ve rekoru tutar |

### `Assets/Scripts/Kartlar/` · Kartlar nereden gelir
| Dosya | Ne yapar |
| --- | --- |
| `Kart.cs` **[H1]** | Kartın veri sınıfı. `kart_formati.md`'deki JSON'un C# karşılığı |
| `IKartKaynagi.cs` **[H1]** | **Arayüz (sözleşme):** "Bana bir kart ver." Kim verirse versin, oyun aynı şekilde kullanır |
| `YedekDeste.cs` **[H1]** | `yedek_deste.json`'dan kart verir. İlk haftalarda oyunun tek kart kaynağı |
| `ModelKartKaynagi.cs` **[H5]** | Python sunucusundan kart ister. Cevap gelmezse ya da bozuksa **otomatik yedek desteye düşer** |
| `KartSecici.cs` **[H3]** | Sıradaki kartta kim konuşacak, konu ne olacak (`rol_konu.json`'a göre) |
| `MetinYerlestirici.cs` **[H1]** | `{hitap}` → "Beyim"/"Hatunum", başlığa "Defterdar Yakup" gibi unvan + isim |

**Neden `IKartKaynagi` var?** Oyun ekibi 1. haftadan itibaren yedek desteyle çalışır. 5. haftada `ModelKartKaynagi` eklenince oyunun geri kalanında **tek satır** değişir: hangi kaynağın kullanılacağı.

### `Assets/Scripts/Arayuz/` · Ekranlar
| Dosya | Ne gösterir |
| --- | --- |
| `AcilisEkrani.cs` **[H1]** | Açılış hikâyesi, cinsiyet seçimi, "Tahta Çık" |
| `KartGorunumu.cs` **[H1]** | Başlık (unvan + isim), portre, kart metni |
| `KaydirmaKontrolu.cs` **[H1]** | Parmakla sürükleme; sürüklerken seçenek yazısı + oklar (Para ▼ Halk ▲); bırakınca karar |
| `GostergeCubugu.cs` **[H1]** | Üstteki 4 gösterge |
| `SonucEkrani.cs` **[H2]** | Sonuç cümlesi + sayılar (Para −10, Halk +5) + "Devam Et" |
| `SonEkrani.cs` **[H2]** | Son resmi ve metni, "Yeniden Dene" |

### `Assets/Scripts/Ag/`
| Dosya | Ne yapar |
| --- | --- |
| `PythonBaglantisi.cs` **[H5]** | `localhost:8000/kart`'a istek atar, 3 saniye bekler (`api.md`) |

### Diğer klasörler
| Klasör | İçinde |
| --- | --- |
| `StreamingAssets/` | Oyunun okuduğu veri dosyaları: `tema.json` [H1], `yedek_deste.json` [H2], `rol_konu.json` [H3]. **Kopya**dır; asılları `docs/` ve `data/`'da durur. Asıl değişince kopya da güncellenir |
| `Art/Portreler/` **[H4]** | 15 rolün portresi (dosya adı = rol anahtarı, ör. `defterdar.png`) |
| `Art/Sonlar/` **[H4]** | 8 son + kazanma sonu resimleri (`halk_0.png`, `kazanma.png`) |
| `Art/Arayuz/` **[H4]** | Çerçeveler, gösterge simgeleri, düğmeler |
| `Audio/` **[H4]** | Müzik ve ses efektleri |

---

## Sık sorulanlar

**Yeni bir dosya ekleyeceğim, nereye koyayım?**
Bu rehberde yeri yoksa Discord'a sor, karar verilince bu rehbere de ekle.

**`tema.json`'u değiştirdim, Unity'deki kopyası ne olacak?**
`unity/Assets/StreamingAssets/tema.json`'u da güncelle. 💡 İleride bunu yapan küçük bir betik yazılabilir.

**Kart biçimini değiştirmem gerekiyor.**
Tek başına değiştirme. `kart_formati.md` iki ekibin ortak dili: Python (`kart_bicimi.py`) ve Unity (`Kart.cs`) birlikte değişmeli. Çarşamba toplantısına getir, `kararlar.md`'ye yaz.

**Büyük bir dosyayı Git'e eklemeye çalışıyorum, eklenmiyor.**
Doğru, `.gitignore` engelliyor. Drive ya da Hugging Face'e koy, yerini raporda ve `data/README.md`'de yaz.
