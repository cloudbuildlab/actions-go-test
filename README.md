# actions-go-test

A reusable GitHub Action for running Go tests with comprehensive coverage and build tag support. This action helps maintain code quality by providing flexible test execution options and detailed coverage reporting.

## Features

- Runs Go tests with customizable options
- Configurable Go version
- Support for build tags
- Test coverage reporting with artifacts
- Race condition detection
- Customizable test patterns
- Verbose output options
- Fail-fast mode
- Coverage summary in GitHub step summary
- Coverage data available as artifacts

## Usage

### Basic Usage

```yaml
name: Go Test

on:
  pull_request: {}
  push:
    branches:
      - main
      - master

permissions:
  contents: read
  pull-requests: write
  checks: write
  statuses: write

jobs:
  test:
    uses: cloudbuildlab/actions-go-test/.github/workflows/go-test.yml@v0
```

### Advanced Usage

```yaml
name: Go Test

on:
  pull_request: {}
  push:
    branches:
      - main

permissions:
  contents: read
  pull-requests: write
  checks: write
  statuses: write

jobs:
  test:
    uses: cloudbuildlab/actions-go-test/.github/workflows/go-test.yml@v0
    with:
      go-version: '1.23'
      working-directory: './cmd'
      build-tags: 'integration'
      coverage: true
      coverage-mode: 'atomic'
      coverage-output: 'coverage.out'
      timeout: '5m'
      race: true
      verbose: true
      test-pattern: './...'
      fail-fast: true
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `go-version` | Go version to use | `stable` |
| `working-directory` | Working directory to run tests in | `.` |
| `build-tags` | Build tags to use when running tests | `` |
| `coverage` | Enable test coverage | `false` |
| `coverage-mode` | Coverage mode (atomic, count, set) | `atomic` |
| `coverage-output` | Output file for coverage data | `coverage.out` |
| `timeout` | Test timeout | `10m` |
| `race` | Enable race detection | `false` |
| `verbose` | Enable verbose test output | `false` |
| `test-pattern` | Pattern to match test files | `./...` |
| `fail-fast` | Fail fast on first test failure | `false` |

## Coverage Features

### Coverage Reporting

When coverage is enabled:

- Coverage data is saved as an artifact named `go-coverage`
- A coverage summary is added to the GitHub step summary
- Coverage data is available even if tests fail

### Coverage Modes

- `atomic`: Counts each statement exactly once
- `count`: Counts each statement's execution count
- `set`: Records whether each statement was executed

## Versioning

This workflow follows semantic versioning. You can use it in two ways:

1. **Major Version Tag** (Recommended):

   ```yaml
   uses: cloudbuildlab/actions-go-test/.github/workflows/go-test.yml@v0
   ```

   This will automatically use the latest release within the v0.x.x series.

2. **Specific Version**:

   ```yaml
   uses: cloudbuildlab/actions-go-test/.github/workflows/go-test.yml@v0.1.0
   ```

   This pins to a specific version for maximum stability.

### Version History

See the [Releases](../../releases) page for a full list of versions and changes.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
