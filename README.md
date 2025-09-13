## Gaussian Mixture Quantile Normalization (GMQN)

GMQN 2.0 is a reference based method that removes unwanted technical variations at signal intensity level between samples for 450K, 850K and 935K DNA methylation array. It can also easily combined with Subset-quantile Within Array Normalization(SWAN) or Beta-Mixture Quantile (BMIQ) Normalisation to remove probe design bias.

## Installation

You can install GMQN R package by following steps. We will submit the R package to Bioconductor soon.

```{r}
devtools::install_github('YangFei1018/gmqn2')
library(gmqn2)
```
## Dependencies
GMQN 2.0 depends on the following packages, all available in CRAN.

* mclust
* RPMM
* minfi

## Demos

### when you have raw(.idat) data

```{r}
# I recommend using minfi to read the raw data and do preprocess.
# But other packages can also be used. 
library(minfi)
RGSet = read.metharray.exp("idat/")
MSet <- preprocessRaw(RGSet) # Other preprocess methods can also be used.
m = data.frame(getMeth(MSet))
um = data.frame(getUnmeth(MSet))

library(gmqn)
# You can skip this line if you want to use default reference.
ref = set_reference(m, um)
beta.GMQN.swan = gmqn_swan_parallel(m, um, ncpu = 45)
beta.GMQN.bmiq = gmqn_bmiq_parallel(m, um, ncpu = 45)

```






