
<!-- README.md is generated from README.Rmd. Please edit that file -->

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/yonicd/details.svg?branch=master)](https://travis-ci.org/yonicd/details)
[![Codecov test
coverage](https://codecov.io/gh/yonicd/details/branch/master/graph/badge.svg)](https://codecov.io/gh/yonicd/details?branch=master)
[![Covrpage
Summary](https://img.shields.io/badge/covrpage-Last_Build_2019_09_08-brightgreen.svg)](http://tinyurl.com/yyodcwc7)
<!-- badges: end -->

# details <img src="https://github.com/yonicd/details/raw/master/input/logo.png" align="right" />

Create and customize details blocks for [markdown](#markdown) documents
and [Roxygen2](#package-documentation) documentation.

## Installation

``` r
remotes::install_github("yonicd/details")
```

## Markdown

### Input

The function `details::details` can handle inputs

  - R object with supported classes:
      - `character`
      - `data.frame`
      - `tibble`
      - `list`
  - File paths will be identified internally and the lines will be read
    in automatically.

### Output

The function `details::details` can output to result to

  - console (default)
  - clipboard via
    [clipr](https://github.com/mdlincoln/clipr)
  - [file.editor](https://stat.ethz.ch/R-manual/R-devel/library/utils/html/file.edit.html)
    useful when clipr not available

### Examples

One the most popular uses for `details` is to paste the sessioninfo at
the bottom of a GitHub issue.

``` r
library(details)

sessioninfo::session_info()%>%
  details::details(summary = 'current session info')
```

<details closed>

<summary> <span title="Click to Expand"> current session info </span>
</summary>

``` r

─ Session info ──────────────────────────────────────────────────────────
 setting  value                       
 version  R version 3.6.1 (2019-07-05)
 os       macOS Mojave 10.14.5        
 system   x86_64, darwin15.6.0        
 ui       X11                         
 language (EN)                        
 collate  en_US.UTF-8                 
 ctype    en_US.UTF-8                 
 tz       America/New_York            
 date     2019-09-09                  

─ Packages ──────────────────────────────────────────────────────────────
 package     * version    date       lib
 assertthat    0.2.1      2019-03-21 [1]
 cli           1.1.0      2019-03-19 [1]
 clipr         0.7.0      2019-07-23 [1]
 crayon        1.3.4      2017-09-16 [1]
 details     * 0.0.9      2019-09-09 [1]
 digest        0.6.20     2019-07-04 [1]
 evaluate      0.14       2019-05-28 [1]
 htmltools     0.3.6.9004 2019-09-08 [1]
 knitr         1.23       2019-05-18 [1]
 magrittr      1.5        2014-11-22 [1]
 Rcpp          1.0.2      2019-07-25 [1]
 rlang         0.4.0      2019-06-25 [1]
 rmarkdown     1.14       2019-07-12 [1]
 sessioninfo   1.1.1      2018-11-05 [1]
 stringi       1.4.3      2019-03-12 [1]
 stringr       1.4.0      2019-02-10 [1]
 withr         2.1.2      2018-03-15 [1]
 xfun          0.8        2019-06-25 [1]
 yaml          2.2.0      2018-07-25 [1]
 source                            
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 local                             
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 Github (rstudio/htmltools@840d786)
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    
 CRAN (R 3.6.0)                    

[1] /Library/Frameworks/R.framework/Versions/3.6/Resources/library
```

</details>

<br>

There are a [number of
objects](https://yonicd.github.io/details/articles/objects.html) that
can be placed in a details block other than a character object. An
example of a object is a device output such as a plot

``` r
details(plot(x=mtcars$mpg,y=mtcars$wt), summary = 'My plot')
```

<details closed>

<summary> <span title="Click to Expand"> My plot </span> </summary>

![](https://i.imgur.com/h9y4KPy.png)

</details>

<br>

## Package Documentation

Many times in documentation there is a lot to say, but you do not want
to overwhelm the user.

To solve this we can use folding blocks in the documentation (which are
then rendered into pkgdown website automatically)

To enable this feature add `Roxygen: list(markdown = TRUE)` to the
DESCRIPTION file before rendering the roxygen2

You can use this feature by wrapping documentation with the macros

    \foldstart{[SUMMARY TEXT]}
    
    #' DOCUMENTATION
    #' ...
    #' DOCUMENTATION
    
    \foldend

The `SUMMARY_TEXT` is optional, where the folded block will have a
header of
<svg style="height:0.8em;top:.04em;position:relative;" viewBox="0 0 192 512"><path d="M0 384.662V127.338c0-17.818 21.543-26.741 34.142-14.142l128.662 128.662c7.81 7.81 7.81 20.474 0 28.284L34.142 398.804C21.543 411.404 0 402.48 0 384.662z"/></svg>
**your text**.

The default will display
<svg style="height:0.8em;top:.04em;position:relative;" viewBox="0 0 192 512"><path d="M0 384.662V127.338c0-17.818 21.543-26.741 34.142-14.142l128.662 128.662c7.81 7.81 7.81 20.474 0 28.284L34.142 398.804C21.543 411.404 0 402.48 0 384.662z"/></svg>
**details**.

These folded blocks can be inserted anywhere in the documentation, eg
`@description`, `@param`, `@details`, `@return`, ….

## Vignettes

More information can be found in the
[articles](https://yonicd.github.io/details/) of the package site.

  - Creating a sessioninfo to paste into Github, Stackoverflow or
    Community Sites.
  - Customizing the details output
  - What R objects details can handle
  - Using details in Roxygen2