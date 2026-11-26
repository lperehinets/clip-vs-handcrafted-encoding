# CLIP vs handcrafted features as voxelwise encoding models

Status: **planning and tutorial stage.** There is no analysis code or result in this repo yet.

This is a course project with Prof. Jack Gallant (UC Berkeley, journal course in computational cognitive neuroscience), planned for about Nov 24 to Dec 8, 2026. I am learning voxelwise encoding methods through this project, and all analysis here will be my own.

## Research question

How well do image features from a contrastively trained vision-language model (CLIP) predict fMRI responses to natural movies, compared with two handcrafted feature spaces from earlier Gallant Lab work?

1. **WordNet semantic labels** (Huth et al. 2012): manually tagged object and action categories in the movies.
2. **Motion energy** (Nishimoto et al. 2011): a spatiotemporal Gabor filter bank applied to the frames.
3. **CLIP image embeddings** (Radford et al. 2021): features extracted from movie frames with a pretrained CLIP image encoder.

Secondary question: how much of the variance CLIP explains is shared with the semantic and motion energy models, and how much is unique to it?

## Data

Gallant Lab Shortclips 3T fMRI dataset (Huth et al. 2022), hosted on G-Node GIN: [gin.g-node.org/gallantlab/shortclips](https://gin.g-node.org/gallantlab/shortclips), DOI [10.12751/g-node.vy1zjd](https://doi.org/10.12751/g-node.vy1zjd).

- 5 subjects, TR = 2 s
- Training set: 3,600 TRs
- Test set: 270 TRs, repeated 10 times

The data is not redistributed in this repo. Download it from the source and cite it as listed below. See [`data/README.md`](data/README.md).

## Method plan

1. Work through the gallantlab `voxelwise_tutorials` on the Shortclips data.
2. Start with subject S01 and repeat on the other subjects if time allows.
3. Use the precomputed motion energy and WordNet feature spaces that the tutorials use.
4. Extract CLIP image embeddings from the stimulus frames and downsample them to the fMRI TRs.
5. Fit a voxelwise ridge regression model for each feature space with `himalaya`, with delayed features to model the hemodynamic response and regularization chosen by cross-validation on the training set.
6. Evaluate each model on the held-out test set, using prediction accuracy against the mean of the 10 repeats.
7. Fit banded ridge models on feature space pairs and the full set, and use variance partitioning to estimate shared and unique explained variance.
8. Plot prediction accuracy and variance partitions on cortical flatmaps with `pycortex`.

## Status

| Step | Status |
| --- | --- |
| Voxelwise tutorials | in progress: tutorial part 1 done |
| Download S01 data | not started |
| Baseline models (motion energy, WordNet) on S01 | not started |
| CLIP feature extraction | not started |
| CLIP encoding model on S01 | not started |
| Banded ridge and variance partitioning on S01 | not started |
| pycortex flatmaps | not started |
| Other subjects | not started |
| Write-up | not started |

## Repository layout

```
notebooks/   analysis notebooks (empty for now)
src/         reusable code (empty for now)
figures/     generated figures (empty for now)
results/     model outputs, not tracked if large (empty for now)
data/        local data, not tracked (see data/README.md)
```

## References

- Huth AG, Nishimoto S, Vu AT, Gallant JL (2012). A continuous semantic space describes the representation of thousands of object and action categories across the human brain. *Neuron* 76(6):1210-1224. doi:[10.1016/j.neuron.2012.10.014](https://doi.org/10.1016/j.neuron.2012.10.014)
- Huth AG, Nishimoto S, Vu AT, Dupré la Tour T, Gallant JL (2022). Gallant Lab Natural Short Clips 3T fMRI Data. G-Node GIN. doi:[10.12751/g-node.vy1zjd](https://doi.org/10.12751/g-node.vy1zjd)
- Dupré la Tour T, Visconti di Oleggio Castello M, Gallant JL (2025). The Voxelwise Encoding Model framework: a tutorial introduction to fitting encoding models to fMRI data. *Imaging Neuroscience*. doi:[10.1162/imag_a_00575](https://doi.org/10.1162/imag_a_00575)
- Dupré la Tour T, Eickenberg M, Nunez-Elizalde AO, Gallant JL (2022). Feature-space selection with banded ridge regression. *NeuroImage*. doi:[10.1016/j.neuroimage.2022.119728](https://doi.org/10.1016/j.neuroimage.2022.119728)
- Gao JS, Huth AG, Lescroart MD, Gallant JL (2015). Pycortex: an interactive surface visualizer for fMRI. *Frontiers in Neuroinformatics*. doi:[10.3389/fninf.2015.00023](https://doi.org/10.3389/fninf.2015.00023)
- Nishimoto S, Vu AT, Naselaris T, Benjamini Y, Yu B, Gallant JL (2011). Reconstructing visual experiences from brain activity evoked by natural movies. *Current Biology* 21(19):1641-1646.
- Radford A, Kim JW, Hallacy C, et al. (2021). Learning transferable visual models from natural language supervision. *ICML*. [arXiv:2103.00020](https://arxiv.org/abs/2103.00020)
