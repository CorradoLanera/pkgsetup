---
title: "Setup (with `{renv}`)"
author: "Corrado Lanera"
date: "Thu Jun 25 21:42:57 2020"
output:
  html_document:
    toc: true
    toc_float: true
    keep_md: true
---



> NOTE: For projects which would not use `{renv}` support,
        see `01-pkgsetup.R` (here, in this gist).


Prerequisites
====================================================================



```r
available::available("pkgsetup")
usethis::create_package("~/Documents/cl/pkgsetup")

usethis::use_directory("dev", ignore = TRUE)
fs::file_create("dev/01-setup.R")
rstudioapi::navigateToFile("dev/01-setup.R")

usethis::use_roxygen_md()
usethis::use_news_md()
```


Documentiation
====================================================================

DESCRIPTION
--------------------------------------------------------------------



```r
usethis::use_gpl3_license("Corrado Lanera")
usethis::use_package_doc()
```


README
--------------------------------------------------------------------

Initialize the README file (ie the package's landing page)



```r
# install.packages("rmarkdown")
usethis::use_readme_rmd()
usethis::use_logo("~/Pictures/pkgsetup_hex.png")
usethis::use_cran_badge()
usethis::use_lifecycle_badge("Maturing")
```


Our package is not on CRAN, change the README accordingly:

   You can install the development version from
   [GitHub](https://github.com/) with the following procedure:

   
   ```r
   # install.packages("devtools")
   devtools::install_github("CorradoLanera/<package_name>")
   ```

Remove everything else that is not necessary and



```r
usethis::use_code_of_conduct()

usethis::use_spell_check()
spelling::spell_check_package()
spelling::update_wordlist()
```


> knit the README


Supporting Folders
====================================================================

Data raw
--------------------------------------------------------------------

If raw data are stored inside the main package folder call


```r
usethis::use_data_raw()
```


and comment the line with `usethis::use_data(...)` in it until it
will be used.


Other folder (eg Analyses)
--------------------------------------------------------------------


    usethis::use_directory("analysis", ignore = TRUE)
    usethis::use_directory("output", ignore = TRUE)


Test suit
====================================================================



```r
usethis::use_testthat()
```


Create a simple test to check everything works.
You can delete it AFTER you have written another test at least.

Check it works:



```r
usethis::use_test("foo") # `test_that("foo works", expect_null(foo()))`
devtools::test()         # see it fails!!
usethis::use_r("foo")    # define `foo <- function() NULL`
devtools::test()         # see it passes!!
```


delete `foo` only after have included another function!


Quality assurance
====================================================================



```r
usethis::use_tidy_description()

# install.packages("lintr)
lintr::lint_package()
```


and fix the spelling script that lint
have opened... ;-)



```r
if (requireNamespace("spelling", quietly = TRUE)) {
  spelling::spell_check_test(
    vignettes = TRUE,
    error = FALSE,
    skip_on_cran = TRUE
  )
}
```


Check again:



```r
lintr::lint_package()

devtools::check_man()
devtools::test()
devtools::check()
```


Activate Git/GitHub
====================================================================



```r
usethis::use_git()
usethis::git_vaccinate()
```


Commit everything before to continue!



```r
# remember to open and activate PuTTY
usethis::use_github(
  # "<organization>", # eg, "UBESP-DCTV"
  # private = TRUE # is a private repo?
)
```


> NOTE: If required set the upstream using your preferred
GUI^[GitKraken: https://www.gitkraken.com/invite/fas3vkyk is free,
multiplatform (Win, Mac, Linux),and super cool :-).], or by command
line running (on the Terminal):

    git push --set-upstream origin master



```r
usethis::use_tidy_github()
```


Activate {renv} for reproducibility
====================================================================

We will use "explicit" snapshot whith the intent
of capture what is included in the
DESCRIPTION file only.



```r
renv::init(settings = list(snapshot.type = "explicit"))
renv::status() # just to check
```


Package website documentation
====================================================================

> Disclaimer (2020-06-22): This and the following actions are mine
modification of the ones you can find in
https://github.com/r-lib/actions/blob/master/examples/pkgdown.yaml
The changes are made to made the action able to be used with `{renv}`
as suggested in
https://rstudio.github.io/renv/articles/ci.html#github-actions

As soon/if there will be implemented _official_ Actions, I will
substitute these with those ones.



```r
usethis::use_github_action(
  url = "https://raw.githubusercontent.com/CorradoLanera/actions/master/pkgdown.yaml"
)
usethis::use_github_actions_badge("pkgdown")
```


Bonus:



```r
renv::install("GuangchuangYu/badger")
badger::badge_custom("WEBsite", "click-me", "orange", "http://corradolanera.github.io/pkgsetup/")
```


And add it between title and logo in the README and knit it.


Continuous Integration
====================================================================

Lint (static code-quality checks)
--------------------------------------------------------------------



```r
usethis::use_github_action(
  url = "https://raw.githubusercontent.com/CorradoLanera/actions/master/lint-renv.yaml"
)
usethis::use_github_actions_badge("lint")
```


WARNING: if you do not use {renv} for your project, call

    usethis::use_github_action("lint")
    usethis::use_github_actions_badge("lint")

R-CDM-check and coverage
--------------------------------------------------------------------


```r
usethis::use_github_action(
  url = "https://raw.githubusercontent.com/CorradoLanera/actions/master/R-CMD-check-renv.yaml"
)
usethis::use_github_actions_badge("R-CMD-check")

usethis::use_github_action(
  url = "https://raw.githubusercontent.com/CorradoLanera/actions/master/covr-renv.yaml"
)
usethis::use_github_actions_badge("test-coverage")
```


WARNING: if you do not use {renv} for your project, call


    usethis::use_github_action("check-full",
      save_as = "R-CMD-check.yaml"
    )
    usethis::use_github_actions_badge("R-CMD-check")

    usethis::use_github_action("test-coverage",
      save_as = "covr.yaml"
    )
    usethis::use_github_actions_badge("covr")


Bonus:
====================================================================

Automating background continuous tests on RStudio (free command line)
--------------------------------------------------------------------



```r
renv::install("CorradoLanera/autotestthat") # {renv} installation
```


Final checks and update version
====================================================================



```r
usethis::use_tidy_description()
devtools::check_man()

spelling::spell_check_package()
spelling::update_wordlist()

lintr::lint_package()
renv::status()
devtools::check()
```


> Update and knit the `README.Rmd`



```r
usethis::use_version("dev")
```


Start to develop
====================================================================



```r
fs::file_create("dev/02-development.R")
rstudioapi::navigateToFile("dev/02-development.R")
```


commit and push...
Happy packaging!

