# Convert to 'lm' object

Convert 'arx'/'gets'/'isat' object to 'lm' object

## Usage

``` r
as.lm(object)
```

## Arguments

- object:

  object of class
  [`arx`](http://moritzschwarz.org/gets/reference/arx.md),
  [`gets`](http://moritzschwarz.org/gets/reference/gets.md) or
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Value

Object of class [`lm`](https://rdrr.io/r/stats/lm.html)

## Author

Moritz Schwarz, <https://www.inet.ox.ac.uk/people/moritz-schwarz>  
Genaro Sucarrat <https://www.sucarrat.net/>  
  

## See also

[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`gets`](http://moritzschwarz.org/gets/reference/gets.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`lm`](https://rdrr.io/r/stats/lm.html)

## Examples

``` r
##generate data, estimate model of class 'arx':
set.seed(123)
y <- rnorm(30)
arxmod <- arx(y, mc=TRUE, ar=1:3)
as.lm(arxmod)
#> 
#> Call:
#> lm(formula = y ~ . - 1, data = yx)
#> 
#> Coefficients:
#>   mconst       ar1       ar2       ar3  
#> -0.06035   0.03829  -0.15922   0.37697  
#> 

##from 'gets' to 'lm':
getsmod <- getsm(arxmod, keep=1)
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> mconst       1    1 -0.060347  0.185054 -0.3261 0.74729  
#> ar1          2    0  0.038286  0.191216  0.2002 0.84306  
#> ar2          3    0 -0.159216  0.192118 -0.8287 0.41577  
#> ar3          4    0  0.376970  0.194771  1.9354 0.06532 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(4)   2.4348  4 0.65635
#> Ljung-Box ARCH(1) 2.4042  1 0.12101
#> 
#> 3 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 
#>   Path 1: 2 3 4 
#>   Path 2: 3 2 4 
#>   Path 3: 4 2 3 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.883843 -37.28396 27 1
#> 
#> Retained regressors (final model):
#> 
#>   mconst 
as.lm(getsmod)
#> 
#> Call:
#> lm(formula = y ~ . - 1, data = yx)
#> 
#> Coefficients:
#>   mconst  
#> -0.08078  
#> 

##from 'isat' to 'lm':
isatmod <- isat(y)
#> 
#> SIS block 1 of 2:
#> 15 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 9 
#> 10 
#> 11 
#> 12 
#> 13 
#> 14 
#> 15 
#> 
#> SIS block 2 of 2:
#> 14 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 9 
#> 10 
#> 11 
#> 12 
#> 13 
#> 14 
#> 
#> GETS of union of retained SIS variables... 
#> 
#> GETS of union of ALL retained variables...
as.lm(isatmod)
#> 
#> Call:
#> lm(formula = y ~ . - 1, data = yx)
#> 
#> Coefficients:
#>  mconst  
#> -0.0471  
#> 
```
