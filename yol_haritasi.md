# Yol Haritası · Kaydır & Karar Ver

*Son güncelleme 26 Ekim 2026 · 8 hafta: 26 Ekim – 20 Aralık 2026*

> **Okuma rehberi**
> - ✅ = Birlikte konuşup **karar verdiğimiz** şeyler.
> - 💡 **Öneri** = Claude'un önerisi. Beğenmediğini söyle, değiştirelim.
> - ⚠️ = İkinci kontrol turunda bulunan, **senin kararını bekleyen** sorunlar (en sonda, 9. bölüm).
> - Her görevde: **ne yapılacak · hangi dosya · ne zaman bitti sayılır · neye bağlı.**

---

## İçindekiler

1. Kararların özeti
2. Ekip ve roller
3. Çalışma düzeni (Git, raporlar, toplantı)
4. Repo yapısı (`ileri-programlama`)
5. Biçimler (model kart biçimi, Godot JSON, Godot ↔ Python bağlantısı)
6. Haftalar (Hazırlık + 1–8)
6b. Kişi kişi haftalık plan
7. Her hafta süren işler (altın set, torbalar)
8. Riskler ve B planı
9. ⚠️ Kontrol turunda bulunanlar (karar bekliyor)

---

## 1. Kararların özeti ✅

| Konu | Karar |
| --- | --- |
| **Süre** | 8 hafta, 26 Ekim – 20 Aralık. 8. hafta sonunda her şey bitmiş: çalışan APK, eğitilmiş 30M model, sunum |
| **Tema** | **Türk tarzı krallık.** "Kral" denir; göstergeler **Yönetim**, Halk, Para, Ordu ✅ (25 Ekim), dünya Türk-İslam kültüründe kalır |
| **Oynanış** | **Düz kart** + kaydırma. Kartlar birbirinden bağımsız |
| **Akış** | Açılış (cinsiyet seçimi, "Tahta Çık") → kart → kaydırma → sonuç ekranı → Devam Et → … → son ekranı |
| **Kart başlığı** | Konuşanın unvanı + ismi ("Hazinedar Yakup"). Oyun kodu koyar, model yazmaz |
| **Hitap** | Oyuncu cinsiyet seçer → "Beyim" / "Hatunum". Model `{hitap}` yazar, **gerektiğinde** (her kartta değil); oyun kodu değiştirir |
| **İsimler** | Oyun kodunda rastgele, her yeni oyunda bir kez. Model isim görmez, kart içinde sadece unvan kullanır |
| **Seçenekler** | Kartın derdine verilen iki farklı **karar** (emir/eylem cümlesi). Soyut başlık yok |
| **Sonuç cümlesi** | Model her seçenek için bir sonuç cümlesi yazar (aynı kartın kapanışı, sonraki karta bağlanmaz) |
| **Etkiler** | 3 kademe: `+` ±5 · `++` ±10 · `+++` ±15. Seçenek başına 1–3 gösterge, iki seçenek de en az birini düşürür |
| **Gösterim** | Kaydırırken sadece ok (Para ▼ Halk ▲), sonuç ekranında sayı (Para −10, Halk +5) |
| **Sonlar** | 8 son (her göstergenin 0'ı ve 100'ü) + kazanma sonu. Hedef süreye ulaşınca kazanır, isterse rekor için devam eder |
| **Karakter–konu uyumu** | Dert, konuşanın işine uygun (Kadı ordu işi getirmez) |
| **Görseller** | 23 rol + "Çift" cinsiyetli 9 rolün ikinci portresi = 32 portre, + açılış + 8 son + kazanma ≈ **42 resim**. Görsel üreticiyle, oyun ekibi |
| **Model** | Sıfırdan: 1M → 10M → 30M. 5. hafta başında karar noktası, gerekirse B planı (LoRA) |
| **Çalıştırma** | Ana hedef: Godot, dizüstündeki Python kart üreticisiyle konuşur. APK yedek desteyle çalışır. Telefona gömme (isteğe bağlı ONNX fizibilitesi) zaman kalırsa |
| **Öğretmen model** | **Gemma 4 E4B** ✅ (25 Ekim). Colab hız ölçümü 1. haftanın ilk işi, hedef veri miktarı ona göre |
| **Ekip** | 2 haftalık dönemler, rol rotasyonu (2. bölüm). Koordinatör: **Mert** |

---

## 2. Ekip ve roller ✅

### Dönemler

| Dönem | Haftalar | Yapay Zekâ: **başkan** + yardımcı | Oyun: **başkan** + yardımcı |
| --- | --- | --- | --- |
| 1 | 1–2 (26 Eki – 8 Kas) | **Mert** + Sokul | **Kara** + Muhammet |
| 2 | 3–4 (9 – 22 Kas) | **Sokul** + Kara | **Muhammet** + Mert |
| 3 | 5–6 (23 Kas – 6 Ara) | **Kara** + Muhammet | **Mert** + Sokul |
| 4 | 7–8 (7 – 20 Ara) | **Muhammet** + Mert | **Sokul** + Kara |

- **Ekip içinde her şey birlikte (eşli) yapılır** ✅: başkan ve yardımcı aynı görevlerde çalışır, görevler kişiye bölünmez.
- Herkes bir alanda **4 hafta** kalır: 2 hafta yardımcı, 2 hafta başkan. (İlk dönemde Mert ve Kara doğrudan başkan başlar.)
- 8 haftanın sonunda herkes iki alanı da, iki rolü de denemiş olur.

### Başkanın iki görevi
1. **Devir teslim:** Yeni gelen yardımcıya durumu anlatır (pazartesiden itibaren).
2. **Dönem raporu:** Dönemin son pazarı o alanda yaptığı her şeyi ayrıntılı raporlar (giden başkan).

### Diğer roller
| Rol | Kim |
| --- | --- |
| **Koordinatör** | Mert |
| **Teslim sorumlusu** | 1. hafta toplantısında (çarşamba 28 Ekim) kura ile seçilecek ✅ |

---

## 3. Çalışma düzeni

### 3.1 Takvim

