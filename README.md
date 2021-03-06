# Terminus Hotfix Plugin

A [Terminus](http://github.com/pantheon-systems/terminus) plugin that adds the commands to facilitate hotfix workflows on [Pantheon](https://pantheon.io/) sites.

## Demo Video

[![Terminus Hotfix Plugin Demo Video](assets/terminus-hotfix-plugin-repo-ss-with-play-button.png?raw=true)](https://youtu.be/T9ukNUGLXnE "Terminus Hotfix Plugin Demo Video")

## Disclaimer

While this plugin has worked well for us your mileage may vary due to local machine configuration. This repository is provided without warranty or direct support. Issues and questions may be filed in GitHub but their resolution is not guaranteed.

## Installation

Clone this project into your Terminus plugins directory found at `$HOME/.terminus/plugins`. If the `$HOME/.terminus/plugins` directory does not exists you can safely create it. You will also need to run `composer install` in the plugin directory after cloning it. See [installing Terminus plugin](https://pantheon.io/docs/terminus/plugins/#install-plugins) for details.

## Purpose

A hotfix is the only way to push code directly to Live without having to go through Dev and Test. Any damage to the source code will be the responsibility of the user. The intended use case is for critical security releases or bug fixes that need to be deployed as quickly and easily as possible. Hotfixes should be used with care and only in emergency situations. Hotfixes should be the exception, not the norm.

Currently hotfix deployments, emergency updates to test/live that skip the normal workflow and potentially undeployed code in `master`, need to be done manually and require more advanced git skills. See the [hotfix doc](https://pantheon.io/docs/hotfixes/) for details. This plugin aims to make that process easier.

## Requirements

* [Terminus](https://github.com/pantheon-systems/terminus) `1.8.0` or greater
* [git command line](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Commands

* `terminus hotfix:env:git-ref <site>.<env>` - returns the deployed git reference of the specifiied environment.
* `terminus hotfix:env:create <site>.<env> <multidev>` - creates a new <multidev> environment for the site <site> with code, database and files from the <env> environment by checking out the lastest git tag associated with <env> environment.
* `terminus hotfix:env:deploy <site>.<env> <multidev>` - deploy the changes from the specified <multidev> environment directly to <env> for the site <site>, skipping the normal workflow, and rebase the changes back to the `master` branch/dev environment.

## License

MIT

## Known Issues

* `terminus hotfix:env:deploy` will fail on environments that have had a backup restored **without** a code deployment since the backup.