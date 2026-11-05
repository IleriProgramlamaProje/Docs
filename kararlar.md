# Karar Günlüğü

Her karar: tarih · karar · neden. Yeni kararlar en alta eklenir. Haftalık toplantıda alınan kararları koordinatör yazar.

## Önceki sohbetlerden gelenler (21 Ekim öncesi)

| Karar | Neden |
| --- | --- |
| Oyun Unity (C#), yapay zekâ Python | Ders C#; model işleri Python'da kolay |
| Oyunda hazır API yok (Claude, Gemini vb.) | Kendi modelimiz; token/para derdi yok |
| Model **sıfırdan** eğitilir: 1M → 10M → 30M (zaman kalırsa 60M) | Asıl amaç bir dil modelinin nasıl doğduğunu baştan sona görmek |
| B planı: hazır Türkçe modele LoRA | Sıfırdan model yetmezse |
| Veri TinyStories yöntemiyle: öğretmen model + torbalar | Küçük modele dar ve temiz bir dünya |
| Toplu üretim açık modelde, altın set sohbet ekranından elle | API ücretli; servis kuralları çıktılarla model eğitmeyi kısıtlayabilir |
| Oyun kodu sayıları ve kuralları, model sadece sözleri yazar | Oyun durumu modelden bağımsız güvenilir kalsın |
| Doğrulayıcı + yedek deste | Model ne çıkarsa çıksın oyun teslim edilebilir |
| Göstergeler: Senato · Halk · Para · Ordu (0–100, 50'den başlar) | — |
| Seçenekler evet/hayır değil, takas | — |
| Kartlar birbirinden bağımsız | — |
| Belgeler .md | PDF istenmiyor |

## 21 Ekim 2026

| Karar | Neden |
| --- | --- |
| 10 torba: kelimeler (~2000, isim/fiil/sıfat), karakterler, olaylar, özellikler, üsluplar, konular, yer, zaman/mevsim, ruh hâli, ikilem | Veri çeşitliliği (TinyStories) |
| Atasözü torbası yok | — |
| Gösterge durumunu kod rastgele üretir | Model farklı durumları görsün |
| Hikâyelerde birkaç torba her zaman, gerisi rastgele | Öğretmene giden istek kısa kalsın |
| Kartlarda hangi torbaların olacağı kart biçimiyle kesinleşir | Oyunda giden bilgi eğitimde de olsun |
| Etkiler sabit şablon değil, kartın mantığına göre | — |
| Seçenek başına en fazla 3 gösterge | Ekran sade kalsın |
| Kelime seçiminde yumuşak sınır | Türkçe eklemeli; sıkı sınır iyi hikâyeleri atar |
| 15 karakter = 15 rol; isimler oyun kodunda rastgele, her yeni oyunda | Model isim değil rolün konuşmasını öğrensin |
| Kart içinde başka karakterden sadece unvanla bahsedilir | İsim karışıklığı olmasın |
| Altın set hedefi 2.500 (2.300 ince ayar, 200 sınav, 600 yedek deste) | — |
| Doğrulayıcı kontrol listesi | — |
| Öğretmen model denemesi bu hafta | — |

## 22 Ekim 2026

| Karar | Neden |
| --- | --- |
| Öğretmen kalite denemesi: Trendyol elendi; Gemma 4 (4B) 1. aday, Qwen 3.5 (9B) 2. aday | `raporlar/ogretmen_secimi.md` |
| Kural: seçenek yazısı kartın derdine verilen karar (emir/eylem) | Denemede modeller soyut başlık yazdı |
| Kural: karakter–konu uyumu | Kadı ordu işi getirmesin |
| Kısıtlı üretim fikri ileride bakılacak | `fikir_notlari.md` |
| 8 haftalık yol haritası: 26 Ekim – 20 Aralık, sonunda her şey bitmiş | — |
| APK: ana hedef dizüstünde Python kart üreticisi + yedek desteli APK; telefona gömme zaman kalırsa | — |
| Oynanış: **düz kart**, kaydırma | — |
| Model her seçenek için sonuç cümlesi yazar | Sonuç ekranı |
| Kart başlığı: konuşanın unvanı + ismi (oyun kodu) | Model başlık uydurmasın |
| Etkiler 3 kademe: ±5 / ±10 / ±15 | ±20 fazla |
| Kaydırırken ok, sonuç ekranında sayı | — |
| 8 son + kazanma sonu (hedef süre, sonra rekor için devam) | — |
| Görseller: karakter başına portre ≈ 25 resim, görsel üreticiyle, oyun ekibi | Model yazdığı için kart başına resim olamaz |
| **Tema: Türk tarzı krallık** ("Kral", "Senato") | — |
| Hitap: cinsiyet seçimi → "Beyim" / "Hatunum"; model `{hitap}` yazar, gerektiğinde | Model cinsiyet öğrenmek zorunda kalmasın |
| Ekip: 2 haftalık dönemler, rol rotasyonu; başkan devir teslim + rapor | Herkes her şeyi öğrensin |
| Koordinatör: Mert | — |
| Repo adı: `ileri-programlama` | — |

## 23 Ekim 2026

| Karar | Neden |
| --- | --- |
| Altın set eşit hızla: haftada ~310 (kişi başı günde ~11); ince ayar 5. haftada eldekiyle, 7. haftada tamamıyla | — |
| Raporlar dönemin son pazarı, devir pazartesiden itibaren | Her 2 haftada iş devredilebilir hâlde |
| Haftalık toplantı: çarşamba öğle arası; gündem serbest | — |
| Karar noktası (30M yeterli mi?): çarşamba 25 Kasım toplantısı | — |
| Ekip içinde işler eşli yapılır | — |
| Altın set okuma sırası: Mert → Sokul → Kara → Muhammet → Mert | — |
| Gece üretimini o dönemin YZ ekibi kendi Colab hesaplarıyla çalıştırır | — |
| Sunum alan alan hazırlanır | — |
| Teslim sorumlusu 1. hafta toplantısında kura ile | — |

## 25 Ekim 2026

| Karar | Neden |
| --- | --- |
| Karakterler: 23 rol, 4 grup (Yönetim 7, Ordu 4, Halk 6, Para 6); Defterdar → Hazinedar | Benzer roller ayıklandı, gruplar göstergelere denk |
| 100'e çıkma sonları ve kazanma sonunun metinleri onaylandı | — |
| Olaylar: 200 olay, her biri iki seçenekli; etkileri Claude yeniden önerdi, ekip onaylayacak | İlk hâlde ~45 olayda etki yönü mantıksızdı |
| Konular 100, yer 60, üslup 60, ikilem 60 | — |
| Kelimeler 2000: yasak, fazla nadir, fazla dinî ve fazla Osmanlı kelimeler çıkarıldı; temel kelimeler eklendi | Orta Çağ beyliği havası, Türkiye Türkçesi, sade dil |
| Öğretmen model: **Gemma 4 E4B** | Denemede kurallara en çok uyan ve Qwen'den hızlı |
| Gösterge adı: **Yönetim** (Senato yerine); açılış ve son metinlerinde "Divan" | Olaylar ve karakter grupları zaten "Yönetim" kullanıyordu |
| "Çift" cinsiyetli roller erkek de kadın da olabilir (rastgele, iki portre) → ~42 resim | — |
| Kart durum satırı: 4 gösterge + konuşan + konu; kartların bir kısmında konu serbest | Model 100 konuya sıkışmasın |
| Veri üretiminde karakter ve 3 kelime zorunlu, diğer torbalardan rastgele 1-2 | Öğretmene giden istek kısa kalsın |
| Olay etkileri önerisi onaylandı | — |
| Karakter kimlik kartları (sık sözler, asla, benzerinden farkı) + kör tahmin testi | Model rolleri ayırt etmeyi öğrensin |
| Ruh hâli, özellik, zaman torbaları 40'a çıktı | — |
| Altın Set sayfası krallık kurallarıyla güncellendi | — |
| Hikâye/kart üretici kodu ve Colab defterleri (hız ölçümü, gece üretimi) hazır | Hazırlık haftasının işi |
| GitHub deposunu ve Drive klasörünü Mert açar | — |

## 26 Ekim 2026 · Teknik durum kaydı

- Çalışma alanı AI, Docs ve Game olarak üç bağımsız depoya ayrılmıştır; oyun kodu Godot + C# kullanır. Güncel kurulum ve rehberler bu duruma uyarlandı. Geçmiş Unity kararları tarihsel kayıt olarak korundu; ekip/öğretmen teyidi Game planındaki açık maddedir.
- AI belge yolu kardeş Docs deposundan okunur; özel konum için `PROJE_DOCS_DIR` desteklenir.
- Öğretmen promptu mevcut etiketli kart gövdesi sözleşmesine uyarlandı. Bu, doğrulayıcının veya JSON dönüştürücüsünün tamamlandığı anlamına gelmez.
- Konu seçimi belgelenen yaklaşık %15 serbest oranına uyarlandı. Sabit tohumla devam etmede eski malzemelerin tekrarı, geçersiz grup boyutu ve bozuk dosyaya devam sorunları düzeltildi.

## 26–27 Ekim 2026

| Karar | Neden |
| --- | --- |
| Altın Set sitesi yerelde çalışır (2 dosya: index.html + data.js); herkes kendi kartını tarayıcıda saklar, günün sonunda JSON indirip gruba atar; Kart + Hikâye modu | Sunucu/kurulum derdi olmasın |
| E4B ilk denemesi (128 hikâye + 128 kart): cümleler dil bilgisi olarak düzgün ama anlamsız; kartların %31'i prompttaki örneğin etkilerini kopyaladı | Zorla kelime + tek sabit örnek + küçük model |
| Kart promptunda örnek her istekte değişir (8 örnek); sıra karar → sonuç → etki | Kopyalama |

## 1 Kasım 2026

| Karar | Neden |
| --- | --- |
| Kelime listesi sadeleşti: 1500 kelime (613 isim · 475 fiil · 412 sıfat) | Zor/nadir kelimeler anlamı bozuyordu |
| **Hikâye: 3 kelime** (1 isim + 1 fiil + 1 sıfat, üçü istenir) · **Kart: 2 kelime** (1 isim + 1 sıfat, en az biri; hiçbiri yoksa filtre eler) | Kısa kart metnine zorla kelime saçma cümle üretiyordu; çeşitlilik için kelime kalsın |
| Torbalardan dine kayan maddeler nötrleriyle değişti (cami avlusu, tekke, medrese, mescit, türbe, ezan, namaz, ramazan, kurban bayramı, vakıf…); kelimelerden dua, cami, medrese, kurban, şükretmek çıktı; Derviş'in sık sözlerinden "dua" çıktı | "Fazla dini olmasın" kararı; hikâyeler dua/evliyaya kayıyordu |
| **Öğretmen model: Gemma 4 12B**. E4B elendi; Gemini kullanılmaz | Aynı 40 promptla karşılaştırmada 12B en tutarlısı. Gemini çıktısıyla eğitim Google kurallarına aykırı; Gemma 4 Apache 2.0 |
| 12B Colab T4'te 4-bit, Kaggle 2×T4'te 8-bit; ikisi aynı anda. Bu hafta 2 kişi üretir (Mert, Sokul) | 4-bit yazımı biraz bozuyor (ünlü uyumu); filtre ayıklamalı, hacim iki ortamla telafi |
| Öğretmen kart gövdesini etiketli değil **satırlı** yazar (26 Ekim'deki "etiketli gövde" kaydının yerine geçer); etiketli eğitim metnine `kart_bicimi.py` çevirir. Prompt ve üretim kodu hazır; dönüştürücü görev (`yz_gorevleri.md`) | Etiketli gövdede ve sabit örnekte etkiler kopyalanıyordu |
| İkinci kontrol turu: söz/ton uymayan ve çağ dışı birkaç kelime daha çıktı (liste 1500); hikâyeyle çelişen üslup/özellikler (şiirsel, manili, tekerleme, sonu açık…) değişti; Kervan Başı'nın görevinden "güvenlik" çıktı | İkinci kontrol turu |

## 2 Kasım 2026

| Karar | Neden |
| --- | --- |
| Kart üretimi bugün başlar: üretim kodu (türe göre kelime, yeni kart promptu, 12B 4-bit/8-bit, Colab+Kaggle defteri) Claude'dan. Filtre, dönüştürücü, tokenizer, hazır veriler ve veri hazırlamayı ekip (Mert, Sokul) yazar: `yz_gorevleri.md` | Üretim beklemesin; ders görevleri ekibin kendi işi |
| Altın set üretilen kartlardan başlar: ekip okur, düzeltir, iyileri altın sete alır | Altın set için hazır malzeme olsun |
| **Gemini de kullanılır** (1 Kasım'daki "Gemini kullanılmaz" kaydının yerine geçer): toplu üretimde Gemma 4 12B'nin yanında Gemini da öğretmen olabilir | Proje ders ödevi, ticari değil; hacim artsın |
| **Altın set herkesin kendi yapay zekâsıyla** (Claude, Gemini… web sohbet ekranından) yazılır, elle düzeltilip altın set sitesine eklenir; ham kartlardan seçmek zorunlu değil. Ham kartlarda görülen hatalar yine filtre (S1) için not edilir | Altın set ham üretimi beklemesin, kalite daha yüksek olsun |
| **Altın set sayfası yenilendi** (`AI/ai/altin_set/`, claude.ai'de "Altın Set Prompt Üretici"): güncel torbalar (1500 kelime), 10/20/30/50 kartlık paketler, her kartın konuşanı/durumu/kelimeleri prompt'ta; cevap yapıştırılınca kurallar otomatik kontrol edilir, hatalılar kaydedilmez. **Çapraz okuma (iyi/at) kaldırıldı**; hikâye modu çıktı. İndirme: oyun JSON'u, eğitim metni, ham JSONL, CSV | Kişi başı günde 1000+ kart hedefi; okuma bu hacimde yapılamaz |

## 5 Kasım 2026

| Karar | Neden |
| --- | --- |
| Altın set sayfasında hikâye modu var (3 Kasım'da geri eklendi; 2 Kasım'daki "hikâye modu kaldırıldı" kaydının yerine geçer) | Hikâye de kendi yapay zekâmızla üretilebilsin |
| Colab'da dosya adı ve tohum artık günlük (`surekli` yerine `aagg`) | `surekli` dosyası Drive'da yer değiştirince defter aynı tohumla baştan başladı: 5 Kasım dosyasındaki 3.276 kaydın hepsi eski malzemelerin tekrarı çıktı, 2.795'i "aynı prompt" diye elendi |
