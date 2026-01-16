# Extracting Indicator Saturation Breakdates

Takes an [`isat`](http://moritzschwarz.org/gets/reference/isat.md)
object and extracts the break dates together with their estimated
coefficients.

## Usage

``` r
isatdates(x)
```

## Arguments

- x:

  an [`isat`](http://moritzschwarz.org/gets/reference/isat.md) object

## Details

The function extracts the breakdates determined by
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) for `iis`,
`sis`, and `tis`, together with their estimated coefficients and
standard errors.

## Value

Returns a list of three elements (one for `iis`, `sis`, and `tis`). Each
element lists the name of the break variable, the time index of the
break (labelled 'date'), the index of the break date, the estimated
coefficient, the standard error of the estimated coefficient, as well as
the corresponding t-statistic and p-value.

## References

Pretis, F., Reade, J., & Sucarrat, G. (2018). Automated
General-to-Specific (GETS) regression modeling and indicator saturation
methods for the detection of outliers and structural breaks. Journal of
Statistical Software, 86(3).

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
###Break date extraction of the Nile data
nile <- as.zoo(Nile)
isat.nile <- isat(nile, sis=TRUE, iis=FALSE, plot=TRUE, t.pval=0.005)
#> 
#> SIS block 1 of 4:
#> 24 path(s) to search
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
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 24 
#> 
#> SIS block 2 of 4:
#> 25 path(s) to search
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
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 24 
#> 25 
#> 
#> SIS block 3 of 4:
#> 25 path(s) to search
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
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 24 
#> 25 
#> 
#> SIS block 4 of 4:
#> 24 path(s) to search
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
#> 16 
#> 17 
#> 18 
#> 19 
#> 20 
#> 21 
#> 22 
#> 23 
#> 24 
#> 
#> GETS of union of retained SIS variables... 
#> 2 path(s) to search
#> Searching: 
#> 1 
#> 2 
#> 
#> GETS of union of ALL retained variables...

isatdates(isat.nile)
#> $iis
#> NULL
#> 
#> $sis
#>    breaks date index      coef   coef.se    coef.t       coef.p
#> 1 sis1899 1899    29 -250.6071  40.07294 -6.253775 1.108303e-08
#> 2 sis1913 1913    43 -391.1429 126.72175 -3.086628 2.645951e-03
#> 3 sis1914 1914    44  401.5789 123.49408  3.251807 1.582717e-03
#> 
#> $tis
#> NULL
#> 
```
