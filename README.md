# Check with OSV Detector

A GitHub Action for checking project dependencies for known security
vulnerabilities using the
[`osv-detector`](https://github.com/G-Rath/osv-detector) CLI tool.

## Usage

```yaml
jobs:
  check-dependencies:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Check dependencies for security vulnerabilities
        uses: g-rath/check-with-osv-detector@main
```

This action assumes it's running on `ubuntu-latest` and so downloads the Linux
amd64 binary. If for some reason you want to use a different OS and
architecture, you can manually specify the binary to download with the
`osv-detector-binary` input:

```yaml
jobs:
  check-dependencies:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Check dependencies for security vulnerabilities
        uses: g-rath/check-with-osv-detector@main
        with:
          osv-detector-binary: osv-detector_0.5.0_darwin_amd64
```

## Passing paths to files and directories

By default, the detector checks the working directory - you can use the `paths`
input to specify alternative files and directories to check:

```yaml
jobs:
  check-dependencies:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Check dependencies for security vulnerabilities
        uses: g-rath/check-with-osv-detector@main
        with:
          # prettier-ignore
          paths:
            backend/
            frontend/
```

## Passing flags

You can provide additional flags to the detector using the `flags` input:

```yaml
jobs:
  check-dependencies:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Check dependencies for security vulnerabilities
        uses: g-rath/check-with-osv-detector@main
        with:
          paths: ./npm-shrinkwrap.json
          # prettier-ignore
          flags:
            --parse-as package-lock.json
            --ignore GHSA-vh95-rmgr-6w4m
```

You can find out what flags are available for a particular version of the
detector by passing the `--help` flag.
