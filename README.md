# SSR
[Under review] Official repository for "Semantic-anchored Cross-modal Reconstruction for Generalizable Brain Decoding"

Decoding visual information from brain activity is a fundamental yet challenging problem in cognitive neuroscience and artificial intelligence, due to the intrinsic noise and substantial intersubject variability of brain signals. Existing retrieval-based brain decoding methods rely on image augmentations of visual stimuli to simulate cognitive priors in human brain visual information processing and capture cross-modal association by maximizing feature similarity between visual stimuli and brain responses. Despite some progress, these practices raise two issues. First, pixel-level perturbations distort the discriminative semantics of visual stimuli and weaken inter-stimulus distinction, leading to learned brain representations with insufficient discriminability. Second, similarity-based contrastive learning is inherently vulnerable to learning spurious correlations from the high-variability brain signals, compromising the robustness of cross-modal correspondence and limiting model generalization. To address these issues, we propose a Semantic-anchored framework for learning brain representations with croSs-modal Reconstruction (SSR). Specifically, to obtain visual stimulus features that are both semantically compact and aligned with cognitive priors, we first construct a feature triplet consisting of a brain, an original image, and an augmented image, and then perform contrastive learning based on the triplet with the original image as semantic anchor, enhancing the discriminative power of learned brain representations. Furthermore, inspired by the brain's predictive coding mechanism, we design a cross-modal masked reconstruction module. Aiming beyond direct similarity maximization, the module learns to reconstruct masked features via cross-modal context, which requires inferring inter-modal dependencies and thus fosters robust, generalizable associations resilient to noise. Extensive experiments demonstrate that our framework significantly enhances both the discrimination and generalizability of brain representations, achieving state-of-the-art performance on two popular brain decoding benchmarks.

# Overreview
![Model Overview](Method.png)  
This paper's framework first simulates cognitive priors by enhancing visual stimuli with augmentations, then uses original image features as semantic anchors to perform triple contrastive learning, acquiring semantic-enhanced visual features with cognitive priors for learning discriminative brain representations. Subsequently, robust cross-modal associations resilient to brain signal noise are established through cross-modal masked reconstruction, optimizing zero-shot decoding. During the inference phase, based on feature similarity, the original visual stimuli are retrieved by directly decoding unseen brain signals.

# Experiments

## 200-way zero-shot retrieval accuracy (%) on THINGS-EEG (Top-1 / Top-5)

### Intra-Subject: train and test on one subject

