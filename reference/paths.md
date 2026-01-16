# Extraction functions for 'arx', 'gets' and 'isat' objects

Extraction functions for objects of class 'arx', 'gets' and 'isat'

## Usage

``` r
paths(object, ...)
terminals(object, ...)
rsquared(object, adjusted=FALSE, ...)
```

## Arguments

- object:

  an object of class 'arx', 'gets' or 'isat'

- adjusted:

  `logical`. If `TRUE` the adjusted R-squared is returned

- ...:

  additional arguments

## Details

`paths` and `terminals` can only be applied on objects of class 'gets'
and 'isat'

## Value

- `paths`::

  a [`list`](https://rdrr.io/r/base/list.html) with the paths searched
  (each number refers to a regressor in the GUM)

- `terminals`::

  a [`list`](https://rdrr.io/r/base/list.html) with the terminal models
  (each number refers to a regressor in the GUM)

- `rsquared`::

  a [`numeric`](https://rdrr.io/r/base/numeric.html), the R-squared of
  the regression, or adjusted R-squared if `adjusted` is set to `TRUE`

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
##Simulate from an AR(1):
set.seed(123)
y <- arima.sim(list(ar=0.4), 50)

##Simulate four independent Gaussian regressors:
xregs <- matrix(rnorm(4*50), 50, 4)

##estimate an AR(2) with intercept and four conditioning
##regressors in the mean:
mymod <- arx(y, mc=TRUE, ar=1:2, mxreg=xregs)
rsquared(mymod)
#> [1] 0.1520805
rsquared(mymod, adjusted=TRUE)
#> [1] 0.02799468

##General-to-Specific (GETS) modelling of the mean:
meanmod <- getsm(mymod)
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> mconst       1    0  0.042884  0.141657  0.3027 0.76362  
#> ar1          2    0  0.345223  0.156817  2.2014 0.03339 *
#> ar2          3    0  0.052468  0.156733  0.3348 0.73951  
#> mxreg1       4    0 -0.140760  0.165009 -0.8530 0.39859  
#> mxreg2       5    0 -0.089124  0.145349 -0.6132 0.54315  
#> mxreg3       6    0 -0.077072  0.145620 -0.5293 0.59947  
#> mxreg4       7    0 -0.225367  0.169838 -1.3270 0.19187  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> 
#> Diagnostics:
#> 
#>                    Chi-sq df p-value
#> Ljung-Box AR(3)   2.97870  3 0.39492
#> Ljung-Box ARCH(1) 0.14075  1 0.70754
#> 
#> 6 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 
#>   Path 1: 1 3 6 5 4 7 
#>   Path 2: 3 1 6 5 4 7 
#>   Path 3: 4 1 3 6 5 7 
#>   Path 4: 5 3 1 6 4 7 
#>   Path 5: 6 3 1 5 4 7 
#>   Path 6: 7 1 3 6 4 5 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.749419 -64.05045 48 1
#> 
#> Retained regressors (final model):
#> 
#>   ar1 
rsquared(meanmod)
#> [1] 0.09401861
rsquared(meanmod, adjusted=TRUE)
#> [1] 0.09401861

##extract the paths searched:
paths(meanmod)
#> [[1]]
#> [1] 1 3 6 5 4 7
#> 
#> [[2]]
#> [1] 3 1 6 5 4 7
#> 
#> [[3]]
#> [1] 4 1 3 6 5 7
#> 
#> [[4]]
#> [1] 5 3 1 6 4 7
#> 
#> [[5]]
#> [1] 6 3 1 5 4 7
#> 
#> [[6]]
#> [1] 7 1 3 6 4 5
#> 

##extract the terminal models:
terminals(meanmod)
#> [[1]]
#> [1] 2
#> 
```
