# Community AWS Collection
The Ansible Community AWS collection includes a variety of Ansible content to help automate the management of AWS services. This collection is maintained by the Ansible community.

## Contents

- [Description](#description)
- [Communication](#communication)
- [Requirements](#requirements)
  - [Ansible version compatibility](#ansible-version-compatibility)
  - [Python version compatibility](#python-version-compatibility)
  - [AWS SDK version compatibility](#aws-sdk-version-compatibility)
- [Included content](#included-content)
- [Installation](#installation)
- [Use Cases](#use-cases)
- [Testing](#testing)
- [Contributing to this collection](#contributing-to-this-collection)
  - [More information about contributing](#more-information-about-contributing)
- [Support](#support)
- [Release notes](#release-notes)
- [Roadmap](#roadmap)
- [Related Information](#related-information)
- [License Information](#license-information)

## Description

The primary purpose of this collection is to simplify and streamline the management of AWS resources through automation. By leveraging this collection, organizations can reduce manual intervention, minimize errors, and ensure consistent and repeatable deployments. This leads to increased efficiency, faster deployments, and a more agile IT infrastructure.

AWS-related modules and plugins supported by the Ansible Cloud Content team are in a similar, but distinct collection: [amazon.aws](https://github.com/ansible-collections/amazon.aws).

## Communication

* Join the Ansible forum:
  * [Get Help](https://forum.ansible.com/c/help/6): get help or help others.
  * [Posts tagged with 'aws'](https://forum.ansible.com/tag/aws): subscribe to participate in collection-related conversations.
  * [AWS Working Group](https://forum.ansible.com/g/AWS): by joining the team, you will automatically be subscribed to posts tagged with [aws](https://forum.ansible.com/tags).
  * [Social Spaces](https://forum.ansible.com/c/chat/4): gather and interact with fellow enthusiasts.
  * [News & Announcements](https://forum.ansible.com/c/news/5): track project-wide announcements including social events.

* The Ansible [Bullhorn newsletter](https://docs.ansible.com/ansible/devel/community/communication.html#the-bullhorn): used to announce releases and important changes.

For more information about communication, see the [Ansible communication guide](https://docs.ansible.com/ansible/devel/community/communication.html).

## Requirements

### Ansible version compatibility

The collection supports ansible-core versions based on `requires_ansible` in [meta/runtime.yml](meta/runtime.yml):
- Tested with Ansible Core 2.17.0 and later, and the current development version of Ansible. Ansible Core versions prior to 2.17.0 are not supported.

Use community.aws 4.x.y if you are using Ansible 2.9 or Ansible Core 2.10.

### Python version compatibility

This collection depends on the AWS SDK for Python (Boto3 and Botocore).  Due to the
[AWS SDK Python Support Policy](https://aws.amazon.com/blogs/developer/python-support-policy-updates-for-aws-sdks-and-tools/)
this collection requires Python 3.8 or greater.

Amazon has also announced the planned end of support for
[Python versions below 3.9](https://aws.amazon.com/blogs/developer/python-support-policy-updates-for-aws-sdks-and-tools/).
As such, support for Python versions below 3.9 will be removed in a release after 2026-05-01.

<!---
### End of Support by Python Versions:

| Python Version | AWS SDK | Collection |
| -------------- | -------- | ---------- |
| 2.7 | July 2021 | Release 2.0.0 (September 2021) |
| 3.4 | February 2021 | Release 1.0.0 (June 2020) |
| 3.5 | February 2021 | Release 2.0.0 (September 2021) |
| 3.6 | May 2022 | Release 7.0.0 (November 2023) |
| 3.7 | December 2023 | *After December 2024* |
| 3.8 | April 2025 | *After April 2026* |
| 3.9 | April 2026 | *After April 2027* |
| 3.10 | April 2027 | *After April 2028* |
| 3.11 | April 2028 | *After April 2029* |
--->

### AWS SDK version compatibility

Starting with the 2.0.0 releases of amazon.aws and community.aws, the collection's policy is generally to support the versions of `botocore` and `boto3` that were released within 12 months prior to the most recent major collection release, following semantic versioning (for example, 2.0.0, 3.0.0).

Version 11.0.0 of this collection supports `boto3 >= 1.35.0` and `botocore >= 1.35.0`

All support for the original AWS SDK `boto` was removed in release 4.0.0.

## Included content
<!--start collection content-->
See the complete list of collection content in the [Plugin Index](https://ansible-collections.github.io/community.aws/branch/main/collections/community/aws/index.html#plugin-index).

<!--end collection content-->

## Installation

The community.aws collection can be installed with the Ansible Galaxy command-line tool:

```shell
ansible-galaxy collection install community.aws
```

You can also include it in a `requirements.yml` file and install it with `ansible-galaxy collection install -r requirements.yml`, using the following format:

```yaml
---
collections:
  - name: community.aws
```

Note that if you install any collections from Ansible Galaxy, they will not be upgraded automatically when you upgrade the Ansible package.
To upgrade the collection to the latest available version, run the following command:

```shell
ansible-galaxy collection install community.aws --upgrade
```
A specific version of the collection can be installed by using the `version` keyword in the `requirements.yml` file:

```yaml
---
collections:
  - name: community.aws
    version: 3.1.1
```

or using the ansible-galaxy command as follows:

```shell
ansible-galaxy collection install community.aws:==3.1.1
```

The python module dependencies are not installed by `ansible-galaxy`.  They can
be manually installed using pip:

```shell
pip install -r requirements.txt
```

or:

```shell
pip install boto3 botocore
```

Refer to the following for more details:

* [Amazon Web Services Guide](https://docs.ansible.com/ansible/latest/collections/amazon/aws/docsite/guide_aws.html)
* [Using Ansible collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html)

## Use Cases

You can call modules by their Fully Qualified Collection Name (FQCN), such as `community.aws.rds_instance`, or by their short name if you list the `community.aws` collection in the playbook's `collections` keyword:

```yaml
---
  - name: Create a DB instance using the default AWS KMS encryption key
    community.aws.rds_instance:
      id: test-encrypted-db
      state: present
      engine: mariadb
      storage_encrypted: True
      db_instance_class: db.t2.medium
      username: "{{ username }}"
      password: "{{ password }}"
      allocated_storage: "{{ allocated_storage }}"
```

## Testing

This collection is tested using GitHub Actions. To learn more about testing, refer to [CI.md](https://github.com/ansible-collections/community.aws/blob/main/CI.md).

## Contributing to this collection

We welcome community contributions to this collection. If you find problems, please open an issue or create a PR against the [Community AWS collection repository](https://github.com/ansible-collections/community.aws).
See [CONTRIBUTING.md](https://github.com/ansible-collections/community.aws/blob/main/CONTRIBUTING.md) for more details.

### More information about contributing

- [Ansible Community Guide](https://docs.ansible.com/ansible/latest/community/index.html) - Details on contributing to Ansible
- [Contributing to Collections](https://docs.ansible.com/ansible/devel/dev_guide/developing_collections.html#contributing-to-collections) - How to check out collection git repositories correctly
- [Guidelines for Ansible Amazon AWS module development](https://docs.ansible.com/ansible/latest/collections/amazon/aws/docsite/dev_guidelines.html)
- [Getting Started With AWS Ansible Module Development and Community Contribution](https://www.ansible.com/blog/getting-started-with-aws-ansible-module-development)

## Support

This collection is community-maintained. For support, please use the following resources:

- Join the [Ansible Forum](https://forum.ansible.com/) for community help and discussions
- The ``#ansible-aws`` channel on [Libera.Chat](https://libera.chat/) (IRC)
- [GitHub Issues](https://github.com/ansible-collections/community.aws/issues) for bug reports and feature requests

## Release notes

See the [rendered changelog](https://ansible-collections.github.io/community.aws/branch/main/collections/community/aws/docsite/CHANGELOG.html) or the [raw generated changelog](https://github.com/ansible-collections/community.aws/tree/main/CHANGELOG.rst).

## Roadmap

<!-- Optional. Include the roadmap for this collection, and the proposed release/versioning strategy so users can anticipate the upgrade/update cycle. -->

## Related Information

- [Ansible Collection overview](https://github.com/ansible-collections/overview)
- [Ansible User guide](https://docs.ansible.com/ansible/latest/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html)
- [Ansible Collection Developer Guide](https://docs.ansible.com/ansible/devel/dev_guide/developing_collections.html)
- [Ansible Community code of conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html)

## License Information

GNU General Public License v3.0 or later.

See [COPYING](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
