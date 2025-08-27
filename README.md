# run-pkg-tests V3

This GitHub action runs the test-suite of a GAP package.

## Usage

The action `run-pkg-tests` has to be called by the workflow of a GAP
package.
By default it runs the file `tst/testall.g`, gathering coverage while doing so.

Its behaviour can be customized via the inputs below.

### Inputs

All of the following inputs are optional.

- `NO_COVERAGE`:
  - Set to a non-empty string to suppress gathering coverage.
  - default: `''`
- `GAP_TESTFILE`:
  - The name of the GAP file to be read for executing the package tests.
  - default: The `TestFile` specified in `PackageInfo.g`
- `only-needed`:
  - If set to a non-empty string, then only needed dependencies of the package being tested are loaded.
  - default: `''`
- `load-all`:
  - If set to a non-empty string, then executed `LoadAllPackages()` before the package being tested.
  - default: `''`
- `pre-gap`:
  - Prefix for the `GAP` shell variable used by this action to launch GAP (e.g.
    setting this to `valgrind --trace-children=yes --leak-check=full` will run
    GAP through valgrind)'
  - default: `''`
- `warnings-as-errors`:
  - If set to a non-empty string, then any errors produced whilst loading the package will be treated as errors.
  - default: `'true'`

### What's new in V3

The main difference between V3 and version V2 is the change to the default
value of `warnings-as-errors`. Specifically, in V2, warnings were not treated as
errors by default, whereas in V3 they are.

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
      - uses: gap-actions/setup-gap@v2
      - uses: gap-actions/build-pkg@v1
      - uses: gap-actions/run-pkg-tests@v3
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
