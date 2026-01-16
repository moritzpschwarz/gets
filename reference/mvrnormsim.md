# Simulate from a Multivariate Normal Distribution

Produces one or more samples from the specified multivariate normal
distribution. Used in  
[`outlierscaletest`](http://moritzschwarz.org/gets/reference/outlierscaletest.md).

## Usage

``` r
mvrnormsim(n = 1, mu, Sigma, tol = 1e-6, empirical = FALSE)
```

## Arguments

- n:

  the number of samples required.

- mu:

  a vector giving the means of the variables.

- Sigma:

  a positive-definite symmetric matrix specifying the covariance matrix
  of the variables.

- tol:

  tolerance (relative to largest variance) for numerical lack of
  positive-definiteness in Sigma.

- empirical:

  logical. If true, mu and Sigma specify the empirical not population
  mean and covariance matrix.

## Value

If n = 1 a vector of the same length as mu, otherwise an n by length(mu)
matrix with one sample in each row.

## Details

Original function `mvrnorm` developed by Venables, W. N. & Ripley. in
package `MASS`, <https://CRAN.R-project.org/package=MASS>.

## References

Venables, W. N. & Ripley, B. D. (2019): 'MASS: Support Functions and
Datasets for Venables and Ripley's MASS'.
<https://CRAN.R-project.org/package=MASS>

Venables, W. N. & Ripley, B. D. (2002) Modern Applied Statistics with S.
Fourth Edition. Springer, New York. ISBN 0-387-95457-0

## Author

Venables, W. N. & Ripley, with modifications by Felix Pretis,
<https://felixpretis.climateeconometrics.org/>

## See also

[`outlierscaletest`](http://moritzschwarz.org/gets/reference/outlierscaletest.md)

## Examples

``` r
Sigma <- matrix(c(3,2,1,7),2,2)
mvrnormsim(n=2, mu=c(1,2), Sigma)
#>            [,1]     [,2]
#> [1,] -0.8938529 2.698007
#> [2,]  1.2614742 1.761862
```
