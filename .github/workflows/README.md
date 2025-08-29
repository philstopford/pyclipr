# GitHub Workflows

This directory contains GitHub Actions workflows for the pyclipr project.

## Active Workflows

- **`build-wheels.yml`**: Modern wheel building workflow using cibuildwheel
  - Builds wheels for Linux, Windows, and macOS
  - Supports Python 3.7-3.12
  - Uses cibuildwheel for cross-platform compatibility
  - Uploads to PyPI on releases
  - Can be triggered manually

- **`ci.yml`**: Continuous integration testing
  - Tests building on multiple platforms and Python versions
  - Runs basic import and functionality tests
  - Lighter weight than full wheel building

## Deprecated Workflows

- **`pythonpublish-old.yml`**: Old wheel building approach (DISABLED)
  - Replaced by `build-wheels.yml`
  - Keep for reference but not used

## Usage

- The `build-wheels.yml` workflow will automatically run on:
  - Push to main branch
  - Pull requests to main branch
  - When a release is published
  - Manual trigger via GitHub UI

- The `ci.yml` workflow runs on pushes and pull requests for testing.

For PyPI publishing, make sure the `PYPI_API_TOKEN` secret is configured in the repository settings.