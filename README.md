# Mac Collection for Ansible

[![MIT licensed][badge-license]][link-license]
[![Galaxy Collection][badge-collection]][link-galaxy]
[![CI][badge-gh-actions]][link-gh-actions]

This collection includes helpful Ansible roles and content to help with macOS automation. For a good example of the collection's usage, see the [Mac Dev Playbook](https://github.com/gabegomes/mac-dev-playbook).

Roles included in this collection (click on the link to see the role's README and documentation):

  - `gabegomes.mac.homebrew` ([documentation](https://github.com/gabegomes/ansible-collection-mac/blob/master/roles/homebrew/README.md))
  - `gabegomes.mac.mas` ([documentation](https://github.com/gabegomes/ansible-collection-mac/blob/master/roles/mas/README.md))
  - `gabegomes.mac.dock` ([documentation](https://github.com/gabegomes/ansible-collection-mac/blob/master/roles/dock/README.md))

## Installation

Install via Ansible Galaxy:

```
ansible-galaxy collection install gabegomes.mac
```

Or include this collection in your playbook's `requirements.yml` file:

```
---
collections:
  - name: gabegomes.mac
```

For a real-world example, see my [Mac Dev Playbook's requirements file](https://github.com/gabegomes/mac-dev-playbook/blob/master/requirements.yml).

### Role Requirements

Requires separate installation of the `elliotweiser.osx-command-line-tools` role. Because Ansible collections are not able to depend on roles, you will need to make sure that role is installed either by manually installing it with the `ansible-galaxy` command, or adding it under the `roles` section of your `requirements.yml` file:

```yaml
---
roles:
  - name: elliotweiser.osx-command-line-tools

collections:
  - name: gabegomes.mac
```

## Usage

Here's an example playbook which installs some Mac Apps (assuming you are signed into the App Store), CLI tools via Homebrew, and Cask Apps using Homebrew:

```yaml
- hosts: localhost
  connection: local
  gather_facts: false

  vars:
    mas_installed_app_ids:
      - 424389933 # Final Cut Pro
      - 497799835 # Xcode

    homebrew_installed_packages:
      - node
      - nvm
      - redis
      - ssh-copy-id
      - pv

    homebrew_cask_apps:
      - docker
      - firefox
      - google-chrome
      - vlc

  roles:
    - gabegomes.mac.homebrew
    - gabegomes.mac.mas
```

For a real-world usage example, see my [Mac Dev Playbook](https://github.com/gabegomes/mac-dev-playbook).

See the full documentation for each role in the role's README, linked above.

## License

MIT

## Author

This collection was created by [Jeff Geerling](https://www.jeffgeerling.com), author of [Ansible for DevOps](https://www.ansiblefordevops.com).

[badge-gh-actions]: https://github.com/gabegomes/ansible-collection-mac/workflows/CI/badge.svg?event=push
[link-gh-actions]: https://github.com/gabegomes/ansible-collection-mac/actions?query=workflow%3ACI
[badge-collection]: https://img.shields.io/badge/collection-gabegomes.mac-blue
[link-galaxy]: https://galaxy.ansible.com/gabegomes/mac
[badge-license]: https://img.shields.io/github/license/gabegomes/ansible-collection-mac.svg
[link-license]: https://github.com/gabegomes/ansible-collection-mac/blob/master/LICENSE
[badge-gh-actions]: https://github.com/gabegomes/ansible-role-homebrew/workflows/CI/badge.svg?event=push
