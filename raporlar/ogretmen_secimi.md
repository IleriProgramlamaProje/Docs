# Öğretmen Model Denemesi · Sonuçlar

*22 Ekim 2026 · Yapay Zekâ ekibi*

> **Amaç:** Yüz binlerce hikâye ve kart üretecek öğretmen model için 1–2 aday belirlemek.
> **Sonuç:** Trendyol 1. turda elendi. **Gemma 1. aday, Qwen 2. aday.** Ayrıntı en altta.

---

## 1. Kullanılan araçlar ve modeller

### Araçlar

| Araç | Sürüm / not |
| --- | --- |
| **LM Studio** | Modelleri bilgisayarda çalıştıran sohbet uygulaması (Linux) |
| **llama.cpp çalışma motoru** | `llama.cpp-linux-x86_64-nvidia-cuda12-avx2` · 2.62.1 · LM Studio'nun içinden otomatik indi. Modeller ekran kartında (CUDA) çalıştı |
| **harmony** | `harmony-linux-x86_64-avx2` · 0.3.5 · LM Studio'nun yardımcı paketi, otomatik indi |
| **Bilgisayar** | NVIDIA ekran kartlı kişisel bilgisayar. Hızlar bu bilgisayara göre; asıl hız Colab'da ölçülecek |

### Modeller

| Model | LM Studio'daki adı | Boyut | Dosya | Durum |
| --- | --- | --- | --- | --- |
| **Trendyol** | tolgadev/Trendyol-LLM-7b-chat-dpo-v1.0-GGUF | 7B | Q4_K_M · 4,44 GB | ❌ 1. turda elendi |
| **Gemma 4** | google/gemma-4-e4b | 4B (etkili) | 6,33 GB | 2. tur |
| **Qwen 3.5** | qwen/qwen3.5-9b | 9B | 6,55 GB | 2. tur |

### Ayarlar

