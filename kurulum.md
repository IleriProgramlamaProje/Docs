# Kurulum Rehberi

*Herkes için · Hazırlık haftası + 1. haftanın ilk günleri*

> **Mantık:** Dört kişinin bilgisayarı **aynı** olmalı. Özellikle Unity sürümü bir rakam bile farklı olursa proje başkasında bozuk açılabilir. Bu yüzden her adımın sonunda bir **kontrol** var. Kontrolü geçmeden sonraki adıma geçme.
> 💡 = öneri (1. hafta toplantısında onaylanır).

---

## 26 Ekim 2026 · Araştırılmış sürüm önerisi 💡

**Durum:** Aşağıdakiler teknik öneridir; ekip kararı olarak onaylanmış değildir. Unity henüz kurulup çalıştırılmadı, APK testi yapılmadı. Önce dört bilgisayarda boş proje açma + telefonda APK denemesi, ardından sürümü sabitleme yapılmalı.

| Bileşen | Öneri | Gerekçe / sınır |
| --- | --- | --- |
| Unity Editor | **Unity 6.3 LTS `6000.3.27f1`** | 20 Ekim 2026 tarihli kararlı sürüm; 6.3 LTS desteği Aralık 2027'ye kadar. 6.0 LTS'nin standart desteği Ekim 2026'da bitiyor. Bu kısa teslim projesinde yeni Update/alpha/beta serilerine ihtiyaç yok. |
| Unity Hub | Kurulum günündeki **kararlı Hub** | Hub sürümü proje biçimini belirlemez; birebir eşit olması gereken Editor sürümüdür. |
| Android araçları | **Editor ile Hub'dan gelen araçlar** | Android Build Support + Android SDK & NDK Tools + OpenJDK birlikte kurulmalı; sistem Java/Android kurulumuna elle bağlanmamalı. |
| Android NDK / Java | **NDK r27c `27.2.12479018` / OpenJDK 17** | Unity 6000.3 resmî bağımlılık tablosuyla uyumlu. |
| Android SDK araçları | **Build Tools 36.0.0, Command-line Tools 16, Platform Tools 37.0.1** | Resmî tabloda 6000.3.26f1 ve sonrası için dağıtılan sürümler. Bunlar minimum/target Android API seviyesi değildir; API seviyesi telefon ve dağıtım hedefiyle ayrıca belirlenir. |
| C# / API profili | **Unity'nin C# 9 derleyicisi / .NET Standard 2.1** | Unity kendi derleme ortamını kullanır. Bilgisayardaki .NET 10 SDK, Unity'yi .NET 10 uygulamasına dönüştürmez; yeni C#/.NET özellikleri varsayılmamalı. |
| Python | **3.11 serisi; bu bilgisayarda `3.11.17`** | Rehberin mevcut tercihiyle uyumlu, mevcut testler geçti. 3.11 güvenlik desteği Ekim 2027'ye kadar; en yeni Python'a geçmek için şu aşamada gerekçe yok. Her AI deposunda ayrı `.venv` kullanılır. |
| PyTorch | **Yerel geliştirmede `2.14.1` CPU** | Resmî kararlı sürüm notları mevcut; bu bilgisayarda `2.14.1+cpu` importu doğrulandı. Colab GPU ortamına CPU paketi kurulmaz. |
| Python yardımcı paketleri | Aşağıdaki **yerel doğrulanmış başlangıç sürümleri** | Mevcut 4 test + import + bağımlılık kontrolü geçti; henüz model eğitimi/sunucu uçtan uca testi yapıldığı anlamına gelmez. |
| Git / Git LFS | İşletim sisteminin güncel kararlı paketleri | Birebir aynı yama sürümü gerekmez. Unity deposunda LFS etkin olmalı. |
| Editör | Zed kullanılabilir; ortak rehber için VS Code kararlı sürüm alternatif | Editör aynı olmak zorunda değil. Esas doğrulama Unity derlemesi ve Python testleridir. |

### Yerel Python başlangıç sürümleri

26 Ekim'de kurulan ve kontrol edilen doğrudan bağımlılıklar:

