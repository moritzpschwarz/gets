# Convert an object to class 'arx'

The function `as.arx` is a generic function and its methods returns an
object of class [`arx`](http://moritzschwarz.org/gets/reference/arx.md).

## Usage

``` r
as.arx(object, ...)

##S3 method for objects of class 'lm':
# S3 method for class 'lm'
as.arx(object, ...)
```

## Arguments

- object:

  object of class [`lm`](https://rdrr.io/r/stats/lm.html)

- ...:

  arguments passed on to and from other methods

## Value

Object of class [`arx`](http://moritzschwarz.org/gets/reference/arx.md)

## Author

Genaro Sucarrat <http://www.sucarrat.net/>  
  

## See also

[`lm`](https://rdrr.io/r/stats/lm.html),
[`arx`](http://moritzschwarz.org/gets/reference/arx.md)

## Examples

``` r
##generate some data:
set.seed(123) #for reproducibility
y <- rnorm(30) #generate Y
x <- matrix(rnorm(30*10), 30, 10) #create matrix of Xs

##typical situation:
mymodel <- lm(y ~ x)
as.arx(mymodel)
#> 
#> Date: Fri Jan 16 14:55:43 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 30 
#> Sample: 1 to 30 
#> 
#> Mean equation:
#> 
#>               coef   std.error  t-stat p-value  
#> mconst  0.27005590  0.21026283  1.2844 0.21445  
#> x1     -0.61303927  0.28160750 -2.1769 0.04230 *
#> x2      0.13398941  0.22947573  0.5839 0.56616  
#> x3      0.30619954  0.21734292  1.4088 0.17504  
#> x4     -0.00018761  0.19034597 -0.0010 0.99922  
#> x5      0.16595175  0.20992401  0.7905 0.43897  
#> x6     -0.16893171  0.21399989 -0.7894 0.43962  
#> x7      0.51949160  0.22562893  2.3024 0.03279 *
#> x8      0.32756857  0.20626559  1.5881 0.12877  
#> x9     -0.51817835  0.24477483 -2.1170 0.04768 *
#> x10    -0.01454824  0.19954250 -0.0729 0.94264  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                       Chi-sq df p-value
#> Ljung-Box AR(1)   0.06042745  1  0.8058
#> Ljung-Box ARCH(1) 0.00067615  1  0.9793
#>                           
#> SE of regression   0.93728
#> R-squared          0.40197
#> Log-lik.(n=30)   -35.12486
                                 
##use hetero-robust vcov:
as.arx(mymodel, vcov.type="white")
#> 
#> Date: Fri Jan 16 14:55:43 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: White (1980) 
#> No. of observations (mean eq.): 30 
#> Sample: 1 to 30 
#> 
#> Mean equation:
#> 
#>               coef   std.error  t-stat p-value  
#> mconst  0.27005590  0.13837697  1.9516 0.06589 .
#> x1     -0.61303927  0.27212423 -2.2528 0.03629 *
#> x2      0.13398941  0.20116413  0.6661 0.51337  
#> x3      0.30619954  0.22901348  1.3370 0.19700  
#> x4     -0.00018761  0.14658909 -0.0013 0.99899  
#> x5      0.16595175  0.14962022  1.1092 0.28121  
#> x6     -0.16893171  0.14592354 -1.1577 0.26134  
#> x7      0.51949160  0.19021354  2.7311 0.01327 *
#> x8      0.32756857  0.16763602  1.9540 0.06558 .
#> x9     -0.51817835  0.22303637 -2.3233 0.03141 *
#> x10    -0.01454824  0.11859578 -0.1227 0.90366  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                       Chi-sq df p-value
#> Ljung-Box AR(1)   0.06042745  1  0.8058
#> Ljung-Box ARCH(1) 0.00067615  1  0.9793
#>                           
#> SE of regression   0.93728
#> R-squared          0.40197
#> Log-lik.(n=30)   -35.12486

##add ar-dynamics:
as.arx(mymodel, ar=1:2)
#> 
#> Date: Fri Jan 16 14:55:43 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 28 
#> Sample: 3 to 30 
#> 
#> Mean equation:
#> 
#>             coef std.error  t-stat p-value  
#> mconst  0.312270  0.241746  1.2917 0.21600  
#> ar1    -0.167514  0.340202 -0.4924 0.62957  
#> ar2    -0.199858  0.266832 -0.7490 0.46544  
#> x1     -0.592040  0.313247 -1.8900 0.07824 .
#> x2      0.080545  0.318537  0.2529 0.80381  
#> x3      0.336700  0.243410  1.3833 0.18683  
#> x4      0.087082  0.252641  0.3447 0.73511  
#> x5      0.180548  0.240054  0.7521 0.46362  
#> x6     -0.153325  0.269165 -0.5696 0.57736  
#> x7      0.497405  0.251823  1.9752 0.06694 .
#> x8      0.282720  0.231063  1.2236 0.23999  
#> x9     -0.515726  0.337073 -1.5300 0.14683  
#> x10    -0.181715  0.291814 -0.6227 0.54283  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                       Chi-sq df p-value
#> Ljung-Box AR(3)   1.25213112  3  0.7405
#> Ljung-Box ARCH(1) 0.00085579  1  0.9767
#>                           
#> SE of regression   1.01385
#> R-squared          0.44128
#> Log-lik.(n=28)   -33.61550

##add log-variance specification:
as.arx(mymodel, arch=1:2)
#> 
#> Date: Fri Jan 16 14:55:43 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 30 
#> Sample: 1 to 30 
#> 
#> Mean equation:
#> 
#>               coef   std.error  t-stat p-value  
#> mconst  0.27005590  0.21026283  1.2844 0.21445  
#> x1     -0.61303927  0.28160750 -2.1769 0.04230 *
#> x2      0.13398941  0.22947573  0.5839 0.56616  
#> x3      0.30619954  0.21734292  1.4088 0.17504  
#> x4     -0.00018761  0.19034597 -0.0010 0.99922  
#> x5      0.16595175  0.20992401  0.7905 0.43897  
#> x6     -0.16893171  0.21399989 -0.7894 0.43962  
#> x7      0.51949160  0.22562893  2.3024 0.03279 *
#> x8      0.32756857  0.20626559  1.5881 0.12877  
#> x9     -0.51817835  0.24477483 -2.1170 0.04768 *
#> x10    -0.01454824  0.19954250 -0.0729 0.94264  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log-variance equation:
#> 
#>            coef std.error  t-stat  p-value   
#> vconst -1.86806   0.66211  7.9601 0.004782 **
#> arch1  -0.29450   0.20609 -1.4290 0.165375   
#> arch2  -0.38209   0.20848 -1.8327 0.078778 . 
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                     Chi-sq df p-value
#> Ljung-Box AR(1)   0.027496  1  0.8683
#> Ljung-Box ARCH(3) 0.574734  3  0.9022
#>                           
#> SE of regression   0.93728
#> R-squared          0.40197
#> Log-lik.(n=28)   -30.52120
```
