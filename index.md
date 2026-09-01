# babelquarto

The goal of {babelquarto} is to render a Quarto multilingual project,
book or website. When using babelquarto, through a single function call
you can render multilingual content (`index.qmd`, `index.es.qmd`,
`index.pt.qmd`, etc.) to a fully functional Quarto book or website
featuring a button to switch languages.

Note that babelquarto does not *translate* the content! Translation
tooling lives in {[babeldown](https://docs.ropensci.org/babeldown)}.

## Installation

You can install the development version of {babelquarto} from rOpenSci
R-universe:

``` r

install.packages('babelquarto', repos = c('https://ropensci.r-universe.dev', 'https://cloud.r-project.org'))
```

Or from [GitHub](https://github.com/) with:

``` r

# install.packages("pak")
pak::pak("ropensci-review-tools/babelquarto")
```

If you want to avoid reading messages from babelquarto such as “Edited
`_quarto.yml`”, set the `"babelquarto.quiet"` option to `TRUE`.

``` r

options("babelquarto.quiet" = TRUE)
```

## Getting Started

The {babelquarto} package allows you to create and render a multilingual
Quarto project, book or website. A multilingual project is based on a
main language and can feature any number of additional languages. The
languages are registered once and are then present in your `_quarto.yml`
configuration file under the `babelquarto` key. Each Quarto Markdown
file in your project can then be translated into these further languages
and these will be used to generate the project in each language.

If you start from scratch, you might want to look at
[`babelquarto::quarto_multilingual_book()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md)
or
[`babelquarto::quarto_multilingual_website()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md)
and read
[`vignette("babelquarto")`](https://docs.ropensci.org/babelquarto/articles/babelquarto.md).

If you already have and existing Quarto project and want to convert it
to a multilingual project, you can use
[`babelquarto::register_main_language()`](https://docs.ropensci.org/babelquarto/reference/register_main_language.md)
and
[`babelquarto::register_further_languages()`](https://docs.ropensci.org/babelquarto/reference/register_further_languages.md)
to get started. For more information you can read
[`vignette("convert")`](https://docs.ropensci.org/babelquarto/articles/convert.md).

## Linking

If you use cross-references in your Quarto book, make sure they use
explicit anchors, not the section title, as that title will be different
between languages.

## Examples

To get a feel of what a multilingual book can look like, you can have a
look at this book: [*rOpenSci Packages: Development, Maintenance, and
Peer Review*](https://devguide.ropensci.org/).

For a multilingual website, you can check out [Joel Nitta’s
website](https://www.joelnitta.com/).
