# Render a Quarto multilingual project

Render a Quarto multilingual project

## Usage

``` r
render_book(
  project_path = ".",
  site_url = NULL,
  profile = NULL,
  preview = rlang::is_interactive()
)

render_website(
  project_path = ".",
  site_url = NULL,
  profile = NULL,
  preview = rlang::is_interactive()
)
```

## Arguments

- project_path:

  Path where the book/website source is located

- site_url:

  Override the base URL of the book/website. If `NULL`, in interactive
  sessions it will be set to "" to allow previewing the whole project
  with [`servr::httw()`](https://rdrr.io/pkg/servr/man/httd.html).

- profile:

  Quarto profile(s) to use.

- preview:

  Logical indicating whether to preview the project using
  [`servr::httw()`](https://rdrr.io/pkg/servr/man/httd.html).

## Value

Nothing, called for its side-effect of rendering a project.

## Details

babelquarto expects a book/website folder with each qmd/Rmd present in
as many languages as needed, with the same basename but,

- once with only `.qmd` as extension for the main language,

- once with `.es.qmd` (using the language code) for each other language.

You also need to register the language in the configuration file, see
[`register_main_language()`](https://docs.ropensci.org/babelquarto/reference/register_main_language.md)
and
[`register_further_languages()`](https://docs.ropensci.org/babelquarto/reference/register_further_languages.md):

    babelquarto:
      mainlanguage: 'en'
      languages: ['es', 'fr']

## Examples

``` r
directory <- withr::local_tempdir()
quarto_multilingual_book(parent_dir = directory, project_dir = "blop")
#> Error in setwd(dir = new): cannot change working directory
render_book(file.path(directory, "blop"))
#> Error in quarto::quarto_inspect(input = path, profile = profile): ! Error running quarto CLI from R.
#> Caused by error in `quarto::quarto_inspect()`:
#> ✖ Error returned by quarto CLI.
#>   -----------------------------
#>   ERROR: /tmp/RtmpYaGRX0/file6687e6209ed/blop not found
#>   
#>   Stack trace:
#>   at inspectConfig (file:///opt/quarto/bin/quarto.js:163919:11)
#>   at _Command.actionHandler (file:///opt/quarto/bin/quarto.js:164109:27)
#>   at async _Command.execute (file:///opt/quarto/bin/quarto.js:102102:7)
#>   at async _Command.parseCommand (file:///opt/quarto/bin/quarto.js:101979:14)
#>   at async quarto4 (file:///opt/quarto/bin/quarto.js:187653:5)
#>   at async file:///opt/quarto/bin/quarto.js:187681:5
#>   at async file:///opt/quarto/bin/quarto.js:187536:14
#>   at async mainRunner (file:///opt/quarto/bin/quarto.js:187538:5)
#>   at async file:///opt/quarto/bin/quarto.js:187674:3
#>   
#> Caused by error in `processx::run()`:
#> ! System command 'quarto' failed
```
