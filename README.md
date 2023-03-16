ansible-role-git-repos
=========

<p align="center">

<a href="https://github.com/iancleary/ansible-role-git-repos/actions?query=workflow%3Aci" target="_blank">
    <img src="https://github.com/iancleary/ansible-role-git-repos/workflows/CI/badge.svg" alt="CI workflow status">
</a>

<a href="https://github.com/iancleary/ansible-role-git-repos/actions?query=workflow%3Arelease" target="_blank">
    <img src="https://github.com/iancleary/ansible-role-git-repos/workflows/Release/badge.svg" alt="Release workflow status">
</a>

<a href="https://raw.githubusercontent.com/iancleary/ansible-role-git-repos/main/LICENSE" target="_blank">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
</a>
</p>

This role clones git repositories according to the role's variables.  It will install from one or multple combinations of remote git servers, users, organizations, etc. and can install each group into it's own folder.

> Only cloning via ssh is supported, at the current moment, as that was my initial use case.

Requirements
------------

`git` should be installed.  See the [geerlingguy.git](https://github.com/geerlingguy/ansible-role-git) ansible role for that!

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

`git_clone_repos` is a list of dictionaries:

* `dest`: Folder to clone this list items `repos` into
* `server`: `git@github.com` equivalent for your server, e.g. `git@git.company.com` or `git@gitlab.org`, etc.
* `user`: user or organization for this list item.  `username` or `org-name`
* `update`: truthy value of whether or not to update the repo, if false, it just checks if the repo exists locally
* `repo`: list of strings that are the repo names

For example, `git@github.com:/iancleary/ansible-role-git-repos.git` would use:

```yaml
---
git_clone_repos:
  - dest: "~/Automation/Ansible"
    server: "git@github.com"
    user: "iancleary"
    update: "yes"
    repos:
      - name: "ansible-role-git-repos"
```

A longer setup, to show mutliple items in the top level list:

```yaml
  - dest: "~/Marketing/"
    server: "git@github.com"
    user: "iancleary"
    update: "yes"
    repos:
      - name: "iancleary"
  - dest: "~/Operations/"
    server: "git@github.com"
    user: "iancleary"
    update: "yes"
    repos:
      - name: "unraid-tailscale"
  - dest: "~/Development/"
    server: "git@github.com"
    user: "iancleary"
    update: "yes"
    repos:
      - name: "ivy-lee-backend"
  - dest: "~/Pictures/"
    server: "git@github.com"
    user: "iancleary"
    update: "yes"
    repos:
      - name: "backgrounds"
```


Dependencies
------------

`git` needs to be installed; the role `geerlingguy.git` is suggested.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  user: unprivelaged
  roles:
    - role: geerlingguy.git
    - role: iancleary.git_repos
```

**Note the underscore in `git_repos`, it is not a dash!**

> This role doesn't need to be run as root, use whatever user you want to clone the repos as.

```yaml
- hosts: servers
  user: root
  roles:
    - role: geerlingguy.git
    - role: iancleary.git_repos
```

> Note: `"- role: geerlingguy.git"` is only there to ensure `git` is installed.  You may remove that line, if `git` is installed by some other method.

License
-------

[MIT](LICENSE)

Author Information
------------------

This role was created in 2023 by [Ian Cleary](https://iancleary.me).

Inspiration for the structure of this repo came from [Jeff Geerling](https://github.com/geerlingguy/ansible-role-nginx).
