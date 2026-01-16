# Estimate an AR-X model with log-ARCH-X errors

Estimation by OLS, two-step OLS if a variance specification is
specified: In the first the mean specification (AR-X) is estimated,
whereas in the second step the log-variance specification (log-ARCH-X)
is estimated.

The AR-X mean specification can contain an intercept, AR-terms, lagged
moving averages of the regressand and other conditioning covariates
('X'). The log-variance specification can contain log-ARCH terms,
asymmetry or 'leverage' terms, log(EqWMA) where EqWMA is a lagged
equally weighted moving average of past squared residuals (a volatility
proxy) and other conditioning covariates ('X').

## Usage

``` r
arx(y, mc=TRUE, ar=NULL, ewma=NULL, mxreg=NULL, vc=FALSE,
  arch=NULL, asym=NULL, log.ewma=NULL, vxreg=NULL, zero.adj=NULL,
  vc.adj=TRUE, vcov.type=c("ordinary", "white", "newey-west"),
  qstat.options=NULL, normality.JarqueB=FALSE, user.estimator=NULL,
  user.diagnostics=NULL, tol=1e-07, LAPACK=FALSE, singular.ok=TRUE,
  plot=NULL)
```

## Arguments

- y:

  `numeric` vector, time-series or
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object. Missing values
  in the beginning and at the end of the series is allowed, as they are
  removed with the [`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html)
  command

- mc:

  `logical`. `TRUE` (default) includes an intercept in the mean
  specification, whereas `FALSE` does not

- ar:

  either `NULL` (default) or an integer vector, say, `c(2,4)` or `1:4`.
  The AR-lags to include in the mean specification. If `NULL`, then no
  lags are included

- ewma:

  either `NULL` (default) or a
  [`list`](https://rdrr.io/r/base/list.html) with arguments sent to the
  [`eqwma`](http://moritzschwarz.org/gets/reference/eqwma.md) function.
  In the latter case a lagged moving average of `y` is included as a
  regressor

- mxreg:

  either `NULL` (default) or a numeric vector or matrix, say, a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object, of conditioning
  variables. Note that, if both `y` and `mxreg` are
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) objects, then their
  samples are chosen to match

- vc:

  `logical`. `TRUE` includes an intercept in the log-variance
  specification, whereas `FALSE` (default) does not. If the log-variance
  specification contains any other item but the log-variance intercept,
  then vc is set to `TRUE`

- arch:

  either `NULL` (default) or an integer vector, say, `c(1,3)` or `2:5`.
  The log-ARCH lags to include in the log-variance specification

- asym:

  either `NULL` (default) or an integer vector, say, `c(1)` or `1:3`.
  The asymmetry (i.e. 'leverage') terms to include in the log-variance
  specification

- log.ewma:

  either `NULL` (default) or a vector of the lengths of the volatility
  proxies, see
  [`leqwma`](http://moritzschwarz.org/gets/reference/eqwma.md)

- vxreg:

  either `NULL` (default) or a numeric vector or matrix, say, a
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object, of conditioning
  variables. If both `y` and `mxreg` are
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) objects, then their
  samples are chosen to match.

- zero.adj:

  `NULL` (default) or a strictly positive `numeric` scalar. If `NULL`,
  the zeros in the squared residuals are replaced by the 10 percent
  quantile of the non-zero squared residuals. If `zero.adj` is a
  strictly positive `numeric` scalar, then this value is used to replace
  the zeros of the squared residuals.

- vc.adj:

  `logical`. If `TRUE` (default), then the log-variance intercept is
  adjusted by the estimate of E\[ln(z^2)\], where z is the standardised
  error. This adjustment is needed for the conditional scale to be equal
  to the conditional standard deviation. If `FALSE`, then the
  log-variance intercept is not adjusted

- vcov.type:

  `character` vector, "ordinary" (default), "white" or "newey-west". If
  "ordinary", then the ordinary variance-covariance matrix is used for
  inference. If "white", then the White (1980) heteroscedasticity-robust
  matrix is used. If "newey-west", then the Newey and West (1987)
  heteroscedasticity and autocorrelation-robust matrix is used

- qstat.options:

  `NULL` (default) or an integer vector of length two, say, `c(1,1)`.
  The first value sets the lag-order of the AR diagnostic test, whereas
  the second value sets the lag-order of the ARCH diagnostic test. If
  `NULL`, then the two values of the vector are set automatically

- normality.JarqueB:

  `FALSE` (default) or `TRUE`. If `TRUE`, then the results of the Jarque
  and Bera (1980) test for non-normality in the residuals are included
  in the estimation results.

- user.estimator:

  `NULL` (default) or a [`list`](https://rdrr.io/r/base/list.html) with
  one entry, `name`, containing the name of the user-defined estimator.
  Additional items, if any, are passed on as arguments to the estimator
  in question

- user.diagnostics:

  `NULL` (default) or a [`list`](https://rdrr.io/r/base/list.html) with
  two entries, `name` and `pval`, see the `user.fun` argument in
  [`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md)

