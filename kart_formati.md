# Kart Biçimi

*25 Ekim 2026 · Kesinleşti. Değişiklik ancak iki ekip birlikte karar verirse.*
✅ = karar verildi · 💡 = öneri

## 1. Oyuncu ne görür?

1. **Kart:** Başlıkta konuşanın unvanı + ismi ("Hazinedar Yakup") ✅, portresi, metni.
2. **Kaydırma:** Sola ya da sağa sürükler. Sürüklerken seçenek yazısı ve sadece **oklar** görünür (Para ▼ Halk ▲) ✅.
3. **Sonuç ekranı:** Sonuç cümlesi + **sayılar** (Para −10, Halk +5) + Devam Et ✅.

## 2. Modelin okuyup yazdığı biçim

```
<yonetim:50> <halk:50> <para:60> <ordu:35> <konu:maaş> <konuşan:akinci_beyi>
<kart> {hitap}, askerler üç aydır maaş alamadı. Kışlada söylenmeler başladı; ödenmezse kaçanlar olacak.
<sol> Maaşları hazineden öde <para--> <ordu++>
<sonuc> Askerler sevindi, ama hazine iyice eridi.
<sag> Beklesinler, hazine boş <ordu--> <halk->
<sonuc> Kışlada homurtular büyüdü, birkaç asker gece kaçtı.
</kart>
```

| Parça | Kim yazar | Not |
| --- | --- | --- |
| İlk satır (durum) | **Oyun kodu** ✅ | 4 gösterge + konuşan + konu. Başka etiket yok ✅. Kartların bir kısmında `<konu:serbest>`: model derdi kendi seçer ✅ |
| `<kart>` metni | **Model** ✅ | 20–35 kelime, en fazla 50 |
| `{hitap}` | Model, gerektiğinde ✅ | Oyun kodu "Beyim" / "Hatunum" yapar |
| `<sol>` / `<sag>` | Model ✅ | Kartın derdine verilen karar, 2–5 kelime |
| Etki etiketleri | Model ✅ | Seçenek başına 1–3; iki seçenek de en az birini düşürür |
| `<sonuc>` | Model ✅ | Her seçenekten sonra bir cümle (etiket adı 💡) |

### Etki işaretleri ✅

| Model yazar | Oyunda |
| --- | --- |
| `+` / `-` | ±5 |
| `++` / `--` | ±10 |
| `+++` / `---` | ±15 |

Gösterge adları etikette küçük harf: `yonetim`, `halk`, `para`, `ordu` ✅ (görünen ad: **Yönetim**, Halk, Para, Ordu). Konuşan etiketi: `tema.json` → `karakterler[].anahtar` (ASCII, alt çizgili: `akinci_beyi`) 💡.

## 3. Godot'taki biçim (JSON) 💡

```json
{
  "konusan": "akinci_beyi",
  "konu": "maas",
  "metin": "{hitap}, askerler üç aydır maaş alamadı. Kışlada söylenmeler başladı; ödenmezse kaçanlar olacak.",
  "sol": { "etiket": "Maaşları hazineden öde", "etki": { "para": -10, "ordu": 10 }, "sonuc": "Askerler sevindi, ama hazine iyice eridi." },
  "sag": { "etiket": "Beklesinler, hazine boş", "etki": { "ordu": -10, "halk": -5 }, "sonuc": "Kışlada homurtular büyüdü, birkaç asker gece kaçtı." },
  "kaynak": "altin_set",
  "lisans": "sadece_ders"
}
```

- `kaynak`: `altin_set` · `model` · `ogretmen`
- `lisans`: Altın set kartları `sadece_ders` ✅ (oyun yayınlanırsa çıkarılır)
- Planlanan dönüşüm: `ai/ortak/kart_bicimi.py` (Python, görev S2) · `Game/game/Betikler/Kartlar/Kart.cs` (Godot)

## 4. Doğrulayıcının kontrol listesi

1. Biçim: `<kart>`, `<sol>`, `<sonuc>`, `<sag>`, `<sonuc>`, `</kart>` yerinde mi?
2. Uzunluk: 20–35 kelime, en fazla 50
3. Altın kural: iki seçenek de en az bir göstergeyi düşürüyor mu?
4. Gösterge sınırı: seçenek başına 1–3; işaretler sadece `+ ++ +++ - -- ---`
5. İsim yok: sadece unvan
6. Hitap: "Beyim/Hatunum" elle yazılmamış, sadece `{hitap}`
7. Modern kelime yok (`docs/tema.json` → `yasak_kelimeler`)
8. Sonuç cümlesi var mı, boş değil mi?

Geçmezse kart yeniden yazdırılır, yine olmazsa yedek desteden kart gelir ✅.

## 5. Üretimin mevcut durumu · 1 Kasım

- **Öğretmen** (Gemma 4 12B) etiketli gövde değil **satırlı** biçim yazar: `Metin / Sol / Sol sonuç / Sol etki / Sağ / Sağ sonuç / Sağ etki`. Etiketli gövdede ve tek sabit örnekte model örneğin etkilerini kopyalıyordu (ilk denemede kartların %31'i); satırlı biçimde her istekte farklı bir örnek gösterilir, etki sonuca bakılarak yazılır.
- **Filtre** (`AI/ai/filtre/filtre.py`, görev S1) ve **dönüştürücü** (`AI/ai/ortak/kart_bicimi.py`, görev S2) henüz yazılmadı; kurallar `yz_gorevleri.md`'de. O zamana kadar üretim `ham/` klasöründe bekler.
- **Konuşan anahtarı** önerisi: `tema.json` → `karakterler[].anahtar` (ASCII, alt çizgili: `akinci_beyi`), hem eğitim satırında hem JSON'da aynısı. Konu: eğitim satırında boşluklar `_` (`<konu:kale_onarımı>`), JSON'da ASCII (`kale_onarimi`). İki ekip onaylayınca kesinleşir.
