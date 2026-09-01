# Convert an existing project

If you want to turn an existing project into a multilingual project, you
can use {babelquarto}’s
[`register_main_language()`](https://docs.ropensci.org/babelquarto/reference/register_main_language.md)
and
[`register_further_languages()`](https://docs.ropensci.org/babelquarto/reference/register_further_languages.md)
functions.

Let’s start with a book whose main language is English.

``` r

parent_dir <- withr::local_tempdir()
project_dir <- "babelbook"
quarto_bin <- quarto::quarto_path()
withr::with_dir(parent_dir, {
  sys::exec_wait(
    quarto_bin,
    args = c("create-project", project_dir, "--type", "book")
  )
})
```

First you’ll need to register the main language in the Quarto
configuration:

``` r

project_path <- file.path(parent_dir, project_dir)
withr::with_dir(project_path, {
  babelquarto::register_main_language(main_language = "en")
})
```

    ✔ Added configuration for en to 'config_path'.

Then you can add further languages, say Spanish and French:

``` r

withr::with_dir(project_path, {
  babelquarto::register_further_languages(further_languages = c("es", "fr"))
})
```

    ✔ Added configuration for es, fr to 'config_path'.

The `project_path` of
[`register_main_language()`](https://docs.ropensci.org/babelquarto/reference/register_main_language.md)
and
[`register_further_languages()`](https://docs.ropensci.org/babelquarto/reference/register_further_languages.md)
defaults to `.` so from within that project path, there’s no need to
specify it.

We end up with a multilingual book in English and Spanish. If you look
at the `_quarto.yml` file in the project directory, you’ll see that the
`main_language` key is `en` and the `languages` key contains `es` and
`fr`.

    _quarto.yml

``` yaml
project:
  type: book

book:
  title: "babelbook"
  author: "Norah Jones"
  date: "9/1/2026"
  chapters:
    - index.qmd
    - intro.qmd
    - summary.qmd
    - references.qmd

bibliography: references.bib

format:
  html:
    theme:
      - cosmo
      - brand
  pdf:
    documentclass: scrreprt

babelquarto:
  languagecodes:
  - name: es
    text: "Version in es"
  - name: fr
    text: "Version in fr"
  - name: en
    text: "Version in en"
  mainlanguage: 'en'
  languages: ['es', 'fr']
title-es: title in es
title-fr: title in fr
description-es: description in es
description-fr: description in fr
abstract-es: abstract in es
abstract-fr: abstract in fr
author-es: author in es
author-fr: author in fr
lang: en
```

You can now start translating your book into Spanish and French. Each
file of you project can be translated by adding a suffix to the file
name. For example, the Spanish version of `index.md` will be in
`index.es.md` and the French version in `index.fr.md`.

You will have to provide the translations yourself. If you want to
translate your multilingual project using automatic translation with
DeepL, you should have a look at
[babeldown](http://docs.ropensci.org/babeldown/articles/quarto.md).

## Next steps

Take a deeper dive into the configuration options available in
{babelquarto} and have a look at
[`vignette("configuration")`](https://docs.ropensci.org/babelquarto/articles/configuration.md).

If you want to deploy your website on continuous integration, have a
look at
[`vignette("render-with-ci")`](https://docs.ropensci.org/babelquarto/articles/render-with-ci.md).

If you need to personalize the quarto templates, have a look at
[`vignette("custom-templates")`](https://docs.ropensci.org/babelquarto/articles/custom-templates.md).
