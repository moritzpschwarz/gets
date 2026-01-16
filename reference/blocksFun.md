# Block-based General-to-Specific (GETS) modelling

Auxiliary function (i.e. not intended for the average user) that enables
block-based GETS-modelling with user-specified estimator, diagnostics
and goodness-of-fit criterion.

## Usage

``` r
blocksFun(y, x, untransformed.residuals=NULL, blocks=NULL,
  no.of.blocks=NULL, max.block.size=30, ratio.threshold=0.8,
  gets.of.union=TRUE, force.invertibility=FALSE,
  user.estimator=list(name="ols"), t.pval=0.001, wald.pval=t.pval,
  do.pet=FALSE, ar.LjungB=NULL, arch.LjungB=NULL, normality.JarqueB=NULL,
  user.diagnostics=NULL, gof.function=list(name="infocrit"),
  gof.method=c("min", "max"), keep=NULL, include.gum=FALSE,
  include.1cut=FALSE, include.empty=FALSE, max.paths=NULL,
  turbo=FALSE, parallel.options=NULL, tol=1e-07, LAPACK=FALSE,
  max.regs=NULL, print.searchinfo=TRUE, alarm=FALSE)
```

## Arguments

- y:

  a numeric vector (with no missing values, i.e. no non-numeric 'holes')

- x:

  a `matrix`, or a `list` of matrices

- untransformed.residuals:

  `NULL` (default) or, when
  [`ols`](http://moritzschwarz.org/gets/reference/ols.md) is used with
  `method=6` in `user.estimator`, a numeric vector containing the
  untransformed residuals

- blocks:

  `NULL` (default) or a `list` of lists with vectors of integers that
  indicate how blocks should be put together. If `NULL`, then the block
  composition is undertaken automatically by an internal algorithm that
  depends on `no.of.blocks`, `max.block.size` and `ratio.threshold`

- no.of.blocks:

  `NULL` (default) or `integer`. If `NULL`, then the number of blocks is
  determined automatically by an internal algorithm

- max.block.size:

  `integer` that controls the size of blocks

- ratio.threshold:

  `numeric` between 0 and 1 that controls the minimum ratio of variables
  in each block to total observations

- gets.of.union:

  `logical`. If `TRUE` (default), then GETS modelling is undertaken of
  the union of retained variables. Otherwise it is not

- force.invertibility:

  `logical`. If `TRUE`, then the x-matrix is ensured to have full
  row-rank before it is passed on to
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md)

- user.estimator:

  `list`, see
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) for
  the details

- t.pval:

  `numeric` value between 0 and 1. The significance level used for the
  two-sided coefficient significance t-tests

- wald.pval:

  `numeric` value between 0 and 1. The significance level used for the
  Parsimonious Encompassing Tests (PETs)

- do.pet:

  `logical`. If `TRUE`, then a Parsimonious Encompassing Test (PET)
  against the GUM is undertaken at each variable removal for the joint
  significance of all the deleted regressors along the current GETS
  path. If `FALSE`, then a PET is not undertaken at each removal

- ar.LjungB:

  a two element `vector`, or `NULL`. In the former case, the first
  element contains the AR-order, the second element the significance
  level. If `NULL`, then a test for autocorrelation in the residuals is
  not conducted

- arch.LjungB:

  a two element `vector`, or `NULL`. In the former case, the first
  element contains the ARCH-order, the second element the significance
  level. If `NULL`, then a test for ARCH in the residuals is not
  conducted

- normality.JarqueB:

  `NULL` or a `numeric` value between 0 and 1. In the latter case, a
  test for non-normality in the residuals is conducted using a
  significance level equal to  
  `normality.JarqueB`. If `NULL`, then no test for non-normality is
  conducted

- user.diagnostics:

  `NULL` (default) or a `list` with two entries, `name` and `pval`. See
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) for
  the details

