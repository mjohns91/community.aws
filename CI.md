# Continuous Integration (CI)

## Community AWS Testing

GitHub Actions are used to run the CI for the community.aws collection. The workflows used for the CI can be found [here](https://github.com/ansible-collections/community.aws/tree/main/.github/workflows). These workflows include jobs to run the unit tests, sanity tests, linters, and changelog checks.

The collection uses reusable workflows from [ansible-network/github_actions](https://github.com/ansible-network/github_actions) for standardized testing.

To learn more about the testing strategy, see [this proposal](https://github.com/ansible-collections/cloud-content-handbook/blob/main/Proposals/core_collection_dependency.md).

### PR Testing Workflows

The following tests run on every pull request:

| Job | Description | Python Versions | ansible-core Versions |
| --- | ----------- | --------------- | --------------------- |
| Changelog | Checks for the presence of changelog fragments | 3.12 | devel |
| Linters | Runs `black`, `isort`, `flynt`, `flake8`, and `ansible-lint` via tox | 3.12 | devel |
| Sanity | Runs ansible sanity checks | See compatibility table below | devel, milestone, stable-2.17, stable-2.18, stable-2.19, stable-2.20 |
| Unit tests | Executes unit test cases | See compatibility table below | devel, milestone, stable-2.17, stable-2.18, stable-2.19, stable-2.20 |
| Galaxy Importer | Validates collection can be imported by Galaxy | 3.12 | latest |

**Note:** Integration tests are not currently part of the automated CI pipeline for community.aws. Integration tests must be run locally with AWS credentials.

### Python Version Compatibility by ansible-core Version

These are outlined in the collection's [/tox.ini](/tox.ini) file (`envlist`) and GitHub Actions workflow exclusions.

For the official Ansible core support matrix, see the [Ansible documentation](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#ansible-core-support-matrix).

The collection requires:
- **ansible-core**: >=2.17.0
- **Python**: >=3.10 (see testing matrix below)

| ansible-core Version | Sanity Tests | Unit Tests |
| -------------------- | ------------ | ---------- |
| devel | 3.12, 3.13, 3.14 | 3.12, 3.13, 3.14 |
| milestone | 3.12, 3.13, 3.14 | 3.12, 3.13, 3.14 |
| stable-2.20 | 3.12, 3.13, 3.14 | 3.12, 3.13, 3.14 |
| stable-2.19 | 3.11, 3.12, 3.13 | 3.11, 3.12, 3.13, 3.14 |
| stable-2.18 | 3.11, 3.12, 3.13 | 3.11, 3.12, 3.13, 3.14 |
| stable-2.17 | 3.10, 3.11, 3.12 | 3.10, 3.11, 3.12 |

**Note**:
- ansible-core 2.17 reached EOL in November 2025.
- ansible-core 2.18 reaches EOL in May 2026.

### Additional Dependencies

The collection has the following dependencies:
- **Python packages**: boto3 >=1.35.0, botocore >=1.35.0
- **Collections**: amazon.aws (for shared module_utils and common AWS functionality)
- **AWS credentials**: Required for running integration tests locally (not part of automated CI)

### Reusable Workflows

The community.aws collection uses the following reusable workflows from [ansible-network/github_actions](https://github.com/ansible-network/github_actions):

- **[sanity.yml](https://github.com/ansible-network/github_actions/blob/main/.github/workflows/sanity.yml)** - Runs ansible-test sanity across multiple ansible-core and Python versions
- **[unit_source.yml](https://github.com/ansible-network/github_actions/blob/main/.github/workflows/unit_source.yml)** - Runs unit tests from source across multiple ansible-core and Python versions
- **[changelog.yml](https://github.com/ansible-network/github_actions/blob/main/.github/workflows/changelog.yml)** - Validates changelog fragments for pull requests
- **[tox.yml](https://github.com/ansible-network/github_actions/blob/main/.github/workflows/tox.yml)** - Runs tox environments for linting
- **[galaxy_importer.yml](https://github.com/ansible-network/github_actions/blob/main/.github/workflows/galaxy_importer.yml)** - Validates the collection with galaxy-importer

## Release Workflows

These workflows handle collection releases, backports, and Galaxy publishing. The following table lists the workflows and how they are triggered.

| Workflow | Description | Trigger |
| -------- | ----------- | ------- |
| galaxy-importer | Validates that collection can be imported into Galaxy | Pull request / Push to main or stable-* / Daily schedule (13:00 UTC) |
| release-tag | Generates GitHub release and publishes to Galaxy | Tag push (e.g., v11.0.0) |
| release-manual | Manually trigger a release | Manual workflow_dispatch by repository maintainer |
| backports | Automatically creates backport PRs for stable branches | Pull request labeled with backport-* labels |
| update-variables | Updates AWS service variables (regions, AZs, etc.) | Manual workflow_dispatch |