| Method | Venue | Accuracy | S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8 | S9 | S10 | Avg |
|--------|-------|----------|----|----|----|----|----|----|----|----|-----|-----|-----|
| BraVL | TPAMI'23 | Top-1 | 6.1 | 4.9 | 5.6 | 5.0 | 4.0 | 6.0 | 6.5 | 8.8 | 4.3 | 7.0 | 5.8 |
| BraVL | TPAMI'23 | Top-5 | 17.9 | 14.9 | 17.4 | 15.1 | 13.4 | 18.2 | 20.4 | 23.7 | 14.0 | 19.7 | 17.5 |
| NICE | ICLR'24 | Top-1 | 13.2 | 13.5 | 14.5 | 20.6 | 10.1 | 16.5 | 17.0 | 22.9 | 15.4 | 17.4 | 16.1 |
| NICE | ICLR'24 | Top-5 | 39.5 | 40.3 | 42.7 | 52.7 | 31.5 | 44.0 | 42.1 | 56.1 | 41.6 | 45.8 | 43.6 |
| ATM | NeurIPS'24 | Top-1 | 25.6 | 22.0 | 25.0 | 31.4 | 12.9 | 21.3 | 30.5 | 38.8 | 34.4 | 29.1 | 27.1 |
| ATM | NeurIPS'24 | Top-5 | 60.4 | 54.5 | 62.4 | 60.9 | 43.0 | 51.1 | 61.5 | 72.0 | 51.5 | 63.5 | 58.1 |
| CogCapturer | AAAI'25 | Top-1 | 27.2 | 28.7 | 37.2 | 37.7 | 21.8 | 31.6 | 32.8 | 47.6 | 33.4 | 35.1 | 33.3 |
| CogCapturer | AAAI'25 | Top-5 | 59.5 | 57.0 | 66.1 | 63.2 | 47.8 | 58.1 | 59.6 | 73.5 | 57.7 | 63.6 | 60.6 |
| Neural-MCRL | ArXiv'24 | Top-1 | 27.5 | 28.5 | 37.0 | 35.0 | 22.5 | 31.5 | 31.5 | 42.0 | 30.5 | 37.5 | 32.4 |
| Neural-MCRL | ArXiv'24 | Top-5 | 64.0 | 61.5 | 69.0 | 66.0 | 51.5 | 61.0 | 62.5 | 74.5 | 59.5 | 71.0 | 64.1 |
| VE-SDN | ArXiv'24 | Top-1 | 32.6 | 34.4 | 38.7 | 39.8 | 29.4 | 34.5 | 34.5 | 49.3 | 39.0 | 39.8 | 37.2 |
| VE-SDN | ArXiv'24 | Top-5 | 63.7 | 69.9 | 73.5 | 72.0 | 58.6 | 68.8 | 68.3 | 79.8 | 69.6 | 75.3 | 70.0 |
| UBP | CVPR'25 | Top-1 | 41.2 | 51.2 | 51.2 | 51.1 | 42.2 | 57.5 | 49.0 | 58.6 | 45.1 | 61.5 | 50.9 |
| UBP | CVPR'25 | Top-5 | 70.5 | 80.9 | 82.0 | 76.9 | 72.8 | 83.5 | 79.9 | 85.8 | 76.2 | 88.2 | 79.7 |
| NeuroBridge | AAAI'26 | Top-1 | 50.0 | 63.2 | 61.6 | 61.4 | 54.8 | 69.7 | 62.7 | 71.2 | 64.0 | 73.6 | 63.2 |
| NeuroBridge | AAAI'26 | Top-5 | 77.6 | 90.6 | 91.1 | 90.0 | 85.0 | 92.9 | 88.8 | 95.1 | 91.0 | 97.1 | 89.9 |
| **Ours** | **-** | **Top-1** | **60.1** | **67.4** | **62.8** | **63.6** | **60.1** | **73.7** | **66.1** | **73.1** | **65.4** | **76.7** | **66.9** |
| **Ours** | **-** | **Top-5** | **88.9** | **94.2** | **93.2** | **92.4** | **87.9** | **94.6** | **91.1** | **96.1** | **92.8** | **98.0** | **92.9** |

### Inter-Subject: leave-one-subject-out test

