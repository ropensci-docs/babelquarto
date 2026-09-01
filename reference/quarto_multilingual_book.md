# Create a starter/example quarto multilingual book or website

Create a starter/example quarto multilingual book or website

## Usage

``` r
quarto_multilingual_book(
  parent_dir,
  project_dir,
  main_language = "en",
  further_languages = c("es", "fr"),
  register_languages = TRUE,
  site_url = "https://example.com",
  placement = c("sidebar", "navbar")
)

quarto_multilingual_website(
  parent_dir,
  project_dir,
  main_language = "en",
  further_languages = c("es", "fr"),
  register_languages = TRUE,
  site_url = "https://example.com",
  placement = c("navbar", "sidebar")
)
```

## Arguments

- parent_dir:

  Folder where to create the project folder.

- project_dir:

  Project (book, website) folder name.

- main_language:

  Code for main languages.

- further_languages:

  Codes for not main languages.

- register_languages:

  Whether to register languages (logical).

- site_url:

  Site URL for the book/site-url or website/site-url part of the Quarto
  configuration.

- placement:

  Where to place the language links (sidebar, navbar).

## Value

The path to the created project.

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
}
```
