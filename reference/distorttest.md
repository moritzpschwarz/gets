# Jiao-Pretis-Schwarz Outlier Distortion Test

Implements the Jiao-Pretis-Schwarz test for coefficient distortion due
to outliers by comparing coefficient estimates obtained using OLS to
estimates obtained using the robust IIS estimator implemented using
`isat`. See the referenced Jiao-Pretis-Schwarz Paper below for more
information.

## Usage

``` r
distorttest(x, coef = "all")
```

## Arguments

- x:

  object of class
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md)

- coef:

  Either "all" (Default) to test the distortion on all coefficients or a
  character vector of explanatory variable names.

## Value

Object of class
[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

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

[`isat`](http://moritzschwarz.org/gets/reference/isat.md)`, `[`distorttestboot`](http://moritzschwarz.org/gets/reference/distorttestboot.md)

## Examples

``` r
if (FALSE) { # \dontrun{  
data(Nile)
nile <- isat(Nile, sis=FALSE, iis=TRUE, plot=TRUE, t.pval=0.01)
distorttest(nile)

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
 } # } 
```
