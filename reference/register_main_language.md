# Register main language in Quarto config

Register main language in Quarto config

## Usage

``` r
register_main_language(main_language = "en", project_path = ".")
```

## Arguments

- main_language:

  Main language code (character, like `"en"`)

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
    main_language = "en",
    register_languages = FALSE
  )
book_path <- file.path(parent_dir, "blop")
register_main_language("en", book_path)
# have a look at the config
file.edit(file.path(parent_dir, "blop", "_quarto.yml"))
}
```
