# Kaydır & Karar Ver · Proje belgeleri

Türk tarzı krallıkta geçen kaydırmalı karar oyunu. Hedef, kartları ekibin sıfırdan eğiteceği küçük Türkçe dil modeliyle üretmek. Dört kişilik ekip; 26 Ekim–20 Aralık 2026.

| Depo | Görevi | Mevcut durum |
| --- | --- | --- |
| [Game](https://github.com/IleriProgramlamaProje/Game) | Godot + C# oyun istemcisi | Dört ekranlı sahne iskeleti ve sahne testi |
| [AI](https://github.com/IleriProgramlamaProje/AI) | Python, veri üretimi, model eğitimi | Torbalar, promptlar, üretim döngüsü ve birim testleri |
| [Docs](https://github.com/IleriProgramlamaProje/Docs) | Ortak kurallar ve plan | Bu depo |

Model, tokenizer, filtre, kart sunucusu ve oynanabilir APK henüz tamamlanmış değildir. Belgelerde haftası belirtilen dosyalar çoğunlukla planlanan dosyalardır.

Başlangıç sırası: [kurulum](kurulum.md) → [repo rehberi](repo_rehberi.md) → [kart biçimi](kart_formati.md) → [yol haritası](yol_haritasi.md). Güncel oyun uygulama görevleri [Game planında](https://github.com/IleriProgramlamaProje/Game/blob/main/docs/oyun_gelistirme_plani.md).

Ürün kuralları ve görev takvimi korunur. Eski motor araştırmaları `arsiv/`, geçmiş kararlar ve deneme raporları kendi tarihleriyle tutulur. Godot geçişi mevcut kodun durumudur; ekip/öğretmen teyidi Game planında açık takip maddesidir.

Çalışma düzeni: `yz/<konu>` veya `oyun/<konu>` dalı → PR → bir ekip üyesinin incelemesi. Büyük veri ve model ağırlıkları Drive/Hugging Face'te tutulur. Dönem raporlarını giden başkan `raporlar/` altına yazar.
