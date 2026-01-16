# Generate LaTeX code of an estimation result

Convenience functions that generates LaTeX-code of an estimation result
in equation-form. `printtex` can, in principle, be applied to any object
for which `coef`, `vcov` and `logLik` methods exist. Note: The generated
LaTeX-code contains an `eqnarray` environment, which requires that the
`amsmath` package is loaded in the preamble of the LaTeX document.

## Usage

``` r
printtex(x, fitted.name=NULL, xreg.names=NULL, digits=4,
      intercept=TRUE, gof=TRUE, diagnostics=TRUE, nonumber=FALSE,
      nobs="T", index="t", dec=NULL, print.info=TRUE)
  # S3 method for class 'arx'
toLatex(object, ...)
  # S3 method for class 'gets'
toLatex(object, ...)
```

## Arguments

- x:

  an estimation result, e.g.
  [`arx`](http://moritzschwarz.org/gets/reference/arx.md), `gets` or
  `isat` object

- object:

  an estimation result of class
  [`arx`](http://moritzschwarz.org/gets/reference/arx.md) or `gets`

- fitted.name:

  `NULL` or a user-specified name of left-hand side variable

- xreg.names:

  `NULL` or a user-specified character vector with the names of
  regressors

- digits:

  integer, the number of digits to be printed

- intercept:

  logical or numeric. The argument determines whether one of the
  regressors is an intercept or not, or its location. If `TRUE`, then
  the intercept is assumed to be located at `coef(x)[1]`, and hence the
  regressor-name of location 1 is excluded from the print. If `FALSE`,
  then it is assumed that there is no intercept among the regressors. If
  numeric, then it is assumed that the regressors contain an intercept
  at the location equal to the numeric value

- gof:

  logical, whether to include goodness-of-fit in the print

- diagnostics:

  logical, whether to include diagnostics in the print

- nonumber:

  logical, whether to remove or not (default) the equation-numbering

- nobs:

  character, the notation to use to denote the number of observations

- index:

  `NULL` or a [`character`](https://rdrr.io/r/base/character.html), only
  relevant if `fitted.name` is not `NULL`, and if the object in question
  is of class [`arx`](http://moritzschwarz.org/gets/reference/arx.md),
  [`gets`](http://moritzschwarz.org/gets/reference/gets.md) or
  [`isat`](http://moritzschwarz.org/gets/reference/isat.md)

- dec:

  `NULL` or a [`character`](https://rdrr.io/r/base/character.html) (for
  example `","`). In the latter case, an attempt is made to replace the
  dot separator `.` with the character in `dec`

- print.info:

  `logical`, whether to print the info at the start or not

- ...:

  arguments passed on to `printtex`

## Details

`toLatex.arx` and `toLatex.gets` are simply wrappers to `printtex`

## Value

LaTeX code of an estimation result

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`arx`](http://moritzschwarz.org/gets/reference/arx.md),
[`logitx`](http://moritzschwarz.org/gets/reference/logitx.md),
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md),
[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
##simulate random variates, estimate model:
y <- rnorm(30)
mX <- matrix(rnorm(30*2), 30, 2)
mymod <- arx(y, ar=1:3, mxreg=mX)

##print latex code of estimation result:
printtex(mymod)
#> % Date: Fri Jan 16 14:37:06 2026 
#> % LaTeX code generated in R 4.5.2 by the gets package
#> % Note: The {eqnarray} environment requires the {amsmath} package
#> \begin{eqnarray}
#>   \widehat{y} &=&  - \underset{(0.2259)}{0.1061} + \underset{(0.2281)}{0.3211}ar1 + \underset{(0.2413)}{0.0292}ar2 - \underset{(0.2391)}{0.0024}ar3 - \underset{(0.2717)}{0.2958}mxreg1 - \underset{(0.2589)}{0.1285}mxreg2 \\[2mm] 
#>    && R^2=0.1457 \qquad \widehat{\sigma}=1.1175 \qquad LogL=-38.3113 \qquad T = 27 \nonumber \\ 
#>    && \underset{[p-val]}{ AR(4) }: \underset{[0.8125]}{1.5791}\qquad \underset{[p-val]}{ ARCH(1)}:\underset{[0.0709]}{3.2632}\qquad \underset{[p-val]}{ Normality }:\underset{[0.7932]}{0.4633} \nonumber 
#> \end{eqnarray}

##add intercept, at the end, to regressor matrix:
mX <- cbind(mX,1)
colnames(mX) <- c("xreg1", "xreg2", "intercept")
mymod <- arx(y, mc=FALSE, mxreg=mX)

##set intercept location to 3:
printtex(mymod, intercept=3)
#> % Date: Fri Jan 16 14:37:06 2026 
#> % LaTeX code generated in R 4.5.2 by the gets package
#> % Note: The {eqnarray} environment requires the {amsmath} package
#> \begin{eqnarray}
#>   \widehat{y} &=&  - \underset{(0.2430)}{0.2304}xreg1 - \underset{(0.2041)}{0.1395}xreg2 - \underset{(0.2000)}{0.0840} \\[2mm] 
#>    && R^2=0.0362 \qquad \widehat{\sigma}=1.0774 \qquad LogL=-43.3052 \qquad T = 30 \nonumber \\ 
#>    && \underset{[p-val]}{ AR(1) }: \underset{[0.0712]}{3.2541}\qquad \underset{[p-val]}{ ARCH(1)}:\underset{[0.0889]}{2.8946}\qquad \underset{[p-val]}{ Normality }:\underset{[0.5928]}{1.0458} \nonumber 
#> \end{eqnarray}
```