- tol:

  `numeric` value (`default = 1e-07`). The tolerance for detecting
  linear dependencies in the columns of the regressors (see
  [`qr`](https://rdrr.io/r/base/qr.html) function). Only used if
  `LAPACK` is `FALSE` (default) and `user.estimator` is `NULL`.

- LAPACK:

  `logical`. If `TRUE`, then use LAPACK. If `FALSE` (default), then use
  LINPACK (see [`qr`](https://rdrr.io/r/base/qr.html) function). Only
  used if `user.estimator` is `NULL`.

- singular.ok:

  `logical`. If `TRUE` (default), the regressors are checked for
  singularity, and the ones causing it are automatically removed.

- plot:

  `NULL` or `logical`. If `TRUE`, the fitted values and the residuals
  are plotted. If `NULL` (default), then the value set by
  [`options`](https://rdrr.io/r/base/options.html) determines whether a
  plot is produced or not.

## Details

For an overview of the AR-X model with log-ARCH-X errors, see Pretis,
Reade and Sucarrat (2018):
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03) .  

The arguments `user.estimator` and `user.diagnostics` enables the
specification of user-defined estimators and user-defined diagnostics.
To this end, the principles of the same arguments in
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) are
followed, see its documentation under "Details", and Sucarrat (2020):
<https://journal.r-project.org/archive/2021/RJ-2021-024/>.

## Value

A list of class 'arx'

## References

C. Jarque and A. Bera (1980): 'Efficient Tests for Normality,
Homoscedasticity and Serial Independence'. Economics Letters 6, pp.
255-259.
[doi:10.1016/0165-1765(80)90024-5](https://doi.org/10.1016/0165-1765%2880%2990024-5)

Felix Pretis, James Reade and Genaro Sucarrat (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44.
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03)

Genaro Sucarrat (2020): 'User-Specified General-to-Specific and
Indicator Saturation Methods'. The R Journal 12:2, pages 388-401.
<https://journal.r-project.org/archive/2021/RJ-2021-024/>

Halbert White (1980): 'A Heteroskedasticity-Consistent Covariance Matrix
Estimator and a Direct Test for Heteroskedasticity', Econometrica 48,
pp. 817-838.

Whitney K. Newey and Kenned D. West (1987): 'A Simple, Positive
Semi-Definite, Heteroskedasticity and Autocorrelation Consistent
Covariance Matrix', Econometrica 55, pp. 703-708.

## Author

|                  |     |                                                   |
|------------------|-----|---------------------------------------------------|
| Jonas Kurle:     |     | <https://www.jonaskurle.com/>                     |
| Moritz Schwarz:  |     | <https://www.inet.ox.ac.uk/people/moritz-schwarz> |
| Genaro Sucarrat: |     | <https://www.sucarrat.net/>                       |

## See also

Extraction functions (mostly S3 methods):
[`coef.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),
[`ES`](http://moritzschwarz.org/gets/reference/ES.md),
[`fitted.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),
[`plot.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),  
[`print.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),
[`recursive`](http://moritzschwarz.org/gets/reference/recursive.md),
[`residuals.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),
[`sigma.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),
[`rsquared`](http://moritzschwarz.org/gets/reference/paths.md),  
[`summary.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md),
[`VaR`](http://moritzschwarz.org/gets/reference/ES.md) and
[`vcov.arx`](http://moritzschwarz.org/gets/reference/coef.arx.md)  

Related functions:
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
##Simulate from an AR(1):
set.seed(123)
y <- arima.sim(list(ar=0.4), 70)

##estimate an AR(2) with intercept:
arx(y, mc=TRUE, ar=1:2)
#> 
#> Date: Fri Jan 16 14:36:45 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 68 
#> Sample: 3 to 70 
#> 
#> Mean equation:
#> 
#>             coef std.error  t-stat p-value  
#> mconst  0.013715  0.115112  0.1191 0.90553  
#> ar1     0.323324  0.125262  2.5812 0.01211 *
#> ar2    -0.040814  0.124257 -0.3285 0.74361  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                      Chi-sq df p-value
#> Ljung-Box AR(3)   3.8157196  3  0.2821
#> Ljung-Box ARCH(1) 0.0087708  1  0.9254
#>                           
#> SE of regression   0.94884
#> R-squared          0.09647
#> Log-lik.(n=68)   -91.41661

##Simulate four independent Gaussian regressors:
xregs <- matrix(rnorm(4*70), 70, 4)

##estimate an AR(2) with intercept and four conditioning
##regressors in the mean:
arx(y, ar=1:2, mxreg=xregs)
#> 
#> Date: Fri Jan 16 14:36:45 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 68 
#> Sample: 3 to 70 
#> 
#> Mean equation:
#> 
#>             coef std.error  t-stat p-value  
#> mconst -0.020030  0.117600 -0.1703 0.86532  
#> ar1     0.314052  0.130041  2.4150 0.01875 *
#> ar2    -0.058036  0.129614 -0.4478 0.65591  
#> mxreg1 -0.045191  0.126042 -0.3585 0.72118  
#> mxreg2  0.108048  0.126116  0.8567 0.39494  
#> mxreg3  0.159350  0.133675  1.1921 0.23785  
#> mxreg4  0.145276  0.114408  1.2698 0.20898  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                    Chi-sq df p-value
#> Ljung-Box AR(3)   2.92995  3  0.4026
#> Ljung-Box ARCH(1) 0.17116  1  0.6791
#>                           
#> SE of regression   0.95304
#> R-squared          0.14454
#> Log-lik.(n=68)   -89.71711

##estimate a log-variance specification with a log-ARCH(4)
##structure:
arx(y, mc=FALSE, arch=1:4)
#> 
#> Date: Fri Jan 16 14:36:45 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Sample: 1 to 70 
#> 
#> Log-variance equation:
#> 
#>             coef std.error  t-stat p-value
#> vconst -0.334531  0.471100  0.5042  0.4776
#> arch1   0.040073  0.128641  0.3115  0.7565
#> arch2  -0.076960  0.133758 -0.5754  0.5672
#> arch3  -0.124580  0.133945 -0.9301  0.3560
#> arch4  -0.058274  0.134204 -0.4342  0.6657
#> 
#> Diagnostics and fit:
#> 
#>                   Chi-sq df p-value  
#> Ljung-Box AR(1)   5.8181  1 0.01586 *
#> Ljung-Box ARCH(5) 3.6677  5 0.59818  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#>                           
#> SE of regression   0.97479
#> R-squared         -0.00002
#> Log-lik.(n=66)   -91.89688

##estimate a log-variance specification with a log-ARCH(4)
##structure and an asymmetry/leverage term:
arx(y, mc=FALSE, arch=1:4, asym=1)
#> 
#> Date: Fri Jan 16 14:36:45 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Sample: 1 to 70 
#> 
#> Log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst -0.123582  0.468464  0.0696 0.79193  
#> arch1   0.246437  0.174802  1.4098 0.16376  
#> arch2  -0.071564  0.131724 -0.5433 0.58895  
#> arch3  -0.130442  0.131916 -0.9888 0.32672  
#> arch4  -0.018810  0.134119 -0.1402 0.88893  
#> asym1  -0.378539  0.221001 -1.7128 0.09191 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                   Chi-sq df p-value  
#> Ljung-Box AR(1)   5.2578  1 0.02185 *
#> Ljung-Box ARCH(5) 1.4461  5 0.91921  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#>                           
#> SE of regression   0.97479
#> R-squared         -0.00002
#> Log-lik.(n=66)   -95.13333

##estimate a log-variance specification with a log-ARCH(4)
##structure, an asymmetry or leverage term, a 10-period log(EWMA) as
##volatility proxy, and the log of the squareds of the conditioning
##regressors in the log-variance specification:
arx(y, mc=FALSE,
  arch=1:4, asym=1, log.ewma=list(length=10), vxreg=log(xregs^2))
#> 
#> Date: Fri Jan 16 14:36:45 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Sample: 1 to 70 
#> 
#> Log-variance equation:
#> 
#>                   coef std.error  t-stat p-value
#> vconst        0.487403  0.749811  0.4225  0.5157
#> arch1         0.267782  0.202055  1.3253  0.1912
#> arch2        -0.037977  0.146493 -0.2592  0.7965
#> arch3        -0.083006  0.147989 -0.5609  0.5774
#> arch4         0.057241  0.157793  0.3628  0.7183
#> asym1        -0.363850  0.249324 -1.4593  0.1509
#> logEqWMA(10) -1.111548  1.102564 -1.0081  0.3183
#> vxreg1       -0.122789  0.184280 -0.6663  0.5083
#> vxreg2        0.062479  0.189227  0.3302  0.7427
#> vxreg3        0.185292  0.167040  1.1093  0.2727
#> vxreg4        0.069712  0.148582  0.4692  0.6410
#> 
#> Diagnostics and fit:
#> 
#>                   Chi-sq df p-value  
#> Ljung-Box AR(1)   4.8085  1 0.02832 *
#> Ljung-Box ARCH(5) 4.1348  5 0.53018  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#>                           
#> SE of regression   0.97479
#> R-squared         -0.00002
#> Log-lik.(n=60)   -90.89802

##estimate an AR(2) with intercept and four conditioning regressors
##in the mean, and a log-variance specification with a log-ARCH(4)
##structure, an asymmetry or leverage term, a 10-period log(EWMA) as
##volatility proxy, and the log of the squareds of the conditioning
##regressors in the log-variance specification:
arx(y, ar=1:2, mxreg=xregs,
  arch=1:4, asym=1, log.ewma=list(length=10), vxreg=log(xregs^2))
#> 
#> Date: Fri Jan 16 14:36:45 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 68 
#> Sample: 3 to 70 
#> 
#> Mean equation:
#> 
#>             coef std.error  t-stat p-value  
#> mconst -0.020030  0.117600 -0.1703 0.86532  
#> ar1     0.314052  0.130041  2.4150 0.01875 *
#> ar2    -0.058036  0.129614 -0.4478 0.65591  
#> mxreg1 -0.045191  0.126042 -0.3585 0.72118  
#> mxreg2  0.108048  0.126116  0.8567 0.39494  
#> mxreg3  0.159350  0.133675  1.1921 0.23785  
#> mxreg4  0.145276  0.114408  1.2698 0.20898  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log-variance equation:
#> 
#>                    coef  std.error  t-stat p-value  
#> vconst       -0.6418794  0.6313424  1.0337 0.30930  
#> arch1         0.0964675  0.1671815  0.5770 0.56668  
#> arch2         0.0100427  0.1557870  0.0645 0.94887  
#> arch3        -0.0358162  0.1435422 -0.2495 0.80405  
#> arch4        -0.0870830  0.1454666 -0.5986 0.55228  
#> asym1        -0.4784833  0.2605120 -1.8367 0.07258 .
#> logEqWMA(10) -0.3209869  0.9299380 -0.3452 0.73151  
#> vxreg1       -0.1216583  0.1350725 -0.9007 0.37235  
#> vxreg2        0.0616220  0.1342431  0.4590 0.64833  
#> vxreg3       -0.0017352  0.1265075 -0.0137 0.98911  
#> vxreg4       -0.0216166  0.1155589 -0.1871 0.85242  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   3.7660  3  0.2879
#> Ljung-Box ARCH(5) 1.1414  5  0.9504
#>                           
#> SE of regression   0.95304
#> R-squared          0.14454
#> Log-lik.(n=58)   -75.68205
```
