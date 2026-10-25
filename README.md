# ileri-programlama · Kaydır & Karar Ver

Türk tarzı bir krallıkta geçen **kaydırmalı kart oyunu**. Kartları, ekibin **sıfırdan eğittiği küçük bir Türkçe dil modeli** oyun sırasında yazar.

- **Oyun:** Unity (C#) → Android APK
- **Yapay zekâ:** Python · öğretmen modelle veri üretimi → tokenizer → model (1M → 10M → 30M) → ince ayar → kart üretici
- **Ders:** İleri Programlama · 4 kişilik ekip · 26 Ekim – 20 Aralık 2026

## Klasörler

| Klasör | İçinde ne var |
| --- | --- |
| `docs/` | Yol haritası, kararlar, kart biçimi, tema, ekip, raporlar |
| `data/` | Küçük veriler: torbalar, altın set, örnekler (büyük veriler Drive / Hugging Face'te, bkz. `data/README.md`) |
| `ai/` | Python kodu: veri üretimi, filtre, tokenizer, model, eğitim, kart üretici, ölçüm |
| `unity/` | Unity projesi |

**Önce oku:** `docs/yol_haritasi.md` → `docs/repo_rehberi.md` (hangi dosya ne işe yarar) → `docs/kart_formati.md` → `docs/kurulum.md`

## İlk kurulum

Ayrıntı: `docs/kurulum.md`.

```bash
git clone <depo-adresi>
cd ileri-programlama
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r ai/requirements.txt
pytest ai/testler        # testler geçmeli
```
Unity: herkes **birebir aynı sürümü** kullanır (`docs/kurulum.md`), `unity/` klasörünü Unity Hub'dan açar.

## Çalışma kuralları (özet)

- `main`'e doğrudan yazılmaz. Dal: `yz/<konu>` ya da `oyun/<konu>` → Pull Request → en az bir kişi onaylar.
- Model ağırlıkları ve büyük veriler Git'e girmez.
- Her dönem sonu (pazar) giden başkan `docs/raporlar/` altına raporunu yazar.
- Kararlar `docs/kararlar.md`'ye yazılır.

Ayrıntı: `docs/yol_haritasi.md` 3. bölüm.
