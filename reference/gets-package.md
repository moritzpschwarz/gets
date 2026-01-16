# General-to-Specific (GETS) and Indicator Saturation (ISAT) Modelling

The gets package provides functions and methods for General-to-Specific
(GETS) and Indicator Saturation (ISAT) modelling. GETS modelling is a
powerful and flexible variable selection algorithm that returns a
parsimonious and interpretable model. It is ideally suited for the
development of models that can be used for counterfactual and predictive
scenario analysis (e.g. conditional forecasting). ISAT modelling
provides a comprehensive, flexible and powerful approach to the
identification of structural breaks and outliers.  

The code of the package originated in relation with the research project
G. Sucarrat and A. Escribano (2012). In 2014, Felix Pretis and James
Reade joined for the development of the
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) code and
related functions. Moritz Schwarz and Jonas Kurle joined the development
team in 2020.

## Details

|          |            |
|----------|------------|
| Version: | 0.38       |
| Date:    | 2024-07-11 |
| Licence: | GPL-2      |

## GETS modelling

In the package gets, GETS methods are available for the following model
classes:  

- Linear regression, both static and dynamic, see
  [`arx`](http://moritzschwarz.org/gets/reference/arx.md),
  [`gets.arx`](http://moritzschwarz.org/gets/reference/gets.md) and
  [`gets.lm`](http://moritzschwarz.org/gets/reference/gets.lm.md)

- Variance models, both static and dynamic, see
  [`arx`](http://moritzschwarz.org/gets/reference/arx.md)

- Logit models, both static and dynamic, see
  [`logitx`](http://moritzschwarz.org/gets/reference/logitx.md) and
  [`gets.logitx`](http://moritzschwarz.org/gets/reference/gets.logitx.md)

The function `arx` estimates a static linear regression, or a dynamic
AR-X model with (optionally) a log-variance specification. The
log-variance specification can either be static or a dynamic
log-variance model with covariates (a 'log-ARCH-X' model). For the
statistical details of the model, see Section 4 in Pretis, Reade and
Sucarrat (2018). The function
[`logitx`](http://moritzschwarz.org/gets/reference/logitx.md) estimates
a static logit model, or a dynamic logit model with covariates
(optionally). For complete user-specified GETS modelling, see
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md).  

## ISAT modelling

ISAT methods are available for:  

- Linear regression, both static and dynamic, see
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md)

The `isat` function undertakes GETS model selection of an indicator
saturated mean specification. Extraction functions (mainly S3 methods)
are also available, together with additional auxiliary functions. For
complete user-specified ISAT modelling, see
[`blocksFun`](http://moritzschwarz.org/gets/reference/blocksFun.md).  

## Vignettes

Two vignettes are available in the package (type
`browseVignettes("gets")` to access them):  

- An introduction to the *gets* package

- User-Specified General-to-Specific (GETS) and Indicator Saturation
  (ISAT) Methods

The former is a mildly modified version of Pretis, Reade and Sucarrat
(2018), whereas the latter is an updated version of Sucarrat (2020).

## Author

|                  |     |                                                   |
|------------------|-----|---------------------------------------------------|
| Jonas Kurle:     |     | <https://www.jonaskurle.com/>                     |
| Felix Pretis:    |     | <https://felixpretis.climateeconometrics.org/>    |
| James Reade:     |     | <https://sites.google.com/site/jjamesreade/>      |
| Moritz Schwarz:  |     | <https://www.inet.ox.ac.uk/people/moritz-schwarz> |
| Genaro Sucarrat: |     | <https://www.sucarrat.net/>                       |

Maintainer: Genaro Sucarrat

## References

Jurgen A. Doornik, David F. Hendry, and Felix Pretis (2013): 'Step
Indicator Saturation', Oxford Economics Discussion Paper, 658.
<https://ideas.repec.org/p/oxf/wpaper/658.html>

Felix Pretis, James Reade and Genaro Sucarrat (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44.
[doi:10.18637/jss.v086.i03](https://doi.org/10.18637/jss.v086.i03)

Carlos Santos, David F. Hendry and Soren Johansen (2007): 'Automatic
selection of indicators in a fully saturated regression'. Computational
Statistics, vol 23:1, pp.317-335.
[doi:10.1007/s00180-007-0054-z](https://doi.org/10.1007/s00180-007-0054-z)

Genaro Sucarrat (2020): 'User-Specified General-to-Specific and
Indicator Saturation Methods'. The R Journal 12:2, pages 388-401.
<https://journal.r-project.org/archive/2021/RJ-2021-024/>

Genaro Sucarrat and Alvaro Escribano (2012): 'Automated Financial Model
Selection: General-to-Specific Modelling of the Mean and Volatility
Specifications', Oxford Bulletin of Economics and Statistics 74, Issue 5
(October), pp. 716-735.

## See also

[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`gets.arx`](http://moritzschwarz.org/gets/reference/gets.md),
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`blocksFun`](http://moritzschwarz.org/gets/reference/blocksFun.md)

## Examples

``` r
##Simulate from an AR(1):
set.seed(123)
y <- arima.sim(list(ar=0.4), 60)

##Estimate an AR(2) with intercept as mean specification
##and a log-ARCH(4) as log-volatility specification:
myModel <- arx(y, mc=TRUE, ar=1:2, arch=1:4)

##GETS modelling of the mean of myModel:
simpleMean <- getsm(myModel)
#> 
#> GUM mean equation:
#> 
#>        reg.no. keep     coef std.error t-stat p-value  
#> mconst       1    0 0.026155  0.117029 0.2235 0.82398  
#> ar1          2    0 0.333996  0.134355 2.4859 0.01599 *
#> ar2          3    0 0.034490  0.133176 0.2590 0.79661  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> GUM log-variance equation:
#> 
#>             coef std.error  t-stat p-value  
#> vconst -0.278502  0.391091  0.5071 0.47639  
#> arch1   0.215508  0.139456  1.5453 0.12870  
#> arch2   0.105365  0.142566  0.7391 0.46340  
#> arch3   0.081331  0.144165  0.5642 0.57522  
#> arch4  -0.306401  0.140825 -2.1758 0.03443 *
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   2.4462  3 0.48509
#> Ljung-Box ARCH(5) 1.3238  5 0.93246
#> 
#> 2 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 
#>   Path 1: 1 3 
#>   Path 2: 3 1 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.372013 -66.75816 58 1
#> 
#> Retained regressors (final model):
#> 
#>   ar1 

##GETS modelling of the log-variance of myModel:
simpleVar <- getsv(myModel)
#> GUM log-variance equation:
#> 
#>        reg.no. keep      coef std.error  t-stat p-value  
#> vconst       1    1 -0.278502  0.391091  0.5071 0.47639  
#> arch1        2    0  0.215508  0.139456  1.5453 0.12870  
#> arch2        3    0  0.105365  0.142566  0.7391 0.46340  
#> arch3        4    0  0.081331  0.144165  0.5642 0.57522  
#> arch4        5    0 -0.306401  0.140825 -2.1758 0.03443 *
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   2.4462  3 0.48509
#> Ljung-Box ARCH(5) 1.3238  5 0.93246
#> 
#> 3 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 
#>   Path 1: 2 4 3 5 
#>   Path 2: 3 4 2 5 
#>   Path 3: 4 3 2 5 
#> 
#> Terminal models:
#> 
#>                 info(sc)      logl  n k
#> spec 1 (1-cut): 2.614267 -66.59622 54 2
#> spec 2:         2.659078 -69.80062 54 1
#> 
#> Retained regressors (final model):
#> 
#>   vconst   arch4 

##results:
print(simpleMean)
#> 
#> Date: Fri Jan 16 14:36:53 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS) 
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 58 
#> Sample: 3 to 60 
#> 
#> SPECIFIC mean equation:
#> 
#>        coef std.error t-stat  p-value   
#> ar1 0.34686   0.12327 2.8138 0.006708 **
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> SPECIFIC log-variance equation:
#> 
#>             coef std.error  t-stat p-value
#> vconst -0.212822  0.473616  0.2019  0.6532
#> arch1   0.194178  0.142006  1.3674  0.1777
#> arch2   0.070728  0.144627  0.4890  0.6270
#> arch3   0.041949  0.145447  0.2884  0.7742
#> arch4  -0.207758  0.142741 -1.4555  0.1519
#> 
#> Diagnostics and fit:
#> 
#>                    Chi-sq df p-value
#> Ljung-Box AR(3)   2.66621  3  0.4460
#> Ljung-Box ARCH(5) 0.50528  5  0.9919
#>                           
#> SE of regression   0.87620
#> R-squared          0.12105
#> Log-lik.(n=54)   -66.75816
print(simpleVar)
#> 
#> Date: Fri Jan 16 14:36:53 2026 
#> Method: Ordinary Least Squares (OLS) 
#> No. of observations (variance eq.): 54 
#> Sample: 7 to 60 
#> 
#> SPECIFIC log-variance equation:
#> 
#>            coef std.error  t-stat p-value  
#> vconst -0.71684   0.31600  5.1459 0.02330 *
#> arch4  -0.26115   0.13804 -1.8918 0.06409 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Diagnostics and fit:
#> 
#>                   Chi-sq df p-value
#> Ljung-Box AR(3)   2.7674  3  0.4289
#> Ljung-Box ARCH(5) 4.5973  5  0.4670
#>                           
#> SE of regression   0.88132
#> Log-lik.(n=54)   -66.59622

##step indicator saturation of an iid normal series:
set.seed(123)
y <- rnorm(30)
isat(y)
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
#> 
#> Date: Fri Jan 16 14:36:53 2026 
#> Dependent var.: y 
#> Method: Ordinary Least Squares (OLS)
#> Variance-Covariance: Ordinary 
#> No. of observations (mean eq.): 30 
#> Sample: 1 to 30 
#> 
#> SPECIFIC mean equation:
#> 
#>             coef std.error t-stat p-value
#> mconst -0.047104  0.179111 -0.263  0.7944
#> 
#> Diagnostics and fit:
#> 
#>                     Chi-sq df p-value  
#> Ljung-Box AR(1)   0.046575  1 0.82913  
#> Ljung-Box ARCH(1) 3.367118  1 0.06651 .
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#>                           
#> SE of regression   0.98103
#> R-squared          0.00000
#> Log-lik.(n=30)   -41.49361
```
