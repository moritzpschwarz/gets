# Bootstrapped Jiao-Pretis-Schwarz Outlier Distortion Test

Implements the Jiao-Pretis-Schwarz bootstrap test for coefficient
distortion due to outliers by comparing coefficient estimates obtained
using OLS to estimates obtained using the robust IIS estimator
implemented using `isat`. Three bootstrap schemes are available - using
the original sample (not recommended), the clean (outlier-removed) data,
and using the clean (outlier-removed) sample with scaled cut-offs used
to detect outliers in IIS implemented using isat. See the referenced
Jiao-Pretis-Schwarz Paper below for more information.

## Usage

``` r
distorttestboot(x, nboot, clean.sample = TRUE, parametric = FALSE, scale.t.pval = 1, 
parallel.options = NULL, quantiles = c(0.90, 0.95, 0.99), ...)

##S3 printing method for objects of class 'distorttestboot':
# S3 method for class 'distorttestboot'
print(x, print.proportion = FALSE, ...)
```

## Arguments

- x:

  object of class
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md) or the
  output of the
  [`distorttest`](http://moritzschwarz.org/gets/reference/distorttest.md)
  function.

- nboot:

  numeric. Number of bootstrap replications. A high number of
  replications are recommended for final estimation (more than 200 at
  least).

- clean.sample:

  logical. Whether the outlier-removed sample should be used in
  resampling.

- parametric:

  logical. Whether to use a parametric bootstrap. Default is
  non-parametric (FALSE). Parametric currently not implemented for
  autoregressive models.

- scale.t.pval:

  numeric. Scaled target p-value (for selection) relative to the initial
  p-value used in isat. Default is 1. E.g. a value of 0.5 would scale an
  initial target p-value of 0.05 to 0.025.

- parallel.options:

  NULL (Default) or an integer, i.e. the number of cores/threads to be
  used for parallel computing (implemented w/makeCluster and parLapply).

- print.proportion:

  logical. Should the bootstraped Jiao-Pretis Outlier Proportion Test be
  printed. Default is FALSE.

- quantiles:

  numeric vector. Quantiles to be shown based on the bootstrapped
  results. Default is c(0.90, 0.95, 0.99).

- ...:

  Further arguments passed to
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md).

## Value

A list including an object of class `h-test`.

## References

Xiyu Jiao, Felix Pretis,and Moritz Schwarz. Testing for Coefficient
Distortion due to Outliers with an Application to the Economic Impacts
of Climate Change. Available at SSRN:
<https://www.ssrn.com/abstract=3915040> or
[doi:10.2139/ssrn.3915040](https://doi.org/10.2139/ssrn.3915040)

## Author

Xiyu Jiao <https://sites.google.com/view/xiyujiao>  
  
Felix Pretis <https://felixpretis.climateeconometrics.org/>  
  
Moritz Schwarz <https://moritzschwarz.org>  
  

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md)`, `[`distorttest`](http://moritzschwarz.org/gets/reference/distorttest.md)

## Examples

``` r
  if (FALSE) { # \dontrun{
  data(Nile)
  nile <- isat(Nile, sis=FALSE, iis=TRUE, plot=TRUE, t.pval=0.01)
  
  distorttest(nile)
  # bootstrap (with nboot = 5 to save time. Higher replications are recommended)
  distorttestboot(nile, nboot = 5)
  
  data("hpdata")
  # Another example with co-variates
  dat <- hpdata[,c("GD", "GNPQ", "FSDJ")]
  Y <- ts(dat$GD,start = 1959, frequency = 4)
  mxreg <- ts(dat[,c("GNPQ","FSDJ")],start = 1959, frequency = 4)
  m1 <- isat(y = Y, mc = TRUE, sis = FALSE, iis = TRUE)
  m2 <- isat(y = Y, mc = TRUE, sis = FALSE, iis = TRUE, ar = 1)
  m3 <- isat(y = Y, mxreg = mxreg, mc = TRUE, sis = FALSE, iis = TRUE)
  m4 <- isat(y = Y, mxreg = mxreg, mc = TRUE, sis = FALSE, iis = TRUE, ar = 1, t.pval = 0.01)
  distorttest(m1, coef = "all")
  distorttest(m2, coef = "all")
  distorttest(m3, coef = "GNPQ")
  distorttest(m4, coef = c("ar1", "FSDJ"))
  
  # bootstrap (with nboot = 5 to save time. Higher replications are recommended)
  distorttestboot(m1, nboot = 5)
  distorttestboot(m2, nboot = 5)
  distorttestboot(m3, nboot = 5)
  distorttestboot(m4, nboot = 5)
  distorttestboot(m4, nboot = 5, parametric = TRUE, scale.t.pval = 0.5)

  } # }
```
