# Pypi Publishing Actions Example

This repository contains GitHub Actions workflows that automate the process of creating GitHub releases and publishing a Python package to PyPI when a new version is specified in the `pyproject.toml` file.

## Repository Structure

```plaintext
.
├── .github
│   ├── workflows
│   │   ├── create_release_if_new_version.yml
│   │   └── publish-to-pypi.yml
│   └
└
```

## Workflows

### Create Release if New Version (`create_release_if_new_version.yml`)

This workflow is responsible for creating a GitHub release when a new version of the Python package is specified in the `pyproject.toml` file. The workflow performs the following steps:

- Gets triggered on pushes to the `main` branch.
- Checks out the repository code.
- Sets up Python.
- Installs necessary Python packages (`toml` and `packaging`) required to read `pyproject.toml` and parse versions.
- Retrieves the current version from `pyproject.toml`.
- Fetches all tags to check against the latest tag.
- Checks if the version is incremented compared to the latest tag.
- If the version is incremented, it creates a new git tag.
- Pushes the new git tag to the repository.
- Creates a new GitHub release with the new tag.

### Publish Python Package to PyPI (`publish-to-pypi.yml`)

This workflow is responsible for building the Python package and publishing it to PyPI. The workflow performs the following steps:

- Gets triggered by the successful completion of the "Create Release if New Version" workflow.
- Checks out the repository code.
- Sets up Python.
- Installs dependencies required to build and publish the package (`build` and `twine`).
- Builds the Python package.
- Publishes the package to PyPI or TestPyPI based on the configuration.

## Setup

- Configure the following secrets in your GitHub repository settings under "Secrets":

  - `PYPI_API_TOKEN` - Your API token for PyPI (production).
  - `TEST_PYPI_API_TOKEN` - Your API token for TestPyPI (testing).

- Ensure that your project contains a valid `pyproject.toml` file with the package version specified.

- Push your changes to the `main` branch.

## Usage

- Make changes to your Python package.

- Update the version in `pyproject.toml` according to semantic versioning.

- Push the changes to the `main` branch.

- The "Create Release if New Version" workflow will run. If the version is incremented, a GitHub release will be created, and the "Publish Python Package to PyPI" workflow will be triggered.

- The "Publish Python Package to PyPI" workflow will build and publish your package to the configured PyPI repository (TestPyPI or production PyPI).

## Note

- It is important to increment the version in `pyproject.toml` according to [semantic versioning](https://semver.org/) standards for the workflow to create a release.

- Ensure you have properly configured the `PYPI_API_TOKEN` and `TEST_PYPI_API_TOKEN` secrets in your GitHub repository.

- When Github Repo is Protected, you need to allow `GITHUB_TOKEN` Read and Write access to the repository. Go to the repository Settings > Actions > General > Workflow Permissions > Allow Read and Write permissions.

## Contributing

Contributions for improving the workflows are welcome. Please submit a pull request with your changes.

## License

This project is licensed under the terms of the [MIT License](LICENSE.md).
