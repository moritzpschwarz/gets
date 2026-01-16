# General-to-Specific (GETS) Modelling of objects of class 'logitx'

General-to-Specific (GETS) Modelling of a dynamic Autoregressive (AR)
logit model with covariates ('X') of class 'dlogitx'.

## Usage

``` r
# S3 method for class 'logitx'
gets(x, t.pval = 0.05, wald.pval = t.pval, do.pet = TRUE, 
    user.diagnostics = NULL, keep = NULL, include.gum = FALSE,
    include.1cut = TRUE, include.empty = FALSE, max.paths = NULL,
    turbo = TRUE, print.searchinfo = TRUE, plot = NULL, alarm = FALSE,
    ...)
```

## Arguments

- x:

  an object of class 'logitx', see
  [`logitx`](http://moritzschwarz.org/gets/reference/logitx.md)

- t.pval:

  numeric value between 0 and 1. The significance level used for the
  two-sided regressor significance t-tests

- wald.pval:

  numeric value between 0 and 1. The significance level used for the
  Parsimonious Encompassing Tests (PETs). By default, it is the same as
  `t.pval`

- do.pet:

  `logical` that determines whether a Parsimonious Encompassing Test
  (PET) against the GUM should be undertaken at each regressor removal
  for the joint significance of all the deleted regressors along the
  current path. If `FALSE`, then a PET is not undertaken at each
  regressor removal

- user.diagnostics:

  `NULL` (default) or a `list` with two entries, `name` and `pval`, see
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md)

- keep:

  `NULL` or a vector of integers that determines which regressors to be
  excluded from removal in the specification search

- include.gum:

  `logical` that determines whether the GUM (i.e. the starting model)
  should be included among the terminal models. If `FALSE` (default),
  then the GUM is not included

- include.1cut:

  `logical` that determines whether the 1-cut model should be added to
  the list of terminal models. If `FALSE` (default), then the 1-cut is
  not added, unless it is a terminal model in one of the paths

- include.empty:

  `logical` that determines whether an empty model should be added to
  the list of terminal models, if it passes the diagnostic tests. If
  `FALSE` (default), then the empty model is not added, unless it is a
  terminal model in one of the paths

- max.paths:

  `NULL` (default) or an integer greater than 0. If `NULL`, then there
  is no limit to the number of paths. If an integer (e.g. 1), then this
  integer constitutes the maximum number of paths searched (e.g. a
  single path)

- turbo:

  `logical`. If `TRUE` (the default), then (parts of) paths are not
  searched twice (or more) unnecessarily, thus yielding a significant
  potential for speed-gain. The checking of whether the search has
  arrived at a point it has already been at comes with a slight
  computational overhead. So faster search is not guaranteed when
  `turbo=TRUE`

- print.searchinfo:

  `logical`. If `TRUE` (default), then a print is returned whenever
  simiplification along a new path is started

- plot:

  `NULL` or logical. If `TRUE`, then a plot is produced. If `NULL`
  (default), then the value set by
  [`options`](https://rdrr.io/r/base/options.html) determines whether a
  plot is produced or not

- alarm:

  `logical`. If `TRUE`, then a sound or beep is emitted (in order to
  alert the user) when the model selection ends

- ...:

  further arguments passed to or from other methods

## Details

The model of class 'logitx' is a dynamic Autoregressive (AR) logit model
with (optional) covariates ('X') proposed by Kauppi and Saikkonen
(2008). Internally, `gets.logitx` undertakes the General-to-Specific
(GETS) modelling with the
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md)
function, see Sucarrat (2020).

## References

Heikki Kauppi and Penti Saikkonen (2008): 'Predicting U.S. Recessions
with Dynamic Binary Response Models'. The Review of Economic Statistics
90, pp. 777-791

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`logitx`](http://moritzschwarz.org/gets/reference/logitx.md),
[`logitxSim`](http://moritzschwarz.org/gets/reference/logitxSim.md),
[`coef.logitx`](http://moritzschwarz.org/gets/reference/coef.logitx.md),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md)

## Examples

``` r
##simulate from ar(1), create covariates:
set.seed(123) #for reproducibility
y <- logitxSim(100, ar=0.3)
x <- matrix(rnorm(5*100), 100, 5)

##estimate model:
mymod <- logitx(y, ar=1:4, xreg=x)

##do gets modelling:
gets(mymod)
#> 10 path(s) to search
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
#> 
#> Date: Fri Jan 16 14:55:50 2026 
#> Dependent var.: y 
#> Method: Maximum Likelihood (logit) 
#> Variance-Covariance: Ordinary 
#> No. of observations: 96 
#> Sample: 5 to 100 
#> 
#> Start model (GUM):
#> 
#>           reg.no. keep       coef std.error    t-stat p-value  
#> intercept       1    0 -0.8500962   0.42943 -1.979613 0.02547 *
#> ar1             2    0  0.6026207   0.47106  1.279290 0.10212  
#> ar2             3    0  0.3959259   0.46187  0.857232 0.19685  
#> ar3             4    0  0.7065778   0.45945  1.537867 0.06388 .
#> ar4             5    0 -0.0086638   0.47389 -0.018282 0.49273  
#> xreg1           6    0 -0.3449343   0.24557 -1.404649 0.08186 .
#> xreg2           7    0 -0.1020382   0.24258 -0.420630 0.33754  
#> xreg3           8    0  0.0946418   0.22873  0.413766 0.34004  
#> xreg4           9    0 -0.0828681   0.22377 -0.370320 0.35603  
#> xreg5          10    0 -0.1679998   0.24140 -0.695929 0.24417  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Paths searched: 
#> 
#> path 1 : 1 9 3 8 7 5 2 10 4 6 
#> path 2 : 2 5 7 9 8 10 3 1 4 6 
#> path 3 : 3 5 8 7 9 10 6 2 1 4 
#> path 4 : 4 9 5 8 7 10 3 1 2 6 
#> path 5 : 5 9 7 8 10 3 6 2 1 4 
#> path 6 : 6 9 7 5 8 10 3 2 1 4 
#> path 7 : 7 5 9 8 10 3 6 2 1 4 
#> path 8 : 8 5 7 9 10 3 6 2 1 4 
#> path 9 : 9 5 7 8 10 3 6 2 1 4 
#> path 10 : 10 5 9 7 8 3 6 2 1 4 
#> 
#> Terminal models: 
#> 
#> spec 1 :  
#> 
#>                 info(sc)     logl  n  k
#> spec 1 (1-cut):   1.3863 -66.5421 96  0
#> 
#>    The empty model
#>                        
#> Log-lik.(n=96) -66.5421
```
