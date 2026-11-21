# Filter the freeze directory

This function removes from freeze directory the files that do not match
the language code to avoid using the wrong cache values for code
computations.

## Usage

``` r
filter_freeze_directory(temporary_directory, project_name, language_code)
```

## Arguments

- temporary_directory:

  Temporary directory where the project is

- project_name:

  Name of the project directory

- language_code:

  The Language code for the current rendering
