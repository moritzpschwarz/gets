# Make matrix of periodicity (e.g. seasonal) dummies

Auxiliary function that creates periodicity dummies (e.g. seasonal
dummies) for regular time series. The function is similar to, but more
general than, the `seasonaldummy` function in the package forecast.

## Usage

``` r
periodicdummies(x, values=1)
```

## Arguments

- x:

  a regular time series (vector or matrix)

- values:

  numeric of length 1 (default) or numeric vector of length equal to
  `frequency(x)`

## Value

A matrix of class [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html) with
periodicity dummies

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`is.regular`](https://rdrr.io/pkg/zoo/man/is.regular.html),
[`zooreg`](https://rdrr.io/pkg/zoo/man/zooreg.html),
[`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html),
[`ts`](https://rdrr.io/r/stats/ts.html)

## Examples

``` r
##quarterly dummies:
x <- zooreg(rnorm(30), start=2000, frequency=4)
periodicdummies(x)
#>         dum1 dum2 dum3 dum4
#> 2000 Q1    1    0    0    0
#> 2000 Q2    0    1    0    0
#> 2000 Q3    0    0    1    0
#> 2000 Q4    0    0    0    1
#> 2001 Q1    1    0    0    0
#> 2001 Q2    0    1    0    0
#> 2001 Q3    0    0    1    0
#> 2001 Q4    0    0    0    1
#> 2002 Q1    1    0    0    0
#> 2002 Q2    0    1    0    0
#> 2002 Q3    0    0    1    0
#> 2002 Q4    0    0    0    1
#> 2003 Q1    1    0    0    0
#> 2003 Q2    0    1    0    0
#> 2003 Q3    0    0    1    0
#> 2003 Q4    0    0    0    1
#> 2004 Q1    1    0    0    0
#> 2004 Q2    0    1    0    0
#> 2004 Q3    0    0    1    0
#> 2004 Q4    0    0    0    1
#> 2005 Q1    1    0    0    0
#> 2005 Q2    0    1    0    0
#> 2005 Q3    0    0    1    0
#> 2005 Q4    0    0    0    1
#> 2006 Q1    1    0    0    0
#> 2006 Q2    0    1    0    0
#> 2006 Q3    0    0    1    0
#> 2006 Q4    0    0    0    1
#> 2007 Q1    1    0    0    0
#> 2007 Q2    0    1    0    0

##monthly dummies:
y <- zooreg(rnorm(30), start=c(2000,1), frequency=12)
periodicdummies(y)
#>          dum1 dum2 dum3 dum4 dum5 dum6 dum7 dum8 dum9 dum10 dum11 dum12
#> Jan 2000    1    0    0    0    0    0    0    0    0     0     0     0
#> Feb 2000    0    1    0    0    0    0    0    0    0     0     0     0
#> Mar 2000    0    0    1    0    0    0    0    0    0     0     0     0
#> Apr 2000    0    0    0    1    0    0    0    0    0     0     0     0
#> May 2000    0    0    0    0    1    0    0    0    0     0     0     0
#> Jun 2000    0    0    0    0    0    1    0    0    0     0     0     0
#> Jul 2000    0    0    0    0    0    0    1    0    0     0     0     0
#> Aug 2000    0    0    0    0    0    0    0    1    0     0     0     0
#> Sep 2000    0    0    0    0    0    0    0    0    1     0     0     0
#> Oct 2000    0    0    0    0    0    0    0    0    0     1     0     0
#> Nov 2000    0    0    0    0    0    0    0    0    0     0     1     0
#> Dec 2000    0    0    0    0    0    0    0    0    0     0     0     1
#> Jan 2001    1    0    0    0    0    0    0    0    0     0     0     0
#> Feb 2001    0    1    0    0    0    0    0    0    0     0     0     0
#> Mar 2001    0    0    1    0    0    0    0    0    0     0     0     0
#> Apr 2001    0    0    0    1    0    0    0    0    0     0     0     0
#> May 2001    0    0    0    0    1    0    0    0    0     0     0     0
#> Jun 2001    0    0    0    0    0    1    0    0    0     0     0     0
#> Jul 2001    0    0    0    0    0    0    1    0    0     0     0     0
#> Aug 2001    0    0    0    0    0    0    0    1    0     0     0     0
#> Sep 2001    0    0    0    0    0    0    0    0    1     0     0     0
#> Oct 2001    0    0    0    0    0    0    0    0    0     1     0     0
#> Nov 2001    0    0    0    0    0    0    0    0    0     0     1     0
#> Dec 2001    0    0    0    0    0    0    0    0    0     0     0     1
#> Jan 2002    1    0    0    0    0    0    0    0    0     0     0     0
#> Feb 2002    0    1    0    0    0    0    0    0    0     0     0     0
#> Mar 2002    0    0    1    0    0    0    0    0    0     0     0     0
#> Apr 2002    0    0    0    1    0    0    0    0    0     0     0     0
#> May 2002    0    0    0    0    1    0    0    0    0     0     0     0
#> Jun 2002    0    0    0    0    0    1    0    0    0     0     0     0
```
