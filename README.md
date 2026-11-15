# BRSpeech-TTS: A High-Quality Dataset in Portuguese for Speech Synthesis

[![Hugging Face Dataset](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-freds0%2FBRSpeech--TTS-blue)](https://huggingface.co/datasets/freds0/BRSpeech-TTS/)
[![Website](https://img.shields.io/badge/Website-BRSpeech--Dataset-green)](https://freds0.github.io/BRSpeech-Dataset/)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

**BRSpeech-TTS** is a high-quality, multi-speaker dataset for training Text-to-Speech (TTS) and voice cloning models in Portuguese, developed at the [Center of Excellence in Artificial Intelligence (CEIA)](https://ceia.ufg.br/) of the Federal University of Goiás (UFG).

**BRSpeech-TTS is an enhanced version of the Portuguese subset of the CML-TTS dataset that underwent studio-grade speech enhancement via Adobe Podcast Enhance (Adobe Speech Enhancement).** All audio files were denoised, de-reverberated, and restored to a full-bandwidth sampling rate of **48 kHz** (compared to 24 kHz in the original CML-TTS dataset). Transcriptions were generated and verified using Automatic Speech Recognition (**OpenAI Whisper Large-v2** and **MMS**) and aligned against public-domain literary works from [Project Gutenberg](https://www.gutenberg.org/) and [LibriVox](https://librivox.org/). Furthermore, all 62 speakers were classified by Portuguese variety (`pt_br` vs. `pt_eu`) using [`lgris/portuguese-accent-classifier`](https://huggingface.co/lgris/portuguese-accent-classifier).

The dataset is publicly available on the Hugging Face Hub at **[https://huggingface.co/datasets/freds0/BRSpeech-TTS/](https://huggingface.co/datasets/freds0/BRSpeech-TTS/)** under the **CC-BY 4.0** license.

---

## Download & Usage

### 1. Hugging Face Hub (Recommended)

You can download or stream **BRSpeech-TTS** directly from the [Hugging Face Hub (`freds0/BRSpeech-TTS`)](https://huggingface.co/datasets/freds0/BRSpeech-TTS/) using the `datasets` library:

```python
from datasets import load_dataset

# Load BRSpeech-TTS from Hugging Face Hub
dataset = load_dataset("freds0/BRSpeech-TTS")

print(dataset)
# DatasetDict({
#     train: Dataset({
#         features: ['wav_filename', 'duration', 'text', 'transcript', 'levenshtein',
#                    'speaker', 'file_size', 'num_words', 'gender', 'accent', 'audio'],
#         num_rows: 73848
#     })
#     validation: Dataset({features: [...], num_rows: 1158})
#     test: Dataset({features: [...], num_rows: 1316})
# })
```

### 2. Archive Downloads & Checksums

- **Hugging Face Dataset Repository:** [https://huggingface.co/datasets/freds0/BRSpeech-TTS/](https://huggingface.co/datasets/freds0/BRSpeech-TTS/)
- **Per-Speaker Accent Classification CSV:** [`resources/accent_por_locutor.csv`](resources/accent_por_locutor.csv)
- **OpenSLR Mirror (Original CML-TTS v0.1):** [http://www.openslr.org/146/](http://www.openslr.org/146/)
  - [CML-TTS Dataset Portuguese (`cml_tts_dataset_portuguese_v0.1.tar.bz`)](https://www.openslr.org/resources/146/cml_tts_dataset_portuguese_v0.1.tar.bz) — MD5: `8c877a4be0eb41f275497609df5a114c`
  - [CML-TTS Dataset Segments (`cml_tts_dataset_segments_v0.1.tar.bz`)](https://www.openslr.org/resources/146/cml_tts_dataset_segments_v0.1.tar.bz) — MD5: `f529a908aba26a6d891b4fb17ab3125b`

After downloading the enhanced BRSpeech-CML-TTS archive, verify its MD5 checksum:
```text
0966023cea9c0f339dae464d0fcfe7f8  BRSpeech_CML_TTS_v14012024.tar.bz
```

---

## Dataset Statistics

**BRSpeech-TTS** comprises audiobooks sourced from public-domain literary works on [Project Gutenberg](https://www.gutenberg.org/), narrated by volunteers from the [LibriVox](https://librivox.org/) project. It includes recordings in **Brazilian Portuguese (`pt_br`, 99.30% of duration / 51 speakers)** and **European Portuguese (`pt_eu`, 0.70% of duration / 11 speakers)**, all enhanced with **Adobe Speech Enhancement** at a **48 kHz** sampling rate (`16-bit PCM Mono`).

### Key Highlights
- **Total Duration:** `159.87 hours` (`55.68 h` Male / `104.19 h` Female)
- **Total Speakers:** `62 speakers` (`37 Male` / `25 Female`; `51 pt_br` / `11 pt_eu`)
- **Total Audio Segments:** `39,230` base FLAC files (`20.59 GB`), segmented into `76,322` utterances in the Hugging Face Hub Parquet release (`73,848` train / `1,158` validation / `1,316` test)
- **Public-Domain Books:** `55` classic literary works
- **Total Vocabulary Volume:** `1,306,913 words` (`7,606,434 characters`)
- **Audio Quality & Format:** `48 kHz`, `16-bit Mono`, enhanced via **Adobe Podcast Enhance**

### Split, Gender & Accent Breakdown

| Subset Split | Male Duration | Female Duration | Total Duration | Male Speakers | Female Speakers | Total Speakers | Accents (`pt_br` / `pt_eu`) | Base FLAC Segments | HF Hub Utterances | Books |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Train** | 51.28 h | 101.23 h | **152.51 h** | 25 | 17 | **42** | 33 `pt_br` / 9 `pt_eu` | 37,533 | 73,848 | 53 |
| **Validation (Dev)** | 2.50 h | 1.13 h | **3.63 h** | 7 | 3 | **10** | 8 `pt_br` / 2 `pt_eu` | 826 | 1,158 | 10 |
| **Test** | 1.90 h | 1.83 h | **3.73 h** | 5 | 5 | **10** | 10 `pt_br` / 0 `pt_eu` | 871 | 1,316 | 9 |
| **Total** | **55.68 h (34.8%)** | **104.19 h (65.2%)** | **159.87 h (100%)** | **37 (59.7%)** | **25 (40.3%)** | **62 (100%)** | **51 `pt_br` / 11 `pt_eu`** | **39,230** | **76,322** | **55** |

### Portuguese Accent Classification (`pt_br` vs. `pt_eu`)

All 39,230 base FLAC recordings across the 62 narrators were classified using [`lgris/portuguese-accent-classifier`](https://huggingface.co/lgris/portuguese-accent-classifier) (`4f287aba669b7688570a213bdab125631a0a0920`). Per-speaker labels are available in [`resources/accent_por_locutor.csv`](resources/accent_por_locutor.csv):

| Accent Label | Variety | Speakers (M / F) | Splits (Train / Dev / Test) | Duration (h) | Share (%) | Speaker Segments | Clip Preds (`pt_br` / `pt_eu`) | Mean Majority Share | Mean Confidence |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **`pt_br`** | Brazilian Portuguese | **51** (33 M / 18 F) | 33 / 8 / 10 | **158.75 h** | 99.30% | 38,971 | 38,926 / 45 | 99.64% | 0.9808 |
| **`pt_eu`** | European Portuguese | **11** (4 M / 7 F) | 9 / 2 / 0 | **1.12 h** | 0.70% | 259 | 0 / 259 | 100.00% | 0.9969 |
| **Total** | **All Varieties** | **62** (37 M / 25 F) | **42 / 10 / 10** | **159.87 h** | **100.00%** | **39,230** | **38,926 / 304** | **99.71%** | **0.9837** |

- **European Portuguese (`pt_eu`) Speakers (11 total, 100% majority agreement on all 259 clips):**
  - **Validation (`dev`):** `6549` (F, 80 clips, 0.38 h, conf 0.9939), `9056` (F, 86 clips, 0.38 h, conf 0.9999)
  - **Train (`train`):** `12428` (M, 26 clips, 0.10 h, conf 0.9987), `3718` (F, 14 clips, 0.05 h, conf 0.9998), `13196` (F, 11 clips, 0.05 h, conf 1.0000), `533` (F, 10 clips, 0.04 h, conf 1.0000), `4341` (M, 11 clips, 0.04 h, conf 0.9740), `4000` (F, 8 clips, 0.03 h, conf 1.0000), `7407` (M, 6 clips, 0.03 h, conf 1.0000), `6187` (F, 4 clips, 0.02 h, conf 1.0000), `3037` (M, 3 clips, 0.01 h, conf 1.0000)

### Acoustic, Lexical & Alignment Metrics

| Metric | Mean ± Std | Median | IQR (25% – 75%) | Min – Max |
| :--- | :---: | :---: | :---: | :---: |
| **Base Segment Duration (s)** | 14.67 ± 2.98 s | 14.61 s | 12.13 – 17.27 s | 5.26 – 21.91 s |
| **HF Sub-Segment Duration (s)** | 8.80 ± 4.46 s | 9.10 s | 4.64 – 12.80 s | 0.12 – 20.00 s |
| **Words per Base Segment** | 33.31 ± 8.99 words | 33.0 words | 27.0 – 40.0 words | 1 – 72 words |
| **Characters per Base Segment** | 193.89 ± 49.07 chars | 192.0 chars | 162.0 – 228.0 chars | 4 – 410 chars |
| **Speaking Rate (Words / Min)** | 136.69 ± 24.59 WPM | 136.46 WPM | 120.2 – 152.8 WPM | 40.0 – 260.0 WPM |
| **Levenshtein Alignment Similarity** | 0.9829 ± 0.021 | 1.0000 | 0.972 – 1.000 | 88.94% ≥ 0.95 (60.5% exact 1.0) |

### Top 6 Speakers Breakdown

| Speaker ID | Gender | Accent | Split | Duration (h) | Share (%) | Base Segments | Total Words | Books Read | Mean Duration |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **2961** | Female (F) | `pt_br` | Train | **83.20 h** | 52.04% | 20,359 | 656,825 | 38 | 14.71 s |
| **12249** | Female (F) | `pt_br` | Train | **17.23 h** | 10.78% | 4,087 | 136,244 | 6 | 15.18 s |
| **9351** | Male (M) | `pt_br` | Train | **16.61 h** | 10.39% | 4,172 | 161,517 | 5 | 14.33 s |
| **10107** | Male (M) | `pt_br` | Train | **13.64 h** | 8.53% | 3,370 | 102,431 | 4 | 14.57 s |
| **4367** | Male (M) | `pt_br` | Train | **11.51 h** | 7.20% | 2,938 | 95,931 | 16 | 14.11 s |
| **5677** | Male (M) | `pt_br` | Train | **8.11 h** | 5.07% | 2,034 | 75,092 | 4 | 14.35 s |
| **Other 56 Speakers** | 33 M / 23 F | 45 `pt_br` / 11 `pt_eu` | All | **9.57 h** | 5.99% | 2,270 | 78,873 | 31 | 15.18 s |

---

## Visualizations

### Dataset Overview (Speaker Share, Gender & Accent)
![BRSpeech-TTS Overview](img/brspeech_overview_pies.png)

### Portuguese Accent Classification (`pt_br` vs. `pt_eu`)
![BRSpeech-TTS Accent Analysis](img/brspeech_accent_analysis.png)

### Split & Gender Summary Table
![BRSpeech-TTS Summary Table](img/brspeech_tts_statistics.png)

### Acoustic, Lexical, Speaking Rate & Alignment Distributions
![BRSpeech-TTS Statistical Distributions](img/brspeech_distributions.png)

### Segment Duration & Word Count Distributions (Top 6 Speakers)
![Duration per Segment - Top 6 Speakers](img/brspeech_duration_per_speaker_colored_top6.png)

![Words per Sentence - Top 6 Speakers](img/brspeech_words_per_speaker_colored_top6.png)

### Top 15 Speakers & Top 15 Public-Domain Literary Works
![Speakers and Literary Works Breakdown](img/brspeech_speakers_books_analysis.png)

---

## Audio Samples

To listen to ground-truth samples from **BRSpeech-TTS** alongside samples synthesized by **YourTTS**, please visit our interactive demo page: **[https://freds0.github.io/BRSpeech-Dataset/](https://freds0.github.io/BRSpeech-Dataset/)**.

---

## Citation

If you use **BRSpeech-TTS** or **CML-TTS** in your research, please cite:

```bibtex
@InProceedings{Cmltts2023,
    title="CML-TTS: A Multilingual Dataset for Speech Synthesis in Low-Resource Languages",
    author="Oliveira, Frederico S. and Casanova, Edresson and Junior, Arnaldo Candido and Soares, Anderson S. and Galv{\~a}o Filho, Arlindo R.", 
    editor="Ek{\v{s}}tein, Kamil and P{\'a}rtl, Franti{\v{s}}ek and Konop{\'i}k, Miloslav",
    booktitle="Text, Speech, and Dialogue",
    year="2023",
    publisher="Springer Nature Switzerland",
    address="Cham",
    pages="188--199",
    isbn="978-3-031-40498-6"
}
```
