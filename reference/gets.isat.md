# General-to-Specific (GETS) Modelling 'isat' objects

General-to-Specific (GETS) Modelling of a objects of class
[`isat`](http://moritzschwarz.org/gets/reference/isat.md).

## Usage

``` r
# S3 method for class 'isat'
gets(x, t.pval=0.05, wald.pval=t.pval, vcov.type=NULL,
  do.pet=TRUE, ar.LjungB=list(lag=NULL, pval=0.025),
  arch.LjungB=list(lag=NULL, pval=0.025), normality.JarqueB=NULL,
  user.diagnostics=NULL, info.method=c("sc","aic","aicc","hq"),
  gof.function=NULL, gof.method=NULL, keep=NULL, include.gum=FALSE,
  include.1cut=TRUE, include.empty=FALSE, max.paths=NULL, tol=1e-07,
  turbo=FALSE, print.searchinfo=TRUE, plot=NULL, alarm=FALSE,...)
```

## Arguments

- x:

  an object of class 'isat'

- t.pval:

  numeric value between 0 and 1. The significance level used for the
  two-sided regressor significance t-tests

- wald.pval:

  numeric value between 0 and 1. The significance level used for the
  Parsimonious Encompassing Tests (PETs). By default, it is the same as
  `t.pval`

- vcov.type:

  the type of variance-covariance matrix used. If `NULL` (default), then
  the type used in the estimation of the 'arx' object is used. This can
  be overridden by either "ordinary" (i.e. the ordinary
  variance-covariance matrix) or "white" (i.e. the White (1980)
  heteroscedasticity robust variance-covariance matrix)

- do.pet:

  logical. If `TRUE` (default), then a Parsimonious Encompassing Test
  (PET) against the GUM is undertaken at each regressor removal for the
  joint significance of all the deleted regressors along the current
  path. If `FALSE`, then a PET is not undertaken at each regressor
  removal

- ar.LjungB:

  a two-item list with names `lag` and `pval`, or `NULL`. In the former
  case `lag` contains the order of the Ljung and Box (1979) test for
  serial correlation in the standardised residuals, and `pval` contains
  the significance level. If `lag=NULL` (default), then the order used
  is that of the estimated 'arx' object. If `ar.Ljungb=NULL`, then the
  standardised residuals are not checked for serial correlation

- arch.LjungB:

  a two-item list with names `lag` and `pval`, or `NULL`. In the former
  case, `lag` contains the order of the Ljung and Box (1979) test for
  serial correlation in the squared standardised residuals, and `pval`
  contains the significance level. If `lag=NULL` (default), then the
  order used is that of the estimated 'arx' object. If
  `arch.Ljungb=NULL`, then the standardised residuals are not checked
  for ARCH

- normality.JarqueB:

  a value between 0 and 1, or `NULL`. In the former case, the Jarque and
  Bera (1980) test for non-normality is conducted using a significance
  level equal to the numeric value. If `NULL`, then no test for
  non-normality is undertaken

- user.diagnostics:

  `NULL` or a [`list`](https://rdrr.io/r/base/list.html) with two
  entries, `name` and `pval`, see the `user.fun` argument in
  [`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md)

- info.method:

  character string, "sc" (default), "aic" or "hq", which determines the
  information criterion to be used when selecting among terminal models.
  The abbreviations are short for the Schwarz or Bayesian information
  criterion (sc), the Akaike information criterion (aic) and the
  Hannan-Quinn (hq) information criterion

- gof.function:

  `NULL` (default) or a `list`, see
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md). If
  `NULL`, then
  [`infocrit`](http://moritzschwarz.org/gets/reference/infocrit.md) is
  used

- gof.method:

  `NULL` (default) or a `character`, see
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md). If
  `NULL` and `gof.function` is also `NULL`, then the best
  goodness-of-fit is characterised by a minimum value

- keep:

  the regressors to be excluded from removal in the specification
  search. Note that `keep=c(1)` is obligatory when using `getsv`. This
  excludes the log-variance intercept from removal. The regressor
  numbering is contained in the `reg.no` column of the GUM

- include.gum:

  logical. If `TRUE`, then the GUM (i.e. the starting model) is included
  among the terminal models. If `FALSE` (default), then the GUM is not
  included

- include.1cut:

  logical. If `TRUE`, then the 1-cut model is added to the list of
  terminal models. If `FALSE` (default), then the 1-cut is not added,
  unless it is a terminal model in one of the paths

- include.empty:

  logical. If `TRUE`, then an empty model is included among the terminal
  models, if it passes the diagnostic tests, even if it is not equal to
  one of the terminals. If `FALSE` (default), then the empty model is
  not included (unless it is one of the terminals)

- max.paths:

  `NULL` (default) or an integer greater than 0. If `NULL`, then there
  is no limit to the number of paths. If an integer (e.g. 1), then this
  integer constitutes the maximum number of paths searched (e.g. a
  single path)

- tol:

  numeric value. The tolerance for detecting linear dependencies in the
  columns of the variance-covariance matrix when computing the
  Wald-statistic used in the Parsimonious Encompassing Tests (PETs), see
  the [`qr.solve`](https://rdrr.io/r/base/qr.html) function

- turbo:

  logical. If `TRUE`, then (parts of) paths are not searched twice (or
  more) unnecessarily, thus yielding a significant potential for
  speed-gain. However, the checking of whether the search has arrived at
  a point it has already been comes with a slight computational
  overhead. Accordingly, if `turbo=TRUE`, then the total search time
  might in fact be higher than if `turbo=FALSE`. This happens if
  estimation is very fast, say, less than quarter of a second. Hence the
  default is `FALSE`

- print.searchinfo:

  logical. If `TRUE` (default), then a print is returned whenever
  simiplification along a new path is started

- plot:

  `NULL` or logical. If `TRUE`, then the fitted values and the residuals
  of the final model are plotted after model selection. If `FALSE`, then
  they are not. If `NULL` (default), then the value set by
  [`options`](https://rdrr.io/r/base/options.html) determines whether a
  plot is produced or not

- alarm:

  logical. If `TRUE`, then a sound or beep is emitted (in order to alert
  the user) when the model selection ends

- ...:

  further arguments passed on to and from methods

## Details

Internally, `gets.isat` invokes
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md) for the
GETS-modelling.

## Value

A list of class
[`gets`](http://moritzschwarz.org/gets/reference/gets.md).

## Author

Moritz Schwarz, <https://www.inet.ox.ac.uk/people/moritz-schwarz>  
Genaro Sucarrat, <https://www.sucarrat.net/>

## See also

[`isat`](http://moritzschwarz.org/gets/reference/isat.md),
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`paths`](http://moritzschwarz.org/gets/reference/paths.md) and
[`terminals`](http://moritzschwarz.org/gets/reference/paths.md)

## Examples

``` r
##generate some data:
#set.seed(123) #for reproducibility
#y <- rnorm(30) #generate Y
#isatmod <- isat(y)
#gets(isatmot)
```
