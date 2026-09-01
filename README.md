# Speech Emotion Recognition on Low-Resource Regional Language

Author: Mohammod Hamed Hasan (GitHub: @Hamed18)  

## Project Overview
This project implements experiments for Speech Emotion Recognition (SER) targeted at a low-resource regional language. The code and experiments are provided as Jupyter Notebooks that demonstrate dataset preparation, feature extraction, model training, evaluation, and analysis. The goal is to explore practical strategies to build robust emotion recognition models when labelled data is scarce.

## Dataset — source & description
Primary dataset was created and annotated in this research project:
- Proprietary low-resource regional language dataset collected by the author (Hamed18).  
  - Data description (example): recordings sampled at 16 kHz, mono, WAV format; collected from M variety of native male and female speakers across these emotion labels: neutral, happy, sad, angry, fear, surprise.
  - Metadata: per-file annotation includes speaker_id, emotion_label, recording_conditions (quiet/noisy), and transcript (if available).

If you are reading this and need access to the proprietary dataset, you must contact the author — see License / Contact below.

## Project details (approach)
- Preprocessing:
  - Resampling to a consistent sampling rate (e.g., 16 kHz)
  - Voice activity detection (VAD) and trimming silence
  - Optional denoising / filtering for noisy recordings
- Feature extraction:
  - Mel-frequency cepstral coefficients (MFCCs)
  - Log Mel spectrograms
  - Delta / Delta-Delta features
  - Optional: prosodic features (pitch, energy, duration)
- Modeling:
  - Baseline classical ML models with aggregated features: SVM, Random Forest, XGBoost
  - Deep learning approaches: 1D/2D CNN on spectrograms; LSTM/GRU on temporal features; CNN+LSTM hybrids
  - Transfer learning: fine-tuning pre-trained audio models (if available)
- Evaluation:
  - Metrics: accuracy, F1 (macro & per-class), confusion matrix
  - Cross-validation / speaker-independent splits where possible

## Experimental challenges and strategies to overcome
1. Low labelled data (data scarcity)
   - Strategy:
     - Data augmentation: time-stretching, pitch-shifting, additive noise, SpecAugment (time/frequency masking)
     - Cross-lingual transfer learning: pretrain on larger speech emotion corpora (different languages), then fine-tune on target language
     - Semi-supervised learning: pseudo-labeling and consistency training
     - Active learning: prioritize annotating most informative samples
2. Class imbalance
   - Strategy:
     - Use class weighting in loss functions
     - Oversampling under-represented classes (with care to avoid overfitting)
     - Synthetic sample generation (audio augmentation targeted at minority classes)
3. High inter-speaker variability and limited speaker diversity
   - Strategy:
     - Speaker normalization (per-speaker mean/variance normalization)
     - Use speaker-independent train/test splits and report speaker-independent evaluation
     - Domain-adaptation techniques
4. Noisy and inconsistent recording conditions
   - Strategy:
     - Denoising preprocessing, adaptive augmentation to match test-time noise
     - Robust feature choices (e.g., log-Mel spectrograms) and normalization
5. Ambiguous emotion labels and subjective annotations
   - Strategy:
     - Multi-rater agreements and soft labels (distributions instead of single labels)
     - Reject low-agreement samples during training or use as unlabeled data

## Future work
- Expand dataset: collect more speakers, more utterances, and more varied recording conditions.
- Explore self-supervised pretraining on unlabeled speech from the same language (wav2vec2 / HuBERT style).
- Implement advanced semi-supervised algorithms and active learning annotation pipelines.
- Build a lightweight real-time inference demo and evaluate latency on edge devices.
- Fine-grained emotion modeling (compound emotions, intensity estimation).
- Cross-lingual and multilingual modeling to leverage related languages.

## Reproducibility notes
- Random seeds: set and record seeds for numpy/tensor frameworks to make experiments reproducible.
- Hardware: document GPU/CPU used and run-time for major experiments.
- Data splits: include the exact split files (CSV of train/val/test) when sharing experiments (if permitted by dataset license).

