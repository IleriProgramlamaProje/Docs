# Fikir Notları

İleride bakılacak fikirler. Karar değil, not.

## Kısıtlı üretim (constrained decoding) · 21 Ekim 2026

- **Ne zaman bakılacak:** 6. hafta, kart üretici adımı (`ai/kart_uretici/kisitli_uretim.py`).
- **Nereden çıktı:** Muhammet'in mimari belgesi (llama.cpp grammar / JSON şeması önerisi).
- **Fikir:** Model kartı parça parça yazarken yanına bir "bekçi" konur. Bekçi her adımda kalıba uymayan seçeneklerin puanını sıfırlar, model sadece izin verilenler arasından seçer.
- **Bizim kart için kalıp (yeni biçimle):**
  1. `<kart>` ile başla
  2. Kart metni, en fazla 50 kelime (50'de sadece `<sol>`'a izin)
  3. `<sol>` + seçenek yazısı
  4. Etiketler: sadece geçerli olanlar (`<para->`, `<ordu+++>`…), en az 1, en fazla 3, en az biri eksi
  5. `<sonuc>` + bir cümle
  6. `<sag>` + seçenek yazısı + aynı etiket kuralları + `<sonuc>`
  7. `</kart>` ile bitir
- **Kazanç:** Doğrulayıcının biçim, altın kural ve gösterge sınırı maddeleri neredeyse kendiliğinden çözülür.
- **Dikkat:** Zorlamak mantıksız etki seçtirebilir; asıl çözüm iyi eğitim, bekçi sadece emniyet kemeri. İçeriği garanti etmez. Doğrulayıcı yine kalır (isim, yasak kelime, hitap).
