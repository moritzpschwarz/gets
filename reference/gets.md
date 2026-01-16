# General-to-Specific (GETS) Modelling

For an overview of the **gets** package, see
[`gets-package`](http://moritzschwarz.org/gets/reference/gets-package.md).
Here, documentation of generic functions for GETS modelling is provided.
Note that `gets.arx` is a convenience wrapper to
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md) and
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md). For
specific GETS methods for `lm`, `logitx` and `isat` models, see
[`gets.lm`](http://moritzschwarz.org/gets/reference/gets.lm.md),
[`gets.logitx`](http://moritzschwarz.org/gets/reference/gets.logitx.md)
and [`gets.isat`](http://moritzschwarz.org/gets/reference/gets.isat.md),
respectively.

## Usage

``` r
gets(x, ...)

# S3 method for class 'arx'
gets(x, spec=NULL, ...)
```

## Arguments

- x:

  an object to be subjected to GETS modelling

- spec:

  `NULL` (default), `"mean"` or `"variance"`. If `"mean"`, then
  [`getsm`](http://moritzschwarz.org/gets/reference/getsm.md) is called.
  If `"variance"`, then
  [`getsv`](http://moritzschwarz.org/gets/reference/getsm.md) is called.
  If `NULL`, then it is automatically determined whether GETS-modelling
  of the mean or log-variance specification should be undertaken.

- ...:

  further arguments passed to or from other methods

## Details

`gets.arx` is a convenience wrapper to
[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md) and
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md).

## Author

Genaro Sucarrat, <http://www.sucarrat.net/>

## See also

[`getsm`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsv`](http://moritzschwarz.org/gets/reference/getsm.md),
[`getsFun`](http://moritzschwarz.org/gets/reference/getsFun.md),
[`blocksFun`](http://moritzschwarz.org/gets/reference/blocksFun.md)
