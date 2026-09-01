# Get started

The goal of this vignette is to show how you can start and maintain a
new multilingual Quarto project using {babelquarto}. There are two types
of projects: a book or a website. We will look at each type separately
below.

If you want to turn an existing project into a multilingual project,
have a look at
[`vignette("convert")`](https://docs.ropensci.org/babelquarto/articles/convert.md).

## Installing babelquarto

Before you can start a new multilingual project, you need to install
{babelquarto}.

``` r

install.packages('babelquarto', repos = c('https://ropensci.r-universe.dev', 'https://cloud.r-project.org'))
```

Or from [GitHub](https://github.com/) with:

``` r

# install.packages("pak")
pak::pak("ropensci-review-tools/babelquarto")
```

## Starting a multilingual book

To start a multilingual book, use
[`quarto_multilingual_book()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md)
with the `parent_dir` argument to specify where you want to create the
project and the `project_dir` argument to specify the name of the
project. The argument `main_language` is used to specify the main
language of the project and `further_languages` lists all additional
languages.

You can set the `site-url` field to your project’s URL directly by using
the `site_url` parameter of
[`quarto_multilingual_website()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md)/[`quarto_multilingual_book()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md).

``` r

parent_dir <- withr::local_tempdir()
project_dir <- "multilingual_book"
babelquarto::quarto_multilingual_book(
  parent_dir = parent_dir,
  project_dir = project_dir,
  main_language = "en",
  further_languages = c("es", "fr")
)
```

    ✔ Added configuration for en to 'config_path'.

    ✔ Added configuration for es, fr to 'config_path'.

Look at the `_quarto.yml` file in the project directory. To get familiar
with the configuration, take a look at the example below:

    _quarto.yml

``` yaml
project:
  type: book

book:
  site-url: https://example.com
  title: "multilingual_book"
  author: "Firstname Lastname"
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

babelquarto:
  languagelinks: sidebar
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

The file structure of the project looks like this:

``` r

fs::dir_tree(file.path(parent_dir, project_dir))
```

    /tmp/RtmpHtatgW/file8a91c717e9b/multilingual_book
    ├── _quarto.yml
    ├── cover.png
    ├── index.es.qmd
    ├── index.fr.qmd
    ├── index.qmd
    ├── intro.es.qmd
    ├── intro.fr.qmd
    ├── intro.qmd
    ├── references.bib
    ├── references.es.qmd
    ├── references.fr.qmd
    ├── references.qmd
    ├── summary.es.qmd
    ├── summary.fr.qmd
    └── summary.qmd

Each Quarto file has a Spanish and a French version. These files aren’t
automatically translated and are just copies of the original English
version. You will have to provide the translations yourself, or look at
{[babeldown](https://docs.ropensci.org/babeldown/)} for automatic
translation. If you look at the `index.qmd` file, you’ll see that the
French file is called `index.fr.qmd` and the Spanish file is called
`index.es.qmd`.

When you’re ready to render your book, use
[`render_book()`](https://docs.ropensci.org/babelquarto/reference/render.md).
From within a directory, you don’t need to specify the `project_path`
argument as it defaults to `.`.

``` r

withr::with_dir(file.path(parent_dir, project_dir), {
  babelquarto::render_book()
})
```

We end up with three books, that cross-link to each other from the left
sidebar. [Example](https://devguide.ropensci.org/).

By default, in interactive sessions a preview of the project will be
opened, using the servr package. See the [Previewing your multilingual
project section](#preview) for further details.

## Starting a multilingual website

To start a multilingual website, use
[`quarto_multilingual_website()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md)
with the `parent_dir` argument to specify where you want to create the
project and the `project_dir` argument to specify the name of the
project. The argument `main_language` is used to specify the main
language of the project and `further_languages` lists all additional
languages.

You can set the `site-url` field to your project’s URL directly by using
the `site_url` parameter of
[`quarto_multilingual_website()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md)/[`quarto_multilingual_book()`](https://docs.ropensci.org/babelquarto/reference/quarto_multilingual_book.md).

``` r

parent_dir <- withr::local_tempdir()
project_dir <- "multilingual_website"
babelquarto::quarto_multilingual_website(
  parent_dir = parent_dir,
  project_dir = project_dir,
  main_language = "en",
  further_languages = c("es", "fr")
)
```

    ✔ Added configuration for en to 'config_path'.

    ✔ Added configuration for es, fr to 'config_path'.

Look at the `_quarto.yml` file in the project directory. To get familiar
with the configuration, take a look at the example below:

    _quarto.yml

``` yaml
project:
  type: website

website:
  site-url: https://example.com
  title: "multilingual_website"
  navbar:
    left:
      - href: index.qmd
        text: Home
      - about.qmd

format:
  html:
    theme:
      - cosmo
      - brand
    css: styles.css
    toc: true

babelquarto:
  languagelinks: navbar
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
author-es: author in es
author-fr: author in fr
lang: en
```

Note that the fields like `title-es`, `description-es`, `author-es` are
not indented so you could choose to cut and paste them below the default
language’s `title`, `description`, `author` to more easily remember to
update them if needed.

The file structure of the project looks like this:

``` r

fs::dir_tree(file.path(parent_dir, project_dir))
```

    /tmp/RtmpHtatgW/file8a934cf1e61/multilingual_website
    ├── _quarto.yml
    ├── about.es.qmd
    ├── about.fr.qmd
    ├── about.qmd
    ├── index.es.qmd
    ├── index.fr.qmd
    ├── index.qmd
    └── styles.css

Each Quarto file has a Spanish and a French version. These files aren’t
automatically translated and are just copies of the original English
version. You will have to provide the translations yourself, or look at
{[babeldown](https://docs.ropensci.org/babeldown/)} for automatic
translation. If you look at the `index.qmd` file, you’ll see that the
French file is called `index.fr.qmd` and the Spanish file is called
`index.es.qmd`.

When you’re ready to render your website, use
[`babelquarto::render_website()`](https://docs.ropensci.org/babelquarto/reference/render.md):

``` r

babelquarto::render_website(file.path(parent_dir, project_dir))
```

We end up with a multilingual website.
[Example](https://maelle.github.io/babelsite),
[source](https://github.com/maelle/babelsite)

Note that the `_quarto.yml` file created in this process has an example
entry set for `site-url:`. Depending on how your multilingual project is
being deployed, you may need to either remove or update this entry or
alternatively, set the url during rendering by using the `site_url`
argument in the render functions (e.g.,
`babelquarto::render_website(site_url = "https://your.blog.net/your-multilingual-book/")`).

## Previewing your multilingual project

Once you have rendered your project, you will have a `_site` or `_book`
folder in your project. In Quarto you would use `quarto preview` to get
a look at what your project looks like. Because of the way {babelquarto}
operates, this isn’t possible. You can however preview your files using
the [{servr}
package](https://cran.rstudio.com/web/packages/servr/index.html).

You can use [`servr::httw()`](https://rdrr.io/pkg/servr/man/httd.html)
to preview your project.

``` r

# For a multilingual website
servr::httw("_site")

# For a multilingual book
servr::httw("_book")
```

This will show an URL that you can open in your IDE or browser to see
your project.

If the publishing source for your multilingual project is a ‘docs’
folder in your repository, you can preview the output with
`servr::httw("docs")`.

## Publishing your project

Your Quarto multilingual website or book is a static website. To publish
it, you need to deploy the output folder, i.e. `_site` or `_book`. That
content can be served on any service, for instance GitHub Pages or
Netlify.

You cannot rely on usual tooling by Quarto because that would only
publish the main language.

You need to publish the entire output folder, including the language
folders. [Example workflow using GitHub Pages by committing the output
folder to a gh-pages
branch](https://github.com/ropensci/dev_guide/blob/6f9d066d0207e83588a4d9c8dabd93e015083e13/.github/workflows/dev.yml#L58).

For details on local rendering and publishing to GitHub Pages project
sites, see
[`vignette("local-render")`](https://docs.ropensci.org/babelquarto/articles/local-render.md).

## Next steps

Take a deeper dive into the configuration options available in
{babelquarto} and have a look at
[`vignette("configuration")`](https://docs.ropensci.org/babelquarto/articles/configuration.md).

If you want to translate your multilingual project using automatic
translation with DeepL, you should have a look at
[babeldown](http://docs.ropensci.org/babeldown/articles/quarto.md).

If you want to setup your own CI and deploy your website, have a look at
[`vignette("render-with-ci")`](https://docs.ropensci.org/babelquarto/articles/render-with-ci.md).

If you need to personalize the Quarto templates, have a look at
[`vignette("custom-templates")`](https://docs.ropensci.org/babelquarto/articles/custom-templates.md).
