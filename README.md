# 🚀 Turkish Fine-Tuned Faster-Whisper with LoRA

Bu proje, **Faster-Whisper** modelinin Türkçe ses verileri ile fine-tune edilmesini ve ardından CTranslate2 formatına dönüştürülerek hızlı ve verimli bir şekilde inference yapılmasını amaçlamaktadır. Eğitim ve inference süreçleri **modüler bir yapıda** ayrı dosyalarda tasarlanmıştır.

---

## 🗂️ Proje Yapısı

```text
turkish-finetuned-faster-whisper/
├── training.py              # Eğitim aşaması
├── inference.py             # İnference aşaması
├── README.md                # Proje dokümantasyonu
├── whisper_finetuned/       # Fine-tune edilmiş model ve tokenizer
└── whisper_ct2_model/       # CTranslate2'ye dönüştürülmüş model
└── whisper_checkpoints/     # Modelin eğitim sırasındaki checkpointleri
```

---

## 🎯 Proje Özeti

* **Model:** Faster-Whisper (Whisper-Tiny)
* **Veri Seti:** Mozilla Common Voice 17.0 (Türkçe)
* **Fine-Tuning Yöntemi:** LoRA (Low-Rank Adaptation)
* **Epoch:** 35
* **Learning Rate:** 1e-5
* **Çıktı:** Her epoch sonunda eğitim ve doğrulama sonuçları (Loss, WER)

---

## ⚙️ Kullanılan Teknolojiler

* Python 3.10+
* Hugging Face Transformers
* Hugging Face Datasets
* Faster-Whisper
* CTranslate2
* LoRA (peft)

---

## 📦 Kurulum

```bash
pip install evaluate jiwer datasets peft faster-whisper ctranslate2
```

---

## 🏋️ Eğitim Aşaması

### `training.ipynb`
📌 Alternatif olarak Google Colab üzerinden çalışmak için:
[📓 Colab'da Eğitim Notebook'u](https://colab.research.google.com/drive/19GAveEqQ7Ks9l4lkWRUOrGp3Tu0Rjgh8?usp=sharing)

Bu dosya şunları yapar:

* Mozilla Common Voice veri setini indirir.
* LoRA ile Whisper Tiny modelini fine-tune eder.
* Her epoch'ta loss ve WER hesaplayıp görselleştirir.
* Modeli hem Hugging Face formatında hem de CTranslate2 formatında kaydeder.
* Checkpoint sistemi ile eğitim kesilse bile devam etmenizi sağlar.

Eğitimden sonra model:

```text
/content/drive/My Drive/whisper_finetuned
```

klasörüne kaydedilir.

---

## 📝 İnference Aşaması

### `inference.ipynb`
📌 Alternatif olarak Google Colab üzerinden çalışmak için:

[📓 Colab'da İnference Notebook'u](https://colab.research.google.com/drive/1zsoZUOCqH8IcjZH_5HArb2NK2b6Y-T9T?usp=sharing)

Bu dosya şunları yapar:

* Eğitilmiş CTranslate2 modelini yükler.
* Belirlenen ses dosyaları için Türkçe transkripsiyon yapar.
* Sonuçları terminalde detaylı şekilde gösterir.

---

## 🚀 Model Dönüştürme

Eğitim sonrası model şu komutla CTranslate2 formatına dönüştürülür:

```bash
ct2-transformers-converter --model "/content/drive/My Drive/whisper_finetuned" \
                           --output_dir "/content/drive/My Drive/whisper_ct2_model" \
                           --quantization float16 --force
```

> ✅ Bu dönüşüm sonrası modeli `faster-whisper` kütüphanesi ile kullanabilirsiniz.

---

## 📊 Çıktı Örnekleri

Transkripsiyon sırasında örnek çıktı:

```text
Transcription Results:
Detected language: tr (probability: 1.00)
Transcription:
[0.00s -> 16.00s] Ne mutlu, türküm diyene.
```

---

## 🗒️ Notlar

* GPU bellek verimliliği için LoRA kullanılmıştır.
* Fine-tune işlemi düşük kaynaklı makinelerde optimize edilmiştir.
* CTranslate2 dönüşümü inference hızını ciddi oranda artırır.
* GitHub'da .ipynb dosyalarının çıktı hücreleri bazen görünmeyebilir. Çıktıları doğrudan görmek isterseniz yukarıda paylaşılan Colab linklerini kullanabilirsiniz.

---

## 🔗 Kaynaklar

* [Faster-Whisper GitHub](https://github.com/SYSTRAN/faster-whisper)
* [Mozilla Common Voice Dataset](https://huggingface.co/datasets/mozilla-foundation/common_voice_17_0)
* [Hugging Face Whisper Modeli](https://huggingface.co/openai/whisper-tiny)

---

## 📌 İletişim

Herhangi bir soru ya da katkı için bana ulaşabilirsiniz.

> ✉️ \[tamerkanak75@gmail.com]
