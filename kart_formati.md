# Kart Biçimi

*25 Ekim 2026 · Kesinleşti. Değişiklik ancak iki ekip birlikte karar verirse.*
✅ = karar verildi · 💡 = öneri

## 1. Oyuncu ne görür?

1. **Kart:** Başlıkta konuşanın unvanı + ismi ("Defterdar Yakup") ✅, portresi, metni.
2. **Kaydırma:** Sola ya da sağa sürükler. Sürüklerken seçenek yazısı ve sadece **oklar** görünür (Para ▼ Halk ▲) ✅.
3. **Sonuç ekranı:** Sonuç cümlesi + **sayılar** (Para −10, Halk +5) + Devam Et ✅.

## 2. Modelin okuyup yazdığı biçim

```
<yonetim:50> <halk:50> <para:60> <ordu:35> <konu:maaş> <konuşan:akıncı_beyi>
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

Gösterge adları etikette küçük harf: `yonetim`, `halk`, `para`, `ordu` ✅ (görünen ad: **Yönetim**, Halk, Para, Ordu). Konuşan etiketi: unvanın küçük harf, alt çizgili hâli (`akıncı_beyi`) 💡.

## 3. Unity'deki biçim (JSON) 💡

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
- Dönüşüm: `ai/ortak/kart_bicimi.py` (Python) · `unity/Assets/Scripts/Kartlar/Kart.cs` (Unity)

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
