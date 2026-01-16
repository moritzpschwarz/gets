# General-to-Specific (GETS) Modelling 'lm' objects

General-to-Specific (GETS) Modelling of objects of class
[`lm`](https://rdrr.io/r/stats/lm.html).

## Usage

``` r
# S3 method for class 'lm'
gets(x, keep = NULL, include.1cut = TRUE, print.searchinfo = TRUE, ...)
```

## Arguments

- x:

  an object of class 'lm', see [`lm`](https://rdrr.io/r/stats/lm.html)

- keep:

  `NULL` or a vector of integers that determines which regressors to be
  excluded from removal in the specification search

- include.1cut:

  `logical`. If `TRUE` (default), then the 1-cut model is added to the
  list of terminal models. If `FALSE`, then the 1-cut is not added,
  unless it is a terminal model in one of the paths

- print.searchinfo:

  `logical`. If `TRUE` (default), then selected info is printed during
  search

- ...:

  further arguments passed on to
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md)

## Details

Internally, `gets.lm` invokes
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) for the
GETS-modelling, which is also invoked by
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md). See their
help pages for more information.

## Value

A list of class [`lm`](https://rdrr.io/r/stats/lm.html). Note that the
'top' of the list contains information (paths and terminal models) from
the GETS modelling, see
[`paths`](http://moritzschwarz.org/gets/reference/paths.md) and
[`terminals`](http://moritzschwarz.org/gets/reference/paths.md)

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`lm`](https://rdrr.io/r/stats/lm.html),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`paths`](http://moritzschwarz.org/gets/reference/paths.md) and
[`terminals`](http://moritzschwarz.org/gets/reference/paths.md)

## Examples

``` r
##generate some data:
set.seed(123) #for reproducibility
y <- rnorm(30) #generate Y
x <- matrix(rnorm(30*10), 30, 10) #matrix of Xs
colnames(x) <- paste0("var", 1:NCOL(x))

##estimate model:
mymod <- lm(y ~ x)

##do gets modelling:
gets(mymod)
#> 
#> Start model (GUM):
#> 
#>             reg.no keep        coef   std.error  t-stat p-value  
#> (Intercept)      1    0  0.27005590  0.21026283  1.2844 0.21445  
#> xvar1            2    0 -0.61303927  0.28160750 -2.1769 0.04230 *
#> xvar2            3    0  0.13398941  0.22947573  0.5839 0.56616  
#> xvar3            4    0  0.30619954  0.21734292  1.4088 0.17504  
#> xvar4            5    0 -0.00018761  0.19034597 -0.0010 0.99922  
#> xvar5            6    0  0.16595175  0.20992401  0.7905 0.43897  
#> xvar6            7    0 -0.16893171  0.21399989 -0.7894 0.43962  
#> xvar7            8    0  0.51949160  0.22562893  2.3024 0.03279 *
#> xvar8            9    0  0.32756857  0.20626559  1.5881 0.12877  
#> xvar9           10    0 -0.51817835  0.24477483 -2.1170 0.04768 *
#> xvar10          11    0 -0.01454824  0.19954250 -0.0729 0.94264  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> 8 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 8 
#> 
#>   Path 1: 1 6 7 8 9 10 11 4 5 2 3 
#>   Path 2: 3 6 7 8 9 10 11 4 5 1 2 
#>   Path 3: 4 6 7 8 9 10 11 3 5 1 2 
#>   Path 4: 5 6 7 8 9 10 11 3 4 1 2 
#>   Path 5: 6 5 7 8 9 10 11 3 4 1 2 
#>   Path 6: 7 5 6 8 9 10 11 3 4 1 2 
#>   Path 7: 9 5 6 7 8 10 11 3 4 1 2 
#>   Path 8: 11 5 6 7 8 9 10 3 4 1 2 
#> 
#> Terminal models:
#> 
#>         info(sc)      logl  n k
#> spec 1: 2.768546 -41.52819 30 0
#> 
#> Retained regressors (final model):
#> 
#>   none
#> 
#> Call:
#> lm(formula = y ~ NULL - 1)
#> 
#> No coefficients
#> 

##ensure intercept is not removed:
gets(mymod, keep=1)
#> 
#> Start model (GUM):
#> 
#>             reg.no keep        coef   std.error  t-stat p-value  
#> (Intercept)      1    1  0.27005590  0.21026283  1.2844 0.21445  
#> xvar1            2    0 -0.61303927  0.28160750 -2.1769 0.04230 *
#> xvar2            3    0  0.13398941  0.22947573  0.5839 0.56616  
#> xvar3            4    0  0.30619954  0.21734292  1.4088 0.17504  
#> xvar4            5    0 -0.00018761  0.19034597 -0.0010 0.99922  
#> xvar5            6    0  0.16595175  0.20992401  0.7905 0.43897  
#> xvar6            7    0 -0.16893171  0.21399989 -0.7894 0.43962  
#> xvar7            8    0  0.51949160  0.22562893  2.3024 0.03279 *
#> xvar8            9    0  0.32756857  0.20626559  1.5881 0.12877  
#> xvar9           10    0 -0.51817835  0.24477483 -2.1170 0.04768 *
#> xvar10          11    0 -0.01454824  0.19954250 -0.0729 0.94264  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> 7 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 3 
#> 4 
#> 5 
#> 6 
#> 7 
#> 
#>   Path 1: 3 7 8 9 10 11 5 6 2 4 
#>   Path 2: 4 7 8 9 10 11 5 6 2 3 
#>   Path 3: 5 7 8 9 10 11 4 6 2 3 
#>   Path 4: 6 7 8 9 10 11 4 5 2 3 
#>   Path 5: 7 6 8 9 10 11 4 5 2 3 
#>   Path 6: 9 6 7 8 10 11 4 5 2 3 
#>   Path 7: 11 6 7 8 9 10 4 5 2 3 
#> 
#> Terminal models:
#> 
#>         info(sc)      logl  n k
#> spec 1: 2.365507 -33.78201 30 1
#> 
#> Retained regressors (final model):
#> 
#>   (Intercept) 
#> 
#> Call:
#> lm(formula = y ~ NULL)
#> 
#> Coefficients:
#> (Intercept)  
#>     -0.0471  
#> 
```