- **Temperature:** 0.8 (Trendyol ve 1. turda varsayılan bırakıldı, LM Studio'da varsayılan buna yakın)
- **Gemma:** Think (düşünme) kapalı
- **Sohbet:** 1. turda üç prompt aynı sohbette verildi; 2. turda her prompt yeni sohbette (önceki prompt karışmasın diye)
- **Hız:** LM Studio'nun cevabın altında gösterdiği tok/s (saniyede üretilen parça)

---

## 2. Girilen promptlar

### Kart · 1. sürüm (sadece Trendyol'da, 1. turda)

```
Orta Çağ'da küçük bir Türk beyliğinde geçen kaydırmalı bir karar oyunu için 5 kart yaz.
Göstergeler: Senato, Halk, Para, Ordu.
Kurallar:
- Her kartta bir karakter derdini doğrudan anlatır, oyuncuya "Beyim" diye hitap etmez.
- Metin 20-35 kelime olsun.
- İki seçenek var, evet/hayır değil: iki göstergeyi birbirine karşı tartan bir takas olsun.
- İki seçenek de en az bir göstergeyi düşürsün.
- 5 kart farklı konularda olsun ve farklı göstergeleri kullansın; dördü de (Senato dahil) en az bir kez geçsin.
- Seçenek yazıları karta özel ve kısa olsun (2-5 kelime).
- Modern kelime kullanma.
Biçim (köşeli parantezleri doldur, örneği kopyalama):
KART 1
Konuşan: [kim]
Metin: [20-35 kelime]
Sol: [etiket] | [Gösterge +/-, ...]
Sağ: [etiket] | [Gösterge +/-, ...]
```

### Kart · 2. sürüm (Gemma ve Qwen, 2. turda)

**Neden değişti?** 1. turda üç model de aynı yerlerde takıldı: soyut seçenek yazıları ("Piyasa Koşuşturması"), konuşanın işine uymayan dertler, sayıyla yazılan etkiler, modern kelimeler. Bunlar promptun eksikleriydi.

```
Orta Çağ'da küçük bir Türk beyliğinde geçen kaydırmalı bir karar oyunu için 5 kart yaz.
Göstergeler: Senato, Halk, Para, Ordu.

Kurallar:
- Konuşan, şu unvanlardan biri olsun (isim yazma, sadece unvan): Vezir, Defterdar, Kadı, Akıncı Beyi, Derviş, Şeyh, Ahi Ustası, Köy Kethüdası, Hekim, Ozan, Saray Hatun, Kervan Başı, Demirci Usta, Karasu Elçisi, Çoban.
- Kartın derdi, konuşanın işine uygun olsun. Örneğin vergiyi Defterdar, din işini Kadı ya da Şeyh, askerlik işini Akıncı Beyi getirir.
- Karakter derdini doğrudan anlatır. Oyuncuya "Beyim" diye hitap etmez.
- Metin 20-35 kelime olsun.
- Sol ve sağ, aynı derde verilen iki farklı karar olsun. Seçenek yazısı bir emir ya da eylem cümlesi olsun, 2-5 kelime. Örnek: "Kanalı kazdır", "Beklesinler, hazine boş". Soyut başlık yazma.
- Her seçenek 1-3 göstergeyi etkilesin. İki seçenek de en az bir göstergeyi düşürsün.
- Etkileri sayıyla değil sadece + ya da - ile yaz.
- 5 kart farklı konularda olsun; dört gösterge de (Senato dahil) en az bir kez geçsin.
- Sade Türkçe kullan. Modern kelime kullanma (bütçe, reform, memur, bakan, vali, depo, politika gibi).
- Sadece kartları yaz. Giriş, açıklama ya da kontrol listesi ekleme.

Biçim (köşeli parantezleri doldur, örneği kopyalama):
KART 1
Konuşan: [unvan]
Metin: [20-35 kelime]
Sol: [karar] | [Gösterge +/-, ...]
Sağ: [karar] | [Gösterge +/-, ...]
```

### Hikâye (iki turda da aynı)

```
Orta Çağ'da küçük bir Türk beyliğinde geçen 3 kısa hikâye yaz. Her biri 100-150 kelime.
Karakter: Derviş. Olay: Kıtlık. Her hikâyede şu kelimeler geçsin: kervan, mühür, kuyu.
Sade ve akıcı Türkçe, modern kelime yok. Başlık koyma.
```

### Üslup (iki turda da aynı)

```
Dede Korkut hikâyelerinin anlatım tarzıyla, bir köy kethüdasının kuraklık yüzünden saraya geldiği 120 kelimelik kısa bir hikâye yaz. Kendi cümlelerinle yaz, gerçek Dede Korkut metninden alıntı yapma.
```

---

## 3. Çıktılar

### ❌ Trendyol · 1. turda elendi (kart 1. sürüm)

**Neden elendi:**
- **Kart:** Kartları dolduramadı. 5 kartın 4'ünde `[kim]` ve `[20-35 kelime]` olduğu gibi kaldı. "Konuşan: Beyim" yazdı, "bütçe" ve "mali politika" gibi modern kelimeler kullandı.
- **Hikâye:** Hikâye yerine kısa özet yazdı. Her biri ~60 kelime (100–150 istendi). "Başlık koyma" dendiği hâlde başlık koydu, iki yerde Almanca "Dervisch" kaçırdı.
- **Üslup:** ~50 kelime yazdı, Dede Korkut havası hiç yok, "kral" dedi.
- **Tek artısı:** En hızlısı (~46 tok/s). Ama en önemli iki başlıkta (Türkçe, kurala uyum) çok zayıf.
- Not: Bu dosya ~2,5 yıllık ve topluluktan biri yüklemiş. Trendyol'un daha yeni bir 8B sürümü varsa Colab'da ayrıca denenebilir.

#### Kart · 46.84 tok/s

Kart 1, Konuşan: Beyim
Metin: Halkınızı bir toplantıya çağırıyorum.
Sol: Senato (+) | Para (-)
Sağ: Ordu (-) | Halkınıza doğru bilgiler sunmak için bir Senato toplantısı düzenlemenizi öneririm.

Kart 2, Konuşan: [kim]
Mentin: [20-35 kelime]
Sol: Senato (-) | Para (+)
Sağ: Halk (-) | Ordu (+)

Kart 3, Konuşan: [kim]
Metin: [20-35 kelime]
Sol: Ordu (-) | Para (-)
Sağ: Senato (+) | Halkınızın güvenliğini sağlamak için bir ordu gücünü kullanmanızı öneririm.

Kart 4, Konuşan: [kim]
Mentin: [20-35 kelime]
Sol: Halk (+) | Para (+)
Sağ: Ordu (-) | Bütçenizi dengelemek için halkın desteğini artırmanızı öneririm.

Kart 5, Konuşan: [kim]
Metin: [20-35 kelime]
Sol: Para (+) | Ordu (-)
Sağ: Halk (+) | Ordu gücünü azaltarak halkın refahını artırmak için bir mali politika öneriyorum.

#### Hikâye · 47.01 tok/s

1. Kervan Üzerine:

Derviş bir kervanla birlikte bir köye doğru ilerlerken, kıtlığın hüküm sürdüğü bir dönem olduğunu öğrenir. Yolculuklarına devam ederken bir kuyuya rastlarlar ve burada suya ulaşmak için bir mücadele verdiklerini görürler. Derviş, bu zor zamanlarda insanların bir araya gelip dayanışma sergilemesi gerektiğini hatırlatır ve kervancılara kuyunun başında mühürlenerek suyunu korumaları gerektiği öğütünü verir.

2. Kuyu Üzerine:

Derviş, bir köyde kuyu başında bekçilik yaparken kıtlığın etkilerini yakından gözlemler. Köy halkı suyun kısıtlı olduğunu ve muhtaç durumdaki insanlara yardım etmek için kuyuya bir mühür koyduğunu anlatır. Derviş, bu tedbirin önemini vurgulayarak toplumun her bireyinin sorumluluğunu yerine getirmesi gerektiğini hatırlatır ve kuyuya zarar verenlerin cezalandırılması gerektiğini söyler.

3. Mühür Üzerine:

Dervisch, bir köye yardım etmek için bir kervanla yola çıkmışken, bir kuyuda bulunan mührün zarar görmüş olduğunu görür. Derviş, bu mühüre yenisini yaptırmanın ve köylülere suyu korumak için birlikte hareket etme cesaretini göstermelerinin önemini anlatır. Mühüre sahip olmanın toplumlar arasında güven ve dayanışma sağladığını vurgulayan Dervisch, bu tür sembollerin korunmasının önemine dikkat çeker.

#### Üslup · 45.27 tok/s

Köy kethüdası, kuraklığın hüküm sürdüğü bir dönemde saraya gelir ve kralın bu zor zamanlarda köylülere nasıl yardım edebileceğini sorar. Kethüdası, köylülerin su kaynaklarını korumak için bir mühür kullandığını ve bu mühüye zarar verenlerin cezalandırıldığını söyler. Kralın bu önlemleri dikkatlice alması ve köylülere yardımcı olmak için harekete geçmesi gerektiğini belirtir.

---

### Gemma ve Qwen · 2. tur

*Kart promptunun 2. sürümüyle, her prompt yeni bir sohbette verildi (promptlar 2. bölümde).*

#### Kart

##### Gemma · 37.58 tok/s

KART 1
Konuşan: Defterdar
Metin: Yeni hasat geldi, ancak geçim derdi büyüyor. Hazineye ne kadar vergi konulursa, halkın eli sıkılır. Bu terazide nasıl bir denge kurulacak?
Sol: Vergiyi düşürün | Para +1, Halk - , Ordu -1
Sağ: Vergiyi artırın | Para +2, Halk -2, Senato +1

KART 2
Konuşan: Akıncı Beyi
Metin: Sınırlarımızda uğultu var. Komşu beylikler güvensiz görünüyor. Bir sefer hazırlığı yapmak şart oldu; askerler dinlenmeli mi yoksa hemen yola çıkmalı mı?
Sol: Yönlendirin sınır boylarına | Ordu +2, Para -1, Senato +1
Sağ: Bekletsinler kış geçene kadar | Ordu -1, Halk +1, Para -

KART 3
Konuşan: Kadı
Metin: Yeni gelen yabancılar arasında anlaşmazlıklar çıktı. Kanunların uygulanışı konusunda bir ihtilaflar yaşanıyor. Adalet yerini bulması için ne yapmalıyız?
Sol: Divan toplayın yargılansın | Senato +1, Halk +1, Ordu -
Sağ: Uzlaşma yolunu seçin | Para +1, Halk +2, Senato -

KART 4
Konuşan: Kervan Başı
Metin: Yollarımızda tüccarlar bekliyor. Ticaret yolları güvenli olmalı ki gelirler aksamasın. Bir koruma gücü mü gerekiyor yoksa geçici bir mola mı verilmeli?
Sol: Garnizon kurun hemen | Ordu +1, Para +2, Senato -
Sağ: Yol güvenliğini bekleyin | Halk +1, Para -1, Ordu -

KART 5
Konuşan: Vezir
Metin: Beyliğin itibarı düşmüş, büyük bir şöhret kazanmak istiyoruz. Bu amaçla ne yapmalıyız? Büyük bir gösteri mi düzenlemeli yoksa tedbiren beklemeli miyiz?
Sol: Kutlama düzenleyin halka | Senato +2, Para -1, Halk -
Sağ: Sessizce güç toplayın gizlice | Ordu +1, Para +1, Senato -


##### Qwen · 25.01 tok/s

KART 1
Konuşan: Defterdar
Metin: Beyim, vergi toplayıcılar köylerde yolda kalmış develere saldırdı. Halk bu zulmün yüküyle eziliyor ve hazineyi doldurmak için aciz kalıyoruz, ne yapmalıyız?
Sol: Çobanlara bağış ver | -Halk, +Para
Sağ: Vergiyi katla | +Senato, -Halk

KART 2
Konuşan: Kadı
Metin: Şehrin kapısında yalvaran bir hıristiyan kadın var; din adamları şefkat çağırırken bazı kimseler onu taşımaya hazırlanıyor. Adalet terazisi nasıl tartılmalı?
Sol: Onu koruyarak dinlerini serbest bırak | -Senato, +Halk
Sağ: Dışarı atıp güvenlik olsun | +Senato, -Halk

KART 3
Konuşan: Akıncı Beyi
Metin: Dağlarda yuvalanan hırsızlar kervanlara saldırdı; ordumuz henüz toplanmadı ve halk bizden koruma bekliyor. Şimdilik ne yapmalıyız beyim?
Sol: Atların üzerine binip avcıya dön | +Ordu, -Para
Sağ: Halka uyarılarla sabretmesini emrederiz | -Ordu, +Senato

KART 4
Konuşan: Şeyh
Metin: Dervişlerimiz yoksulluğa karşı çaresizlik içinde dua edip yardım istiyorlar; halkın manevi desteği bizi güçlendirirken para sıkıntısı büyüyor. Yol nerden açılmalı?
Sol: Zekat toplayıp yoksullara dağıt | +Halk, -Para
Sağ: Mirasçıların mallarını harakere sür | +Para, -Halk

KART 5
Konuşan: Saray Hatun
Metin: Çocuklarımızın eğitimi ve sarayın görkemli olması için yeni dokuma işçileri lazım; ancak para yetersiz kalırken halkın memnuniyeti de azalmaya başladı. Ne deneliyoruz?
Sol: Emeği zorla çalışanları serbest bırak | -Senato, +Halk
Sağ: Gümüşten süslü şerbetlikler yapdırırız | +Senato, -Halk


---

#### Hikâye

##### Gemma · 37.15 tok/s

Yaz ayları kavurucu bir sıcaklıkla üzerimize çökmüştü. Toprak çatlamış, nehirler çekilmişti. Kasabanın ortasındaki eski kuyu, artık yalnızca dipteki kurumuş çamurla bizi selamlıyordu. Birkaç gün önce uğrayan ticaret kervanı, umut ışığı gibi görünmüştü; üzerindeki mallar bir nebze olsun nefes almamıza yetebilirdi. Lakin o kervanın taşıdığı değerli mühürler, sadece birkaç günlük lüksümüzün garantisiydi. Derviş, çömelmiş kalabalığa baktı. Karnımızdaki boşluktan ziyade, ruhumuzun susuzluğu daha ağırdı. Omuzlarımdaki yorgunluğa rağmen, kuyuya doğru eğildim. "Allah'ın lütfu nerede kaldı?" diye fısıldadım. Ya bu zor zamanlar, sadece sabırla geçilecek bir sınavdan ibaretti?

Kış yağmurları beklenirken, günler uzadı ve açlık gölgesi üzerimize çöktü. Mahalle meydanındaki kuyu, artık yalnızca derin bir karanlıktan ibaretti; su sesi yoktu. Geçenlerde gelen bir kervan, nadiren görülen tahıl yığınlarıyla dikkatimizi çekmişti. Lakin o kervanın yanından geçen heybetli görevliler, üzerlerindeki özel mühürleri göstererek kimseye yaklaşmamamızı emretmişlerdi. Birkaç yaşlı kadın, o eşyaların bir parça bile bize kalmayacağını fısıldıyordu. Derviş, tüm bu zorluklara rağmen, umudu kaybetmemek gerektiğini biliyordu. Belki de yardım, en beklenmedik yerden, kurumuş kuyuya düşecek ilk damla yağmurdan gelecekti.

Bir hafta süren sessizlikten sonra, ufukta bir hareketlenme oldu. Uzaktan gelen o tok sesler, beklediğimiz kervandı. Yükleri arasında sadece tuz değil, aynı zamanda hayat anlamına gelen su fıskiyeleri vardı. Bu kutsal kervan, kasabanın kenarındaki eski ve kullanılmayan kuyuya yaklaştı. O günkü manzara, sanki bir mucizenin sahnesiydi. Kervandaki yetkili, üzerindeki büyük mührü göstererek geçiş izni vermişti. Derviş, kalabalığın arasında titreyen ellerle o suyun şükrünü etti. Bu kervan sayesinde, sadece fiziksel susuzluğumuz dinmemiş, aynı zamanda ruhumuza da bir bahar esintisi gelmişti.


##### Qwen · 23.69 tok/s

Güneşin yakıcı bakışları altında topraklar çatlarken, Derviş yorgun adımlarla köyün kenarına gelmişti. Elindeki mühür, geçen kervanların getirdiği son bahşişin deliliği gibi parlıyordu. Ancak kuyular kurumuştu; sıska bir umutla suya uzanan elle karşılaşılan sadece çamurlu bir tabakaydı. Derviş, "Su yoksa ibadet de olmaz" diye fısıldadı ve elindeki mührü yere bırakarak yalvardı. Yolda geçen kervan başını eğdi; yüklerine ek olarak su taşıyan deri torbalar eklediler. Mührün altına basılan iz, bu acil yardımı resimliyordu. Derviş, toplanan suyu dağıtıp yüzlerindeki çaresizliği bir nebze olsun azalttı. Kervanın ilerlemesiyle birlikte umut tekrar yerini buldu, kuyu başında yapılan dua, kuraklığın ağır yükünü hafifletti. Artık bekleyen kalplerde sadece susuzluk değil, yardımın sıcaklığı vardı. Derviş, mührü alıp yola koyuldu; kervanın izinde güvenle yürüdüğü bu yolda, hayatta kalmanın birer mucize olduğunu tekrar öğrendi.

Kışın sert nefesleriyle birlikte gelen kıtlık, köyün her sokağını sararken Derviş'in yüzünde derin bir hüzün belirdi. Elindeki mühür, yetimhanedeki son unluğun deliliği gibiydi; kuyular ise yıllardır dolduramadıkları su rezervuarları gibi boştu. Bir kervan yaklaşırken gökyüzünde beliren bulutlar umut tufanını andırıyordu. Derviş, "Bu mühürle yetimi korudum, şimdi su buldum" diyerek kalbine dokundu. Kervanın getirdiği suyla kuyular tekrar dolmaya başladı. İnsanlar, kurumuş bağrında kalan susuzluğu atıp yeniden canlanıyorlardı. Mührün üzerinde yazan ibadetin suları, Derviş'in dualarıyla birleşerek toprağa inmişti. Kervanın geçtiği yoldaki ayak izleri, bu kıtlık döneminin en güzel hatırasıydı. Derviş, kuyu kenarında oturup düşündü; hayatın zorluklarında bile birlik ve dayanışmanın gücünü bir kez daha kanıtlamıştı.

Derviş, kıtlığın gölgesinde dolaşırken elindeki mührün ısısını hissediyordu. Köyün tek kuyusu kurumuştu ve insanlar susuzlukla boğuşuyorlardı. O gün geçecek bir kervan haberini aldı; Derviş derhal yola koyuldu. Yolda bulduğu su torbalarını toplarken, mührü sıkıca elinde tuttu. "Bu mühür, adaletin ve merhametin delilidir," diye içinden geçti. Kervanın getirdiği suyla kuyu tekrar dolmaya başladı; topraklar susuzluğa dayanamayarak ağlamaya benzer bir ses çıkardı. İnsanlar, Derviş'in yanına gelip minnetle baktı. Mührün altına basılan izler, bu büyük yardımın şahidiydi. Kervanın gidişiyle birlikte köyde yeniden yaşam döngüsü başladı. Derviş, kuyu başında durup dua etti; kıtlık sadece fiziksel bir acı değil, aynı zamanda manevi bir sınavdı. Bu sınavdan geçen herkes, merhametin gücünü kalbine kazıdı.


---

#### Üslup

##### Gemma · 35.44 tok/s

Ey dinleyenler, kulak verin de beni dinleyin. Bu köyün kethüdasıdır ki, eli kolu bağlı kalmıştır. Topraklar susuzluktan çatlamış, koyunların sesi bile solgun gelmiştir. Nehir yatağı yalnızca bir çizgi, boş bir vaattir artık.

Bu durumla saray kapılarına kadar geldim ben. Gözümde ne bir lütuf bekleyen hırs vardır, ne de bir nimet peşinde koşan gönül. Yalnızca hakikat arayan bir adamın çaresizliği var yüreğimde. Sarayın ihtişamı karşısında, bu kuru toprakların ahı çok ağır geldi ey sultanlar!

Kethüda der ki: "Bize sadece göklerden yağmur yağdıracak kudretiniz kaldı. Bu kış, oğulmuş gibi aç kalırız bizler. Lütfen, bir lütfunuzla bu topraklara bereket saçın." Der ki, sesi boğazında düğümlenmiş çaresizlikten başka bir şey değildir.

##### Qwen · 22.76 tok/s

Şimşek gökyüzüne çaktı, yağmur yoktu, toprak da kurumuştu. Köyün kethüdası, elinde eski bir kağıt ve mühürle saraya geldi. "Beyim," dedi, "halk susuzluğa dayanamıyor. Kuyular boş, nehirler kurumuş. Sen de padişahın huzuruna gidip su istemek için izin ver." Bey gülümsedi: "Bu mesele büyük devletten geçer." Kethüda, "Böyle bir zamanlarda halk acımaz, can verir," dedi. Saraydaki vezirler tartıştı, nihayet padişah karardı. Hemen kervan gönderildi, su taşıyan devrik tencereler ve mühürlü kağıtlarla köye yardım geldi. Kethüda, bu haberle halka sevindirdi: "Padişah sizi unutmamış." İnsanlar tekrar güldü, kuyu doldu, toprak yeşerdi. Dede Korkut der ki: "Merhametli olan devlet, her zaman haklıdır."

---

## 4. Değerlendirme (Claude)

### Özet

| | Gemma 4 (4B) | Qwen 3.5 (9B) |
| --- | --- | --- |
| **Hız** | ~37 tok/s | ~24 tok/s |
| **"Beyim" kuralı** | ✅ Hiç demedi | ❌ 3 yerde dedi |
| **Unvan + karakter–konu uyumu** | ✅ | ✅ |
| **Seçenek = karar cümlesi** | ✅ Çoğunlukla | ✅ Çoğunlukla |
| **Etki biçimi (sadece +/-)** | ⚠️ Sayı yazmaya devam etti | ✅ Uydu |
| **Altın kural, en fazla 3 gösterge** | ✅ | ✅ |
| **Türkçe hataları** | Az | Birkaç ("harakere", "yapdırırız", "Ne deneliyoruz?") |
| **Hikâye** | İyi ama anlatıcı karışık | İyi, sade |
| **Dede Korkut** | ✅ Çok iyi | ⚠️ İyi ama söz uydurdu, "Beyim" dedi |
| **Sonuç** | **1. aday** | **2. aday** |

### Prompt düzeltmesi işe yaradı mı?

Evet, ikisinde de belirgin iyileşme var. Konuşanlar artık listedeki unvanlar, dertler işlerine uygun (vergiyi Defterdar, adaleti Kadı getiriyor), seçenekler de soyut başlık yerine karar cümlesi ("Vergiyi artırın", "Zekat toplayıp yoksullara dağıt").

### Gemma 4

- **Kart:** Kurallara en iyi uyan. "Beyim" yok, her seçenekte tam 3 gösterge, altın kurala uyuyor, seçenekler karar cümlesi ("Divan toplayın yargılansın", "Bekletsinler kış geçene kadar").
- **Kusurlar:**
  - "Sadece +/- yaz" dendiği hâlde çoğu yerde sayı yazdı (Para +1, Halk -2).
  - Bir mantık hatası: "Vergiyi düşürün" → Para artıyor, Halk düşüyor (tersi olmalıydı).
  - Bazı seçenekler hâlâ belirsiz ("Uzlaşma yolunu seçin", "Yol güvenliğini bekleyin").
  - Döneme uymayan kelimeler: garnizon, şöhret, gösteri, lüks, fıskiye.
- **Hikâye:** Türkçesi akıcı, ama anlatıcı karışmış: hem "Derviş baktı" diyor hem "eğildim, fısıldadım" diyor. Kelimeler (kervan, mühür, kuyu) geçiyor, uzunluk doğru.
- **Üslup:** Üç model içinde en iyisi. "Ey dinleyenler, kulak verin de beni dinleyin", "ey sultanlar" gibi gerçek bir anlatıcı sesi var. Söz uydurmadı.
- **Hız:** ~37 tok/s. Qwen'den ~1,5 kat hızlı.

### Qwen 3.5

- **Kart:** Etkileri doğru biçimde (+/-) yazdı, altın kurala uyuyor, konuşanlar doğru.
- **Kusurlar:**
  - **"Beyim" hâlâ var:** Kart 1 ve Kart 3'te, üslup hikâyesinde de. Açıkça yasaklandığı hâlde iki turda da dedi.
  - Mantık hataları: "Çobanlara bağış ver" → Para artıyor. Kart 5'in seçenekleri derde cevap vermiyor ("Emeği zorla çalışanları serbest bırak").
  - Türkçe hataları: harakere, yapdırırız, "Ne deneliyoruz?", "devrik tencereler".
  - Modern kelimeler: güvenlik, rezervuar.
- **Hikâye:** Sade ve akıcı, bizim küçük model için iyi bir okuma metni. Ama bazı benzetmeler anlamsız ("son bahşişin deliliği gibi parlıyordu").
- **Üslup:** Havayı yakalamış, ama yine "Dede Korkut der ki…" diye söz uydurdu. Bey ve padişah da karışmış.
- **Hız:** ~24 tok/s, en yavaşı.

### Fikrim

1. **Gemma 1. aday.** Kurallara en çok uyan, Dede Korkut havası en iyi olan ve Qwen'den hızlı olan model. Model daha küçük (4B) olduğu için Colab'da da hızlı çalışması beklenir. Sayı yazma alışkanlığı sorun değil: biz zaten çıktıyı bir programla okuyacağız, sayıları +/-'ya çevirmek kolay.
2. **Qwen 2. aday.** Hikâye Türkçesi iyi, ama iki turda da "Beyim" kuralını çiğnemesi kötü bir işaret: Yüz binlerce üretimde kurallarımızı dinlemesi lazım. Üstelik ~1,5 kat yavaş.
3. **Her iki modelde de görülen sorunlar** (mantıksız etki, döneme uymayan kelime) filtre ve doğrulayıcının işi olacak. Hiçbir öğretmen model kusursuz değil.

### Sonraki adım

- Gemma ve Qwen için **Colab'da hız ölçümü** (saatte kaç hikâye).
- İstenirse Gemma'nın **12B** sürümü de denenebilir: daha kaliteli ama daha yavaş olur. Hız ölçümünden sonra karar verilir.
