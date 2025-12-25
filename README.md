# 🗣️ Phoneme Analysis using Convolutional Neural Networks (CNN)

This project implements a **phoneme category classification system** using **pure Convolutional Neural Networks (CNNs)** and **mel-spectrogram–based audio features**.  
It focuses on **robust audio preprocessing, deterministic augmentation, leakage-safe evaluation**, and **phonetic error analysis**.

The project is designed to demonstrate **practical signal-processing knowledge** and **sound ML evaluation practices**, rather than chasing inflated accuracy numbers.

---

## 📌 Problem Statement

Phonemes are the smallest distinguishable units of sound in spoken language.  
Many phonemes exhibit **high acoustic similarity**, overlapping formants, and subtle temporal differences, making automatic classification a challenging task.

This project aims to:
- Classify phonemes into **7 broad phoneme categories**
- Analyze **confusion patterns between acoustically similar phonemes**
- Evaluate the effect of **augmentation and feature engineering**
- Build a **leakage-safe CNN pipeline** with realistic performance metrics

---

## 🎙️ Phoneme Dataset (Self-Recorded)

> **Important:**  
> The phoneme dataset used in this project was **created entirely using my own voice recordings**.

### Dataset Characteristics
- **Source:** Self-recorded speech samples
- **Speaker:** Single speaker (author)
- **Format:** WAV files
- **Sampling Rate:** 22,050 Hz
- **Organization:** Phonemes grouped into linguistic categories

Using a self-recorded dataset allows:
- Full control over pronunciation and articulation
- Clean phoneme isolation
- Transparent discussion of dataset limitations
- Ethical and licensing clarity

---

## 🧠 Phoneme Categories

The dataset is organized into **7 phoneme groups**:

| Category | Description |
|--------|-------------|
| Plosives | p, t, k, b, d, g |
| Nasals | m, n, ŋ |
| Affricates | tʃ, dʒ |
| Fricatives | f, v, θ, ð, s, z, ʃ, ʒ, h |
| Approximants | w, l, r, j |
| Diphthongs | Vowel glides |
| Monophthongs | Pure vowel sounds |

Each category contains multiple `.wav` files recorded separately.

---

## 🎵 Feature Extraction

Each audio file is converted into a **3-channel time–frequency representation**:

### Features Used
- **Mel-Spectrogram** (128 mel bands)
- **Delta (Δ)** – first-order temporal derivative
- **Delta-Delta (ΔΔ)** – second-order temporal derivative

Final input shape:
(128, Time, 3)

These features allow the CNN to learn:
- Spectral envelopes
- Temporal transitions
- Articulatory dynamics of speech sounds

---

## 🔄 Data Augmentation Strategy

To improve robustness and generalization, **deterministic audio augmentation** is applied **only to the training set**.

### Augmentation Techniques
- Pitch shifting (±2 semitones)
- Time stretching (0.9×, 1.1×)
- Original (no augmentation)

⚠️ **Data Leakage Prevention**
- Train–test split is performed **before augmentation**
- Test data is **never augmented**
- Normalization statistics are **fit on training data only**

This ensures **realistic and defensible evaluation**.

---

## 🧪 Dataset Preparation Pipeline

- Augmented samples per phoneme class: **100**
- Variable-length audio padded to a common time dimension
- Feature normalization using `StandardScaler`
- Stratified train–test split

This pipeline prioritizes **stability, reproducibility, and correctness**.

---

## 🤖 Model Architecture (Pure CNN)

The classifier uses a **pure CNN architecture** (no RNNs, no attention):

Input (128 × T × 3)

↓

Conv2D (32 filters) + BatchNorm + ReLU + MaxPool

↓

Conv2D (64 filters) + BatchNorm + ReLU + MaxPool

↓

Conv2D (96 filters) + BatchNorm + ReLU

↓

Global Average Pooling

↓

Dense (64) + Dropout

↓

Dense (7) + Softmax


### Design Rationale
- CNNs capture local spectro-temporal patterns effectively
- Global Average Pooling reduces overfitting
- Moderate depth matches dataset scale
- Batch normalization stabilizes training

---

## 📊 Evaluation Metrics

The model is evaluated using:
- Accuracy
- Precision, Recall, F1-Score
- Confusion Matrix
- Training vs Validation curves

### Typical Performance
- **Leakage-safe validation accuracy:** ~65–75%
- Higher scores achievable with leakage, but not reported
- Strong diagonal dominance in confusion matrices

---

## 🔍 Phoneme Confusion Analysis

Observed confusions align with phonetic theory:

- **Affricates ↔ Fricatives** (shared noise components)
- **Monophthongs ↔ Diphthongs** (formant transitions)
- **Approximants ↔ Vowels** (similar spectral envelopes)

This indicates the model is learning **meaningful acoustic representations**, not memorizing data.

---

## 📈 Visualizations Included

- Mel-spectrogram visualizations
- Training vs validation accuracy curves
- Training vs validation loss curves
- Confusion matrices (raw and normalized)
- Sample predictions on original phoneme files

---

## 🧪 Experiments Conducted

- Feature ablation (Mel vs Mel+Δ vs Mel+Δ+ΔΔ)
- Model depth vs generalization
- Augmented vs clean evaluation
- Leakage-safe vs leakage-prone pipelines

---

## 🛠️ Technologies Used

- Python
- Librosa
- TensorFlow / Keras
- NumPy
- scikit-learn
- Matplotlib / Seaborn
- Jupyter Notebook

---

## 📌 Key Takeaways

- CNNs can effectively model phoneme-level acoustics
- Proper evaluation matters more than high accuracy
- Feature engineering significantly improves stability
- Confusion analysis provides linguistic insight
- Self-recorded datasets are viable with correct methodology

---

## 📄 License

This project is released under the **MIT License**.

---

## 📬 Contact

For questions, feedback, or collaboration ideas, please open an issue on GitHub.

