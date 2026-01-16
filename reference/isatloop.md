# Repeated Impulse Indicator Saturation

Runs [`isat`](http://moritzschwarz.org/gets/reference/isat.md)
repeatedly at pre-specified significance levels to yield multiple
iterations used in  
[`outlierscaletest`](http://moritzschwarz.org/gets/reference/outlierscaletest.md).

## Usage

``` r
isatloop(num=c(seq(from=20, to=1, by=-1)), t.pval.spec = FALSE,  
  print=FALSE, y, ar=NULL, iis=TRUE, sis=FALSE, ...)
```

## Arguments

- num:

  numeric, target expected number of outliers under the null hypothesis,
  or target proportion of outliers if `t.pval.spec==TRUE`

- t.pval.spec:

  logical, if `TRUE`, then `num` specifies proportion rather than number
  of targeted outliers

- print:

  logical, if `TRUE`, then iterations are printed

- y:

  numeric vector, time-series or
  [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) object. Missing values
  in the beginning and at the end of the series is allowed, as they are
  removed with the [`na.trim`](https://rdrr.io/pkg/zoo/man/na.trim.html)
  command

- ar:

  integer vector, say, c(2,4) or 1:4. The AR-lags to include in the mean
  specification

- iis:

  logical, whether to use `iis`

- sis:

  logical, whether to use `sis`, default is `FALSE`

- ...:

  any argument from
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md) can also be
  used in `isatloop`

## Details

The function repeatedly runs
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) detecting
outliers in a model of `y` at different chosen target levels of
significance speciefied in `num`. The output of this function is used as
the input for the
[`outlierscaletest`](http://moritzschwarz.org/gets/reference/outlierscaletest.md)
function. All additional arguments from
[`isat`](http://moritzschwarz.org/gets/reference/isat.md) can be passed
to `isatloop`.

## Value

Returns a list of two items. The first item is the number of
observations. The second item is a dataframe containing the expected and
observed proportion (and number of outliers) for each specified
significance level of selection.

## References

Jiao, X. & Pretis, F. (2019). Testing the Presence of Outliers in
Regression Models. Discussion Paper.

Pretis, F., Reade, J., & Sucarrat, G. (2018). Automated
General-to-Specific (GETS) regression modeling and indicator saturation
methods for the detection of outliers and structural breaks. Journal of
Statistical Software, 86(3).

## Author

Felix Pretis, <https://felixpretis.climateeconometrics.org/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`outlierscaletest`](http://moritzschwarz.org/gets/reference/outlierscaletest.md)

## Examples

``` r
  ###Repeated isat models using the Nile dataset
  ### where p-values are chosen such that the expected number of outliers under the null
  ### corresponds to 1, 2, 3, 4 and 5.
  nile <- as.zoo(Nile)
  isat.nile.loop <- isatloop(y=nile, iis=TRUE, num=c(1,2, 3, 4, 5))
#> 
#> IIS block 1 of 4:
#> 12 path(s) to search
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
#> 
#> IIS block 2 of 4:
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
#> IIS block 3 of 4:
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
#> IIS block 4 of 4:
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
#> GETS of union of retained IIS variables... 
#> 
#> GETS of union of ALL retained variables...
#> 
#> IIS block 1 of 4:
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
#> IIS block 2 of 4:
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
#> IIS block 3 of 4:
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
#> IIS block 4 of 4:
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
#> GETS of union of retained IIS variables... 
#> 
#> GETS of union of ALL retained variables...
#> 
#> IIS block 1 of 4:
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
#> IIS block 2 of 4:
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
#> IIS block 3 of 4:
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
#> IIS block 4 of 4:
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
#> GETS of union of retained IIS variables... 
#> 
#> GETS of union of ALL retained variables...
#> 
#> IIS block 1 of 4:
#> 19 path(s) to search
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
#> 
#> IIS block 2 of 4:
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
#> IIS block 3 of 4:
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
#> IIS block 4 of 4:
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
#> GETS of union of retained IIS variables... 
#> 
#> GETS of union of ALL retained variables...
#> 
#> IIS block 1 of 4:
#> 21 path(s) to search
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
#> 
#> IIS block 2 of 4:
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
#> IIS block 3 of 4:
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
#> IIS block 4 of 4:
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
#> GETS of union of retained IIS variables... 
#> 
#> GETS of union of ALL retained variables...
  
```
