---
title: "Development"
author: "Corrado Lanera"
date: "Thu Jun 25 21:43:08 2020"
output:
  html_document:
    toc: true
    toc_float: true
    keep_md: true
---




Development history
====================================================================
List here all the command executed during development of the package



```r
# renv::install("CorradoLanera/autotestthat")
autotestthat::auto_test_package_job() # before every start!


# usethis::use_test("<function_name>")
# usethis::use_r("<function_name>")


# ...
# ...
# ...
```


Check cycles
====================================================================

Before pushes
--------------------------------------------------------------------



```r
usethis::use_tidy_description()
spelling::spell_check_package()
spelling::update_wordlist()
```


Before pull requests
--------------------------------------------------------------------



```r
lintr::lint_package()
goodpractice::gp()

# The following calls run into your (interactive) session
# Use the corresponding RStudio button under the "Build"
# tab to execute them mantaining free your console
# (and running them in a non-interactive session)
devtools::test()
devtools::check()
```


> Update the `NEWS.md` file



```r
usethis::use_version()
```


CRAN submission's cycle
====================================================================



```r
# usethis::use_release_issue() # at the first start only
devtools::build_readme()
devtools::check(remote = TRUE, manual = TRUE)
devtools::check_win_devel()
cran_prep <- rhub::check_for_cran()
```

