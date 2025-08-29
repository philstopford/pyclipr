# Wheel Building System

This document describes the wheel building system for pyclipr using GitHub Actions.

## Overview

The project now uses a modern wheel building system based on [cibuildwheel](https://cibuildwheel.readthedocs.io/) to create distributable wheels for multiple platforms and Python versions.

## Supported Platforms

- **Linux**: manylinux wheels compatible with most Linux distributions
- **Windows**: Native Windows wheels for x64 architecture  
- **macOS**: Universal wheels for both Intel and Apple Silicon Macs

## Supported Python Versions

- Python 3.7
- Python 3.8  
- Python 3.9
- Python 3.10
- Python 3.11
- Python 3.12

## Workflows

### `build-wheels.yml`

The main wheel building workflow that:
- Builds wheels for all supported platforms and Python versions
- Installs system dependencies (eigen, cmake) automatically
- Tests each built wheel by importing the module
- Uploads wheels as artifacts for manual inspection
- Publishes to PyPI when a release is created

### `ci.yml`

A lightweight continuous integration workflow that:
- Tests basic building across platforms
- Runs on every push and pull request
- Provides quick feedback on build issues

## Configuration

Wheel building is configured via:
- `pyproject.toml`: cibuildwheel configuration
- Workflow environment variables
- Platform-specific dependency installation scripts

## Dependencies

The system automatically handles installation of:
- **eigen3**: Linear algebra library (system package)
- **cmake**: Build system (≥3.15 required)
- **Python build tools**: setuptools, wheel, etc.

## Publishing

Wheels are automatically published to PyPI when:
1. A GitHub release is created/published
2. The `PYPI_API_TOKEN` secret is configured

## Local Development

For local development, you can still use the traditional approach:

```bash
git clone --recursive https://github.com/philstopford/pyclipr.git
cd pyclipr
python setup.py build_ext --inplace
```

## Migration from Old System

The previous `pythonpublish.yml` workflow has been deprecated and replaced with this new system. The old workflow:
- Only supported Windows and macOS publishing
- Didn't provide Linux wheels
- Used a custom build matrix instead of cibuildwheel

The new system provides better platform compatibility and follows modern Python packaging best practices.