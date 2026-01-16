# Daily Standard and Poor's 500 index data

Daily Standard and Poor's 500 (SP500) index data from 3 January 1950 to
8 March 2016.

## Usage

``` r
data("sp500data")
```

## Format

A data frame with 16652 observations on the following 7 variables:

- `Date`:

  the dates

- `Open`:

  the opening values of the index

- `High`:

  the daily maximum value of the index

- `Low`:

  the daily minimum value of the index

- `Close`:

  the closing values of the index

- `Volume`:

  the traded volume

- `Adj.Close`:

  the adjusted closing values of the index

## Source

Yahoo Finance, retrieved 9 March 2016

## References

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

## Examples

``` r
data(sp500data)
sp500data <- zoo(sp500data[, -1], order.by = as.Date(sp500data[, "Date"]))
plot(window(sp500data, start = as.Date("2000-01-03")))
```
