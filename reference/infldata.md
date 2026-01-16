# Quarterly Norwegian year-on-year CPI inflation

Quarterly Norwegian year-on-year CPI inflation from 1989(1) to 2015(4).

## Usage

``` r
data("infldata")
```

## Format

A data frame with 108 observations on the following 5 variables:

- `date`:

  a factor containing the dates

- `infl`:

  year-on-year inflation

- `q2dum`:

  a dummy variable equal to 1 in quarter 2 and 0 otherwise

- `q3dum`:

  a dummy variable equal to 1 in quarter 3 and 0 otherwise

- `q4dum`:

  a dummy variable equal to 1 in quarter 4 and 0 otherwise

## Source

Statistics Norway (SSB): <https://www.ssb.no/>. The raw data comprise
monthly CPI data obtained via <https://www.ssb.no/statbank/table/08183>.

## References

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44

## Examples

``` r
data(infldata)
infldata <- zooreg(infldata[,-1], frequency=4, start=c(1989,1))
plot(infldata[,"infl"])
```
