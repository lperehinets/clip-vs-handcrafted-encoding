# Data

This folder is a local download location. The data is not included in this repo and is not redistributed. If you use it, cite Huth et al. (2022) as listed in the main README.

Source: Gallant Lab Shortclips 3T fMRI dataset, [gin.g-node.org/gallantlab/shortclips](https://gin.g-node.org/gallantlab/shortclips), DOI [10.12751/g-node.vy1zjd](https://doi.org/10.12751/g-node.vy1zjd).

## How to download

Option 1: follow the data download steps in the gallantlab `voxelwise_tutorials` documentation.

Option 2: install the GIN repository with DataLad, then use `datalad get` to fetch only the files you need: the shared feature files and one subject's response file, starting with S01. Use the file layout on the GIN repository page as the reference.

```
datalad install https://gin.g-node.org/gallantlab/shortclips
```

Everything in this folder except this README is ignored by git.
