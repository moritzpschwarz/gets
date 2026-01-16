# Generalised Method of Moment (GMM) estimation of linear models

Generalised Method of Moment (GMM) estimation of linear models with
either ordinary (homoscedastic error) or robust (heteroscedastic error)
coefficient-covariance, see Hayashi (2000) chapter 3.

## Usage

``` r
gmm(y, x, z, tol = .Machine$double.eps,
  weighting.matrix = c("efficient", "2sls", "identity"),
  vcov.type = c("ordinary", "robust"))
```

## Arguments

- y:

  numeric vector, the regressand

- x:

  numeric matrix, the regressors

- z:

  numeric matrix, the instruments

- tol:

  numeric value. The tolerance for detecting linear dependencies in the
  columns of the matrices that are inverted, see the
  [`solve`](https://rdrr.io/r/base/solve.html) function

- weighting.matrix:

  a character that determines the weighting matrix to bee used, see
  "details"

- vcov.type:

  a character that determines the expression for the
  coefficient-covariance, see "details"

## Details

`weighting.matrix = "identity"` corresponds to the Instrumental
Variables (IV) estimator, `weighting.matrix = "2sls"` corresponds to the
2 Stage Least Squares (2SLS) estimator, whereas
`weighting.matrix = "efficient"` corresponds to the efficient GMM
estimator, see chapter 3 in Hayashi(2000).

`vcov.type = "ordinary"` returns the ordinary expression for the
coefficient-covariance, which is valid under conditionally homoscedastic
errors. `vcov.type = "robust"` returns an expression that is also valid
under conditional heteroscedasticity, see chapter 3 in Hayashi (2000).

## Value

A list with, amongst other, the following items:

- n:

  number of observations

- k:

  number of regressors

- df:

  degrees of freedom, i.e. n-k

- coefficients:

  a vector with the coefficient estimates

- fit:

  a vector with the fitted values

- residuals:

  a vector with the residuals

- residuals2:

  a vector with the squared residuals

- rss:

  the residual sum of squares

- sigma2:

  the regression variance

- vcov:

  the coefficient-covariance matrix

- logl:

  the normal log-likelihood

## References

F. Hayashi (2000): 'Econometrics'. Princeton: Princeton University Press

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`solve`](https://rdrr.io/r/base/solve.html),
[`ols`](http://moritzschwarz.org/gets/reference/ols.md)

## Examples

``` r
##generate data where regressor is correlated with error:
set.seed(123) #for reproducibility
n <- 100
z1 <- rnorm(n) #instrument
eps <- rnorm(n) #ensures cor(z,eps)=0
x1 <- 0.5*z1 + 0.5*eps #ensures cor(x,eps) is strong
y <- 0.4 + 0.8*x1 + eps #the dgp
cor(x1, eps) #check correlatedness of regressor
#> [1] 0.7109826
cor(z1, eps) #check uncorrelatedness of instrument
#> [1] -0.04953215

x <- cbind(1,x1) #regressor matrix
z <- cbind(1,z1) #matrix with instruments

##efficient gmm estimation:
mymod <- gmm(y, x, z)
mymod$coefficients
#> [1] 0.2915040 0.6892453

##ols (for comparison):
mymod <- ols(y,x)
mymod$coefficients
#> [1] 0.3015429 1.8605825
```
