# General-to-Specific (GETS) Modelling of an AR-X model (the mean specification) with log-ARCH-X errors (the log-variance specification).

The starting model, an object of the 'arx' class, is referred to as the
General Unrestricted Model (GUM). The `getsm` function undertakes
multi-path GETS modelling of the mean specification, whereas `getsv`
does the same for the log-variance specification. The diagnostic tests
are undertaken on the standardised residuals, and the `keep` option
enables regressors to be excluded from possible removal.

## Usage

``` r
##GETS-modelling of mean specification:
getsm(object, t.pval=0.05, wald.pval=t.pval, vcov.type=NULL, 
    do.pet=TRUE, ar.LjungB=list(lag=NULL, pval=0.025), 
    arch.LjungB=list(lag=NULL, pval=0.025), normality.JarqueB=NULL, 
    user.diagnostics=NULL, info.method=c("sc","aic","aicc", "hq"),
    gof.function=NULL, gof.method=NULL, keep=NULL, include.gum=FALSE,
    include.1cut=TRUE, include.empty=FALSE, max.paths=NULL, tol=1e-07,
    turbo=FALSE, print.searchinfo=TRUE, plot=NULL, alarm=FALSE)

##GETS modelling of log-variance specification:
getsv(object, t.pval=0.05, wald.pval=t.pval,
    do.pet=TRUE, ar.LjungB=list(lag=NULL, pval=0.025),
    arch.LjungB=list(lag=NULL, pval=0.025), normality.JarqueB=NULL,
    user.diagnostics=NULL, info.method=c("sc","aic","aicc","hq"),
    gof.function=NULL, gof.method=NULL, keep=c(1), include.gum=FALSE,
    include.1cut=TRUE, include.empty=FALSE, max.paths=NULL, tol=1e-07,
    turbo=FALSE, print.searchinfo=TRUE, plot=NULL, alarm=FALSE)
```

## Arguments

- object:

  an object of class 'arx'

- t.pval:

  numeric value between 0 and 1. The significance level used for the
  two-sided regressor significance t-tests

- wald.pval:

  numeric value between 0 and 1. The significance level used for the
  Parsimonious Encompassing Tests (PETs). By default, it is the same as
  `t.pval`

- vcov.type:

  the type of variance-covariance matrix used. If `NULL` (default), then
  the type used in the estimation of the 'arx' object is used. This can
  be overridden by either "ordinary" (i.e. the ordinary
  variance-covariance matrix) or "white" (i.e. the White (1980)
  heteroscedasticity robust variance-covariance matrix)

- do.pet:

  logical. If `TRUE` (default), then a Parsimonious Encompassing Test
  (PET) against the GUM is undertaken at each regressor removal for the
  joint significance of all the deleted regressors along the current
  path. If `FALSE`, then a PET is not undertaken at each regressor
  removal