| Ne | Ne zaman |
| --- | --- |
| Hafta | Pazartesi – pazar |
| Haftalık toplantı | **Çarşamba öğle arası**, yüz yüze ✅ + Discord · gündem serbest ✅, alınan kararlar `docs/kararlar.md`'ye yazılır |
| Dönem raporu | Dönemin son **pazarı** (2., 4., 6., 8. haftanın pazarı) giden başkan raporu atar ✅ |
| Devir | **Pazartesiden itibaren** (3., 5., 7. hafta) yeni başkan yeni gelene anlatır ✅ |
| Haftanın planı | Her haftalık toplantıda bu haritaya bakılır, gerekirse güncellenir |

### 3.2 Devredilebilir durum ✅ (her 2 haftada bir)

Her dönemin sonunda (pazar) iş, **hiç görmemiş biri pazartesi devam edebilecek** hâlde bırakılır. Giden başkan raporu atmadan önce bu listeyi kontrol eder:

- [ ] Bütün işler PR ile `main`'e birleşti, `main` çalışıyor
- [ ] Yarım kalan işler kendi dalında, raporda "yarım" diye yazılı
- [ ] Raporda **"nasıl çalıştırılır"** bölümü güncel (komutlar, hangi Colab defteri, hangi ayar)
- [ ] Büyük dosyaların (Drive / Hugging Face) yeri ve adı raporda yazılı
- [ ] Colab defterleri baştan sona "Tümünü çalıştır" ile çalışıyor
- [ ] `docs/kararlar.md` güncel
- [ ] O dönemin **devir paketi** (aşağıda) tamam

**Devir paketleri:** Her dönemin sonunda elde ne olmalı:

| Dönem sonu | Yapay Zekâ ekibi devreder | Oyun ekibi devreder |
| --- | --- | --- |
| **1** (pazar 8 Kas) | Çalışan üretim hattı (torba → öğretmen → filtre) · üretilen veri · tokenizer · `train.bin`/`val.bin` | Yedek desteyle baştan sona oynanabilen oyun (açılış, kaydırma, sonuç ekranı, 8 son) |
| **2** (pazar 22 Kas) | Eğitilmiş 1M / 10M / 30M · ölçüm araçları · karşılaştırma tablosu (karar noktası için) | İlk APK · kayıt, kazanma sonu · görseller · denge testi raporu |
| **3** (pazar 6 Ara) | İnce ayarlı model · kart üretici + doğrulayıcı + sunucu | Gerçek modelle çalışan oyun · yedek desteye düşme |
| **4** (pazar 20 Ara) | Son ölçümler · sunum bölümü | Son APK · sunum |

### 3.3 Dönem raporu şablonu 💡

Dosya: `docs/raporlar/donem-{N}-{alan}.md` (ör. `docs/raporlar/donem-1-yapay-zeka.md`)

```markdown
# Dönem N · Yapay Zekâ · Başkan: … · Yardımcı: …
## Ne yapıldı (dosya yollarıyla)
## Ne yarım kaldı, neden
## Nasıl çalıştırılır (komutlar, Colab defterleri)
## Bilinen sorunlar
## Sayılar (ör. üretilen hikâye sayısı, eğitim kaybı, test sonuçları)
## Yeni gelen için ilk 3 adım
```

### 3.4 Git kuralları 💡

| Kural | Ayrıntı |
| --- | --- |
| **Ana dal** | `main` her zaman çalışır durumda. Doğrudan `main`'e yazılmaz |
| **Dal adları** | `yz/<konu>` ve `oyun/<konu>` (ör. `yz/tokenizer`, `oyun/sonuc-ekrani`) |
| **Pull Request** | Her iş PR ile gelir. **En az bir kişi** okuyup onaylar. Tercihen diğer alandan biri; herkes her şeyi görsün |
| **Commit mesajı** | Türkçe, ne yapıldığını söyleyen kısa cümle ("Doğrulayıcıya sonuç cümlesi kontrolü eklendi") |
| **Hafta etiketi** | Her pazar `main` etiketlenir: `hafta-1`, `hafta-2`… Geri dönmek kolay olur |
| **Büyük dosyalar** | Model ağırlıkları, büyük veri setleri Git'e **girmez** (3.5) |

### 3.5 Büyük dosyalar nerede? 💡

