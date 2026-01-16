# Variance of the coefficient path

Takes an 'isat' object returned by the `isat` function as input and
returns the coefficient path of the constant (and long-run equilibrium
if 'lr' is specified) together with its approximate variance and
standard errors. If `mxfull` and `mxbreak` are specified, then the
function returns the coefficient path of the user-specified variable.

## Usage

``` r
isatvar(x, lr=FALSE, conscorr=FALSE, effcorr=FALSE, mcor = 1, 
    mxfull = NULL, mxbreak=NULL)
```

## Arguments

- x:

  a 'gets' object obtained with the
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md) function

- lr:

  logical. If TRUE and 'x' contains autoregressive elements, then
  `isatvar` also returns the long-run equilibrium coefficient path with
  its variance and standard deviation. See Pretis (2015).

- conscorr:

  logical. If TRUE then the Johansen and Nielsen (2016)
  impulse-indicator consistency correction is applied to estimated
  residual variance.

- effcorr:

  logical. If TRUE then the Johansen and Nielsen (2016) m-step
  efficiency correction is applied to estimated standard errors of
  \`fixed' regressors.

- mcor:

  integer. The m-step efficiency correction factor, where m=mcor.

- mxfull:

  string. The name of the full-sample variable when constructing the
  coefficient path of user-specified break variables.

- mxbreak:

  string. The name of the break variables used to construct the
  coefficient path of user-specified break variables.

## Details

The function computes the approximate variance and standard errors of
the intercept term with structural breaks determined by
[`isat`](http://moritzschwarz.org/gets/reference/isat.md). This permits
hypothesis testing and plotting of approximate confidence intervals for
the intercept in the presence of structural breaks. For dynamic
autoregressive models in
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) the `lr`
argument returns the time-varying long-run equilibrium together with its
approximate variance and standard errors. If `mxfull` and `mxbreak` are
specified, then the function returns the coefficient path of the
user-specified variable, where `mxfull` denotes the ful-sample variable
name, to which the `mxbreak` variables are added. To correct for the
under-estimation of the residual variance, the argument `conscorr`
implements the Johansen and Nielsen (2016) consistency correction, and
`effcorr` adds the efficiency correction for standard errors on fixed
regressors which are not selected over.

## Value

If `lr=FALSE`: A Tx4 matrix (with T = number of observations) where the
first column denotes the coefficient path relative to the full sample
coefficient, the second column the coefficient path of the intercept,
the third the approximate variance of the coefficient path, and the
fourth column the approximate standard errors of the coefficient path.
If `lr=TRUE`: A Tx7 matrix where the first four columns are identical to
the `lr=FALSE` case, and the additional columns denote the long-run
equilibrium coefficient path, together with the approximate variance and
standard errors of the long-run equilibrium coefficient path.

## References

Pretis, F. (2015): 'Testing for time-varying predictive accuracy using
bias-corrected indicator saturation'. Oxford Department of Economics
???orking Paper.

Johansen, S., & Nielsen, B. (2016): 'Asymptotic theory of outlier
detection algorithms for linear time series regression models.'
Scandinavian Journal of Statistics, 43(2), 321-348.

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>  
James Reade, <https://sites.google.com/site/jjamesreade/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`coef.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`plot.gets`](http://moritzschwarz.org/gets/reference/coef.gets.md),
[`biascorr`](http://moritzschwarz.org/gets/reference/biascorr.md),
[`isattest`](http://moritzschwarz.org/gets/reference/isattest.md)

## Examples

``` r
##Variance in presence of a break
#nile <- as.zoo(Nile)
#isat.nile <- isat(nile, sis=TRUE, iis=FALSE, plot=FALSE, t.pval=0.005)
#var <- isatvar(isat.nile)

#plot(nile)
#lines(isat.nile$mean.fit, col="red")
#lines(isat.nile$mean.fit + 2*var$const.se, col="blue", lty=3)
#lines(isat.nile$mean.fit - 2*var$const.se, col="blue", lty=3)

##Variance when there is no break
#set.seed(1)
#x <- as.zoo(rnorm(100, 0, 1))
#isat.x <- isat(x, sis=TRUE, iis=FALSE, plot=TRUE, t.pval=0.005)
#var.x <- isatvar(isat.x)

#plot(x)
#lines(isat.x$mean.fit, col="red")
#lines(isat.x$mean.fit + 2*var.x[,2], col="blue", lty=3)
#lines(isat.x$mean.fit - 2*var.x[,2], col="blue", lty=3)

##Variance of the long-run equilibrium coefficient path

#nile <- as.zoo(Nile)
#isat.nile <- isat(nile, sis=TRUE, iis=FALSE, plot=TRUE, t.pval=0.005, ar=1:2)
#var <- isatvar(isat.nile, lr=TRUE)
```