- ar.LjungB:

  a [`list`](https://rdrr.io/r/base/list.html) with named items `lag`
  and `pval`, a two-element numeric vector where the first element
  contains the lag and the second the p-value, or `NULL`. In the first
  case, `lag` contains the order of the Ljung and Box (1979) test for
  serial correlation in the standardised residuals, and `pval` contains
  the significance level. If `lag=NULL` (default), then the order used
  is that of the estimated 'arx' object. If `ar.Ljungb=NULL`, then the
  standardised residuals are not checked for serial correlation

- arch.LjungB:

  a [`list`](https://rdrr.io/r/base/list.html) with named items `lag`
  and `pval`, a two-element numeric vector where the first element
  contains the lag and the second the p-value, or `NULL`. In the first
  case, `lag` contains the order of the Ljung and Box (1979) test for
  serial correlation in the squared standardised residuals, and `pval`
  contains the significance level. If `lag=NULL` (default), then the
  order used is that of the estimated 'arx' object. If
  `arch.Ljungb=NULL`, then the standardised residuals are not checked
  for ARCH

- normality.JarqueB:

  a value between 0 and 1, or `NULL`. In the former case, the Jarque and
  Bera (1980) test for non-normality is conducted using a significance
  level equal to the numeric value. If `NULL`, then no test for
  non-normality is undertaken

- user.diagnostics:

  `NULL` or a [`list`](https://rdrr.io/r/base/list.html) with two
  entries, `name` and `pval`, see the `user.fun` argument in
  [`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md)

- info.method:

  character string, "sc" (default), "aic" or "hq", which determines the
  information criterion to be used when selecting among terminal models.
  The abbreviations are short for the Schwarz or Bayesian information
  criterion (sc), the Akaike information criterion (aic) and the
  Hannan-Quinn (hq) information criterion

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

  the regressors to be excluded from removal in the specification
  search. Note that `keep=c(1)` is obligatory when using `getsv`. This
  excludes the log-variance intercept from removal. The regressor
  numbering is contained in the `reg.no` column of the GUM

- include.gum:

  logical. If `TRUE`, then the GUM (i.e. the starting model) is included
  among the terminal models. If `FALSE` (default), then the GUM is not
  included

- include.1cut:

  logical. If `TRUE`, then the 1-cut model is added to the list of
  terminal models. If `FALSE` (default), then the 1-cut is not added,
  unless it is a terminal model in one of the paths

- include.empty:

  logical. If `TRUE`, then an empty model is included among the terminal
  models, if it passes the diagnostic tests, even if it is not equal to
  one of the terminals. If `FALSE` (default), then the empty model is
  not included (unless it is one of the terminals)

- max.paths:

  `NULL` (default) or an integer greater than 0. If `NULL`, then there
  is no limit to the number of paths. If an integer (e.g. 1), then this
  integer constitutes the maximum number of paths searched (e.g. a
  single path)

- tol:

  numeric value. The tolerance for detecting linear dependencies in the
  columns of the variance-covariance matrix when computing the
  Wald-statistic used in the Parsimonious Encompassing Tests (PETs), see
  the [`qr.solve`](https://rdrr.io/r/base/qr.html) function

- turbo:

  logical. If `TRUE`, then (parts of) paths are not searched twice (or
  more) unnecessarily, thus yielding a significant potential for
  speed-gain. However, the checking of whether the search has arrived at
  a point it has already been comes with a slight computational
  overhead. Accordingly, if `turbo=TRUE`, then the total search time
  might in fact be higher than if `turbo=FALSE`. This happens if
  estimation is very fast, say, less than quarter of a second. Hence the
  default is `FALSE`

- print.searchinfo:

  logical. If `TRUE` (default), then a print is returned whenever
  simiplification along a new path is started

- plot:

  `NULL` or logical. If `TRUE`, then the fitted values and the residuals
  of the final model are plotted after model selection. If `FALSE`, then
  they are not. If `NULL` (default), then the value set by
  [`options`](https://rdrr.io/r/base/options.html) determines whether a
  plot is produced or not

- alarm:

  logical. If `TRUE`, then a sound or beep is emitted (in order to alert
  the user) when the model selection ends

## Details

For an overview, see Pretis, Reade and Sucarrat (2018):
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03) .  

The arguments `user.diagnostics` and `gof.function` enable the
specification of user-defined diagnostics and a user-defined
goodness-of-fit function. For the former, see the documentation of
[`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md).
For the latter, the principles of the same arguments in
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) are
followed, see its documentation under "Details", and Sucarrat (2020):
<https://journal.r-project.org/archive/2021/RJ-2021-024/>.

## Value

A list of class 'gets'

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

Extraction functions:
[`coef.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`fitted.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`paths`](http://moritzschwarz.org/gets/reference/paths.md),
[`plot.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`print.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),  
[`residuals.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`summary.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`terminals`](http://moritzschwarz.org/gets/reference/paths.md),
[`vcov.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md)  

Related functions:
[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`eqwma`](http://moritzschwarz.org/gets/reference/eqwma.md),
[`leqwma`](http://moritzschwarz.org/gets/reference/eqwma.md),
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`qr.solve`](https://rdrr.io/r/base/qr.html)

## Examples

``` r
##Simulate from an AR(1):
set.seed(123)
y <- arima.sim(list(ar=0.4), 80)

##Simulate four independent Gaussian regressors:
xregs <- matrix(rnorm(2*80), 80, 2)

##estimate an AR(2) with intercept and four conditioning
##regressors in the mean, and a log-ARCH(3) with log(xregs^2) as
##regressors in the log-variance:
gum01 <- arx(y, mc=TRUE, ar=1:2, mxreg=xregs, arch=1:3,
  vxreg=log(xregs^2))

##GETS model selection of the mean:
meanmod01 <- getsm(gum01)
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep      coef std.error  t-stat  p-value   
#> mconst       1    0  0.052513  0.101817  0.5158 0.607583   
#> ar1          2    0  0.312720  0.115433  2.7091 0.008401 **
#> ar2          3    0 -0.062448  0.118204 -0.5283 0.598886   
#> mxreg1       4    0  0.166409  0.101452  1.6403 0.105250   
#> mxreg2       5    0 -0.013699  0.111233 -0.1232 0.902323   
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> GUM log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst  0.406367  0.414376  0.9617 0.32675  
#> arch1   0.192973  0.117722  1.6392 0.10572  
#> arch2   0.245569  0.125909  1.9504 0.05519 .
#> arch3  -0.076098  0.118621 -0.6415 0.52331  
#> vxreg1 -0.196355  0.127679 -1.5379 0.12865  
#> vxreg2  0.158193  0.131686  1.2013 0.23374  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.9061  3 0.27179
#> Ljung-Box ARCH(4) 4.8830  4 0.29952
#> 
#> 4 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 
#>   Path 1: 1 5 3 4 
#>   Path 2: 3 5 1 4 
#>   Path 3: 4 5 3 1 
#>   Path 4: 5 1 3 4 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.776498 -106.1051 78 1
#> 
#> Retained regressors (final model):
#> 
#>   ar1 

##GETS model selection of the log-variance:
varmod01 <- getsv(gum01)
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1  0.406367  0.414376  0.9617 0.32675  
#> arch1        2    0  0.192973  0.117722  1.6392 0.10572  
#> arch2        3    0  0.245569  0.125909  1.9504 0.05519 .
#> arch3        4    0 -0.076098  0.118621 -0.6415 0.52331  
#> vxreg1       5    0 -0.196355  0.127679 -1.5379 0.12865  
#> vxreg2       6    0  0.158193  0.131686  1.2013 0.23374  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.9061  3 0.27179
#> Ljung-Box ARCH(4) 4.8830  4 0.29952
#> 
#> 5 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 
#>   Path 1: 2 4 6 5 3 
#>   Path 2: 3 4 6 5 
#>   Path 3: 4 6 5 3 
#>   Path 4: 5 4 6 3 
#>   Path 5: 6 4 5 3 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.632361 -96.55478 75 1
#> spec 2:         2.748094 -98.73603 75 2
#> 
#> Retained regressors (final model):
#> 
#>   vconst 

##GETS model selection of the mean with the mean intercept
##excluded from removal:
meanmod02 <- getsm(gum01, keep=1)
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep      coef std.error  t-stat  p-value   
#> mconst       1    1  0.052513  0.101817  0.5158 0.607583   
#> ar1          2    0  0.312720  0.115433  2.7091 0.008401 **
#> ar2          3    0 -0.062448  0.118204 -0.5283 0.598886   
#> mxreg1       4    0  0.166409  0.101452  1.6403 0.105250   
#> mxreg2       5    0 -0.013699  0.111233 -0.1232 0.902323   
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> GUM log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst  0.406367  0.414376  0.9617 0.32675  
#> arch1   0.192973  0.117722  1.6392 0.10572  
#> arch2   0.245569  0.125909  1.9504 0.05519 .
#> arch3  -0.076098  0.118621 -0.6415 0.52331  
#> vxreg1 -0.196355  0.127679 -1.5379 0.12865  
#> vxreg2  0.158193  0.131686  1.2013 0.23374  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.9061  3 0.27179
#> Ljung-Box ARCH(4) 4.8830  4 0.29952
#> 
#> 3 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 
#>   Path 1: 3 5 4 
#>   Path 2: 4 5 3 
#>   Path 3: 5 3 4 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.656706 -99.25482 78 2
#> 
#> Retained regressors (final model):
#> 
#>   mconst   ar1 

##GETS model selection of the mean with non-default
#serial-correlation diagnostics settings:
meanmod03 <- getsm(gum01, ar.LjungB=list(pval=0.05))
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep      coef std.error  t-stat  p-value   
#> mconst       1    0  0.052513  0.101817  0.5158 0.607583   
#> ar1          2    0  0.312720  0.115433  2.7091 0.008401 **
#> ar2          3    0 -0.062448  0.118204 -0.5283 0.598886   
#> mxreg1       4    0  0.166409  0.101452  1.6403 0.105250   
#> mxreg2       5    0 -0.013699  0.111233 -0.1232 0.902323   
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> GUM log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst  0.406367  0.414376  0.9617 0.32675  
#> arch1   0.192973  0.117722  1.6392 0.10572  
#> arch2   0.245569  0.125909  1.9504 0.05519 .
#> arch3  -0.076098  0.118621 -0.6415 0.52331  
#> vxreg1 -0.196355  0.127679 -1.5379 0.12865  
#> vxreg2  0.158193  0.131686  1.2013 0.23374  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.9061  3 0.27179
#> Ljung-Box ARCH(4) 4.8830  4 0.29952
#> 
#> 4 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 
#>   Path 1: 1 5 3 4 
#>   Path 2: 3 5 1 4 
#>   Path 3: 4 5 3 1 
#>   Path 4: 5 1 3 4 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.776498 -106.1051 78 1
#> 
#> Retained regressors (final model):
#> 
#>   ar1 

##GETS model selection of the mean with very liberal
##(20 percent) significance levels:
meanmod04 <- getsm(gum01, t.pval=0.2)
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep      coef std.error  t-stat  p-value   
#> mconst       1    0  0.052513  0.101817  0.5158 0.607583   
#> ar1          2    0  0.312720  0.115433  2.7091 0.008401 **
#> ar2          3    0 -0.062448  0.118204 -0.5283 0.598886   
#> mxreg1       4    0  0.166409  0.101452  1.6403 0.105250   
#> mxreg2       5    0 -0.013699  0.111233 -0.1232 0.902323   
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> GUM log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst  0.406367  0.414376  0.9617 0.32675  
#> arch1   0.192973  0.117722  1.6392 0.10572  
#> arch2   0.245569  0.125909  1.9504 0.05519 .
#> arch3  -0.076098  0.118621 -0.6415 0.52331  
#> vxreg1 -0.196355  0.127679 -1.5379 0.12865  
#> vxreg2  0.158193  0.131686  1.2013 0.23374  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.9061  3 0.27179
#> Ljung-Box ARCH(4) 4.8830  4 0.29952
#> 
#> 3 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 
#>   Path 1: 1 5 3 
#>   Path 2: 3 5 1 
#>   Path 3: 5 1 3 
#> 
#> Terminal models:
#> 
#>                 info(sc)     logl  n k
#> spec 1 (1-cut): 2.767504 -103.576 78 2
#> 
#> Retained regressors (final model):
#> 
#>   ar1   mxreg1 

##GETS model selection of log-variance with all the
##log-ARCH terms excluded from removal:
varmod03 <- getsv(gum01, keep=2:4)
#> Warning: Regressor 1 included into 'keep'
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1  0.406367  0.414376  0.9617 0.32675  
#> arch1        2    1  0.192973  0.117722  1.6392 0.10572  
#> arch2        3    1  0.245569  0.125909  1.9504 0.05519 .
#> arch3        4    1 -0.076098  0.118621 -0.6415 0.52331  
#> vxreg1       5    0 -0.196355  0.127679 -1.5379 0.12865  
#> vxreg2       6    0  0.158193  0.131686  1.2013 0.23374  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.9061  3 0.27179
#> Ljung-Box ARCH(4) 4.8830  4 0.29952
#> 
#> 2 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 
#>   Path 1: 5 6 
#>   Path 2: 6 5 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.811774 -96.80654 75 4
#> 
#> Retained regressors (final model):
#> 
#>   vconst   arch1   arch2   arch3 
```
