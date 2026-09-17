# Changelog

## babelquarto (development version)

- Add support for language-specific abstract in books.
- Improve support and documentation for quarto profiles (now using
  [`quarto::quarto_inspect()`](https://quarto-dev.github.io/quarto-r/reference/quarto_inspect.html)
  to obtain correct profile-specific configuration).
- Fix and document behavior for `CNAME` files
  ([\#120](https://github.com/ropensci-review-tools/babelquarto/issues/120),
  [@luisDVA](https://github.com/luisDVA))

## babelquarto 0.1.0

### Features

- In interactive sessions, the `render_` functions now override
  `site-url` to be `""` so that previewing with
  [`servr::httw()`](https://rdrr.io/pkg/servr/man/httd.html) works.
- For easier styling, the language button now has the class
  `"babelquarto-languages-button"`.
- Add verbosity to `register_` functions, that one can turn off through
  an option.

\## Documentation improvements

- clarify the default value of `project_path` in
  [`render_book()`](https://docs.ropensci.org/babelquarto/reference/render.md),
  in the “Get started” vignette.
- clarify the default value of `project_path` in `register_` functions,
  in the “Converting an existing project” vignette.
- strengthen the case for the package in the README.
- mention `site-url` param of `quarto_multilingual_` functions.
- new section in the Get started vignette, “publishing your project”.
- clarify `languagecodes` in configuration vignette.
- clarify `site-url` in configuration vignette.
- document how to get no icon, in configuration vignette.
- clarify profile naming convention, in configuration vignette.
- clarify `BABELQUARTO_CI_URL`, in render-with-ci vignette.

### Bug fixes

- make it possible to
  [`register_further_languages()`](https://docs.ropensci.org/babelquarto/reference/register_further_languages.md)
  for more languages in a second step.
- The `render_` functions now correctly use `site_url` when provided.
- avoid unnecessary empty lines in Quarto config when using
  [`register_main_language()`](https://docs.ropensci.org/babelquarto/reference/register_main_language.md).

## babelquarto 0.0.1

- Initial rOpenSci submission.
- Fix handling on sitemap: it needed to be conditional on there being a
  sitemap.
