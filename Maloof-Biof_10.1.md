# Update of Maloof-Biof_10

## Building on top of Maloof-Biofv10

### Updating installed packages

```
sudo apt-get update
sudo apt-get upgrade
```

### R packages and Kallisto added

### Installing Rstan

```
sudo -s
cd /etc/skel
mkdir .R
cd .R
nano Makevars
# Paste in "nCXXFLAGS=-O3 -mtune=native -march=native -Wno-unused-variable -Wno-unused-function"
R
## Inside R
install.packages("rstan", repos = "https://cloud.r-project.org/", dependencies=TRUE)
fx <- inline::cxxfunction( signature(x = "integer", y = "numeric" ) , '
    return ScalarReal( INTEGER(x)[0] * REAL(y)[0] ) ;
' )
fx( 2L, 5 ) # should be 10, was 10 when ran
```

### Installing Rethinking

```
install.packages(c("coda","mvtnorm","devtools","loo"))
library(devtools)
devtools::install_github("rmcelreath/rethinking")
```

### Installing brms

```
install.packages("brms")
```

### Installing rstanarm

```
install.packages("rstanarm")
```
