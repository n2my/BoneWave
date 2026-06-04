# Toward Flexible Phone Call Quality Enhancement via Contactless Bone-Conduction Sensing with mmWave

### 📥 Code Download

The BoneWave code package can be downloaded here:  
[Code Download Link]

### 🎬 Demo Video

A demonstration of BoneWave is available at:  
[Demo Video Link]

This repository contains the core implementation of **BoneWave**, a mmWave-based contactless bone-conduction sensing framework for flexible phone call quality enhancement. BoneWave captures speech-induced bone-conducted vibrations around the ear using mmWave radar and fuses them with noisy audio signals to enhance speech quality under challenging acoustic conditions.

---

## 📦 Environment

The experiments were conducted under the following environment:

* Python 3.10.16
* PyTorch 2.1.1+cu121

---

# BoneWave Dataset: Paired mmWave-Audio Speech Dataset

## 📘 Overview

### 📥 Download Link

The dataset includes:

* **Processed HDF5 files (~6.54 GB)**
* **Raw mmWave + audio data (~87.2 GB)**

The dataset can be downloaded here:  
[Dataset Download Link]

The BoneWave dataset is a paired **mmWave-audio speech dataset** designed for phone call quality enhancement. The speech content is selected from the **TIMIT corpus** [1]. Each recording contains synchronized audio and raw mmWave intermediate-frequency (IF) signals, enabling research on mmWave-based bone-conduction sensing for speech enhancement, and mmWave-audio multimodal learning.

Each raw sample has a duration of **25 seconds** and includes two synchronized modalities:

* **Audio data**: speech waveform
* **mmWave data**: raw mmWave IF signal

---

## 📡 Data Modalities

Two data formats are provided:

1. **Processed HDF5 data**
2. **Raw audio + mmWave IF data**

---

## 1. Processed HDF5 Format

Each sample is stored as a group in an HDF5 file with the naming scheme:

```text
corpusID_subjectID_repeatIndex
```

Example:

```text
TIMIT1_person1_time0
```

Meaning:

* `TIMIT1` — corpus subset ID
* `person1` — subject ID
* `time0` — repetition index

### Keys in each group

Each HDF5 group contains the following keys:

* **audio_spectrogram** — the spectrogram of the speech audio signal
* **frame_labels** — mmWave-based speech segment extraction results represented as a frame-level sequence, where `1` indicates speech presence and `0` indicates silence
* **mmwave_spectrogram** — the raw mmWave spectrogram, which contains both bone-conduction vibration components and radar noise floors
* **refinend_mmWave_spectrogram** — the refined mmWave spectrogram, where bone-conduction vibration frequencies are separated to obtain a cleaner mmWave representation

All modalities and labels are time-aligned within each sample.

---

## 2. Raw Data Format

Raw audio and mmWave IF signals are stored in a hierarchical directory structure.

Example audio path:

```text
BoneWave/TIMIT/audio/TIMIT1/person_1/0/audio.wav
```

Example mmWave path:

```text
BoneWave/TIMIT/mmwave/TIMIT1/person_1/0/adc_data_Raw_0.bin
```

Meaning:

* `audio` / `mmwave` — modality
* `TIMIT1` — corpus subset ID
* `person_1` — subject ID
* `0` — repetition index
* `audio.wav` — recorded speech waveform
* `adc_data_Raw_0.bin` — raw mmWave IF signal

The audio and mmWave folders follow the same hierarchical structure. Audio and mmWave samples are paired by their relative directory paths.

For example:

```text
TIMIT/audio/TIMIT1/person_1/0/audio.wav
TIMIT/mmwave/TIMIT1/person_1/0/adc_data_Raw_0.bin
```

represent the paired audio and mmWave data from the same recording session.

---

## 📝 Summary Table

| Component       | Description                                      |
| --------------- | ------------------------------------------------ |
| Participants    | 54 volunteers (27 male and 27 female             |
| Speech corpus   | DARPA TIMIT acoustic-phonetic speech corpus      |
| Modalities      | Audio + raw mmWave IF signals                    |
| Sample length   | 25 seconds per raw sample                        |
| Formats         | HDF5 processed data, raw audio & mmWave data     |
| Processed size  | ~6.54 GB                                         |
| Raw data size   | ~87.2 GB                                         |
| Synchronization | Time-aligned audio and mmWave recordings         |

---

## Reference

[1] J. S. Garofolo et al., “DARPA TIMIT acoustic-phonetic speech database,” *National Institute of Standards and Technology (NIST)*, vol. 15, pp. 29–50, 1988.