## License — IMPORTANT
All Rights Reserved — No Use Without Permission.
Copyright (c) 2026 Hamed18
All Rights Reserved — No Use Without Prior Written Permission

1. Ownership
   The copyright holder (\"Copyright Holder\") of this repository and its contents is:
   Hamed18 (GitHub: https://github.com/Hamed18)
   Effective date: 2026-09-01

   The term "Materials" in this License means all repository contents including, but not limited to:
   - source code, scripts, Jupyter notebooks, models, configuration files;
   - datasets, annotations, and any derived data;
   - documentation, experiments, and analysis results;
   - any other files, media, or digital assets distributed with or referenced by this repository.

2. Permission and Prohibited Uses
   Except as expressly authorized in a separate, written license agreement signed by the Copyright Holder,
   you are strictly prohibited from doing any of the following with the Materials:

   a. Copying, reproducing, distributing, publishing, displaying, or publicly performing the Materials;
   b. Creating derivative works, modifications, adaptations, translations, compilations, or other
      works based upon the Materials;
   c. Licensing, sublicensing, selling, renting, leasing, lending, or otherwise transferring rights to
      the Materials to any third party;
   d. Using the Materials in whole or in part to train, fine-tune, evaluate, or produce machine learning
      or generative models that are redistributed or offered as a service, without prior written permission;
   e. Sharing, publishing, or otherwise making available the proprietary dataset(s) used in this repository,
      in whole or in part, to any third party;
   f. Using the Materials for any commercial purpose, including internal commercial use, without prior
      written permission.

3. Permitted Use by Permission Only
   Any use of the Materials is permitted only if and to the extent a written license or permission
   (\"Permission\") is granted by the Copyright Holder. Permission, if granted, may be subject to
   additional terms and conditions, including limitations on purpose, duration, distribution, attribution,
   confidentiality, indemnity, and financial compensation.

4. Requesting Permission
   To request Permission, provide the Copyright Holder with:
   - Your full name and affiliation;
   - Contact information (email and phone, if available);
   - A clear description of which Materials you wish to use;
   - The intended purpose and scope of use (research, educational, commercial, derivative works, etc.);
   - Whether you intend to redistribute, publish, or otherwise make the Materials (or derivatives) public;
   - Any proposed terms or agreements (e.g., collaboration, licensing fee, attribution).
   Contact:
   - GitHub: https://github.com/Hamed18
   - Email: hamedhasan.dev@gmail.com

5. Attribution and Notices
   If Permission is granted, the Copyright Holder may require:
   - Preservation of copyright and other proprietary notices in the Materials;
   - Clear attribution in derivative works or publications, as specified in the agreement.

6. Termination
   Any unauthorized use of the Materials is a material breach of this License and any granted Permission.
   The Copyright Holder may immediately terminate any Permission for breach, and may pursue available
   legal and equitable remedies, including injunctive relief and damages.

7. No Warranty
   The Materials are provided \"AS IS\" and without warranty of any kind, express or implied, including but
   not limited to warranties of merchantability, fitness for a particular purpose, non-infringement, or
   accuracy. The Copyright Holder disclaims all liability for damages arising from use or inability to use
   the Materials.

8. Limitation of Liability
   To the fullest extent permitted by applicable law, in no event shall the Copyright Holder be liable for
   any direct, indirect, incidental, special, consequential, or exemplary damages arising out of or in
   connection with access to, use of, or inability to use the Materials.

9. Governing Law
   This License and any disputes arising out of or related to it shall be governed by the laws of the
   jurisdiction where the Copyright Holder resides (unless otherwise agreed in writing), without regard to
   its conflict of laws rules. The Copyright Holder may elect to pursue enforcement in any competent forum.

10. DMCA and Enforcement
    If you believe someone has used the Materials in violation of this License, contact the Copyright Holder
    with details of the alleged infringement. The Copyright Holder may pursue removal, takedown, or other
    enforcement actions as appropriate.

11. Miscellaneous
    - This License does not grant any patent or trademark rights except as explicitly stated in a separate
      written agreement.
    - No waiver of any provision of this License shall be effective unless in writing signed by the Copyright Holder.

© 2026 Hamed18 — All Rights Reserved