```text
torch==2.14.1              # Bu bilgisayarda CPU varyantı: 2.14.1+cpu
numpy==2.4.6
tokenizers==0.23.3
pyyaml==6.0.3
tqdm==4.70.1
matplotlib==3.11.2
openpyxl==3.1.5
pytest==9.1.1
fastapi==0.162.0
uvicorn==0.54.0
```

Notebook için ayrıca `ipykernel==7.4.0`, Hugging Face istemcisi için `huggingface_hub==2.3.0` kuruldu. Bu liste tam, platformlar arası kilit dosyası değildir. Ekip onayından sonra AI deposunda işletim sistemi/CPU-GPU ayrımını gözeten bağımlılık sabitlemesi yapılmalı; bu araştırmada `AI/ai/requirements.txt` değiştirilmedi.

**Colab ayrı ortamdır:** Mevcut notebook'lar `vllm`, `transformers`, `accelerate` paketlerini `-U` ile kuruyor. Bu, tekrar üretilebilir değildir. Bunları yerel CPU ortamına eklemiyoruz. Öğretmen modeliyle gerçek GPU denemesi geçtikten sonra birlikte çözümlenen sürümler notebook'ta sabitlenmeli; yalnızca yerel birim testine bakarak GPU sürümü önerilmemeli.

### Linux ve proje tercihi

- Unity 6.3 Editor için resmî Linux desteği **Ubuntu 22.04 / 24.04** ve belirtilen masaüstü/ekran kartı koşullarıdır. Yeni bir standart Linux ortamı seçilecekse **Ubuntu 24.04 LTS** önerilir.
- Muhammed'in bilgisayarı **LMDE 7 / Debian 13 tabanlıdır**; resmî destek listesinde değildir. Bu, kesin çalışmaz demek değildir. Mevcut sistemi değiştirmeden önce Hub kurulumu, Editor açılışı, Play Mode ve Android build testi yapılmalı. Sorun çıkarsa desteklenen Ubuntu ortamı değerlendirilir.
- Oyun tek sahneli, kart/panel ağırlıklıdır. İlk proje için **2D Built-In + Canvas/uGUI ve TextMeshPro** önerilir; HDRP ve ek render paketleri gerekli değildir. Bu mimari öneridir, zorunlu resmî gereksinim değildir.
- Sürüm notlarında `6000.3.27f1` için tekrarlı `LoadSceneAsync` sahne geçişlerinde kilitlenme ve Android cihaz döndürmede SRP hataları bulunuyor. Tek sahne yaklaşımı ilk riski azaltır; cihaz döndürme ve build davranışı yine test edilmeli. “LTS” hatasızlık garantisi değildir.
- Proje oluşturulunca Editor'ın ürettiği `ProjectSettings/ProjectVersion.txt`, `Packages/manifest.json`, `Packages/packages-lock.json` ve varlıkların `.meta` dosyaları Git'e alınmalı. Bu dosyalar Editor çalıştırılmadan elle uydurulmamalı. Paketler daha sonra tek kişinin bilgisayarında bağımsız yükseltilmemeli.

### Mevcut üç-repo düzeni

Eski bölümlerdeki tek-repo yolları yerine çalışma alanı şu şekildedir:

```text
ileri programlama proje/
├── AI/       # ai/, data/, .venv/
├── Docs/     # Bu rehber, kart_formati.md, tema.json
└── Unity/    # Unity projesi Unity/unity/ altında oluşturulacak
```

Linux'taki mevcut kurulumda eski AI belge yollarını karşılamak için `AI/docs -> ../Docs` yerel sembolik bağlantısı vardır. Windows'ta aynı bağlantı otomatik oluşmaz; AI ekibi ayrı repo yollarını taşınabilir şekilde düzenlemelidir.

### Kaynaklar

26 Ekim 2026 tarihinde kontrol edildi:

- [Unity 6 destek politikası](https://unity.com/releases/unity-6/support)
- [6000.3.27f1 sürüm notları ve bilinen sorunlar](https://unity.com/releases/editor/whats-new/6000.3.27f1)
- [Unity 6.3 sistem gereksinimleri](https://docs.unity.com/en-us/engine/6000.3/manual/get-started/install-and-upgrade/getting-started-installing-unity/system-requirements)
- [Android bağımlılık sürümleri](https://docs.unity.com/en-us/engine/6000.3/manual/platform-specific/android/getting-started/sdksetup/supported-dependency-versions)
- [Android modüllerini kurma](https://docs.unity.com/en-us/engine/6000.3/manual/platform-specific/android/getting-started/sdksetup/install-dependencies)
- [Unity C# derleyicisi](https://docs.unity3d.com/6000.3/Documentation/Manual/csharp-compiler.html)
- [.NET Standard 2.1 API profili](https://docs.unity3d.com/6000.3/Documentation/ScriptReference/ApiCompatibilityLevel.NET_Standard.html)
- [Python sürüm destek takvimi](https://devguide.python.org/versions/)
- [Resmî PyTorch sürümleri](https://github.com/pytorch/pytorch/releases)

---

## Genel bakış: ne kuruyoruz, neden?

| # | Ne | Neden lazım | Kim |
| --- | --- | --- | --- |
| 1 | **Hesaplar** (GitHub, Google, Hugging Face, Unity, Discord) | Kod, Colab, model deposu, Unity lisansı, iletişim | Herkes |
| 2 | **Git + Git LFS** | Kodu birlikte yazmak; LFS büyük görselleri/sesleri taşır | Herkes |
| 3 | **Kod editörü** (VS Code) | Python ve C# yazmak | Herkes |
| 4 | **Unity Hub + Unity 6 LTS + Android modülleri** | Oyun ve APK | Herkes (YZ'deki de, çünkü roller dönüyor) |
| 5 | **Python 3.11 + paketler** | Yapay zekâ kodunu bilgisayarda denemek | Herkes |
| 6 | **Google Colab** | Ekran kartı gereken işler: veri üretimi, eğitim | Herkes |
| 7 | **Hugging Face girişi** | Tokenizer, model ve büyük veri setlerini saklamak | Herkes |
| 8 | **Google Drive klasörü** | Colab'ın ürettiği büyük dosyalar | Bir kişi açar, herkes erişir |
| 9 | **LM Studio** *(isteğe bağlı)* | Hazır modelleri bilgisayarda denemek (öğretmen denemesinde kullanıldı) | İsteyen |
| 10 | **Telefon ayarı** | APK'yı telefonda denemek | En az bir Android telefon |

> Neden herkes her şeyi kuruyor? Çünkü her 2 haftada bir alan değişiyor. Bugün oyun ekibinde olan, 3. haftada yapay zekâ ekibine geçecek.

---

## 1. Hesaplar

| Hesap | Nereden | Not |
| --- | --- | --- |
| GitHub | github.com | Kullanıcı adını Discord'a yaz, depoya davet edilirsin |
| Google | — | Colab ve Drive için. Üniversite hesabı da olur |
| Hugging Face | huggingface.co | Kullanıcı adını Discord'a yaz, ekip organizasyonuna davet edilirsin 💡 |
| Unity | unity.com | Ücretsiz "Personal" lisans yeterli |
| Discord | discord.com | Ekip sunucusu |

**Kontrol:** Dört hesap açık, kullanıcı adların Discord'da paylaşıldı.

---

## 2. Git + Git LFS

**Git nedir?** Kodun her değişikliğini kaydeden bir defter. Dört kişi aynı dosyalarda çalışınca kimin neyi değiştirdiği karışmasın diye.
**Git LFS nedir?** Git büyük dosyalarda (görsel, ses) yavaşlar. LFS bunları ayrı bir yerde tutar, Git'te sadece "adresleri" durur.

1. **git-scm.com** → indir → kur (varsayılan seçenekler).
2. **git-lfs.com** → indir → kur. (Windows'ta Git ile birlikte gelir.)
3. Terminalde bir kez:
   ```bash
   git config --global user.name "Adın Soyadın"
   git config --global user.email "github-epostan@ornek.com"
   git lfs install
   ```
4. İsteyen **GitHub Desktop**'u da kurabilir (görsel arayüz). Komut satırı zorunlu değil.

**Kontrol:**
```bash
git --version        # git version 2.x
git lfs version      # git-lfs/3.x
```

### Depoyu indir
```bash
git clone https://github.com/<ekip>/ileri-programlama.git
cd ileri-programlama
```

### İlk Pull Request alıştırması
1. Dal aç: `git checkout -b oyun/ekip-<adin>`
2. `docs/ekip.md`'de kendi satırına bir not yaz.
3. `git add docs/ekip.md` → `git commit -m "Ekip dosyasına kendimi ekledim"` → `git push -u origin oyun/ekip-<adin>`
4. GitHub'da **Pull Request** aç, bir arkadaşın onaylasın, birleştir.

**Kontrol:** Herkesin bir PR'ı `main`'e birleşti.

---

## 3. Kod editörü: VS Code 💡

**Neden VS Code?** Hem Python hem C# için ücretsiz, tek editör. (Visual Studio ya da Rider kullanmak isteyen kullanabilir.)

1. **code.visualstudio.com** → kur.
2. Eklentiler: **Python**, **Jupyter**, **C# Dev Kit**, **Unity** (Microsoft).
3. Unity'de: *Edit → Preferences → External Tools → External Script Editor* = Visual Studio Code.

**Kontrol:** Unity'de bir C# dosyasına çift tıklayınca VS Code açılıyor, kod renkli görünüyor.

---

## 4. Unity

**Mantık:** Unity projesi, Unity sürümüne çok bağlıdır. **Herkes birebir aynı sürümü** kurar. Sürüm 1. hafta toplantısında yazılır ve bir daha değişmez.

1. **unity.com/download** → **Unity Hub**'ı kur, Unity hesabınla gir.
2. Hub → *Installs* → *Install Editor* → **Unity 6.3 LTS `6000.3.27f1` önerilir** 💡 (yukarıdaki araştırmaya bak). **Ekip onayı: bekliyor.** Onaydan sonra herkes tam olarak aynı sürümü kurar; listede görünmezse resmî sürüm arşivinden Hub ile açılır.
3. Modüller ekranında işaretle:
   - ☑ **Android Build Support**
     - ☑ OpenJDK
     - ☑ Android SDK & NDK Tools
   - ☑ (Windows'taysan) Visual Studio istemiyorsan işareti kaldır, VS Code kullanacağız
4. Kurulum bitince Hub → *Projects* → *Add* → çalışma alanındaki `Unity/unity/` klasörünü seç. *(Gerçek Unity projesi 1. haftada oluşturulunca; şu an yalnızca README var.)*

**Kontrol:** Proje açılıyor, *File → Build Settings*'te **Android** seçilebiliyor.

### Boş APK denemesi
1. *File → Build Settings → Android → Switch Platform*.
2. Telefonda **Geliştirici seçenekleri** → **USB hata ayıklama** açık (telefon ayarlarında "Yapı numarası"na 7 kez dokunarak açılır).
3. Telefonu USB ile bağla → *Build And Run*.

**Kontrol:** Boş sahne telefonda açıldı.

---

## 5. Python

**Mantık:** Asıl ağır işler Colab'da, ama kodu yazarken küçük denemeleri bilgisayarda yaparız (kart biçimi dönüştürücüsü, filtre, testler).

1. **python.org** → **Python 3.11** 💡 (Windows'ta kurulumda **"Add Python to PATH"** işaretli olsun).
2. **AI deposunun kökünde** sanal ortam (Python 3.11 ile):
   ```bash
   python -m venv .venv
   # Windows:  .venv\Scripts\activate
   # Mac/Linux: source .venv/bin/activate
   python -m pip install -r ai/requirements.txt
   ```
   Linux'ta `uv` kullanılıyorsa Python serisini açıkça seçebilirsiniz: `uv venv --python 3.11 .venv`. Mevcut bilgisayarda ortam zaten kuruldu; yeniden oluşturmak gerekmez. CPU/GPU PyTorch kaynağını ortama göre seçin.
3. **Sanal ortam nedir?** Projenin paketlerini bilgisayarın geri kalanından ayıran bir kutu. Her seferinde terminali açınca `activate` komutunu çalıştır.

**Kontrol:**
```bash
python -c "import torch, numpy, tokenizers, yaml; print('tamam', torch.__version__)"
pytest ai/testler   # 1. haftadan sonra testler gelince
```

---

## 6. Google Colab

**Mantık:** Model eğitimi ve öğretmen modelle veri üretimi ekran kartı (GPU) ister. Colab bunu tarayıcıdan verir. Ekipte 2 hesapta 200'er birim var; gece üretimini o dönemin YZ ekibi kendi hesaplarıyla çalıştırır.

1. **colab.research.google.com** → yeni defter.
2. *Çalışma zamanı → Çalışma zamanı türünü değiştir → T4 GPU*.
3. Bir hücreye yaz, çalıştır:
   ```python
   import torch
   print(torch.cuda.is_available(), torch.cuda.get_device_name(0))
   ```

**Kontrol:** `True Tesla T4` (ya da başka bir GPU adı) yazıyor.

**Dikkat:** Colab birimleri sınırlı. Defteri işin bitince kapat (*Çalışma zamanı → Bağlantıyı kes ve sil*), boşta açık bırakma.

---

## 7. Hugging Face

**Mantık:** Model ağırlıkları ve tokenizer Git'e sığmaz. Hugging Face, bunlar için yapılmış bir depo (model için GitHub gibi). Colab'dan da kolay erişilir.

1. huggingface.co → *Settings → Access Tokens* → **write** yetkili bir token oluştur. **Token'ı kimseyle paylaşma, Git'e koyma.**
2. Bilgisayarda ve Colab'da:
   ```bash
   pip install huggingface_hub
   huggingface-cli login     # token'ı yapıştır
   ```
3. Ekip organizasyonu 💡: `ileri-programlama` (özel depolar: `tokenizer`, `model-1m`, `model-10m`, `model-30m`, `veri`).

**Kontrol:** `huggingface-cli whoami` kullanıcı adını yazıyor.

---

## 8. Google Drive klasörü 💡

Bir kişi açar, herkesle paylaşır. Colab defterleri buraya yazar.

```
ileri-programlama/
├── 01_Belgeler/        Toplantı notları, sunum taslakları
├── 02_Veri/
│   ├── uretilen/       Öğretmenin gece ürettikleri (ham)
│   ├── temiz/          Filtreden geçenler
│   └── hazir/          train.bin / val.bin
├── 03_Modeller/        Eğitim kayıt noktaları (sonra Hugging Face'e)
└── 04_Gorseller/       Görsel üreticiden çıkan ham resimler
```

**Kontrol:** Herkes klasörü görüyor, Colab'dan `drive.mount` ile erişilebiliyor.

---

## 9. LM Studio *(isteğe bağlı)*

Hazır modelleri bilgisayarda çalıştıran sohbet uygulaması. Öğretmen model kalite denemesi bununla yapıldı (`raporlar/ogretmen_secimi.md`). Projede zorunlu değil.

---

## 10. Son kontrol listesi

- [ ] Hesaplar açık, kullanıcı adları Discord'da
- [ ] `git --version` ve `git lfs version` çalışıyor
- [ ] Depo klonlandı, **ilk PR birleşti**
- [ ] VS Code + eklentiler, Unity'den açılıyor
- [ ] Unity **ekipteki sürüm** + Android modülleri; proje açılıyor
- [ ] **Boş APK** bir telefonda açıldı
- [ ] `import torch` çalışıyor
- [ ] Colab'da GPU testi geçti
- [ ] `huggingface-cli whoami` çalışıyor
- [ ] Drive klasörü görünüyor

---

## Sunum dizüstü kurulumu (8. hafta)

- [ ] Depo güncel, sanal ortam kurulu
- [ ] Model ağırlıkları Hugging Face'ten indirilmiş (internetsiz çalışacak)
- [ ] `python ai/kart_uretici/sunucu.py` internetsiz başlıyor
- [ ] Unity sunucuya bağlanıyor; sunucu kapatılınca yedek desteye düşüyor
- [ ] Wi-Fi kapalıyken baştan sona bir oyun oynandı
