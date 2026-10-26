# Kurulum · Godot + C# ve Python

26 Ekim 2026. Mevcut kaynak kodu üç bağımsız Git deposundadır. Eski Unity araştırması [arşivde](arsiv/kurulum_unity_2026-10-26.md) tutulur.

## Depolar

Aynı çalışma klasöründe:

```sh
git clone https://github.com/IleriProgramlamaProje/AI.git
git clone https://github.com/IleriProgramlamaProje/Docs.git
git clone https://github.com/IleriProgramlamaProje/Game.git
```

Depolar özeldir; GitHub hesabının erişimi olmalı. Kimlik bilgilerini repo URL'sine veya kaynak dosyasına yazmayın. Üst klasör Git deposu değildir; commit/pull/push ilgili alt depoda yapılır.

## Python

AI deposunun içinde Python 3.11 ile:

```sh
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install -r ai/requirements.txt
python -m pytest ai/testler -q
```

`ai/requirements.txt` henüz platformlar arası kilit dosyası değildir. CPU/GPU PyTorch paket kaynağını ortama göre seçin; yerel CPU kurulumunu Colab GPU ortamına taşımayın.

Kod varsayılan olarak kardeş `Docs/tema.json` dosyasını okur; sembolik bağlantı gerekmez. Eski `AI/docs` düzeni de desteklenir. Belgeler başka konumdaysa Python'u başlatmadan `PROJE_DOCS_DIR` ortam değişkenini Docs klasörünün tam yoluna ayarlayın. `Docs` içinde yapılan değişiklikler Docs deposunda commit edilir.

## Godot + C#

Projenin sürümleri `Game/game/Game.csproj` ve `Game/global.json` dosyalarıyla tanımlıdır: Godot .NET SDK **4.7.2**, .NET SDK **10.0.402** (aynı özellik bandında güncel yama kabul edilir), hedef **net10.0**. Godot'un C# içeren **.NET** editörünü kullanın.

Game deposu içinde:

```sh
dotnet build game/Game.csproj
```

Godot ile `game/project.godot` açılır; **F5** ana sahne `Sahneler/Oyun.tscn`'yi çalıştırır. F6 yalnız açık sahneyi çalıştırır. Şu an dört panelden oluşan geliştirme önizlemesi vardır; kart oynanışı tamamlanmamıştır.

Kurulu Godot .NET çalıştırılabilir dosyasını `godot` yerine kullanarak:

```sh
godot --headless --path game res://Testler/SahneIskeletiTesti.tscn
```

Test üç boyutta panel geçişlerini kontrol eder. Gerçek fare/klavye/dokunma testi ayrıca yapılır. Makineye özel açma komutu ve ayrıntılar [Game README](https://github.com/IleriProgramlamaProje/Game/blob/main/README.md) içindedir.

## Colab ve öğretmen üretimi

Önce `AI/ai/veri_uretimi/hiz_olcumu.ipynb`, sonra `uretim.ipynb` kullanılır. Notebook AI ve Docs depolarını ayrı klonlar; mevcut klasörleri silmez. Özel depolar için token gizli girişle alınır, diske veya URL'ye yazılmaz. Hugging Face oturumu ayrıca açılır. GPU çalışma zamanı seçilmeli.

Notebook paketleri henüz gerçek GPU denemesiyle sabitlenmedi. Yerel sahte motor testleri öğretmenin yüklenmesini, GPU belleğini veya üretim kalitesini doğrulamaz. Varsayılan grup 8'dir; hız/bellek ölçümünden sonra artırılabilir. Hız ölçümü her çalışmada ayrı çıktı dosyası kullanır.

## Android ve tamamlanma ölçütü

Android dışa aktarma araçları ve gerçek APK bu çalışma alanında henüz doğrulanmadı. Masaüstü derlemesini APK başarısı saymayın. G0 küçük cihaz denemesi, araç sürümleri ve kabul ölçütleri [oyun geliştirme planında](https://github.com/IleriProgramlamaProje/Game/blob/main/docs/oyun_gelistirme_plani.md) takip edilir. Unity Hub araçları bu projede kullanılmaz.

Ana APK hedefi çevrimdışı yedek destedir. Model sunucusu dizüstünde çalışır; telefona model gömme ayrı, isteğe bağlı fizibilitedir.
