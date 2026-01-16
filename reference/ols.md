# OLS estimation

OLS estimation with the QR decomposition and, for some options,
computation of variance-covariance matrices

## Usage

``` r
ols(y, x, untransformed.residuals=NULL, tol=1e-07, LAPACK=FALSE, method=3, 
  variance.spec=NULL, ...)
```

## Arguments

- y:

  numeric vector, the regressand

- x:

  numeric matrix, the regressors

- untransformed.residuals:

  `NULL` (default) or, when `ols` is used with `method=6`, a numeric
  vector containing the untransformed residuals

- tol:

  numeric value. The tolerance for detecting linear dependencies in the
  columns of the regressors, see the
  [`.lm.fit`](https://rdrr.io/r/stats/lmfit.html) function

- LAPACK:

  deprecated and ignored

- method:

  an integer, 1 to 6, that determines the estimation method

- variance.spec:

  `NULL` or a [`list`](https://rdrr.io/r/base/list.html) with items that
  specifies the log-variance model to be estimated, see
  [`arx`](http://moritzschwarz.org/gets/reference/arx.md)

- ...:

  further arguments (currently ignored)

## Details

`method = 1` or `method = 2` only returns the OLS coefficient estimates
together with the QR- information, the former being slightly faster.
`method=3` returns, in addition, the ordinary variance-covariance matrix
of the OLS estimator. `method=4` returns the White (1980)
heteroscedasticity robust variance-covariance matrix in addition to the
information returned by `method=3`, whereas `method=5` does the same
except that the variance-covariance matrix now is that of Newey and West
(1987). `method=6` undertakes OLS estimation of a log-variance model,
see Pretis, Reade and Sucarrat (2018, Section 4). Alternatively, for
`method` 1 to 5, a log-variance model is also estimated if
`variance.spec` is not `NULL`.

## Value

A list with items depending on `method`

## References

W. Newey and K. West (1987): 'A Simple Positive Semi-Definite,
Heteroskedasticity and Autocorrelation Consistent Covariance Matrix',
Econometrica 55, pp. 703-708.

F. Pretis, J. Reade and G. Sucarrat (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks', Journal of Statistical Software 86,
Issue 3, pp. 1-44, DOI: https://doi.org/10.18637/jss.v086.i03

H. White (1980): 'A Heteroskedasticity-Consistent Covariance Matrix and
a Direct Test for Heteroskedasticity', Econometrica 48, pp. 817-838.

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`.lm.fit`](https://rdrr.io/r/stats/lmfit.html),
[`qr`](https://rdrr.io/r/base/qr.html),
[`solve.qr`](https://rdrr.io/r/base/qr.html),
[`arx`](http://moritzschwarz.org/gets/reference/arx.md)
