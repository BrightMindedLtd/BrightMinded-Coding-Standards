# BrightMinded Coding Standards for PHP_CodeSniffer

* [Introduction](#introduction)
* [Installation](#installation)
* [Setup](#setup)
* [Usage](#usage)

## Introduction

This project is a collection of [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) rules (sniffs) to validate code developed by BrightMinded. It ensures code quality and adherence to coding conventions across BrightMinded's client and public projects.

Currently this project contains a single ruleset designed for WordPress projects. It is likely we will add extra rulesets for other project types (e.g. Laravel) in the future.

## Installation

### Requirements

The BrightMinded Coding Standards are designed to run on any PHP version which still receives official support.

### composer

We recommend installation on a project-by-project basis via the [Composer](https://getcomposer.org/) dependency manager. In your projects `composer.json` file require:

	[phpcodesniffer-composer-installer](https://github.com/DealerDirect/phpcodesniffer-composer-installer):"^0.7"
	BrightMindedLtd/BrightMinded-Coding-Standards:dev-main

Note: You will need to add the GitHub repository to your composer repositories config: https://getcomposer.org/doc/05-repositories.md#loading-a-package-from-a-vcs-repository

### Standalone

Standalone installation should work with the following steps (untested):

```bash
cd ~/projects
git clone https://github.com/squizlabs/PHP_CodeSniffer.git phpcs
git clone -b master https://github.com/BrightMindedLtd/BrightMinded-Coding-Standards BrightMinded-Coding-Standards
cd phpcs
./bin/phpcs --config-set installed_paths ../BrightMinded-Coding-Standards
```

And then add the `~/projects/phpcs/bin` directory to your `PATH` environment variable via your `.bashrc`.

You should then see `WordPress-Core` et al listed when you run `phpcs -i`.

## Setup

Add a `phpcs.xml` file to the root of your project. Sample rulesets can be found in the `sample-rulesets` folder.

For WordPress projects we highly recommend also installing the [PHPCompatibilityWP](https://github.com/PHPCompatibility/PHPCompatibilityWP) ruleset. Once installed specify the PHP and WordPress versions you wish to support:

```xml
<config name="testVersion" value="5.2-"/>
<rule ref="PHPCompatibilityWP">
    <include-pattern>*\.php$</include-pattern>
</rule>
```
If in doubt we suggest supporting the oldest version of PHP that still receives offical support.

## Usage

Assuming a composer installation, run:

	vendor/bin/phpcs

To automatically apply fixes:

	vendor/bin/phpcbf

To view warnings (as well as errors)

	vendor/bin/phpcs --severity=1

To lint a single file

	vendor/bin/phpcs ./path-to-file

You can also configure your code editor to run PHPCS