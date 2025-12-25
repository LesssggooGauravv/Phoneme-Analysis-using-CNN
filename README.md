# Phoneme Classification using CNN

This project performs phoneme-category classification using
mel-spectrogram based features and a pure CNN architecture.

## Highlights
- Mel + Δ + ΔΔ feature extraction
- Deterministic augmentation
- Leakage-safe train/test split
- CNN with global average pooling
- Detailed confusion analysis

## Classes
- Affricates
- Approximants
- Diphthongs
- Fricatives
- Monophthongs
- Nasals
- Plosives

## Results
- Test Accuracy: ~90% (with augmentation)
- Leakage-safe accuracy: ~60–70%
- Strong diagonal dominance in confusion matrix

## Tech Stack
- Python
- Librosa
- TensorFlow / Keras
- NumPy, Matplotlib, Seaborn
