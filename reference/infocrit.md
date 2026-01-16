# Computes the Average Value of an Information Criterion

Given a log-likelihood, the number of observations and the number of
estimated parameters, the average value of a chosen information
criterion is computed. This facilitates comparison of models that are
estimated with a different number of observations, e.g. due to different
lags.

## Usage

``` r
infocrit(x, method=c("sc","aic","aicc","hq"))

info.criterion(logl, n=NULL, k=NULL, method=c("sc","aic","aicc","hq"))
```

## Arguments

- x:

  a `list` that contains, at least, three items: `logl` (a numeric, the
  log-likelihood), `k` (a numeric, usually the number of estimated
  parameters) and `n` (a numeric, the number of observations)

- method:

  character, either "sc" (default), "aic", "aicc" or "hq"

- logl:

  numeric, the value of the log-likelihood

- n:

  integer, number of observations

- k:

  integer, number of parameters

## Details

Contrary to [`AIC`](https://rdrr.io/r/stats/AIC.html) and
[`BIC`](https://rdrr.io/r/stats/AIC.html), `info.criterion` computes the
average criterion value (i.e. division by the number of observations).
This facilitates comparison of models that are estimated with a
different number of observations, e.g. due to different lags.

## Value

`infocrit`: a numeric (i.e. the value of the chosen information
criterion)

`info.criterion`: a list with elements

- method:

  type of information criterion

- n:

  number of observations

- k:

  number of parameters

- value:

  the value on the information criterion

## References

H. Akaike (1974): 'A new look at the statistical model identification'.
IEEE Transactions on Automatic Control 19, pp. 716-723

E. Hannan and B. Quinn (1979): 'The determination of the order of an
autoregression'. Journal of the Royal Statistical Society B 41, pp.
190-195

C.M. Hurvich and C.-L. Tsai (1989): 'Regression and Time Series Model
Selection in Small Samples'. Biometrika 76, pp. 297-307

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

G. Schwarz (1978): 'Estimating the dimension of a model'. The Annals of
Statistics 6, pp. 461-464

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>
