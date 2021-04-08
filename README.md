# run-test-for-packages

This GitHub action runs tests and uploads coverage data for GAP packages.

## Usage

The action `run-test-for-packages` has to be called by the workflow of a GAP
package `gap-package`.
By default it
- runs the file `tst/testall.g`,
- gathers coverage data during the run of `tst/testall.g`, and
- uploads the coverage data to `codecov.io`.

Its behaviour can be customized via the inputs below.

### Inputs

All of the following inputs are optional.

- `NO_COVERAGE`:
  - Set to a non-empty string to suppress gathering coverage.
  - default: `''`
- `GAP_TESTFILE`:
  - If set to a non-empty string, the file with that name is read by `run_tests.sh`
  - default: `''`

### Example

The following is a minimal example to run this action.

```yaml
name: CI

on:
  push:
    branches:
      - master # change this to 'main' if necessary!
  pull_request:

jobs:
  # The CI test job
  test:
    name: CI test
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - uses: gap-actions/setup-gap-for-packages@v1
      - uses: gap-actions/run-test-for-packages@v1
```

## Contact
Please submit bug reports, suggestions for improvements and patches via
the [issue tracker](https://github.com/gap-actions/run-test-for-packages/issues)
or via email to
[Sergio Siccha](mailto:siccha@mathematik.uni-kl.de).

## License
The action `run-test-for-packages` is free software; you can redistribute
and/or modify it under the terms of the GNU General Public License as published
by the Free Software Foundation; either version 2 of the License, or (at your
opinion) any later version. For details, see the file `LICENSE` distributed
with this action or the FSF's own site.
