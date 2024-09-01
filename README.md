# run-pkg-tests V2

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
  - default: `'tst/testall.g'`
- `pre-gap`:
  - Commands to be executed immediately before GAP is launched. For example,
    specifying `'valgrind --trace-children=yes --leak-check=full'` will ensure
    that GAP is launched using Valgrind, and the test-suite will be checked for
    memory leaks.
  - default: `''`

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
      - uses: actions/checkout@v4
      - uses: gap-actions/setup-gap@v2
      - uses: gap-actions/build-pkg@v1
      - uses: gap-actions/run-pkg-tests@v2
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
