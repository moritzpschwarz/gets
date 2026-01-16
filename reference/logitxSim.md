# Simulate from a dynamic logit-x model

Simulate from a dynamic Autoregressive (AR) logit model with covariates
('X'). This model is essentially a logit-version of the model of Kauppi
and Saikkonen (2008).

## Usage

``` r
logitxSim(n, intercept = 0, ar = NULL, xreg = NULL, verbose = FALSE, 
    as.zoo = TRUE)

dlogitxSim(n, ...)
```

## Arguments

- n:

  integer, the number of observations to generate

- intercept:

  numeric, the value of the intercept in the logit specification

- ar:

  `NULL` or a numeric vector with the autoregressive parameters

- xreg:

  `NULL` or numeric vector with the values of the X-term

- verbose:

  `logical`. If `FALSE`, then only the binary process (a vector) is
  returned. If `TRUE`, then a matrix with all the simulated information
  is returned (binary process, probabilities, etc.)

- as.zoo:

  `logical`. If `TRUE`, then the returned object - a vector or matrix -
  will be of class [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html)

- ...:

  arguments passed on to `logitxSim`

## Details

No details, for the moment.

## Value

A vector or matrix, depending on whether `verbose` is `FALSE` or `TRUE`,
of class [`zoo`](https://rdrr.io/pkg/zoo/man/zoo.html), depending on
whether `as.zoo` is `TRUE` or `FALSE`

## References

Heikki Kauppi and Penti Saikkonen (2008): 'Predicting U.S. Recessions
with Dynamic Binary Response Models'. The Review of Economic Statistics
90, pp. 777-791

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`logitx`](http://moritzschwarz.org/gets/reference/logitx.md)

## Examples

``` r
##simulate from ar(1):
set.seed(123) #for reproducibility
y <- logitxSim(100, ar=0.3)

##more output (value, probability, logit):
set.seed(123) #for reproducibility
y <- logitxSim(100, ar=0.3, verbose=TRUE)
```
