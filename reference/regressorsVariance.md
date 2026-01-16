# Create regressors for a log-variance model

The function creates the regressors of a log-variance model, e.g. in a
[`arx`](http://moritzschwarz.org/gets/reference/arx.md) model. The
returned value is a `matrix` with the regressors and, by default, the
regressand in the first column. By default, observations (rows) with
missing values are removed in the beginning and the end with
[`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html), and the returned
matrix is a [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

## Usage

``` r
regressorsVariance(e, vc = TRUE, arch = NULL, harch = NULL, asym = NULL,
  asymind = NULL, log.ewma = NULL, vxreg = NULL, prefix = "v", zero.adj = NULL,
  vc.adj = TRUE, return.regressand = TRUE, return.as.zoo = TRUE, na.trim = TRUE,
  na.omit = FALSE)
```

## Arguments

- e:

  numeric vector, time-series or
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

- vc:

  logical. `TRUE` includes an intercept in the log-variance
  specification, whereas `FALSE` (default) does not. If the log-variance
  specification contains any other item but the log-variance intercept,
  then vc is set to `TRUE`.

- arch:

  either `NULL` (default) or an integer vector, say, `c(1,3)` or `2:5`.
  The log-ARCH lags to include in the log-variance specification.

- harch:

  either `NULL` (default) or an integer vector, say, `c(5,20)`. The log
  of heterogenous ARCH-terms as proposed by Muller et al. (1997).

- asym:

  either `NULL` (default) or an integer vector, say, `c(1)` or `1:3`.
  The asymmetry (i.e. 'leverage') terms to include in the log-variance
  specification.

- asymind:

  either `NULL` (default) or an integer vector, say, `c(1)` or `1:3`.
  The indicator ('binary') asymmetry terms to include in the
  log-variance specification.

- log.ewma:

  either `NULL` (default) or a vector of the lengths of the volatility
  proxies, see
  [`leqwma`](http://moritzschwarz.org/gets/reference/eqwma.md). The log
  of heterogenous volatility proxies similar to those of Corsi (2009).

- vxreg:

  either `NULL` (default) or a numeric vector or matrix, say, a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object, of conditioning
  variables. If both `y` and `mxreg` are
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) objects, then their
  samples are chosen to match.

- prefix:

  a `character` used as prefix in the labelling of the variables in
  `vxreg` and of the intercept.

- zero.adj:

  `NULL` (default) or a strictly positive `numeric` scalar. If `NULL`,
  the zeros in the squared e's are replaced by the 10 percent quantile
  of the non-zero squared e's. If `zero.adj` is a strictly positive
  `numeric` scalar, then this value is used to replace the zeros of the
  squared e's.

- vc.adj:

  deprecated and ignored.

- return.regressand:

  `logical`. `TRUE` (default) includes the regressand as column one in
  the returned matrix.

- return.as.zoo:

  `logical`. `TRUE` (default) returns the matrix as a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

- na.trim:

  `logical`. `TRUE` (default) removes observations with `NA`-values in
  the beginning and the end with
  [`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html).

- na.omit:

  `logical`. `FALSE` (default) means `NA`-observations that are not in
  the beginning or at the end are kept (i.e. not omitted). `TRUE`
  removes with [`na.omit`](https://rdrr.io/r/stats/na.fail.html).

## Value

A `matrix`, by default of class
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html), with the regressand as
column one (the default).

## References

Corsi, Fulvio (2009): 'A Simple Approximate Long-Memory Model of
Realized Volatility', Journal of Financial Econometrics 7, pp. 174-196

Muller, Ulrich A., Dacorogna, Michel M., Dave, Rakhal D., Olsen, Richard
B, Pictet, Olivier, Weizsaker, Jacob E. (1997): 'Volatilities of
different time resolutions - Analyzing the dynamics of market
components'. Journal of Empirical Finance 4, pp. 213-239

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44. DOI: https://www.jstatsoft.org/article/view/v086i03

Sucarrat, Genaro and Escribano, Alvaro (2012): 'Automated Financial
Model Selection: General-to-Specific Modelling of the Mean and
Volatility Specifications', Oxford Bulletin of Economics and Statistics
74, Issue 5 (October), pp. 716-735

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`regressorsMean`](http://moritzschwarz.org/gets/reference/regressorsMean.md),
[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html),
[`leqwma`](http://moritzschwarz.org/gets/reference/eqwma.md),
[`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html) and
[`na.omit`](https://rdrr.io/r/stats/na.fail.html).

## Examples

``` r
##generate some data:
eps <- rnorm(10) #error term
x <- matrix(rnorm(10*5), 10, 5) #regressors

##create regressors (examples):
regressorsVariance(eps, vxreg=x)
#>         loge2 vconst      vxreg1        vxreg2      vxreg3      vxreg4
#> 1   0.8605019      1 -0.52069415 -0.7074116272 -0.41714329  1.26706961
#> 2  -0.6750271      1  0.48559693  1.1835345128 -0.53009412 -0.21457269
#> 3  -1.6646218      1 -0.60161402 -0.4284557029  0.72215363  0.73344466
#> 4   0.8268130      1 -0.58727414 -1.9855426992  2.55981987 -0.05893913
#> 5  -4.3510169      1  0.77890156 -1.0098119005 -0.55778408  1.13043653
#> 6  -0.6897965      1  1.85465879 -0.1281453368 -0.08235274  0.76247928
#> 7  -0.8045264      1 -0.36611661 -1.4664402136 -1.90744533 -0.35578297
#> 8  -2.1400139      1  0.50644120  0.5132418443  0.48435318  1.38183780
#> 9   0.4730325      1 -0.57849893  1.2300639371 -1.01534253  0.53277462
#> 10 -1.2478511      1 -0.01510772  0.0003588142  0.05616500 -0.32518627
#>         vxreg5
#> 1  -1.32926819
#> 2  -0.52779093
#> 3   1.49037243
#> 4  -0.02900963
#> 5   0.01237915
#> 6   1.73204559
#> 7  -0.13704585
#> 8  -1.47720991
#> 9  -1.61247517
#> 10  0.91271496
regressorsVariance(eps, vxreg=x, return.regressand=FALSE)
#>    vconst      vxreg1        vxreg2      vxreg3      vxreg4      vxreg5
#> 1       1 -0.52069415 -0.7074116272 -0.41714329  1.26706961 -1.32926819
#> 2       1  0.48559693  1.1835345128 -0.53009412 -0.21457269 -0.52779093
#> 3       1 -0.60161402 -0.4284557029  0.72215363  0.73344466  1.49037243
#> 4       1 -0.58727414 -1.9855426992  2.55981987 -0.05893913 -0.02900963
#> 5       1  0.77890156 -1.0098119005 -0.55778408  1.13043653  0.01237915
#> 6       1  1.85465879 -0.1281453368 -0.08235274  0.76247928  1.73204559
#> 7       1 -0.36611661 -1.4664402136 -1.90744533 -0.35578297 -0.13704585
#> 8       1  0.50644120  0.5132418443  0.48435318  1.38183780 -1.47720991
#> 9       1 -0.57849893  1.2300639371 -1.01534253  0.53277462 -1.61247517
#> 10      1 -0.01510772  0.0003588142  0.05616500 -0.32518627  0.91271496
regressorsVariance(eps, arch=1:3, vxreg=x)
#>         loge2 vconst      arch1      arch2      arch3      vxreg1        vxreg2
#> 4   0.8268130      1 -1.6646218 -0.6750271  0.8605019 -0.58727414 -1.9855426992
#> 5  -4.3510169      1  0.8268130 -1.6646218 -0.6750271  0.77890156 -1.0098119005
#> 6  -0.6897965      1 -4.3510169  0.8268130 -1.6646218  1.85465879 -0.1281453368
#> 7  -0.8045264      1 -0.6897965 -4.3510169  0.8268130 -0.36611661 -1.4664402136
#> 8  -2.1400139      1 -0.8045264 -0.6897965 -4.3510169  0.50644120  0.5132418443
#> 9   0.4730325      1 -2.1400139 -0.8045264 -0.6897965 -0.57849893  1.2300639371
#> 10 -1.2478511      1  0.4730325 -2.1400139 -0.8045264 -0.01510772  0.0003588142
#>         vxreg3      vxreg4      vxreg5
#> 4   2.55981987 -0.05893913 -0.02900963
#> 5  -0.55778408  1.13043653  0.01237915
#> 6  -0.08235274  0.76247928  1.73204559
#> 7  -1.90744533 -0.35578297 -0.13704585
#> 8   0.48435318  1.38183780 -1.47720991
#> 9  -1.01534253  0.53277462 -1.61247517
#> 10  0.05616500 -0.32518627  0.91271496
regressorsVariance(eps, arch=1:2, asym=1, vxreg=x)
#>         loge2 vconst      arch1      arch2      asym1      vxreg1        vxreg2
#> 3  -1.6646218      1 -0.6750271  0.8605019  0.0000000 -0.60161402 -0.4284557029
#> 4   0.8268130      1 -1.6646218 -0.6750271 -1.6646218 -0.58727414 -1.9855426992
#> 5  -4.3510169      1  0.8268130 -1.6646218  0.0000000  0.77890156 -1.0098119005
#> 6  -0.6897965      1 -4.3510169  0.8268130 -4.3510169  1.85465879 -0.1281453368
#> 7  -0.8045264      1 -0.6897965 -4.3510169 -0.6897965 -0.36611661 -1.4664402136
#> 8  -2.1400139      1 -0.8045264 -0.6897965 -0.8045264  0.50644120  0.5132418443
#> 9   0.4730325      1 -2.1400139 -0.8045264  0.0000000 -0.57849893  1.2300639371
#> 10 -1.2478511      1  0.4730325 -2.1400139  0.0000000 -0.01510772  0.0003588142
#>         vxreg3      vxreg4      vxreg5
#> 3   0.72215363  0.73344466  1.49037243
#> 4   2.55981987 -0.05893913 -0.02900963
#> 5  -0.55778408  1.13043653  0.01237915
#> 6  -0.08235274  0.76247928  1.73204559
#> 7  -1.90744533 -0.35578297 -0.13704585
#> 8   0.48435318  1.38183780 -1.47720991
#> 9  -1.01534253  0.53277462 -1.61247517
#> 10  0.05616500 -0.32518627  0.91271496
regressorsVariance(eps, arch=1:2, asym=1, log.ewma=5)
#>         loge2 vconst      arch1      arch2      asym1 logEqWMA(5)
#> 6  -0.6897965      1 -4.3510169  0.8268130 -4.3510169  0.06983704
#> 7  -0.8045264      1 -0.6897965 -4.3510169 -0.6897965 -0.35696118
#> 8  -2.1400139      1 -0.8045264 -0.6897965 -0.8045264 -0.37479370
#> 9   0.4730325      1 -2.1400139 -0.8045264  0.0000000 -0.39584758
#> 10 -1.2478511      1  0.4730325 -2.1400139  0.0000000 -0.62198875

##example where eps and x are time-series:
eps <- ts(eps, frequency=4, end=c(2018,4))
x <- ts(x, frequency=4, end=c(2018,4))
regressorsVariance(eps, vxreg=x)
#>              loge2 vconst    Series 1      Series 2    Series 3    Series 4
#> 2016 Q3  0.8605019      1 -0.52069415 -0.7074116272 -0.41714329  1.26706961
#> 2016 Q4 -0.6750271      1  0.48559693  1.1835345128 -0.53009412 -0.21457269
#> 2017 Q1 -1.6646218      1 -0.60161402 -0.4284557029  0.72215363  0.73344466
#> 2017 Q2  0.8268130      1 -0.58727414 -1.9855426992  2.55981987 -0.05893913
#> 2017 Q3 -4.3510169      1  0.77890156 -1.0098119005 -0.55778408  1.13043653
#> 2017 Q4 -0.6897965      1  1.85465879 -0.1281453368 -0.08235274  0.76247928
#> 2018 Q1 -0.8045264      1 -0.36611661 -1.4664402136 -1.90744533 -0.35578297
#> 2018 Q2 -2.1400139      1  0.50644120  0.5132418443  0.48435318  1.38183780
#> 2018 Q3  0.4730325      1 -0.57849893  1.2300639371 -1.01534253  0.53277462
#> 2018 Q4 -1.2478511      1 -0.01510772  0.0003588142  0.05616500 -0.32518627
#>            Series 5
#> 2016 Q3 -1.32926819
#> 2016 Q4 -0.52779093
#> 2017 Q1  1.49037243
#> 2017 Q2 -0.02900963
#> 2017 Q3  0.01237915
#> 2017 Q4  1.73204559
#> 2018 Q1 -0.13704585
#> 2018 Q2 -1.47720991
#> 2018 Q3 -1.61247517
#> 2018 Q4  0.91271496
regressorsVariance(eps, arch=1:3, vxreg=x)
#>              loge2 vconst      arch1      arch2      arch3    Series 1
#> 2017 Q2  0.8268130      1 -1.6646218 -0.6750271  0.8605019 -0.58727414
#> 2017 Q3 -4.3510169      1  0.8268130 -1.6646218 -0.6750271  0.77890156
#> 2017 Q4 -0.6897965      1 -4.3510169  0.8268130 -1.6646218  1.85465879
#> 2018 Q1 -0.8045264      1 -0.6897965 -4.3510169  0.8268130 -0.36611661
#> 2018 Q2 -2.1400139      1 -0.8045264 -0.6897965 -4.3510169  0.50644120
#> 2018 Q3  0.4730325      1 -2.1400139 -0.8045264 -0.6897965 -0.57849893
#> 2018 Q4 -1.2478511      1  0.4730325 -2.1400139 -0.8045264 -0.01510772
#>              Series 2    Series 3    Series 4    Series 5
#> 2017 Q2 -1.9855426992  2.55981987 -0.05893913 -0.02900963
#> 2017 Q3 -1.0098119005 -0.55778408  1.13043653  0.01237915
#> 2017 Q4 -0.1281453368 -0.08235274  0.76247928  1.73204559
#> 2018 Q1 -1.4664402136 -1.90744533 -0.35578297 -0.13704585
#> 2018 Q2  0.5132418443  0.48435318  1.38183780 -1.47720991
#> 2018 Q3  1.2300639371 -1.01534253  0.53277462 -1.61247517
#> 2018 Q4  0.0003588142  0.05616500 -0.32518627  0.91271496
regressorsVariance(eps, arch=1:2, asym=1, vxreg=x)
#>              loge2 vconst      arch1      arch2      asym1    Series 1
#> 2017 Q1 -1.6646218      1 -0.6750271  0.8605019  0.0000000 -0.60161402
#> 2017 Q2  0.8268130      1 -1.6646218 -0.6750271 -1.6646218 -0.58727414
#> 2017 Q3 -4.3510169      1  0.8268130 -1.6646218  0.0000000  0.77890156
#> 2017 Q4 -0.6897965      1 -4.3510169  0.8268130 -4.3510169  1.85465879
#> 2018 Q1 -0.8045264      1 -0.6897965 -4.3510169 -0.6897965 -0.36611661
#> 2018 Q2 -2.1400139      1 -0.8045264 -0.6897965 -0.8045264  0.50644120
#> 2018 Q3  0.4730325      1 -2.1400139 -0.8045264  0.0000000 -0.57849893
#> 2018 Q4 -1.2478511      1  0.4730325 -2.1400139  0.0000000 -0.01510772
#>              Series 2    Series 3    Series 4    Series 5
#> 2017 Q1 -0.4284557029  0.72215363  0.73344466  1.49037243
#> 2017 Q2 -1.9855426992  2.55981987 -0.05893913 -0.02900963
#> 2017 Q3 -1.0098119005 -0.55778408  1.13043653  0.01237915
#> 2017 Q4 -0.1281453368 -0.08235274  0.76247928  1.73204559
#> 2018 Q1 -1.4664402136 -1.90744533 -0.35578297 -0.13704585
#> 2018 Q2  0.5132418443  0.48435318  1.38183780 -1.47720991
#> 2018 Q3  1.2300639371 -1.01534253  0.53277462 -1.61247517
#> 2018 Q4  0.0003588142  0.05616500 -0.32518627  0.91271496
regressorsVariance(eps, arch=1:2, asym=1, log.ewma=5)
#>              loge2 vconst      arch1      arch2      asym1 logEqWMA(5)
#> 2017 Q4 -0.6897965      1 -4.3510169  0.8268130 -4.3510169  0.06983704
#> 2018 Q1 -0.8045264      1 -0.6897965 -4.3510169 -0.6897965 -0.35696118
#> 2018 Q2 -2.1400139      1 -0.8045264 -0.6897965 -0.8045264 -0.37479370
#> 2018 Q3  0.4730325      1 -2.1400139 -0.8045264  0.0000000 -0.39584758
#> 2018 Q4 -1.2478511      1  0.4730325 -2.1400139  0.0000000 -0.62198875
```
