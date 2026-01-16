# Bias-correction of coefficients following general-to-specific model selection

Takes a vector of coefficients (valid for orthogonal variables), their
standard errors, the significance level the variables were selected at,
and the sample size, to return bias-corrected coefficient estimates to
account for the bias induced by model selection.

## Usage

``` r
biascorr(b, b.se, p.alpha, T)
```

## Arguments

- b:

  a Kx1 vector of coefficients.

- b.se:

  a Kx1 vector of standard errors of the coefficients in 'b'.

- p.alpha:

  numeric value between 0 and 1, the significance level at which
  selection was conducted.

- T:

  integer, the sample size of the original model selection regression.

## Details

The function computes the bias-corrected estimates of coefficients in
regression models post general-to-specific model selection using the
approach by Hendry and Krolzig (2005). The results are valid for
orthogonal regressors only. Bias correction can be applied to the
coefficient path in
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) models where
the only additional covariate besides indicators is an intercept - see
Pretis (2015).

## Value

Returns a Kx3 matrix, where the first column lists the original
coefficients, the second column the one-step corrected coefficients, and
the third column the two-step bias-corrected coefficients.

## References

Hendry, D.F. and Krolzig, H.M. (2005): 'The properties of automatic Gets
modelling'. Economic Journal, 115, C32-C61.

Pretis, F. (2015): 'Testing for time-varying predictive accuracy using
bias-corrected indicator saturation'. Oxford Department of Economics
Discussion Paper.

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`coef.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`plot.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`isatvar`](http://moritzschwarz.org/gets/reference/isatvar.md),
[`isattest`](http://moritzschwarz.org/gets/reference/isattest.md)

## Examples

``` r
###Bias-correction of the coefficient path of the Nile data
#nile <- as.zoo(Nile)
#isat.nile <- isat(nile, sis=TRUE, iis=FALSE, plot=TRUE, t.pval=0.005)
#var <- isatvar(isat.nile)
#biascorr(b=var$const.path, b.se=var$const.se, p.alpha=0.005, T=length(var$const.path))

##Bias-correction of the coefficient path on artificial data
#set.seed(123)
#d <- matrix(0,100,1)
#d[35:55] <- 1
#e <- rnorm(100, 0, 1)
#y <- d*1  +e
  
#ys <- isat(y, sis=TRUE, iis=FALSE, t.pval=0.01)
#var <- isatvar(ys)
#biascorr(b=var$const.path, b.se=var$const.se, p.alpha=0.01, T=length(var$const.path))
```
