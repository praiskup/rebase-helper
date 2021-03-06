# rebase-helper

[![Code Health](https://landscape.io/github/phracek/rebase-helper/master/landscape.svg?style=flat)](https://landscape.io/github/phracek/rebase-helper/master)

## Rebase-helper workflow

This tool helps you to rebase package to the latest version

How the rebase-helper works:
- Each action should be logged and visible by user.
    - extract tarball with the existing sources to directory old_sources/<package_name>
    - extract tarball with the new sources to directory new_sources/<package_name>
    - Provide a list of patches mentioned in SPEC file
    - New spec file is stored in results/
- for all patches
    - apply all patches with git command to old_sources/<package_name> directory
    - add new_sources<package_name> to old_sources/<package_name> 
        with command git rebase --onto new_sources <inital_commit> <last_commit>
    - solve all conflicts which arrise during the git rebase
- create srpm from old and new spec files & new sources & patches (Builder)
- rebuild srpm -> RPMs (Builder)
- Run rpmdiff tool for finding libraries and header changes.
- Inform user what libraries and header files were changed.

## Landscape scans

[**Landscape.io scans of rebase-helper**](https://landscape.io/github/phracek/rebase-helper/)

## Requirements

Packages which needs to be installed before you execute rebase-helper for first time:
- meld
- mock
- rpm-build
- pkgdiff at least 1.6.3
- python-six
- fedpkg
- pyrpkg
- libabigail

## How to execute rebase-helper from CLI

Go to a git directory of your package and execute command /path_to_rebase-helper/rebase-helper.py <new_upstream_version> (e.g. /home/user/phracek/rebase-helper/rebase-helper.py "3.1.10")
