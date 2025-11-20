# run-pkg-tests

This GitHub action runs the test-suite of a GAP package.

## Usage

The action `run-pkg-tests` has to be called by the workflow of a GAP
package.
By default it runs the file `tst/testall.g`, gathering coverage while doing so.

Its behaviour can be customized via the inputs below.

### Inputs

All of the following inputs are optional.

- `coverage`:
  - Boolean that determines whether GAP is instructed to collect code coverage via the `--cover` argument.
  - default: `'true'`
- `testfile`:
  - Name of the GAP file to be read for executing the package tests.
  - default: The `TestFile` specified in `PackageInfo.g`
- `mode`:
  - Value that determines which packages are loaded before the package is tested. The possible values
    are `'default'`, `'onlyneeded'` or `'loadall'`. The option `'default'` loads GAP with default
    set of package; `'onlyneeded'` loads only the needed dependencies of the package being tested;
    `'loadall'` executes `LoadAllPackages()` before the package being tested.
  - default: `'default'`
- `pre-gap`:
  - Prefix for the `GAP` shell variable used by this action to launch GAP (e.g.
    setting this to `valgrind --trace-children=yes --leak-check=full` will run
    GAP through valgrind)'
  - default: `''`
- `warnings-as-errors`:
  - Boolean that determines whether any warnings produced whilst loading the package will be treated as errors.
  - default: `'true'`

### What's new in v4

There are several changes between v3 and v4: the introduction of the `mode` option,
the renaming of some options,
and the restriction of the allowed values for boolean-like options.

#### Renamed options

The `GAP_TESTFILE` input was renamed to `testfile`, with no functional changes.

The `NO_COVERAGE` input was replaced by the `coverage` input with flipped
meaning. Thus if you previously set `NO_COVERAGE` to `false` you should now
set `coverage` to `true`.

#### The `mode` option

The `mode` option was introduced to replace the `only-needed` and `load-all`
options. In particular:

- the setting `only-needed: 'true'` with v3 should be replaced by
  `mode: 'onlyneeded'` with v4, which will result in `GAP` only loading the
  needed dependencies of the package being tested;
- the setting `load-all: 'true'` with v3 should be replaced by `mode: 'loadall'`
  with v4, which will result in GAP executing `LoadAllPackages()` before running
  the package tests;
- the combination of `only-needed: 'false'` and `load-all: 'false'` with v3
  should be replaced with by `mode :'default'` with v4, which loads `GAP` with
  the default set of packages.

It is no longer possible to exactly replicate the behaviour obtained by setting
`only-needed: 'true'` and `load-all: 'true'`. Instead, this should be replaced
with `mode: 'loadall'`.

#### Restricted boolean-like options

In v3, the boolean-like options such as `warnings-as-errors` accepted
any string value. In v4, they only accept the values `'true'` and
`'false'`, anything else results in an error.

### What's new in v3

The main difference between v3 and version v2 is the change to the default
value of `warnings-as-errors`. Specifically, in v2, warnings were not treated as
errors by default, whereas in v3 they are.

### Example

The following is a minimal example to run this action.

```yaml
name: CI

on:
  push:
  pull_request:

jobs:
  # The CI test job
  test:
    name: CI test
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - uses: gap-actions/setup-gap@v3
      - uses: gap-actions/build-pkg@v2
      - uses: gap-actions/run-pkg-tests@v4
```

## Contact

Please submit bug reports, suggestions for improvements and patches via
the [issue tracker](https://github.com/gap-actions/run-pkg-tests/issues).

## License

The action `run-pkg-tests` is free software; you can redistribute
and/or modify it under the terms of the GNU General Public License as published
by the Free Software Foundation; either version 2 of the License, or (at your
opinion) any later version. For details, see the file `LICENSE` distributed
with this action or the FSF's own site.
