# Exporting results to EViews and STATA

Functions that facilitate the export of results to the commercial
econometric softwares EViews and STATA, respectively.

## Usage

``` r
eviews(object, file=NULL, print=TRUE, return=FALSE)
stata(object, file=NULL, print=TRUE, return=FALSE)
```

## Arguments

- object:

  an `arx`, `gets` or `isat` object

- file:

  filename, i.e. the destination of the exported data

- print:

  logical. If TRUE, then the estimation code in EViews (or STATA) is
  printed

- return:

  logical. If TRUE, then a list is returned

## Value

Either printed text or a `list` (if return=TRUE)

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
##simulate random variates, estimate model:
y <- rnorm(30)
mX <- matrix(rnorm(30*2), 30, 2)
mymod <- arx(y, mc=TRUE, mxreg=mX)

##print EViews code:
eviews(mymod)
#> EViews code to estimate the model:
#>   equation mymod.ls y c mxreg1 mxreg2
#> R code (example) to export the data of the model:
#>   eviews(mymod, file='C:/Users/myname/Documents/getsdata.csv')

##print Stata code:
stata(mymod)
#> STATA code to estimate the model:
#>  regress y mxreg1 mxreg2
#> R code (example) to export the data of the model:
#>   stata(mymod, file='C:/Users/myname/Documents/getsdata.csv')
```
