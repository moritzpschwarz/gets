# Create the regressors of the mean equation

The function generates the regressors of the mean equation in an
[`arx`](http://moritzschwarz.org/gets/reference/arx.md) model. The
returned value is a `matrix` with the regressors and, by default, the
regressand in column one. By default, observations (rows) with missing
values are removed in the beginning and the end with
[`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html), and the returned
matrix is a [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

## Usage

``` r
regressorsMean(y, mc = FALSE, ar = NULL, ewma = NULL, mxreg = NULL,
  prefix="m", return.regressand = TRUE, return.as.zoo = TRUE, na.trim = TRUE,
  na.omit=FALSE)
```

## Arguments

- y:

  numeric vector, time-series or
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

- mc:

  logical. `TRUE` includes an intercept, whereas `FALSE` (default) does
  not.

- ar:

  either `NULL` (default) or an integer vector, say, `c(2,4)` or `1:4`
  with the AR-lags to include in the mean specification. If `NULL`, then
  no lags are included.

- ewma:

  either `NULL` (default) or a
  [`list`](https://rdrr.io/r/base/list.html) with arguments sent to the
  [`eqwma`](http://moritzschwarz.org/gets/reference/eqwma.md) function.
  In the latter case a lagged moving average of `y` is included as a
  regressor.

- mxreg:

  either `NULL` (default), numeric vector or matrix, say, a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object, or
  [`data.frame`](https://rdrr.io/r/base/data.frame.html) containing
  conditioning variables (covariates). Note that, if both `y` and
  `mxreg` are [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) objects,
  then their samples are matched.

- prefix:

  character, possibly of length zero, e.g. `""` or `character(0)`. The
  prefix added to the constant and covariate labels. The default is
  `"m"`, so that the default labels are `"mconst"` and `"mxreg"`.

- return.regressand:

  logical. `TRUE`, the default, includes the regressand as column one in
  the returned matrix.

- return.as.zoo:

  `TRUE`, the default, returns the matrix as a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object.

- na.trim:

  `TRUE`, the default, removes observations with `NA`-values in the
  beginning and the end with
  [`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html).

- na.omit:

  `TRUE`, the non-default, removes observations with `NA`-values, not
  necessarily in the beginning or in the end, with
  [`na.omit`](https://rdrr.io/r/stats/na.fail.html).

## Value

A matrix, by default of class
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html), with the regressand as
column one (the default).

## References

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44. DOI: https://www.jstatsoft.org/article/view/v086i03

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`regressorsVariance`](http://moritzschwarz.org/gets/reference/regressorsVariance.md),
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html),
[`eqwma`](http://moritzschwarz.org/gets/reference/eqwma.md),
[`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html) and
[`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html).

## Examples

``` r
##generate some data:
y <- rnorm(10) #regressand
x <- matrix(rnorm(10*5), 10, 5) #regressors

##create regressors (examples):
regressorsMean(y, mxreg=x)
#>              y      mxreg1     mxreg2      mxreg3     mxreg4       mxreg5
#> 1  -0.86357664  0.75439623 -0.4293480 -1.44569311 -1.2659095  0.535436378
#> 2  -0.98729366 -0.03665632  1.8174858 -0.32953481 -0.6776105 -1.327136437
#> 3  -0.04148188  0.06776830  1.7839376  0.08334871  0.6678258  1.371680955
#> 4  -1.02505398 -2.57267355 -1.0502001 -0.09801576  0.2394278  0.328505174
#> 5  -1.07696951 -0.63668837 -0.4884562 -0.78468636 -0.5226493  0.401875490
#> 6   0.92930845 -0.67702521  1.4318177 -0.68567176 -1.4594364  0.608878794
#> 7  -0.24258145 -1.28738037  1.3931588 -0.92063615  0.5670741  0.213785826
#> 8   1.46997845 -1.58012049 -0.4680864  1.36548818  1.7657239 -0.403817757
#> 9   0.11882472 -0.39370834 -0.4907391 -0.91487931  1.0738832  0.004448152
#> 10  0.45574257  0.87944780 -1.2739741  1.40782539 -0.3441977  1.018187644
regressorsMean(y, mxreg=x, return.regressand=FALSE)
#>         mxreg1     mxreg2      mxreg3     mxreg4       mxreg5
#> 1   0.75439623 -0.4293480 -1.44569311 -1.2659095  0.535436378
#> 2  -0.03665632  1.8174858 -0.32953481 -0.6776105 -1.327136437
#> 3   0.06776830  1.7839376  0.08334871  0.6678258  1.371680955
#> 4  -2.57267355 -1.0502001 -0.09801576  0.2394278  0.328505174
#> 5  -0.63668837 -0.4884562 -0.78468636 -0.5226493  0.401875490
#> 6  -0.67702521  1.4318177 -0.68567176 -1.4594364  0.608878794
#> 7  -1.28738037  1.3931588 -0.92063615  0.5670741  0.213785826
#> 8  -1.58012049 -0.4680864  1.36548818  1.7657239 -0.403817757
#> 9  -0.39370834 -0.4907391 -0.91487931  1.0738832  0.004448152
#> 10  0.87944780 -1.2739741  1.40782539 -0.3441977  1.018187644
regressorsMean(y, mc=TRUE, ar=1:3, mxreg=x)
#>             y mconst         ar1         ar2         ar3     mxreg1     mxreg2
#> 4  -1.0250540      1 -0.04148188 -0.98729366 -0.86357664 -2.5726736 -1.0502001
#> 5  -1.0769695      1 -1.02505398 -0.04148188 -0.98729366 -0.6366884 -0.4884562
#> 6   0.9293085      1 -1.07696951 -1.02505398 -0.04148188 -0.6770252  1.4318177
#> 7  -0.2425814      1  0.92930845 -1.07696951 -1.02505398 -1.2873804  1.3931588
#> 8   1.4699785      1 -0.24258145  0.92930845 -1.07696951 -1.5801205 -0.4680864
#> 9   0.1188247      1  1.46997845 -0.24258145  0.92930845 -0.3937083 -0.4907391
#> 10  0.4557426      1  0.11882472  1.46997845 -0.24258145  0.8794478 -1.2739741
#>         mxreg3     mxreg4       mxreg5
#> 4  -0.09801576  0.2394278  0.328505174
#> 5  -0.78468636 -0.5226493  0.401875490
#> 6  -0.68567176 -1.4594364  0.608878794
#> 7  -0.92063615  0.5670741  0.213785826
#> 8   1.36548818  1.7657239 -0.403817757
#> 9  -0.91487931  1.0738832  0.004448152
#> 10  1.40782539 -0.3441977  1.018187644
regressorsMean(log(y^2), mc=TRUE, ar=c(2,4))
#>      log(y^2) mconst         ar2         ar4
#> 5   0.1483022      1 -6.36499736 -0.29334527
#> 6  -0.1466291      1  0.04949054 -0.02557551
#> 7  -2.8328355      1  0.14830218 -6.36499736
#> 8   0.7704955      1 -0.14662914  0.04949054
#> 9  -4.2602116      1 -2.83283552  0.14830218
#> 10 -1.5716543      1  0.77049549 -0.14662914

##let y and x be time-series:
y <- ts(y, frequency=4, end=c(2018,4))
x <- ts(x, frequency=4, end=c(2018,4))
regressorsMean(y, mxreg=x)
#>                   y    Series 1   Series 2    Series 3   Series 4     Series 5
#> 2016 Q3 -0.86357664  0.75439623 -0.4293480 -1.44569311 -1.2659095  0.535436378
#> 2016 Q4 -0.98729366 -0.03665632  1.8174858 -0.32953481 -0.6776105 -1.327136437
#> 2017 Q1 -0.04148188  0.06776830  1.7839376  0.08334871  0.6678258  1.371680955
#> 2017 Q2 -1.02505398 -2.57267355 -1.0502001 -0.09801576  0.2394278  0.328505174
#> 2017 Q3 -1.07696951 -0.63668837 -0.4884562 -0.78468636 -0.5226493  0.401875490
#> 2017 Q4  0.92930845 -0.67702521  1.4318177 -0.68567176 -1.4594364  0.608878794
#> 2018 Q1 -0.24258145 -1.28738037  1.3931588 -0.92063615  0.5670741  0.213785826
#> 2018 Q2  1.46997845 -1.58012049 -0.4680864  1.36548818  1.7657239 -0.403817757
#> 2018 Q3  0.11882472 -0.39370834 -0.4907391 -0.91487931  1.0738832  0.004448152
#> 2018 Q4  0.45574257  0.87944780 -1.2739741  1.40782539 -0.3441977  1.018187644
regressorsMean(y, mc=TRUE, ar=1:3, mxreg=x)
#>                  y mconst         ar1         ar2         ar3   Series 1
#> 2017 Q2 -1.0250540      1 -0.04148188 -0.98729366 -0.86357664 -2.5726736
#> 2017 Q3 -1.0769695      1 -1.02505398 -0.04148188 -0.98729366 -0.6366884
#> 2017 Q4  0.9293085      1 -1.07696951 -1.02505398 -0.04148188 -0.6770252
#> 2018 Q1 -0.2425814      1  0.92930845 -1.07696951 -1.02505398 -1.2873804
#> 2018 Q2  1.4699785      1 -0.24258145  0.92930845 -1.07696951 -1.5801205
#> 2018 Q3  0.1188247      1  1.46997845 -0.24258145  0.92930845 -0.3937083
#> 2018 Q4  0.4557426      1  0.11882472  1.46997845 -0.24258145  0.8794478
#>           Series 2    Series 3   Series 4     Series 5
#> 2017 Q2 -1.0502001 -0.09801576  0.2394278  0.328505174
#> 2017 Q3 -0.4884562 -0.78468636 -0.5226493  0.401875490
#> 2017 Q4  1.4318177 -0.68567176 -1.4594364  0.608878794
#> 2018 Q1  1.3931588 -0.92063615  0.5670741  0.213785826
#> 2018 Q2 -0.4680864  1.36548818  1.7657239 -0.403817757
#> 2018 Q3 -0.4907391 -0.91487931  1.0738832  0.004448152
#> 2018 Q4 -1.2739741  1.40782539 -0.3441977  1.018187644
regressorsMean(log(y^2), mc=TRUE, ar=c(2,4))
#>           log(y^2) mconst         ar2         ar4
#> 2017 Q3  0.1483022      1 -6.36499736 -0.29334527
#> 2017 Q4 -0.1466291      1  0.04949054 -0.02557551
#> 2018 Q1 -2.8328355      1  0.14830218 -6.36499736
#> 2018 Q2  0.7704955      1 -0.14662914  0.04949054
#> 2018 Q3 -4.2602116      1 -2.83283552  0.14830218
#> 2018 Q4 -1.5716543      1  0.77049549 -0.14662914

##missing values (NA):
y[1] <- NA
x[10,3] <- NA
regressorsMean(y, mxreg=x)
#>                   y    Series 1   Series 2    Series 3   Series 4     Series 5
#> 2016 Q4 -0.98729366 -0.03665632  1.8174858 -0.32953481 -0.6776105 -1.327136437
#> 2017 Q1 -0.04148188  0.06776830  1.7839376  0.08334871  0.6678258  1.371680955
#> 2017 Q2 -1.02505398 -2.57267355 -1.0502001 -0.09801576  0.2394278  0.328505174
#> 2017 Q3 -1.07696951 -0.63668837 -0.4884562 -0.78468636 -0.5226493  0.401875490
#> 2017 Q4  0.92930845 -0.67702521  1.4318177 -0.68567176 -1.4594364  0.608878794
#> 2018 Q1 -0.24258145 -1.28738037  1.3931588 -0.92063615  0.5670741  0.213785826
#> 2018 Q2  1.46997845 -1.58012049 -0.4680864  1.36548818  1.7657239 -0.403817757
#> 2018 Q3  0.11882472 -0.39370834 -0.4907391 -0.91487931  1.0738832  0.004448152
regressorsMean(y, mxreg=x, na.trim=FALSE)
#>                   y    Series 1   Series 2    Series 3   Series 4     Series 5
#> 2016 Q3          NA  0.75439623 -0.4293480 -1.44569311 -1.2659095  0.535436378
#> 2016 Q4 -0.98729366 -0.03665632  1.8174858 -0.32953481 -0.6776105 -1.327136437
#> 2017 Q1 -0.04148188  0.06776830  1.7839376  0.08334871  0.6678258  1.371680955
#> 2017 Q2 -1.02505398 -2.57267355 -1.0502001 -0.09801576  0.2394278  0.328505174
#> 2017 Q3 -1.07696951 -0.63668837 -0.4884562 -0.78468636 -0.5226493  0.401875490
#> 2017 Q4  0.92930845 -0.67702521  1.4318177 -0.68567176 -1.4594364  0.608878794
#> 2018 Q1 -0.24258145 -1.28738037  1.3931588 -0.92063615  0.5670741  0.213785826
#> 2018 Q2  1.46997845 -1.58012049 -0.4680864  1.36548818  1.7657239 -0.403817757
#> 2018 Q3  0.11882472 -0.39370834 -0.4907391 -0.91487931  1.0738832  0.004448152
#> 2018 Q4  0.45574257  0.87944780 -1.2739741          NA -0.3441977  1.018187644
```
