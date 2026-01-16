# General-to-Specific (GETS) Modelling of a heterogeneous log-ARCH-X model

The starting model, an object of the 'larch' class (see
[`larch`](http://moritzschwarz.org/gets/reference/larch.md), is referred
to as the General Unrestricted Model (GUM). The `gets.larch()` function
undertakes multi-path GETS modelling of the log-variance specification.
The diagnostic tests are undertaken on the standardised residuals, and
the `keep` option enables regressors to be excluded from possible
removal.

## Usage

``` r
# S3 method for class 'larch'
gets(x, t.pval=0.05, wald.pval=t.pval, do.pet=TRUE, 
    ar.LjungB=NULL, arch.LjungB=NULL, normality.JarqueB=NULL, 
    user.diagnostics=NULL, info.method=c("sc", "aic", "aicc", "hq"),
    gof.function=NULL, gof.method=NULL, keep=c(1), include.gum=FALSE,
    include.1cut=TRUE, include.empty=FALSE, max.paths=NULL, tol=1e-07,
    turbo=FALSE, print.searchinfo=TRUE, plot=NULL, alarm=FALSE, ...)
```

## Arguments

- x:

  an object of class 'larch'

- t.pval:

  numeric value between 0 and 1. The significance level used for the
  two-sided regressor significance t-tests

- wald.pval:

  numeric value between 0 and 1. The significance level used for the
  Parsimonious Encompassing Tests (PETs). By default, `wald.pval` is
  equal to `t.pval`

- do.pet:

  logical. If `TRUE` (default), then a Parsimonious Encompassing Test
  (PET) against the GUM is undertaken at each regressor removal for the
  joint significance of all the deleted regressors along the current
  path. If `FALSE`, then a PET is not undertaken at each regressor
  removal

- ar.LjungB:

  `NULL` (default), or a [`list`](https://rdrr.io/r/base/list.html) with
  named items `lag` and `pval`, or a two-element numeric vector where
  the first element contains the lag and the second the p-value. If
  `NULL`, then the standardised residuals are not checked for
  autocorrelation. If `ar.LjungB` is a `list`, then `lag` contains the
  order of the Ljung and Box (1979) test for serial correlation in the
  standardised residuals, and `pval` contains the significance level. If
  `lag=NULL`, then the order used is that of the estimated 'larch'
  object

- arch.LjungB:

  `NULL` (default), or a [`list`](https://rdrr.io/r/base/list.html) with
  named items `lag` and `pval`, or a two-element numeric vector where
  the first element contains the lag and the second the p-value. If
  `NULL`, then the standardised residuals are not checked for ARCH
  (autocorrelation in the squared standardised residuals). If
  `ar.LjungB` is a `list`, then `lag` contains the order of the test,
  and `pval` contains the significance level. If `lag=NULL`, then the
  order used is that of the estimated 'larch' object

- normality.JarqueB:

  `NULL` (default) or a numeric value between 0 and 1. If `NULL`, then
  no test for non-normality is undertaken. If a numeric value between 0
  and 1, then the Jarque and Bera (1980) test for non-normality is
  conducted using a significance level equal to the numeric value

- user.diagnostics:

  `NULL` (default) or a [`list`](https://rdrr.io/r/base/list.html) with
  two entries, `name` and `pval`, see the `user.fun` argument in
  [`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md)

- info.method:

  character string, "sc" (default), "aic", "aicc" or "hq", which
  determines the information criterion to be used when selecting among
  terminal models. See
  [`infocrit`](http://moritzschwarz.org/gets/reference/infocrit.md) for
  the details

- gof.function:

  `NULL` (default) or a `list`, see
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md). If
  `NULL`, then
  [`infocrit`](http://moritzschwarz.org/gets/reference/infocrit.md) is
  used

- gof.method:

  `NULL` (default) or a `character`, see
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md). If
  `NULL` and `gof.function` is also `NULL`, then the best
  goodness-of-fit is characterised by a minimum value

- keep:

  the regressors to be kept (i.e. excluded from removal) in the
  specification search. Currently, `keep=c(1)` is obligatory, which
  excludes the log-variance intercept from removal

- include.gum:

  logical. If `TRUE`, the GUM (i.e. the starting model) is included
  among the terminal models. If `FALSE` (default), the GUM is not
  included

- include.1cut:

  logical. If `TRUE` (default), then the 1-cut model is added to the
  list of terminal models. If `FALSE`, the 1-cut is not added, unless it
  is a terminal model in one of the paths

- include.empty:

  logical. If `TRUE`, then an empty model is included among the terminal
  models, if it passes the diagnostic tests. If `FALSE` (default), then
  the empty model is not included

- max.paths:

  `NULL` (default) or an integer equal to or greater than 0. If `NULL`,
  then there is no limit to the number of paths. If an integer (e.g. 1),
  then this integer constitutes the maximum number of paths searched
  (e.g. a single path)

- tol:

  numeric value. The tolerance for detecting linear dependencies in the
  columns of the variance-covariance matrix when computing the
  Wald-statistic used in the Parsimonious Encompassing Tests (PETs), see
  the [`qr.solve`](https://rdrr.io/r/base/qr.html) function

- turbo:

  logical. If `TRUE`, then paths are not searched twice (or more)
  unnecessarily, thus yielding a significant potential for speed-gain.
  However, the checking of whether the search has arrived at a point it
  has already been comes with a computational overhead. Accordingly, if
  `turbo=TRUE`, the total search time might in fact be higher than if
  `turbo=FALSE`. This is particularly likely to happen if estimation is
  very fast, say, less than a quarter of a second. Hence the default is
  `FALSE`

- print.searchinfo:

  logical. If `TRUE` (default), then a print is returned whenever
  simiplification along a new path is started

- plot:

  `NULL` or logical. If `TRUE`, then the fitted values and the
  standardised residuals of the final model are plotted after model
  selection. If `FALSE`, then they are not plotted. If `NULL` (default),
  then the value set by [`options`](https://rdrr.io/r/base/options.html)
  determines whether a plot is produced or not

- alarm:

  logical. If `TRUE`, then a sound or beep is emitted (in order to alert
  the user) when the model selection ends, see
  [`alarm`](https://rdrr.io/r/utils/alarm.html)

- ...:

  additional arguments

## Details

See Pretis, Reade and Sucarrat (2018):
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03) , and
Sucarrat (2020):
<https://journal.r-project.org/archive/2021/RJ-2021-024/>.  

The arguments `user.diagnostics` and `gof.function` enable the
specification of user-defined diagnostics and a user-defined
goodness-of-fit function. For the former, see the documentation of
[`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md).
For the latter, the principles of the same arguments in
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) are
followed, see its documentation under "Details", and Sucarrat (2020):
<https://journal.r-project.org/archive/2021/RJ-2021-024/>.

## Value

A list of class 'larch', see
[`larch`](http://moritzschwarz.org/gets/reference/larch.md), with
additional information about the GETS modelling

## References

C. Jarque and A. Bera (1980): 'Efficient Tests for Normality,
Homoscedasticity and Serial Independence'. Economics Letters 6, pp.
255-259.
[doi:10.1016/0165-1765(80)90024-5](https://doi.org/10.1016/0165-1765%2880%2990024-5)

G. Ljung and G. Box (1979): 'On a Measure of Lack of Fit in Time Series
Models'. Biometrika 66, pp. 265-270

Felix Pretis, James Reade and Genaro Sucarrat (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44.
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03)

Genaro Sucarrat (2020): 'User-Specified General-to-Specific and
Indicator Saturation Methods'. The R Journal 12:2, pages 388-401.
<https://journal.r-project.org/archive/2021/RJ-2021-024/>

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

Methods and extraction functions (mostly S3 methods):
[`coef.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`ES`](http://moritzschwarz.org/gets/reference/ES.md),
[`fitted.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
`gets.larch`,  
[`logLik.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`nobs.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`plot.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`predict.larch`](http://moritzschwarz.org/gets/reference/predict.larch.md),
[`print.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),  
[`residuals.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`summary.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`VaR`](http://moritzschwarz.org/gets/reference/ES.md),
[`toLatex.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md)
and [`vcov.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md)  

Related functions:
[`eqwma`](http://moritzschwarz.org/gets/reference/eqwma.md),
[`leqwma`](http://moritzschwarz.org/gets/reference/eqwma.md),
[`regressorsVariance`](http://moritzschwarz.org/gets/reference/regressorsVariance.md),
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`qr.solve`](https://rdrr.io/r/base/qr.html)

## Examples

``` r
##Simulate some data:
set.seed(123)
e <- rnorm(40)
x <- matrix(rnorm(4*40), 40, 4)

##estimate a log-ARCH(3) with asymmetry and log(x^2) as regressors:
gum <- larch(e, arch=1:3, asym=1, vxreg=log(x^2))

##GETS modelling of the log-variance:
simple <- gets(gum)
#> 
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1 -0.623183  0.561349 -1.1102 0.29571  
#> arch1        2    0  0.075856  0.206463  0.3674 0.72181  
#> arch2        3    0 -0.125252  0.147240 -0.8507 0.41701  
#> arch3        4    0  0.076151  0.163485  0.4658 0.65243  
#> asym1        5    0 -0.178412  0.237220 -0.7521 0.47120  
#> vxreg1       6    0  0.064916  0.116349  0.5579 0.59049  
#> vxreg2       7    0 -0.190337  0.129783 -1.4666 0.17654  
#> vxreg3       8    0  0.142136  0.137520  1.0336 0.32831  
#> vxreg4       9    0 -0.224855  0.121049 -1.8576 0.09619 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                     Chi-sq df p-value
#> Ljung-Box AR(1)   0.050748  1 0.82177
#> Ljung-Box ARCH(4) 4.228739  4 0.37593
#> 
#> 8 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 
#>   Path 1: 2 4 6 5 8 9 7 
#>   Path 2: 3 4 6 5 9 7 8 
#>   Path 3: 4 6 5 3 9 7 8 
#>   Path 4: 5 6 4 3 9 7 8 
#>   Path 5: 6 4 5 3 9 7 8 
#>   Path 6: 7 6 5 4 3 9 8 
#>   Path 7: 8 5 4 6 3 9 7 
#>   Path 8: 9 6 4 3 5 7 8 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.682133 -47.81400 37 1
#> spec 2:         2.769014 -47.61585 37 2
#> spec 3:         2.774207 -47.71192 37 2
#> 
#> Retained regressors (final model):
#>   vconst 

##GETS modelling with intercept and log-ARCH(1) terms
##excluded from removal:
simple <- gets(gum, keep=c(1,2))
#> 
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1 -0.623183  0.561349 -1.1102 0.29571  
#> arch1        2    1  0.075856  0.206463  0.3674 0.72181  
#> arch2        3    0 -0.125252  0.147240 -0.8507 0.41701  
#> arch3        4    0  0.076151  0.163485  0.4658 0.65243  
#> asym1        5    0 -0.178412  0.237220 -0.7521 0.47120  
#> vxreg1       6    0  0.064916  0.116349  0.5579 0.59049  
#> vxreg2       7    0 -0.190337  0.129783 -1.4666 0.17654  
#> vxreg3       8    0  0.142136  0.137520  1.0336 0.32831  
#> vxreg4       9    0 -0.224855  0.121049 -1.8576 0.09619 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                     Chi-sq df p-value
#> Ljung-Box AR(1)   0.050748  1 0.82177
#> Ljung-Box ARCH(4) 4.228739  4 0.37593
#> 
#> 7 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 
#>   Path 1: 3 6 5 7 9 8 
#>   Path 2: 4 6 5 8 9 7 
#>   Path 3: 5 6 4 8 9 7 
#>   Path 4: 6 4 5 8 9 7 
#>   Path 5: 7 6 5 4 9 8 
#>   Path 6: 8 5 4 6 9 7 
#>   Path 7: 9 6 4 5 7 8 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.774207 -47.71192 37 2
#> spec 2:         2.854352 -47.38913 37 3
#> spec 3:         2.860846 -47.50927 37 3
#> 
#> Retained regressors (final model):
#>   vconst   arch1 

##GETS modelling with non-default autocorrelation
##diagnostics settings:
simple <- gets(gum, ar.LjungB=list(pval=0.05))
#> 
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1 -0.623183  0.561349 -1.1102 0.29571  
#> arch1        2    0  0.075856  0.206463  0.3674 0.72181  
#> arch2        3    0 -0.125252  0.147240 -0.8507 0.41701  
#> arch3        4    0  0.076151  0.163485  0.4658 0.65243  
#> asym1        5    0 -0.178412  0.237220 -0.7521 0.47120  
#> vxreg1       6    0  0.064916  0.116349  0.5579 0.59049  
#> vxreg2       7    0 -0.190337  0.129783 -1.4666 0.17654  
#> vxreg3       8    0  0.142136  0.137520  1.0336 0.32831  
#> vxreg4       9    0 -0.224855  0.121049 -1.8576 0.09619 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                     Chi-sq df p-value
#> Ljung-Box AR(1)   0.050748  1 0.82177
#> Ljung-Box ARCH(4) 4.228739  4 0.37593
#> 
#> 8 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 
#>   Path 1: 2 4 6 5 8 9 7 
#>   Path 2: 3 4 6 5 9 7 8 
#>   Path 3: 4 6 5 3 9 7 8 
#>   Path 4: 5 6 4 3 9 7 8 
#>   Path 5: 6 4 5 3 9 7 8 
#>   Path 6: 7 6 5 4 3 9 8 
#>   Path 7: 8 5 4 6 3 9 7 
#>   Path 8: 9 6 4 3 5 7 8 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.682133 -47.81400 37 1
#> spec 2:         2.769014 -47.61585 37 2
#> spec 3:         2.774207 -47.71192 37 2
#> 
#> Retained regressors (final model):
#>   vconst 

##GETS modelling with very liberal (40%) significance level:
simple <- gets(gum, t.pval=0.4)
#> 
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1 -0.623183  0.561349 -1.1102 0.29571  
#> arch1        2    0  0.075856  0.206463  0.3674 0.72181  
#> arch2        3    0 -0.125252  0.147240 -0.8507 0.41701  
#> arch3        4    0  0.076151  0.163485  0.4658 0.65243  
#> asym1        5    0 -0.178412  0.237220 -0.7521 0.47120  
#> vxreg1       6    0  0.064916  0.116349  0.5579 0.59049  
#> vxreg2       7    0 -0.190337  0.129783 -1.4666 0.17654  
#> vxreg3       8    0  0.142136  0.137520  1.0336 0.32831  
#> vxreg4       9    0 -0.224855  0.121049 -1.8576 0.09619 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                     Chi-sq df p-value
#> Ljung-Box AR(1)   0.050748  1 0.82177
#> Ljung-Box ARCH(4) 4.228739  4 0.37593
#> 
#> 5 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 
#>   Path 1: 2 4 6 5 
#>   Path 2: 3 4 6 5 
#>   Path 3: 4 6 5 
#>   Path 4: 5 6 4 
#>   Path 5: 6 4 5 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.975554 -47.82591 37 4
#> spec 2:         3.116885 -48.63508 37 5
#> spec 3:         3.075614 -47.87156 37 5
#> spec 4:         3.214387 -48.63341 37 6
#> 
#> Retained regressors (final model):
#>   vconst   vxreg2   vxreg3   vxreg4 
```
