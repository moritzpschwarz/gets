# Drop variable

Drops columns in a matrix to avoid perfect multicollinearity.

## Usage

``` r
dropvar(x, tol=1e-07, LAPACK=FALSE, silent=FALSE)
```

## Arguments

- x:

  a matrix, possibly less than full column rank.

- tol:

  numeric value. The tolerance for detecting linear dependencies among
  regressors, see [`qr`](https://rdrr.io/r/base/qr.html) function. Only
  used if LAPACK is FALSE

- LAPACK:

  logical, TRUE or FALSE (default). If true use LAPACK otherwise use
  LINPACK, see [`qr`](https://rdrr.io/r/base/qr.html) function

- silent:

  logical, TRUE (default) or FALSE. Whether to print a notification
  whenever a regressor is removed

## Value

a matrix whose regressors linearly independent

## Details

Original function `drop.coef` developed by Rune Haubo B. Christensen in
package `ordinal`, <https://cran.r-project.org/package=ordinal>.

## References

Rune H.B. Christensen (2014): 'ordinal: Regression Models for Ordinal
Data'. <https://cran.r-project.org/package=ordinal>

## Author

Rune Haubo B. Christensen, with modifications by Genaro Sucarrat,
<http://www.sucarrat.net/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
set.seed(1)
x <- matrix(rnorm(20), 5)
dropvar(x) #full rank, none are dropped
#>            [,1]       [,2]       [,3]        [,4]
#> [1,] -0.6264538 -0.8204684  1.5117812 -0.04493361
#> [2,]  0.1836433  0.4874291  0.3898432 -0.01619026
#> [3,] -0.8356286  0.7383247 -0.6212406  0.94383621
#> [4,]  1.5952808  0.5757814 -2.2146999  0.82122120
#> [5,]  0.3295078 -0.3053884  1.1249309  0.59390132

x[,4] <- x[,1]*2
dropvar(x) #less than full rank, last column dropped
#> regressor-matrix is column rank deficient, so dropping 1 regressors
#> 
#>            [,1]       [,2]       [,3]
#> [1,] -0.6264538 -0.8204684  1.5117812
#> [2,]  0.1836433  0.4874291  0.3898432
#> [3,] -0.8356286  0.7383247 -0.6212406
#> [4,]  1.5952808  0.5757814 -2.2146999
#> [5,]  0.3295078 -0.3053884  1.1249309
```
