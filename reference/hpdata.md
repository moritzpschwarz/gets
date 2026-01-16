# Hoover and Perez (1999) data

Data used by Hoover and Perez (1999) in their evaluation of
General-to-Specific (GETS) modelling. A detailed description of the data
is found in their Table 1 (page 172). The data are quarterly, comprise
20 variables (the first variable is the quarterly index) and runs from
1959:1 to 1995:1. This corresponds to 145 observations. The original
source of the data is Citibank.

## Usage

``` r
data(hpdata)
```

## Format

- `Date`:

  a factor that contains the (quarterly) dates of the observations

- `DCOINC`:

  index of four coincident indicators

- `GD`:

  GNP price deflator

- `GGEQ`:

  government purchases of goods and services

- `GGFEQ`:

  federal purchases of goods and services

- `GGFR`:

  federal government receipts

- `GNPQ`:

  GNP

- `GYDQ`:

  disposable personal income

- `GPIQ`:

  gross private domestic investment

- `FMRRA`:

  total member bank reserves

- `FMBASE`:

  monetary base (feredal reserve bank of St. Louis)

- `FM1DQ`:

  M1

- `FM2DQ`:

  M2

- `FSDJ`:

  Dow Jones stock price

- `FYAAAC`:

  Moody's AAA corporate bond yield

- `LHC`:

  labour force (16 years+, civilian)

- `LHUR`:

  unemployment rate

- `MU`:

  unfilled orders (manufacturing, all industries)

- `MO`:

  new orders (manufacturing, all industries)

- `GCQ`:

  personal consumption expenditure

## Details

The data have been used for comparison and illustration of GETS model
selection in several studies of the GETS methodology, including Hendry
and Krolzig (1999, 2005), Doornik (2009) and Sucarrat and Escribano
(2012).

## Source

Retrieved 14 October 2014 from:
<https://www.csus.edu/indiv/p/perezs/data/data.htm>

## References

David F. Hendry and Hans-Martin Krolzig (1999): 'Improving on 'Data
mining reconsidered' by K.D. Hoover and S.J Perez', Econometrics
Journal, Vol. 2, pp. 202-219.

David F. Hendry and Hans-Martin Krolzig (2005): 'The properties of
automatic Gets modelling', Economic Journal 115, C32-C61.

Jurgen Doornik (2009): 'Autometrics', in Jennifer L. Castle and Neil
Shephard (eds), 'The Methodology and Practice of Econometrics: A
Festschrift in Honour of David F. Hendry', Oxford University Press,
Oxford, pp. 88-121.

Pretis, Felix, Reade, James and Sucarrat, Genaro (2018): 'Automated
General-to-Specific (GETS) Regression Modeling and Indicator Saturation
for Outliers and Structural Breaks'. Journal of Statistical Software 86,
Number 3, pp. 1-44.

## Examples

``` r
##load Hoover and Perez (1999) data:
data(hpdata)

##make quarterly data-matrix of zoo type:
newhpdata <- zooreg(hpdata[,-1], start=c(1959,1), frequency=4)

##plot data:
plot(newhpdata)


##transform data to log-differences in percent:
dloghpdata <- diff(log(newhpdata))*100

##plot log-differenced data:
plot(dloghpdata)
```
