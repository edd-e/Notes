# npm<!-- omit in toc -->

npm is a package manager for JavaScript runtime environments using Node.js.

## Table of contents<!-- omit in toc -->

- [Official website](#official-website)
- [Initializing a package](#initializing-a-package)
- [Versioning](#versioning)
- [Installing dependencies](#installing-dependencies)
  - [Existing dependencies](#existing-dependencies)
  - [New dependencies](#new-dependencies)
  - [The node_modules folder](#the-node_modules-folder)
  - [Development dependencies](#development-dependencies)
- [package-lock.json file](#package-lockjson-file)
- [Updating installed packages](#updating-installed-packages)

## Official website

For more information see: <https://www.npmjs.com>.

## Initializing a package

Use `npm init` within the package’s root directory to create a `package.json` file. You must provide the package name, and version.

## Versioning

npm uses semantic versioning. When specifying versions, you can use the following syntax:

| Desired version              | Example | Compatible versions |
| ---------------------------- | ------- | ------------------- |
| Exact version                | 2.5.9   | 2.5.9               |
| Version greater than         | >2.5.9  | 2.x and higher      |
| Same major release version   | ^2.5.9  | 2.x                 |
| Version with (minor) changes | ~2.5.9  | 2.5.x               |

## Installing dependencies

### Existing dependencies

Use `npm install` to install all packages listed in `package.json`.

### New dependencies

Use `npm install <package>` to download and install packages to the project folder and save them to `package.json`.

### The node_modules folder

When installing dependencies, all packages are downloaded and installed to the `node_modules` folder.

If a package "sampleA" is installed, and that package has additional dependencies ("sampleB", "sampleC", etc.) then that package and all of its dependencies will be installed.

### Development dependencies

Use `npm install -D <package>` to install development dependencies packages.

## package-lock.json file

The `package-lock.json` file is an automatically generated and updated file that contains information about the versions of installed packages. This file helps keep the consistency of package versions.

## Updating installed packages

Use the command `npm update` to update all installed packages or `npm update <package>` to update a specific package.
