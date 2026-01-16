# Estimate a heterogeneous log-ARCH-X model

The function `larch()` estimates a heterogeneous log-ARCH-X model, which
is a generalisation of the dynamic log-variance model in Pretis, Reade
and Sucarrat (2018). Internally, estimation is undertaken by a call to
[`larchEstfun`](http://moritzschwarz.org/gets/reference/larchEstfun.md).
The log-variance specification can contain log-ARCH terms, log-HARCH
terms, asymmetry terms ('leverage'), the log of volatility proxies made
up of past returns and other covariates ('X'), for example Realised
Volatility (RV), volume or the range.

## Usage

``` r
larch(e, vc=TRUE, arch = NULL, harch = NULL, asym = NULL, asymind = NULL,
  log.ewma = NULL, vxreg = NULL, zero.adj = NULL, 
  vcov.type = c("robust", "hac"), qstat.options = NULL,
  normality.JarqueB = FALSE, tol = 1e-07, singular.ok = TRUE,  plot = NULL)
```

## Arguments

- e:

  `numeric` vector, time-series or
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object. Missing values
  in the beginning and at the end of the series is allowed, as they are
  removed with the [`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html)
  command

- vc:

  `logical`. `TRUE` includes an intercept in the log-variance
  specification. Currently, `vc` cannot be set to any other value than
  `TRUE`

- arch:

  either `NULL` (default) or an integer vector, say, `c(1,3)` or `2:5`.
  The log-ARCH lags to include in the log-variance specification

- harch:

  either `NULL` (default) or an integer vector, say, `c(5,10)`. The (log
  of) heterogeneous ARCH terms (Muller et al. 1997) to include

- asym:

  either `NULL` (default) or an integer vector, say, `c(1)` or `1:3`.
  The asymmetry (i.e. 'leverage') terms to include in the log-variance
  specification

- asymind:

  either `NULL` (default or an integer vector. The indicator asymmetry
  terms to include

- log.ewma:

  either `NULL` (default) or a vector of the lengths of the volatility
  proxies, see
  [`leqwma`](http://moritzschwarz.org/gets/reference/eqwma.md). The
  terms serve as (log of) volatility proxies similar to RVs in the
  HAR-model of Corsi (2009). Here, the `log.ewma` terms are made up of
  past e's

- vxreg:

  either `NULL` (default) or a numeric vector or matrix, say, a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object. If both `e` and
  `vxreg` are [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) objects,
  then their samples are chosen to match

- zero.adj:

  `NULL` (default) or a strictly positive `numeric` scalar. If `NULL`,
  the zeros in the squared residuals are replaced by the 10 percent
  quantile of the non-zero squared residuals. If `zero.adj` is a
  strictly positive `numeric` scalar, then this value is used to replace
  the zeros of the squared e's

- vcov.type:

  `character`. "robust" (default) or "hac" (partial matching is
  allowed). If "robust", the robust variance-covariance matrix of the
  White (1980) type is used. If "hac", the Newey and West (1987)
  heteroscedasticity and autocorrelation-robust matrix is used

- qstat.options:

  `NULL` (default) or an integer vector of length two, say, `c(1,1)`.
  The first value sets the lag-order of the AR diagnostic test of the
  standardised residuals, whereas the second value sets the lag-order of
  the ARCH diagnostic test of the standardised residuals. If `NULL`,
  then the two values of the vector are set automatically

- normality.JarqueB:

  `FALSE` (default) or `TRUE`. If `TRUE`, then the results of the Jarque
  and Bera (1980) test for non-normality in the residuals are included
  in the estimation results

- tol:

  `numeric` value. The tolerance (the default is `1e-07`) for detecting
  linear dependencies in the columns of the regressors (see
  [`ols`](http://moritzschwarz.org/gets/reference/ols.md) and
  [`qr`](https://rdrr.io/r/base/qr.html)). Only used if `LAPACK` is
  `FALSE` (default)

- singular.ok:

  `logical`. If `TRUE` (default), the regressors are checked for
  singularity, and the ones causing it are automatically removed. If
  `FALSE`, then the function returns an error

- plot:

  `NULL` (default) or `logical`. If `TRUE`, the fitted values and the
  residuals are plotted. If `NULL`, then the value set by
  [`options`](https://rdrr.io/r/base/options.html) determines whether a
  plot is produced or not

## Details

No details for the moment

## Value

A list of class 'larch'

## References

G. Ljung and G. Box (1979): 'On a Measure of Lack of Fit in Time Series
Models'. Biometrika 66, pp. 265-270

F. Corsi (2009): 'A Simple Approximate Long-Memory Model of Realized
Volatility', Journal of Financial Econometrics 7, pp. 174-196

C. Jarque and A. Bera (1980): 'Efficient Tests for Normality,
Homoscedasticity and Serial Independence'. Economics Letters 6, pp.
255-259.
[doi:10.1016/0165-1765(80)90024-5](https://doi.org/10.1016/0165-1765%2880%2990024-5)

U. Muller, M. Dacorogna, R. Dave, R. Olsen, O. Pictet and J. von
Weizsacker (1997): 'Volatilities of different time resolutions -
analyzing the dynamics of market components'. Journal of Empirical
Finance 4, pp. 213-239

F. Pretis, J. Reade and G. Sucarrat (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44.
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03)

H. White (1980): 'A Heteroskedasticity-Consistent Covariance Matrix
Estimator and a Direct Test for Heteroskedasticity', Econometrica 48,
pp. 817-838.

W.K. Newey and K.D. West (1987): 'A Simple, Positive Semi-Definite,
Heteroskedasticity and Autocorrelation Consistent Covariance Matrix',
Econometrica 55, pp. 703-708.

## Author

Genaro Sucarrat: <https://www.sucarrat.net/>

## See also

Methods and extraction functions (mostly S3 methods):
[`coef.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`ES`](http://moritzschwarz.org/gets/reference/ES.md),
[`fitted.larch`](http://moritzschwarz.org/gets/reference/coef.larch.md),
[`gets.larch`](http://moritzschwarz.org/gets/reference/gets.larch.md),  
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

[`regressorsVariance`](http://moritzschwarz.org/gets/reference/regressorsVariance.md)

## Examples

``` r
##Simulate some data:
set.seed(123)
e <- rnorm(40)
x <- matrix(rnorm(40*2), 40, 2)

##estimate a log-variance specification with a log-ARCH(4)
##structure:
larch(e, arch=1:4)
#> 
#> Date: Fri Jan 16 14:55:58 2026 
#> Dependent var.: e 
#> Variance-Covariance: Robust (default) 
#> No. of observations: 36 
#> Sample: 5 to 40 
#> 
#> Log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst -0.887676  0.327234 -2.7127 0.04214 *
#> arch1   0.095588  0.119125  0.8024 0.45874  
#> arch2  -0.203163  0.123729 -1.6420 0.16151  
#> arch3   0.051273  0.117283  0.4372 0.68022  
#> arch4  -0.362734  0.129071 -2.8103 0.03753 *
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                    Chi-sq df p-value
#> Ljung-Box AR(1)   0.37831  1  0.5385
#> Ljung-Box ARCH(5) 3.09101  5  0.6860
#>                         
#> Log-lik.(n=36): -42.9794

##estimate a log-variance specification with a log-ARCH(4)
##structure, a log-HARCH(5) term and a first-order asymmetry/leverage
##term:
larch(e, arch=1:4, harch=5, asym=1)
#> 
#> Date: Fri Jan 16 14:55:58 2026 
#> Dependent var.: e 
#> Variance-Covariance: Robust (default) 
#> No. of observations: 35 
#> Sample: 6 to 40 
#> 
#> Log-variance equation:
#> 
#>              coef  std.error  t-stat p-value  
#> vconst -0.9798902  0.2823343 -3.4707 0.01040 *
#> arch1   0.0048135  0.1473334  0.0327 0.97485  
#> arch2  -0.1643365  0.1243636 -1.3214 0.22791  
#> arch3  -0.0620451  0.1267956 -0.4893 0.63957  
#> arch4  -0.3875460  0.1369073 -2.8307 0.02538 *
#> harch5 -0.1215850  0.1446098 -0.8408 0.42825  
#> asym1  -0.0805486  0.2242473 -0.3592 0.73004  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(1)   0.2082  1  0.6482
#> Ljung-Box ARCH(5) 5.1941  5  0.3927
#>                         
#> Log-lik.(n=35): -43.0298

##estimate a log-variance specification with a log-ARCH(4)
##structure, an asymmetry/leverage term, a 10-period log(EWMA) as
##volatility proxy, and the log of the squareds of the conditioning
##regressors in the log-variance specification:
larch(e, arch=1:4, asym=1, log.ewma=list(length=10), vxreg=log(x^2))
#> 
#> Date: Fri Jan 16 14:55:58 2026 
#> Dependent var.: e 
#> Variance-Covariance: Robust (default) 
#> No. of observations: 30 
#> Sample: 11 to 40 
#> 
#> Log-variance equation:
#> 
#>                   coef std.error  t-stat p-value  
#> vconst       -0.891993  0.451570 -1.9753 0.07966 .
#> arch1        -0.195556  0.212075 -0.9221 0.38053  
#> arch2        -0.370430  0.203381 -1.8214 0.10188  
#> arch3        -0.115784  0.150598 -0.7688 0.46169  
#> arch4        -0.393912  0.235987 -1.6692 0.12942  
#> asym1        -0.114630  0.217382 -0.5273 0.61072  
#> logEqWMA(10)  4.263016  2.054292  2.0752 0.06779 .
#> vxreg1        0.072216  0.112665  0.6410 0.53751  
#> vxreg2       -0.105502  0.119036 -0.8863 0.39852  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                     Chi-sq df p-value
#> Ljung-Box AR(1)   0.028824  1  0.8652
#> Ljung-Box ARCH(5) 2.708187  5  0.7449
#>                         
#> Log-lik.(n=30): -36.3623
```