| Ne | Nerede | Neden |
| --- | --- | --- |
| Kod, küçük örnek veriler, belgeler | **GitHub** | Sürüm takibi |
| Üretilen yüz binlerce hikâye | **Google Drive** (Colab'dan kolay erişim) + son hâli **Hugging Face** (özel veri seti) | Git'e sığmaz |
| Tokenizer, model ağırlıkları | **Hugging Face** (özel depo) | Sürümlü, büyük dosyaya uygun |
| Görseller, sesler | GitHub, **Git LFS** ile | Godot projesinin parçası |

---

## 4. Repo yapısı · üç bağımsız depo

```text
çalışma-alanı/
├── AI/           # ai/ Python kodu, data/ küçük veri
├── Docs/         # ortak belgeler ve tema.json
└── Game/         # game/ Godot projesi, docs/ oyun planı
```

Bu üst klasör bir Git deposu değildir. Gelecekte oluşturulacak dosyalar ve sorumlulukları [repo rehberinde](repo_rehberi.md), Godot hedef dizinleri ve kabul testleri [Game planında](https://github.com/IleriProgramlamaProje/Game/blob/main/docs/oyun_gelistirme_plani.md) bulunur. Aşağıdaki kısa `ai/` ve `data/` yolları AI deposuna; `docs/` atıfları Docs deposunun köküne aittir. Görev tablosunda bir dosyanın yazması, uygulanmış olduğu anlamına gelmez.

---

## 5. Biçimler

### 5.1 Modelin okuyup yazdığı biçim 💡 (yeni kararlara göre güncellendi)

```
<yonetim:50> <halk:50> <para:60> <ordu:35> <konu:maaş> <konuşan:akıncı_beyi>
<kart> {hitap}, askerler üç aydır maaş alamadı. Kışlada söylenmeler başladı; ödenmezse kaçanlar olacak.
<sol> Maaşları hazineden öde <para--> <ordu++>
<sonuc> Askerler borçlarını ödeyip sevindi, ama hazine iyice eridi.
<sag> Beklesinler, hazine boş <ordu--> <halk->
<sonuc> Kışlada homurtular büyüdü, birkaç asker gece kaçtı.
</kart>
```

- İlk satırı (durum) **oyun kodu** yazar; `<kart>` … `</kart>` arasını **model** yazar. ✅
- Etki işaretleri: `+` ±5 · `++` ±10 · `+++` ±15. ✅
- `{hitap}` gerektiğinde, cümlenin başında ya da ortasında. ✅
- Her seçenekten sonra bir `<sonuc>` cümlesi. ✅ (etiket adı öneri)
- Durum satırı: **4 gösterge + konuşan + konu** ✅. Kartların ~%15'inde `<konu:serbest>`: model derdi kendi seçer ✅.

### 5.2 Godot'taki biçim (JSON) 💡

```json
{
  "konusan": "akinci_beyi",
  "konu": "maas",
  "metin": "{hitap}, askerler üç aydır maaş alamadı…",
  "sol": { "etiket": "Maaşları hazineden öde", "etki": { "para": -10, "ordu": 10 }, "sonuc": "Askerler borçlarını ödeyip sevindi…" },
  "sag": { "etiket": "Beklesinler, hazine boş", "etki": { "ordu": -10, "halk": -5 }, "sonuc": "Kışlada homurtular büyüdü…" },
  "kaynak": "altin_set",
  "lisans": "sadece_ders"
}
```
- `kaynak`: `altin_set` · `model` · `ogretmen`. `lisans`: altın set "sadece ders" diye etiketlenir ✅ (oyun yayınlanırsa çıkarılır).
- Dönüşümü `ai/ortak/kart_bicimi.py` yapar, Godot'ta `Kart.cs` okur.

### 5.3 Godot ↔ Python bağlantısı 💡

| | |
| --- | --- |
| **Yöntem** | Python, dizüstünde **yerel bir sunucu** açar (`localhost:8000`). Godot `HttpRequest` ile istek atar. İnternet gerekmez ✅ |
| **İstek** | `POST /kart` · gövde: `{yonetim, halk, para, ordu, konu, konusan}` |
| **Cevap** | 5.2'deki JSON |
| **Hata** | Sunucu yoksa, 3 sn içinde cevap gelmezse ya da kart doğrulayıcıdan geçmezse → **yedek deste** ✅ |
| **Sözleşme** | `docs/api.md` (5. hafta). Önce `sahte_sunucu.py` ile test, sonra gerçek model |

### 5.4 Doğrulayıcının kontrol listesi (güncel)

1. **Biçim:** `<kart>`, `<sol>`, `<sonuc>`, `<sag>`, `<sonuc>`, `</kart>` yerinde mi?
2. **Uzunluk:** Kart metni 20–35 kelime, en fazla 50
3. **Altın kural:** İki seçenek de en az bir göstergeyi düşürüyor mu?
4. **Gösterge sınırı:** Her seçenek 1–3 gösterge; işaretler sadece `+ ++ +++ - -- ---`
5. **İsim yok:** Sadece unvan
6. **Hitap:** "Beyim/Hatunum" elle yazılmamış; sadece `{hitap}`
7. **Modern kelime yok:** `tema.json`'daki yasak kelimeler
8. **Sonuç cümlesi var mı, boş değil mi?** *(yeni)*

---

## 6. Haftalar

### Hazırlık · 22 – 25 Ekim (bu hafta)

| # | Görev | Kim | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- | --- |
| Hz.1 | GitHub'da **`ileri-programlama`** deposunu aç, `ileri-programlama.zip`'teki iskeleti yükle; Drive klasörünü aç ✅ karar | Mert | Zip'in tamamı | Herkes klonlayabiliyor | — |
| Hz.2 | Kurulum haftasının eksikleri (Godot aynı sürüm, Python, Colab GPU) | Herkes | `docs/kurulum.md` | `kurulum.md`'deki "bitti" listesi tamam | — |
| Hz.3 | **Öğretmen model hız ölçümü** (Gemma 4 E4B, Colab). Defter hazır ✓ | Mert (1. haftanın başı) | `ai/veri_uretimi/hiz_olcumu.ipynb` | "Saatte kaç hikâye / kart" sayısı var | — |
| Hz.4 | ✅ **Öğretmen modeli seçildi:** Gemma 4 E4B | — | `docs/raporlar/ogretmen_secimi.md` | — | — |
| Hz.5 | ✓ **Hikâye/kart üretici kodu yazıldı** (torba → prompt → öğretmen → JSONL, kaldığı yerden devam) + testler. Colab'da ilk gerçek çalıştırma 1. hafta | Claude / Mert | `ai/veri_uretimi/*`, `ai/testler/test_veri_uretimi.py` | Testler geçiyor ✓; Colab'da 20 hikâye üretti | — |
| Hz.6 | Torbalar sürüyor | Herkes | Drive’daki `Torba_Listesi` tablosu | — | — |

### 1. hafta · 26 Ekim – 1 Kasım · Dönem 1

**Hedef:** Kart biçimi kesin · büyük üretim başladı · oyunda ilk kart kaydırılıyor.

**İlk günler, herkes** (💡 pazartesi Discord'da taslak, en geç **çarşamba 28 Ekim toplantısında** onay):
| # | Görev | Dosya | Bitti sayılır |
| --- | --- | --- | --- |
| 1.0a | ✅ **Kart biçimi kesinleşti** (25 Ekim). İki ekip okuyup bilgi edinir | `docs/kart_formati.md` | Herkes okudu |
| 1.0b | ✅ Karakterler hazır (23 rol + kimlik kartı). Bu hafta: **kör tahmin testi** (öğretmene her rolden 3 kart yazdır, isimsiz oku, "kim söyledi?" tahmin et; tutmayan rolün kimliğini keskinleştir) | `docs/tema.json`, `data/torbalar/karakterler.csv` | 23 rol, unvan + kimlik kartı ve kör tahmin sonuçları |
| 1.0c | Teslim sorumlusunu kura ile seç (çarşamba toplantısı) | `docs/ekip.md` | Yazıldı |
| 1.0d | Karar günlüğünü güncel tut (bugüne kadarkiler zip'te yazılı) | `docs/kararlar.md` | Toplantı kararları eklendi |

**Yapay Zekâ ekibi** (Mert + Sokul)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 1.1 | Kart biçimi dönüştürücüsü | `ai/ortak/kart_bicimi.py`, `ai/testler/test_kart_bicimi.py` | Model metni ↔ JSON dönüşümü testlerden geçiyor | 1.0a |
| 1.2 | ✓ Kart promptu yazıldı (sonuç cümlesi, `{hitap}`, 3 kademe, kimlik kartı). Bu hafta: 20 kartlık deneme | `ai/veri_uretimi/promptlar/kart.txt` | 20 kartlık deneme, çoğu kurala uyuyor | Hz.3 |
| 1.3 | ✅ Torbalar dosyada (2000 kelime, 23 rol, 200 olay, 100 konu, 60 yer/üslup/ikilem, 40 ruh hâli/özellik/zaman) | `data/torbalar/*` | — | — |
| 1.4 | **Küçük deneme üretimi:** 500 hikâye + 100 kart, ekip okur | `data/uretilen/ornekler/` | Ekip "bu kalitede devam" dedi | 1.2 |
| 1.5 | **Filtre** | `ai/filtre/filtre.py`, `kurallar.py`, `ai/testler/test_filtre.py` | Deneme üretiminden kötüleri ayıklıyor; kaçının atıldığı raporlanıyor | 1.4 |
| 1.6 | **Büyük üretim başlar** (Colab, gece boyu; o dönemin YZ ekibi kendi hesaplarıyla) ✅ | `ai/veri_uretimi/uretim.ipynb` | Her gece üretim Drive'a yazılıyor, sayısı takip ediliyor | 1.4 |

**Oyun ekibi** (Kara + Muhammet)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 1.7 | Godot projesi, tek sahne, paneller | `Game/game/Sahneler/Oyun.tscn` | Proje herkeste açılıyor | Hz.2 |
| 1.8 | Oyun durumu + göstergeler | `OyunDurumu.cs`, `Gostergeler.cs`, `GostergeCubugu.cs` | 4 gösterge ekranda, etki uygulanınca değişiyor | — |
| 1.9 | Kart verisi + yedek deste okuma | `Kart.cs`, `IKartKaynagi.cs`, `YedekDeste.cs` | Elle yazılmış 10 kartlık JSON'dan kart geliyor | 1.0a |
| 1.10 | Kart ekranı | `KartGorunumu.cs`, `MetinYerlestirici.cs` | Başlık (unvan + isim), metin, `{hitap}` yerine Beyim/Hatunum | 1.9 |
| 1.11 | **Kaydırma** | `KaydirmaKontrolu.cs` | Sürüklerken seçenek yazısı + ok önizlemesi; bırakınca etki uygulanıyor | 1.8, 1.10 |
| 1.12 | Açılış ekranı | `AcilisEkrani.cs` | Hikâye metni, cinsiyet seçimi, Tahta Çık | 1.8 |
| 1.13 | Oyun akışı | `OyunYoneticisi.cs` | Açılış → kart → kart → … döngüsü | 1.11, 1.12 |

**Herkes:** ✅ Altın Set sayfası krallık kurallarıyla güncellendi (25 Ekim); Mert ekiple paylaşır · **altın set üretimi pazartesi başlar.**

### 2. hafta · 2 – 8 Kasım · Dönem 1

**Hedef:** Oyun modelsiz baştan sona oynanıyor · tokenizer hazır.

**Yapay Zekâ ekibi** (Mert + Sokul)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 2.1 | Üretim sürer, filtreden geçir | `uretim.ipynb`, `filtre.py` | Günlük sayı takip ediliyor | 1.6 |
| 2.2 | Hazır veriler: BİLGEM basit Türkçe hikâyeler + lisansı temiz edebiyat | `data/edebiyat/`, `data/README.md` | İndirildi, kaynak ve lisans notu yazıldı | — |
| 2.3 | **Tokenizer** | `ai/tokenizer/egit_tokenizer.py`, `incele.ipynb` | Türkçe kelimelerin nasıl bölündüğü görülüyor; HF'ye yüklendi | 2.1 (veri alt kümesi yeter) |
| 2.4 | **Veri hazırlama** (karışım oranlarına göre) | `ai/veri_hazirlama/hazirla.py` | `train.bin` / `val.bin` oluştu, token sayıları raporlandı | 2.3 |

**Oyun ekibi** (Kara + Muhammet)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 2.5 | **Sonuç ekranı** | `SonucEkrani.cs` | Sonuç cümlesi + sayılar (Para −10, Halk +5) + Devam Et | 1.13 |
| 2.6 | **8 son** + Yeniden Dene | `SonKontrolu.cs`, `SonEkrani.cs` | Her göstergenin 0'ı ve 100'ü ayrı son açıyor (şimdilik yer tutucu resim) | 1.8 |
| 2.7 | Yıl sayacı | `YilSayaci.cs` | Her N kartta yıl artıyor (N şimdilik 5) | 1.13 |
| 2.8 | Yedek desteyi Godot'ya bağla | `Veri/yedek_deste.json` | Altın setten gelen kartlarla oynanıyor | 7.1 |
| 2.9 | **Modelsiz tam oyun** | — | Açılıştan bir sona kadar hatasız oynanıyor | 2.5–2.8 |

**Dönem 1 sonu (pazar 8 Kasım):** 📄 Raporlar atılır · `donem-1-yapay-zeka.md` (Mert) · `donem-1-oyun.md` (Kara)

### 3. hafta · 9 – 15 Kasım · Dönem 2

🔄 **Devir (pazartesi 9 Kasım'dan itibaren):** Yeni başkanlar yeni gelenlere anlatır: YZ'de **Sokul → Kara**, Oyun'da **Muhammet → Mert**.

**Hedef:** İlk modeller eğitiliyor · ilk APK telefonda.

**Yapay Zekâ ekibi** (Sokul + Kara)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 3.1 | Üretimi bitir (hedef sayıya ulaş) | — | Hedef veri miktarı tamam, son `train.bin` | 2.4 |
| 3.2 | **Model kodu** (nanoGPT örnek, satır satır anlayarak) | `ai/model/model.py` | Her bölümün ne yaptığı ekip notunda yazılı | — |
| 3.3 | Eğitim döngüsü + Colab defteri | `ai/egitim/egit.py`, `egitim.ipynb` | Kayıp grafiği çiziliyor, kayıt noktası alınıyor | 3.2 |
| 3.4 | **1M deneme** ("her şey çalışıyor mu") | `ai/model/boyutlar/1m.yaml` | Kayıp düşüyor, düzgün cümleye benzer bir şeyler çıkıyor | 3.3 |
| 3.5 | Örnek üretme | `ai/ornekleme/ornek_uret.py` | Modelden hikâye ve kart çıkarılabiliyor | 3.4 |
| 3.6 | **10M eğitim** | `10m.yaml` | Eğitim bitti, örnekler okundu | 3.4 |

**Oyun ekibi** (Muhammet + Mert)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 3.7 | Rol–konu tablosu | `docs/rol_konu.json`, `KartSecici.cs` | Kart seçilirken konuşan ile konu uyumlu | 1.0b |
| 3.8 | Kazanma sonu + rekor | `SonKontrolu.cs`, `KayitSistemi.cs` | Hedef yıla ulaşınca kazanma sonu; devam edip rekor kırılabiliyor | 2.6 |
| 3.9 | Kayıt | `KayitSistemi.cs` | Oyun kapanıp açılınca devam ediyor | — |
| 3.10 | **İlk APK** | — | Bir Android telefonda modelsiz tam oyun oynandı | 2.9 |

### 4. hafta · 16 – 22 Kasım · Dönem 2

**Hedef:** 30M model eğitiliyor · ölçüm hazır · oyun görselleri ve dengesi.

**Yapay Zekâ ekibi** (Sokul + Kara)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 4.1 | **30M eğitim** | `30m.yaml` | Eğitim bitti (Colab birimlerine dikkat) | 3.6 |
| 4.2 | **Sınav setini ayır** (200 kart) | `data/altin_set/sinav.jsonl` | 200 kart ayrıldı, eğitim verisinde yok | 7.1 |
| 4.3 | Sınav ölçümü | `ai/olcum/sinav.py` | Biçim geçerlilik %, doğrulayıcıdan geçme % | 4.2 |
| 4.4 | Öğretmen-puanlama | `ai/olcum/ogretmen_puanlama.py` | Türkçe / tutarlılık / takas puanı | 4.2 |
| 4.5 | Ezber testi | `ai/olcum/ezber_testi.py` | 4–5 kelimelik parçaların eğitim verisinde geçme oranı | 3.1 |
| 4.6 | 1M / 10M / 30M karşılaştırması | `ai/olcum/sonuclar/` | Tablo + grafik; 5. hafta kararına girdi | 4.1, 4.3–4.5 |

**Oyun ekibi** (Muhammet + Mert)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 4.7 | **Görseller** (tek tarz tarifi ile) | `Gorseller/Portreler/`, `Gorseller/Sonlar/` | ~42 resim (32 portre + 10), aynı tarzda; tarz tarifi `docs/`'ta yazılı | 1.0b |
| 4.8 | Arayüz + ses | `Gorseller/Arayuz/`, `Sesler/` | Görseldeki taslağa yakın görünüm | — |
| 4.9 | **Denge testi** | `docs/raporlar/denge_testi.md` | Ekip 10+ oyun oynadı; hedef süre, kaç kartta bir yıl, kademe değerleri belirlendi | 3.10 |

**Kararlar:** Hedef süre · kaç kartta bir yıl (denge testinden) · **oyunun adı**
**Dönem 2 sonu (pazar 22 Kasım):** 📄 Raporlar atılır · `donem-2-yapay-zeka.md` (Sokul) · `donem-2-oyun.md` (Muhammet)

### 5. hafta · 23 – 29 Kasım · Dönem 3

🔄 **Devir (pazartesi 23 Kasım'dan itibaren):** YZ'de **Kara → Muhammet**, Oyun'da **Mert → Sokul**.

⚠️ **Karar noktası (çarşamba 25 Kasım toplantısı)** ✅: 4.6'daki sonuçlara bakılır. **30M yeterli mi?**
- **Evet** → ince ayara geçilir.
- **Hayır** → B planı (8. bölüm). Ayrıntısı bu toplantıda konuşulur.

**Yapay Zekâ ekibi** (Kara + Muhammet)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 5.1 | **İnce ayar · 1. tur** (eldeki ~1.250 altın set kartıyla, sınav kartları hariç) | `ai/egitim/ince_ayar.py` | Sınav ölçümünde ince ayar öncesine göre iyileşme | karar noktası |
| 5.2 | Bağlantı sözleşmesi (oyun ekibiyle) | `docs/api.md` | İki ekip onayladı | 1.0a |
| 5.3 | Sahte sunucu | `ai/kart_uretici/sahte_sunucu.py` | Yedek desteden kart dönüyor | 5.2 |

**Oyun ekibi** (Mert + Sokul)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 5.4 | Python bağlantısı | `PythonBaglantisi.cs`, `ModelKartKaynagi.cs` | Godot sahte sunucudan kart alıyor | 5.3 |
| 5.5 | Yedek desteye düşme | `ModelKartKaynagi.cs` | Sunucu kapalıyken oyun takılmadan yedek desteyle devam ediyor | 5.4 |
| 5.6 | Bekleme ekranı | `KartGorunumu.cs` | Kart gelirken kısa bir "yazılıyor…" görünümü | 5.4 |

### 6. hafta · 30 Kasım – 6 Aralık · Dönem 3

**Hedef:** Oyun gerçek modelle çalışıyor.

**Yapay Zekâ ekibi** (Kara + Muhammet)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 6.1 | **Kart üretici** | `ai/kart_uretici/uretici.py` | Oyun durumundan kart üretiyor | 5.1 |
| 6.2 | **Doğrulayıcı** (5.4 listesi) + testler | `dogrulayici.py`, `test_dogrulayici.py` | 8 kontrol testlerden geçiyor | 1.1 |
| 6.3 | Kısıtlı üretim ("bekçi") | `kisitli_uretim.py` | Biçim hatası oranı düştü (öncesi/sonrası ölçüldü) | 6.1 |
| 6.4 | **Gerçek sunucu** | `sunucu.py` | `api.md`'ye uygun; 3 sn içinde cevap | 6.1, 6.2 |

**Oyun ekibi** (Mert + Sokul)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 6.5 | **Gerçek modelle bağlantı** (YZ ile birlikte) | — | Dizüstünde oyun modelin yazdığı kartlarla oynanıyor | 6.4, 5.5 |
| 6.6 | Model kartlarının oyunda görünümü | `KartGorunumu.cs`, `SonucEkrani.cs` | Uzun/kısa metinler ekrana düzgün sığıyor | 6.5 |

**Dönem 3 sonu (pazar 6 Aralık):** 📄 Raporlar atılır · `donem-3-yapay-zeka.md` (Kara) · `donem-3-oyun.md` (Mert)

### 7. hafta · 7 – 13 Aralık · Dönem 4

🔄 **Devir (pazartesi 7 Aralık'tan itibaren):** YZ'de **Muhammet → Mert**, Oyun'da **Sokul → Kara**.

**Hedef:** Ölçüm, iyileştirme, dış test.

**Yapay Zekâ ekibi** (Muhammet + Mert)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 7.0y | **İnce ayar · 2. tur** (bütün altın setle, ~2.300 kart) | `ai/egitim/ince_ayar.py` | 1. tura göre sınav ölçümü karşılaştırıldı | 5.1, 7.1 |
| 7.1y | **Son ölçüm turu** (sınav, öğretmen-puanlama, ezber, oyunda doğrulayıcıdan geçme oranı) | `ai/olcum/sonuclar/` | Tablo + grafikler | 6.4 |
| 7.2y | İyileştirme (ölçümün gösterdiği en büyük sorun) | — | Öncesi/sonrası ölçüldü | 7.1y |
| 7.3y | Modelin içine bakış (sunum için) | `ai/olcum/ic_bakis.ipynb` | En az bir anlaşılır dikkat başlığı görseli | 4.1 |
| 7.4y | *Zaman kalırsa:* ONNX'e çevirme + Godot/ONNX fizibilitesi | `ai/disa_aktarma/` | Model Godot içinde bir kart üretti | 6.4 |

**Oyun ekibi** (Sokul + Kara)
| # | Görev | Dosya | Bitti sayılır | Bağlı |
| --- | --- | --- | --- | --- |
| 7.5o | **Ekip dışından oyuncularla test** (en az 5 kişi) | `docs/raporlar/oyun_testi.md` | Gözlemler ve sorunlar yazıldı | 6.5 |
| 7.6o | Hata düzeltme + denge | — | Testteki önemli sorunlar düzeltildi | 7.5o |

### 8. hafta · 14 – 20 Aralık · Dönem 4

**Hedef:** Teslim.

| # | Görev | Kim | Dosya | Bitti sayılır |
| --- | --- | --- | --- | --- |
| 8.1 | Cila (son görsel/ses düzeltmeleri) | Oyun | — | — |
| 8.2 | **Son APK** (yedek desteyle) | Oyun + teslim sorumlusu | — | Telefonda hatasız oynanıyor |
| 8.3 | Dizüstü sunum kurulumu (Godot + Python sunucu, internetsiz) | YZ + Oyun | `docs/kurulum.md` | Sıfırdan kurulup çalıştırıldı |
| 8.4 | **Sunumun model bölümü** (merdiven 1M→30M, ölçüm grafikleri, modelin içi) | YZ ekibi (Muhammet + Mert) ✅ | sunum | Bölüm bitti, provası yapıldı |
| 8.5 | **Sunumun oyun bölümü** (oynanış, canlı gösterim, test sonuçları) | Oyun ekibi (Sokul + Kara) ✅ | sunum | Bölüm bitti, provası yapıldı |
| 8.5b | Sunumu birleştir, tam prova | Herkes | sunum | Baştan sona bir prova yapıldı |
| 8.6 | README'nin son hâli | Teslim sorumlusu | `README.md` | Biri sıfırdan okuyup çalıştırabiliyor |

**Dönem 4 sonu (pazar 20 Aralık):** 📄 Son raporlar · `donem-4-yapay-zeka.md` (Muhammet) · `donem-4-oyun.md` (Sokul)

---

## 6b. Kişi kişi haftalık plan ✅

> Ekip içinde görevler **eşli** yapılır, o yüzden aynı ekipteki iki kişinin görev listesi aynıdır. Bu bölüm, herkesin **kendi haftasını** tek bakışta görmesi için.
> Her hafta herkes ayrıca: **altın set ~78 iyi kart** (günde ~11) + **çapraz okuma** + **çarşamba toplantısı**.

| Kişi | Okuduğu kartlar |
| --- | --- |
| Mert | Sokul'un kartları |
| Sokul | Kara'nın kartları |
| Kara | Muhammet'in kartları |
| Muhammet | Mert'in kartları |

### Mert

| Hafta | Alan · rol | Görevler (6. bölümdeki numaralar) | Ek görev |
| --- | --- | --- | --- |
| Hazırlık | — | Hz.3–Hz.5: hız ölçümü, öğretmen seçimi, hikâye üretici · Hz.2, Hz.6 | Koordinatör |
| **1** (26 Eki – 1 Kas) | Yapay Zekâ · **başkan** (+ Sokul) | 1.1–1.6: Kart biçimi, kart promptu, deneme üretimi, filtre, büyük üretim | Gece üretimi (Colab) · 1.0a–1.0d (herkes) · Koordinatör |
| **2** (2 – 8 Kas) | Yapay Zekâ · **başkan** (+ Sokul) | 2.1–2.4: Üretim, hazır veriler, tokenizer, veri hazırlama | Gece üretimi (Colab) · 📄 Pazar raporu: `donem-1-yapay-zeka.md` · Koordinatör |
| **3** (9 – 15 Kas) | Oyun · yardımcı (+ Muhammet) | 3.7–3.10: Rol–konu tablosu, kazanma sonu, kayıt, ilk APK | 🔄 Yeni geldi; Muhammet'ten devir alır · Koordinatör |
| **4** (16 – 22 Kas) | Oyun · yardımcı (+ Muhammet) | 4.7–4.9: Görseller, arayüz, ses, denge testi | Denge testinde oyna (herkes) · Koordinatör |
| **5** (23 – 29 Kas) | Oyun · **başkan** (+ Sokul) | 5.4–5.6: Python bağlantısı, yedek desteye düşme, bekleme ekranı | 🔄 Pazartesiden itibaren Sokul'a devir anlatır · Karar noktası toplantısı (çar 25 Kas) · Koordinatör |
| **6** (30 Kas – 6 Ara) | Oyun · **başkan** (+ Sokul) | 6.5–6.6: Gerçek modelle bağlantı, model kartlarının görünümü | 📄 Pazar raporu: `donem-3-oyun.md` · Koordinatör |
| **7** (7 – 13 Ara) | Yapay Zekâ · yardımcı (+ Muhammet) | 7.0y–7.4y: İnce ayar 2. tur, son ölçüm, iyileştirme, modelin içi, (isteğe bağlı ONNX fizibilitesi) | 🔄 Yeni geldi; Muhammet'ten devir alır · Oyun testi için tanıdık getir · Koordinatör |
| **8** (14 – 20 Ara) | Yapay Zekâ · yardımcı (+ Muhammet) | 8.3, 8.4: Dizüstü sunum kurulumu, sunumun model bölümü | Tam prova (herkes) · Koordinatör |

### Sokul

| Hafta | Alan · rol | Görevler (6. bölümdeki numaralar) | Ek görev |
| --- | --- | --- | --- |
| Hazırlık | — | Hz.2 kurulum eksikleri · Hz.6 torbalar | — |
| **1** (26 Eki – 1 Kas) | Yapay Zekâ · yardımcı (+ Mert) | 1.1–1.6: Kart biçimi, kart promptu, deneme üretimi, filtre, büyük üretim | Gece üretimi (Colab) · 1.0a–1.0d (herkes) |
| **2** (2 – 8 Kas) | Yapay Zekâ · yardımcı (+ Mert) | 2.1–2.4: Üretim, hazır veriler, tokenizer, veri hazırlama | Gece üretimi (Colab) |
| **3** (9 – 15 Kas) | Yapay Zekâ · **başkan** (+ Kara) | 3.1–3.6: Üretimi bitirme, model kodu, eğitim döngüsü, 1M, 10M | Gece üretimi (Colab) · 🔄 Pazartesiden itibaren Kara'ya devir anlatır |
| **4** (16 – 22 Kas) | Yapay Zekâ · **başkan** (+ Kara) | 4.1–4.6: 30M, sınav seti, ölçüm araçları, karşılaştırma | 📄 Pazar raporu: `donem-2-yapay-zeka.md` · Denge testinde oyna (herkes) |
| **5** (23 – 29 Kas) | Oyun · yardımcı (+ Mert) | 5.4–5.6: Python bağlantısı, yedek desteye düşme, bekleme ekranı | 🔄 Yeni geldi; Mert'ten devir alır · Karar noktası toplantısı (çar 25 Kas) |
| **6** (30 Kas – 6 Ara) | Oyun · yardımcı (+ Mert) | 6.5–6.6: Gerçek modelle bağlantı, model kartlarının görünümü |  |
| **7** (7 – 13 Ara) | Oyun · **başkan** (+ Kara) | 7.5o–7.6o: Ekip dışı oyun testi, hata düzeltme, denge | 🔄 Pazartesiden itibaren Kara'ya devir anlatır · Oyun testi için tanıdık getir |
| **8** (14 – 20 Ara) | Oyun · **başkan** (+ Kara) | 8.1, 8.2, 8.5: Cila, son APK, sunumun oyun bölümü | 📄 Pazar raporu: `donem-4-oyun.md` · Tam prova (herkes) |

### Kara

| Hafta | Alan · rol | Görevler (6. bölümdeki numaralar) | Ek görev |
| --- | --- | --- | --- |
| Hazırlık | — | Hz.2 kurulum eksikleri · Hz.6 torbalar | — |
| **1** (26 Eki – 1 Kas) | Oyun · **başkan** (+ Muhammet) | 1.7–1.13: Godot sahnesi, göstergeler, kart ekranı, kaydırma, açılış, oyun akışı | 1.0a–1.0d (herkes) |
| **2** (2 – 8 Kas) | Oyun · **başkan** (+ Muhammet) | 2.5–2.9: Sonuç ekranı, 8 son, yıl sayacı, yedek deste, modelsiz tam oyun | 📄 Pazar raporu: `donem-1-oyun.md` |
| **3** (9 – 15 Kas) | Yapay Zekâ · yardımcı (+ Sokul) | 3.1–3.6: Üretimi bitirme, model kodu, eğitim döngüsü, 1M, 10M | Gece üretimi (Colab) · 🔄 Yeni geldi; Sokul'dan devir alır |
| **4** (16 – 22 Kas) | Yapay Zekâ · yardımcı (+ Sokul) | 4.1–4.6: 30M, sınav seti, ölçüm araçları, karşılaştırma | Denge testinde oyna (herkes) |
| **5** (23 – 29 Kas) | Yapay Zekâ · **başkan** (+ Muhammet) | 5.1–5.3: İnce ayar 1. tur, api.md, sahte sunucu | 🔄 Pazartesiden itibaren Muhammet'e devir anlatır · Karar noktası toplantısı (çar 25 Kas) |
| **6** (30 Kas – 6 Ara) | Yapay Zekâ · **başkan** (+ Muhammet) | 6.1–6.4: Kart üretici, doğrulayıcı, kısıtlı üretim, sunucu | 📄 Pazar raporu: `donem-3-yapay-zeka.md` |
| **7** (7 – 13 Ara) | Oyun · yardımcı (+ Sokul) | 7.5o–7.6o: Ekip dışı oyun testi, hata düzeltme, denge | 🔄 Yeni geldi; Sokul'dan devir alır · Oyun testi için tanıdık getir |
| **8** (14 – 20 Ara) | Oyun · yardımcı (+ Sokul) | 8.1, 8.2, 8.5: Cila, son APK, sunumun oyun bölümü | Tam prova (herkes) |

### Muhammet

| Hafta | Alan · rol | Görevler (6. bölümdeki numaralar) | Ek görev |
| --- | --- | --- | --- |
| Hazırlık | — | Hz.2 kurulum eksikleri · Hz.6 torbalar | — |
| **1** (26 Eki – 1 Kas) | Oyun · yardımcı (+ Kara) | 1.7–1.13: Godot sahnesi, göstergeler, kart ekranı, kaydırma, açılış, oyun akışı | 1.0a–1.0d (herkes) |
| **2** (2 – 8 Kas) | Oyun · yardımcı (+ Kara) | 2.5–2.9: Sonuç ekranı, 8 son, yıl sayacı, yedek deste, modelsiz tam oyun |  |
| **3** (9 – 15 Kas) | Oyun · **başkan** (+ Mert) | 3.7–3.10: Rol–konu tablosu, kazanma sonu, kayıt, ilk APK | 🔄 Pazartesiden itibaren Mert'e devir anlatır |
| **4** (16 – 22 Kas) | Oyun · **başkan** (+ Mert) | 4.7–4.9: Görseller, arayüz, ses, denge testi | 📄 Pazar raporu: `donem-2-oyun.md` · Denge testinde oyna (herkes) |
| **5** (23 – 29 Kas) | Yapay Zekâ · yardımcı (+ Kara) | 5.1–5.3: İnce ayar 1. tur, api.md, sahte sunucu | 🔄 Yeni geldi; Kara'dan devir alır · Karar noktası toplantısı (çar 25 Kas) |
| **6** (30 Kas – 6 Ara) | Yapay Zekâ · yardımcı (+ Kara) | 6.1–6.4: Kart üretici, doğrulayıcı, kısıtlı üretim, sunucu |  |
| **7** (7 – 13 Ara) | Yapay Zekâ · **başkan** (+ Mert) | 7.0y–7.4y: İnce ayar 2. tur, son ölçüm, iyileştirme, modelin içi, (isteğe bağlı ONNX fizibilitesi) | 🔄 Pazartesiden itibaren Mert'e devir anlatır · Oyun testi için tanıdık getir |
| **8** (14 – 20 Ara) | Yapay Zekâ · **başkan** (+ Mert) | 8.3, 8.4: Dizüstü sunum kurulumu, sunumun model bölümü | 📄 Pazar raporu: `donem-4-yapay-zeka.md` · Tam prova (herkes) |

---

## 7. Her hafta süren işler

### 7.1 Altın set
- Hedef **2.500 iyi kart** ✅ (2.300 ince ayar · 200 sınav · en iyi 600 yedek deste).
- **Yeni kurallar:** sonuç cümlesi, `{hitap}`, 3 kademe, karar cümlesi seçenekler, karakter–konu uyumu, krallık.
- Üreten değil **başka biri** okuyup "iyi / at" der ✅. **Okuma sırası sabit** ✅: Mert, Sokul'un kartlarını okur · Sokul, Kara'nınkileri · Kara, Muhammet'inkileri · Muhammet, Mert'inkileri.
- Kişi başı: günde ~11 iyi kart, haftada ~78.
- **Hız: eşit, haftada ~310 iyi kart** ✅ (kişi başı günde ~11). Çapraz okumada atılanlar yüzünden üretilen biraz daha fazla olmalı.
- Ara hedefler: 2. hafta sonu ~100 kart (yedek deste ile oynanabilir oyun) · 4. hafta ~1.000+ (200 sınav kartı ayrılır) · 5. hafta ~1.250 (ince ayar 1. tur) · 7. hafta ~2.300 (ince ayar 2. tur) · 8. hafta 2.500.
- Yedek deste (en iyi 600) her hafta büyür; 2. haftada küçük başlar.

### 7.2 Torbalar
- 1. hafta sonuna kadar torbaların ilk hâli bitsin 💡; sonra gerektiğinde eklenir.
- Kelimeler ~2000 ✅; diğer torba boyutları hâlâ öneri.

---

## 8. Riskler ve B planı

| Risk | Erken işaret | Ne yapılır |
| --- | --- | --- |
| Öğretmen yavaş, veri yetmiyor | 1. hafta sonunda günlük üretim beklenenin altında | Daha küçük öğretmen, daha kısa hikâye, 2 hesap paralel |
| Colab birimleri bitiyor | Birim takibi (her hafta) | 30M'den önce 10M'le ince ayar denemesi; eğitim süresi kısaltılır |
| 30M kötü yazıyor | 4.6 ölçümü | **B planı:** hazır Türkçe bir modele LoRA (ayrıntısı 5. hafta toplantısında; "sıfırdan mı, ince ayar mı" konusu da o zaman açılır) |
| Model biçimi bozuyor | Doğrulayıcıdan geçme oranı düşük | Kısıtlı üretim (6.3) + yedek deste |
| Godot ↔ Python bağlantısı sorunlu | 5. hafta | Sahte sunucuyla erken test; olmazsa APK yedek desteyle teslim edilebilir |
| Model ne çıkarsa çıksın | — | **Oyun her durumda yedek desteyle teslim edilebilir** ✅ |

---

## 9. ⚠️ Kontrol turunda bulunanlar (karar bekliyor)

Taslağı ikinci kez baştan sona kontrol ettim. Bunlar senin kararını gerektiriyor:

1. ~~Altın set hızı ile takvim çakışıyor.~~ ✅ **Çözüldü:** Eşit hız (haftada ~310). İnce ayar 5. haftada eldeki kartlarla, 7. haftada bütün kartlarla tekrarlanır.
2. **Kart biçimi değiştiği için 2. tur model denemesi eski biçimle yapıldı.** Öğretmen seçimi yine geçerli, ama 1.2'deki 20 kartlık deneme yeni biçimle (sonuç cümlesi, `{hitap}`) tekrar bakılmalı. Haritada var, bilgin olsun.
3. **Hedef veri miktarı belli değil** (kaç hikâye, kaç token). Hız ölçümünden (Hz.3, 1. haftanın başı) sonra belirlenecek; 3.1 buna bağlı. Öneri: 30M model için birkaç yüz bin hikâye.
4. ~~Haftalık toplantının günü belli değil.~~ ✅ **Çözüldü:** Çarşamba öğle arası. Raporlar pazar, devir pazartesiden itibaren.
5. ~~Eski belgeler güncellenmeli.~~ ✅ `hazirlik_haftasi.md` güncellendi. `Kart_Mekanikleri.html` artık geçersiz (düz kart seçildi), zip'e konmadı.
