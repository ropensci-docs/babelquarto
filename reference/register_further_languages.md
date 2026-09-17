# Register further languages in Quarto config

Register further languages in Quarto config

## Usage

``` r
register_further_languages(further_languages, project_path = ".")
```

## Arguments

- further_languages:

  Languages to be registered (character vector)

- project_path:

  Path where the book/website source is located

## Value

Nothing, called for its side-effect of editing the Quarto configuration
file.

## Examples

``` r
if (FALSE) { # interactive()
parent_dir <- withr::local_tempdir()
  quarto_multilingual_book(
    parent_dir = parent_dir,
    project_dir = "blop",
    further_languages = c("es", "fr"),
    main_language = "en"
  )
register_further_languages(
  "pt",
  project_path = file.path(parent_dir, "blop")
)
# have a look at the configuration
file.edit(file.path(parent_dir, "blop", "_quarto.yml"))
}
```