- gof.function:

  `list`. The first item should be named `name` and contain the name (a
  character) of the Goodness-of-Fit (GOF) function used. Additional
  items in the list `gof.function` are passed on as arguments to the
  GOF-function. . See
  [`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) for
  the details

- gof.method:

  `character`. Determines whether the best Goodness-of-Fit is a minimum
  (default) or maximum

- keep:

  `NULL` (default), `vector` of integers or a `list` of vectors of
  integers. In the latter case, the number of vectors should be equal to
  the number of matrices in `x`

- include.gum:

  `logical`. If `TRUE`, then the GUM (i.e. the starting model) is
  included among the terminal models

- include.1cut:

  `logical`. If `TRUE`, then the 1-cut model is added to the list of
  terminal models

- include.empty:

  `logical`. If `TRUE`, then the empty model is added to the list of
  terminal models

- max.paths:

  `NULL` (default) or `integer` greater than 0. If `NULL`, then there is
  no limit to the number of paths. If `integer` (e.g. 1), then this
  integer constitutes the maximum number of paths searched (e.g. a
  single path)

- turbo:

  `logical`. If `TRUE`, then (parts of) paths are not searched twice (or
  more) unnecessarily in each GETS modelling. Setting `turbo` to `TRUE`
  entails a small additional computational costs, but may be outweighed
  substantially if estimation is slow, or if the number of variables to
  delete in each path is large

- parallel.options:

  `NULL` or `integer` that indicates the number of cores/threads to use
  for parallel computing (implemented w/`makeCluster` and `parLapply`)

- tol:

  `numeric` value, the tolerance for detecting linear dependencies in
  the columns of the variance-covariance matrix when computing the
  Wald-statistic used in the Parsimonious Encompassing Tests (PETs), see
  the [`qr.solve`](https://rdrr.io/r/base/qr.html) function

- LAPACK:

  currently not used

- max.regs:

  `integer`. The maximum number of regressions along a deletion path. Do
  not alter unless you know what you are doing!

- print.searchinfo:

  `logical`. If `TRUE` (default), then a print is returned whenever
  simiplification along a new path is started

- alarm:

  `logical`. If `TRUE`, then a sound or beep is emitted (in order to
  alert the user) when the model selection ends

## Details

`blocksFun` undertakes block-based GETS modelling by a repeated but
structured call to `getsFun`. For the details of how to user-specify an
estimator via `user.estimator`, diagnostics via `user.diagnostics` and a
goodness-of-fit function via `gof.function`, see documentation of
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md) under
"Details".

The algorithm of `blocksFun` is similar to that of
[`isat`](http://moritzschwarz.org/gets/reference/isat.md), but more
flexible. The main use of `blocksFun` is the creation of user-specified
methods that employs block-based GETS modelling, e.g. indicator
saturation techniques.

## Value

A [`list`](https://rdrr.io/r/base/list.html) with the results of the
block-based GETS-modelling.

## References

F. Pretis, J. Reade and G. Sucarrat (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

G. sucarrat (2020): 'User-Specified General-to-Specific and Indicator
Saturation Methods'. The R Journal 12 issue 2, pp. 388-401,
<https://journal.r-project.org/archive/2021/RJ-2021-024/>

## Author

Genaro Sucarrat, with contributions from Jonas kurle, Felix Pretis and
James Reade  

## See also

[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`ols`](http://moritzschwarz.org/gets/reference/ols.md),
[`diagnostics`](http://moritzschwarz.org/gets/reference/diagnostics.md),
[`infocrit`](http://moritzschwarz.org/gets/reference/infocrit.md) and
[`isat`](http://moritzschwarz.org/gets/reference/isat.md)

## Examples

``` r
## more variables than observations:
y <- rnorm(20)
x <- matrix(rnorm(length(y)*40), length(y), 40)
blocksFun(y, x)
#> 
#> x block 1 of 3:
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
#> x block 2 of 3:
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
#> x block 3 of 3:
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
#> $call
#> blocksFun(y, x)
#> 
#> $time.started
#> [1] "Fri Jan 16 14:36:47 2026"
#> 
#> $time.finished
#> [1] "Fri Jan 16 14:36:47 2026"
#> 
#> $y
#>  [1]  0.89512566  0.87813349  0.82158108  0.68864025  0.55391765 -0.06191171
#>  [7] -0.30596266 -0.38047100 -0.69470698 -0.20791728 -1.26539635  2.16895597
#> [13]  1.20796200 -1.12310858 -0.40288484 -0.46665535  0.77996512 -0.08336907
#> [19]  0.25331851 -0.02854676
#> 
#> $x
#> $x$x
#>  [1] "X1.xreg1"  "X1.xreg2"  "X1.xreg3"  "X1.xreg4"  "X1.xreg5"  "X1.xreg6" 
#>  [7] "X1.xreg7"  "X1.xreg8"  "X1.xreg9"  "X1.xreg10" "X1.xreg11" "X1.xreg12"
#> [13] "X1.xreg13" "X1.xreg14" "X1.xreg15" "X1.xreg16" "X1.xreg17" "X1.xreg18"
#> [19] "X1.xreg19" "X1.xreg20" "X1.xreg21" "X1.xreg22" "X1.xreg23" "X1.xreg24"
#> [25] "X1.xreg25" "X1.xreg26" "X1.xreg27" "X1.xreg28" "X1.xreg29" "X1.xreg30"
#> [31] "X1.xreg31" "X1.xreg32" "X1.xreg33" "X1.xreg34" "X1.xreg35" "X1.xreg36"
#> [37] "X1.xreg37" "X1.xreg38" "X1.xreg39" "X1.xreg40"
#> 
#> 
#> $blocks
#> $blocks$x
#> $blocks$x[[1]]
#>  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14
#> 
#> $blocks$x[[2]]
#>  [1] 15 16 17 18 19 20 21 22 23 24 25 26 27 28
#> 
#> $blocks$x[[3]]
#>  [1] 29 30 31 32 33 34 35 36 37 38 39 40
#> 
#> 
#> 
#> $specific.spec
#> $specific.spec$x
#> integer(0)
#> 
#> 

## 'x' as list of matrices:
z <- matrix(rnorm(length(y)*40), length(y), 40)
blocksFun(y, list(x,z))
#> 
#> X1 block 1 of 3:
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
#> X1 block 2 of 3:
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
#> X1 block 3 of 3:
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
#> X2 block 1 of 3:
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
#> X2 block 2 of 3:
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
#> X2 block 3 of 3:
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
#> $call
#> blocksFun(y, list(x, z))
#> 
#> $time.started
#> [1] "Fri Jan 16 14:36:47 2026"
#> 
#> $time.finished
#> [1] "Fri Jan 16 14:36:48 2026"
#> 
#> $y
#>  [1]  0.89512566  0.87813349  0.82158108  0.68864025  0.55391765 -0.06191171
#>  [7] -0.30596266 -0.38047100 -0.69470698 -0.20791728 -1.26539635  2.16895597
#> [13]  1.20796200 -1.12310858 -0.40288484 -0.46665535  0.77996512 -0.08336907
#> [19]  0.25331851 -0.02854676
#> 
#> $x
#> $x$X1
#>  [1] "X1.xreg1"  "X1.xreg2"  "X1.xreg3"  "X1.xreg4"  "X1.xreg5"  "X1.xreg6" 
#>  [7] "X1.xreg7"  "X1.xreg8"  "X1.xreg9"  "X1.xreg10" "X1.xreg11" "X1.xreg12"
#> [13] "X1.xreg13" "X1.xreg14" "X1.xreg15" "X1.xreg16" "X1.xreg17" "X1.xreg18"
#> [19] "X1.xreg19" "X1.xreg20" "X1.xreg21" "X1.xreg22" "X1.xreg23" "X1.xreg24"
#> [25] "X1.xreg25" "X1.xreg26" "X1.xreg27" "X1.xreg28" "X1.xreg29" "X1.xreg30"
#> [31] "X1.xreg31" "X1.xreg32" "X1.xreg33" "X1.xreg34" "X1.xreg35" "X1.xreg36"
#> [37] "X1.xreg37" "X1.xreg38" "X1.xreg39" "X1.xreg40"
#> 
#> $x$X2
#>  [1] "X2.xreg1"  "X2.xreg2"  "X2.xreg3"  "X2.xreg4"  "X2.xreg5"  "X2.xreg6" 
#>  [7] "X2.xreg7"  "X2.xreg8"  "X2.xreg9"  "X2.xreg10" "X2.xreg11" "X2.xreg12"
#> [13] "X2.xreg13" "X2.xreg14" "X2.xreg15" "X2.xreg16" "X2.xreg17" "X2.xreg18"
#> [19] "X2.xreg19" "X2.xreg20" "X2.xreg21" "X2.xreg22" "X2.xreg23" "X2.xreg24"
#> [25] "X2.xreg25" "X2.xreg26" "X2.xreg27" "X2.xreg28" "X2.xreg29" "X2.xreg30"
#> [31] "X2.xreg31" "X2.xreg32" "X2.xreg33" "X2.xreg34" "X2.xreg35" "X2.xreg36"
#> [37] "X2.xreg37" "X2.xreg38" "X2.xreg39" "X2.xreg40"
#> 
#> 
#> $blocks
#> $blocks$X1
#> $blocks$X1[[1]]
#>  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14
#> 
#> $blocks$X1[[2]]
#>  [1] 15 16 17 18 19 20 21 22 23 24 25 26 27 28
#> 
#> $blocks$X1[[3]]
#>  [1] 29 30 31 32 33 34 35 36 37 38 39 40
#> 
#> 
#> $blocks$X2
#> $blocks$X2[[1]]
#>  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14
#> 
#> $blocks$X2[[2]]
#>  [1] 15 16 17 18 19 20 21 22 23 24 25 26 27 28
#> 
#> $blocks$X2[[3]]
#>  [1] 29 30 31 32 33 34 35 36 37 38 39 40
#> 
#> 
#> 
#> $specific.spec
#> $specific.spec$X1
#> integer(0)
#> 
#> $specific.spec$X2
#> integer(0)
#> 
#> 

## ensure regressor no. 3 in matrix no. 2 is not removed:
blocksFun(y, list(x,z), keep=list(integer(0), 3))
#> 
#> X1 block 1 of 3:
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
#> X1 block 2 of 3:
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
#> X1 block 3 of 3:
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
#> X2 block 1 of 3:
#> 13 path(s) to search
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
#> 
#> X2 block 2 of 3:
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
#> X2 block 3 of 3:
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
#> GETS of union of retained X2 variables... 
#> 
#> $call
#> blocksFun(y, list(x, z), keep = list(integer(0), 3))
#> 
#> $time.started
#> [1] "Fri Jan 16 14:36:48 2026"
#> 
#> $time.finished
#> [1] "Fri Jan 16 14:36:48 2026"
#> 
#> $y
#>  [1]  0.89512566  0.87813349  0.82158108  0.68864025  0.55391765 -0.06191171
#>  [7] -0.30596266 -0.38047100 -0.69470698 -0.20791728 -1.26539635  2.16895597
#> [13]  1.20796200 -1.12310858 -0.40288484 -0.46665535  0.77996512 -0.08336907
#> [19]  0.25331851 -0.02854676
#> 
#> $x
#> $x$X1
#>  [1] "X1.xreg1"  "X1.xreg2"  "X1.xreg3"  "X1.xreg4"  "X1.xreg5"  "X1.xreg6" 
#>  [7] "X1.xreg7"  "X1.xreg8"  "X1.xreg9"  "X1.xreg10" "X1.xreg11" "X1.xreg12"
#> [13] "X1.xreg13" "X1.xreg14" "X1.xreg15" "X1.xreg16" "X1.xreg17" "X1.xreg18"
#> [19] "X1.xreg19" "X1.xreg20" "X1.xreg21" "X1.xreg22" "X1.xreg23" "X1.xreg24"
#> [25] "X1.xreg25" "X1.xreg26" "X1.xreg27" "X1.xreg28" "X1.xreg29" "X1.xreg30"
#> [31] "X1.xreg31" "X1.xreg32" "X1.xreg33" "X1.xreg34" "X1.xreg35" "X1.xreg36"
#> [37] "X1.xreg37" "X1.xreg38" "X1.xreg39" "X1.xreg40"
#> 
#> $x$X2
#>  [1] "X2.xreg1"  "X2.xreg2"  "X2.xreg3"  "X2.xreg4"  "X2.xreg5"  "X2.xreg6" 
#>  [7] "X2.xreg7"  "X2.xreg8"  "X2.xreg9"  "X2.xreg10" "X2.xreg11" "X2.xreg12"
#> [13] "X2.xreg13" "X2.xreg14" "X2.xreg15" "X2.xreg16" "X2.xreg17" "X2.xreg18"
#> [19] "X2.xreg19" "X2.xreg20" "X2.xreg21" "X2.xreg22" "X2.xreg23" "X2.xreg24"
#> [25] "X2.xreg25" "X2.xreg26" "X2.xreg27" "X2.xreg28" "X2.xreg29" "X2.xreg30"
#> [31] "X2.xreg31" "X2.xreg32" "X2.xreg33" "X2.xreg34" "X2.xreg35" "X2.xreg36"
#> [37] "X2.xreg37" "X2.xreg38" "X2.xreg39" "X2.xreg40"
#> 
#> 
#> $blocks
#> $blocks$X1
#> $blocks$X1[[1]]
#>  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14
#> 
#> $blocks$X1[[2]]
#>  [1] 15 16 17 18 19 20 21 22 23 24 25 26 27 28
#> 
#> $blocks$X1[[3]]
#>  [1] 29 30 31 32 33 34 35 36 37 38 39 40
#> 
#> 
#> $blocks$X2
#> $blocks$X2[[1]]
#>  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14
#> 
#> $blocks$X2[[2]]
#>  [1]  3 15 16 17 18 19 20 21 22 23 24 25 26 27 28
#> 
#> $blocks$X2[[3]]
#>  [1]  3 29 30 31 32 33 34 35 36 37 38 39 40
#> 
#> 
#> 
#> $keep
#> $keep$X1
#> integer(0)
#> 
#> $keep$X2
#> X2.xreg3 
#>        3 
#> 
#> 
#> $specific.spec
#> $specific.spec$X1
#> integer(0)
#> 
#> $specific.spec$X2
#> [1] "X2.xreg3"
#> 
#> 
```