| Method | Venue | Accuracy | S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8 | S9 | S10 | Avg |
|--------|-------|----------|----|----|----|----|----|----|----|----|-----|-----|-----|
| BraVL | TPAMI'23 | Top-1 | 2.3 | 1.5 | 1.4 | 1.7 | 1.5 | 1.8 | 2.1 | 2.2 | 1.6 | 2.3 | 1.8 |
| BraVL | TPAMI'23 | Top-5 | 8.0 | 6.3 | 5.9 | 6.7 | 5.6 | 7.2 | 8.1 | 7.6 | 6.4 | 8.5 | 7.0 |
| NICE | ICLR'24 | Top-1 | 7.6 | 5.9 | 6.0 | 6.3 | 4.4 | 5.6 | 5.6 | 6.3 | 5.7 | 8.4 | 6.2 |
| NICE | ICLR'24 | Top-5 | 22.8 | 20.5 | 22.3 | 20.7 | 18.3 | 22.2 | 19.7 | 22.0 | 17.6 | 28.3 | 21.4 |
| ATM | NeurIPS'24 | Top-1 | 10.5 | 7.1 | 11.9 | 14.7 | 7.0 | 11.1 | 16.1 | 15.0 | 4.9 | 20.5 | 11.9 |
| ATM | NeurIPS'24 | Top-5 | 26.8 | 24.8 | 33.8 | 39.4 | 23.9 | 35.8 | 43.5 | 40.3 | 22.7 | 46.5 | 33.8 |
| UBP | CVPR'25 | Top-1 | 11.5 | 15.5 | 9.8 | 13.0 | 8.8 | 11.7 | 10.2 | 12.2 | 15.5 | 16.0 | 12.4 |
| UBP | CVPR'25 | Top-5 | 29.7 | 40.0 | 27.0 | 32.3 | 33.8 | 31.0 | 23.8 | 32.2 | 40.5 | 43.5 | 33.4 |
| Neural-MCRL | ArXiv'24 | Top-1 | 13.0 | 12.0 | 14.5 | 12.5 | 11.5 | 13.5 | 14.0 | 18.5 | 13.5 | 17.0 | 14.0 |
| Neural-MCRL | ArXiv'24 | Top-5 | 31.5 | 30.5 | 35.5 | 35.5 | 29.0 | 35.5 | 36.0 | 38.5 | 32.5 | 39.0 | 34.3 |
| NeuroBridge | AAAI'26 | Top-1 | 23.2 | 21.2 | 13.2 | 17.0 | 14.5 | 25.0 | 15.3 | 20.1 | 13.7 | 27.2 | 19.0 |
| NeuroBridge | AAAI'26 | Top-5 | 52.4 | 49.3 | 36.5 | 45.3 | 37.7 | 55.0 | 45.1 | 44.9 | 36.5 | 56.3 | 45.9 |
| **Ours** | **-** | **Top-1** | **23.4** | **24.9** | **15.8** | **21.5** | **19.9** | **27.6** | **16.5** | **21.2** | **21.1** | **34.5** | **22.6** |
| **Ours** | **-** | **Top-5** | **56.8** | **56.5** | **41.8** | **50.7** | **49.1** | **57.4** | **49.3** | **51.2** | **50.5** | **66.4** | **53.0** |

## Accuracy (%) of 200-way zero-shot retrieval on THINGS-MEG: Top-1 and Top-5

### Intra-Subject: train and test on one subject

| Method | Venue | Accuracy | S1 | S2 | S3 | S4 | Avg |
|--------|-------|----------|----|----|----|----|-----|
| NICE | ICLR'24 | Top-1 | 9.6 | 18.5 | 14.2 | 9.0 | 12.8 |
| NICE | ICLR'24 | Top-5 | 27.8 | 47.8 | 41.6 | 26.6 | 36.0 |
| UBP | CVPR'25 | Top-1 | 15.0 | 46.0 | 27.3 | 18.5 | 26.7 |
| UBP | CVPR'25 | Top-5 | 38.0 | 80.5 | 59.0 | 43.5 | 55.2 |
| NeuroBridge | AAAI'26 | Top-1 | 16.5 | 53.7 | 40.4 | 18.1 | 32.2 |
| NeuroBridge | AAAI'26 | Top-5 | 41.6 | 85.3 | 73.2 | 43.1 | 60.8 |
| **Ours** | **-** | **Top-1** | **19.3** | **66.6** | **50.8** | **28.5** | **41.3** |
| **Ours** | **-** | **Top-5** | **50.6** | **93.5** | **82.6** | **57.9** | **71.1** |

### Inter-Subject: leave one subject out for test

| Method | Venue | Accuracy | S1 | S2 | S3 | S4 | Avg |
|--------|-------|----------|----|----|----|----|-----|
| UBP | CVPR'25 | Top-1 | 2.0 | 1.5 | 2.7 | 2.5 | 2.2 |
| UBP | CVPR'25 | Top-5 | 5.7 | 17.2 | 10.5 | 8.0 | 10.4 |
| NeuroBridge | AAAI'26 | Top-1 | 4.3 | 3.6 | 3.0 | 2.5 | 3.4 |
| NeuroBridge | AAAI'26 | Top-5 | 13.1 | 15.6 | 11.2 | 11.3 | 12.8 |
| **Ours** | **-** | **Top-1** | **5.5** | **6.0** | **4.6** | **3.6** | **4.9** |
| **Ours** | **-** | **Top-5** | **14.2** | **19.4** | **15.4** | **13.1** | **15.5** |
