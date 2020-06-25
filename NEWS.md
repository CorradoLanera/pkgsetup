# pkgsetup (development version)

* Created `dev/02-development.R` to keep track of the development
process.








# pkgsetup 0.0.0.9000

* Added support for automatic background continuous tests for testthat
powered by `{CorradoLanera/autotestthat}`.
* Added full tidy's CIs powered by GitHub Actions.
* Added automatic lint checks powered by `{lintr}` package and GitHub
  Actions.
* Added WEBsite documentation powered by `{pkgdown}`, automatically
  deployed by a GitHub Action. Including a Badge-button for the `README`
  file.
* Activate GitHub support, including Contrib, issue template, support,
  and CoC.
* Initialize git repo
* Initialize `{renv}` library and environment (with setting
  `snapshot.type = "explicit"`) to track the packages effectively used
  by the package.
* Activate `{lintr}` static checks.
* Added support for unit tests using `{testthat}`.
* Added support for raw data with a folder `data-raw/` and `data-raw/DATASET.R` inside it to prepare the data for the package.
* Added support for and activate spellcheck
  (`usethis::use_spell_check()`.)
* Added a GPL-3 license and the corresponding `LICENSE.md` file.
* Added a `README.Rmd` (knitted to `README.md`) has the landing
  page of the project, including the logo, the lifecycle badge
  ("maturing"), and the Code of Conduct (including the
  `CODE_OF_CONDUCT.md` file).
* Added `R/pkgsetup-package.R` to create the standard R package
  documentation.
* Updated the `DESCRIPTION` file with the project's informations.
* Created `dev/01-setup.R` (`.Rbuildignore`d) to keep track 
  of the setup process.
* Added a `NEWS.md` file to track changes to the package.
