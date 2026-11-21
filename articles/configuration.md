# Configuration

The goal of this vignette is to show the configuration options that are
available in {babelquarto}.

## Basic configuration

When you start a {babelquarto} project, from scratch or from an existing
project, your `_quarto.yml` file will contain a number of new options:

    _quarto.yml

``` yaml
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

By default, {babelquarto} will have the following options under the
`babelquarto` key:

|  |  |
|----|----|
| `languagelinks` | Where the menu with the links to other languages will be placed. Can be either `sidebar` (default for books) or `navbar` (default for websites). |
| `languagecodes` | A list with each language defined. Each entry has a `name` with the language abbreviation (for example *en* or *es*. The `text` key changes the text used for the links to this language. It should follow the same standard as for the [`lang` Quarto parameter](https://quarto.org/docs/authoring/language.html#lang-option) and should be used in filenames e.g. `index.es.qmd` except for the main language. |
| `mainlanguage` | The main language of the project. |
| `languages` | An array of the additional languages (not including the main language). |

In addition to the `babelquarto` key, you will see language specific
keys for `title`, `description` and `author`. These keys allow you to
have a specific title, description or author for each additional
language.

### Customizing the language menu labels

If you want the choice to be between, say “English” and “Español” rather
than “Version in en” and “Version in es”, add these fields under the
`babelquarto/languagecodes` key, in `_quarto.yml`:

    _quarto.yml

``` yaml
babelquarto:
  languagecodes:
  - name: es
    text: "Español"
  - name: en
    text: "English"
```

Using
[`register_main_language()`](https://docs.ropensci.org/babelquarto/reference/register_main_language.md)
and
[`register_further_languages()`](https://docs.ropensci.org/babelquarto/reference/register_further_languages.md)
will create the boilertemplate for these fields.

## Configure the base URL

If you need to configure a base URL, you can use the [usual Quarto
field](https://quarto.org/docs/websites/website-tools.html), or use the
`site_url` argument of
[`render_book()`](https://docs.ropensci.org/babelquarto/reference/render.md)
to temporarily override the `site-url` from the configuration file.

    _quarto.yml

``` yaml
book:
  site-url: https://example.com
```

    _quarto.yml

``` yaml
website:
  site-url: https://example.com
```

In interactive sessions, the
[`render_book()`](https://docs.ropensci.org/babelquarto/reference/render.md)
and
[`render_website()`](https://docs.ropensci.org/babelquarto/reference/render.md)
functions will automatically set the `site-url` to `""` to allow
previewing with
[`servr::httw()`](https://rdrr.io/pkg/servr/man/httd.html) on a
localhost.

If you render your multilingual book or website in a CI context, you
need will need to set the `BABELQUARTO_CI_URL` environment variable. See
[`vignette("render-with-ci")`](https://docs.ropensci.org/babelquarto/articles/render-with-ci.md)
for more information.

## Configure the icon of the language switch button

Any [Bootstrap icon](https://icons.getbootstrap.com/) can be used
instead of the globe button. For getting a backpack icon you’d use:

    _quarto.yml

``` yaml
babelquarto:
  icon: "bi bi-backpack"
```

For getting no icon you’d use:

    _quarto.yml

``` yaml
babelquarto:
  icon: ""
```

If you want to style the button with CSS, note it has the id
`"languages-button"` and the class `"babelquarto-languages-button"`.

## Translate parts in multilingual books

In multilingual books, if you use parts to structure your book, you can
translate the part titles like so:

    _quarto.yml

``` yaml
book:
  chapters:
    - index.qmd
    - part: Foreword
      part-fr: Préface
      chapters:
        - foreword.qmd
    - part: Explore
      part-fr: Explorer
      chapters:
        - intro-explore.qmd
        - data-visualisation.qmd
```

For each additional language, you can use a `part-xx` key to translate
the part title.

## Using profiles for advanced configuration

You can leverage [Quarto project
profiles](https://quarto.org/docs/projects/profiles.html) to have both
language-specific and general configuration profiles in the same
project.

### Language-specific profiles

{babelquarto} automatically loads a language profile if it exists in the
project directory and follows our naming convention:
`_quarto-<languagecode>.yml`. Settings specified in the
language-specific profile always take precedence over other profiles for
files in that language (see details on [metadata merging in Quarto
documentation](https://quarto.org/docs/projects/quarto-projects.html#metadata-merging))

For example, let’s say you have a project with English as the main
language and French as an additional language. {babelquarto} will load
the *en* profile when rendering the English version of the project, and
then the *fr* profile when rendering the French version.

You could for example have different navigation menus for each language:

    _quarto.yml

``` yaml
website:
  navbar:
    title: "My Website"
    left:
      - label: "Home"
        href: "index.qmd"
    right:
      - label: "About"
        href: "about.qmd"
```

    _quarto-fr.yml

``` yaml
website:
  navbar:
    title: "Mon site web"
    left:
      - label: "Accueil"
        href: "index.qmd"
    right:
      - label: "À propos"
        href: "about.qmd"
```

Note that `output-dir` and `bablquarto` YAML options cannot be specified
in the language-specific profile.

### Additional profiles

For complex projects, you might also want to use different profiles.
When you render a project, you can pass a `profile` argument to
[`render_book()`](https://docs.ropensci.org/babelquarto/reference/render.md)
and
[`render_website()`](https://docs.ropensci.org/babelquarto/reference/render.md)
to use [Quarto project
profiles](https://quarto.org/docs/projects/profiles.html). This feature
allows {babelquarto} options (described in this vignette) to be
specified in a file other than `_quarto.yml`.
