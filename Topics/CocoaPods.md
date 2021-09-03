# CocoaPods<!-- omit in toc -->

CocoaPods is a dependency manager for Xcode.

## Table of contents<!-- omit in toc -->

- [Official website](#official-website)
- [Installation](#installation)
- [Initializing CocoaPods](#initializing-cocoapods)
- [The podfile](#the-podfile)
- [Using CocoaPods](#using-cocoapods)
- [.xcworkspace](#xcworkspace)
- [Import installed dependencies](#import-installed-dependencies)

## Official website

The official website: <https://cocoapods.org>.

## Installation

CocoaPods is installed through the terminal.

See <https://guides.cocoapods.org/using/getting-started.html>.

## Initializing CocoaPods

To use CocoaPods in a project, navigate to the project directory and run the command:

```sh
pod init
```

## The podfile

The pod init command creates the default `podfile`, a specification where you can list the dependencies to install. The file also specifies the minimum target runtime and the extensions' version.

See <https://guides.cocoapods.org/using/the-podfile.html>.

## Using CocoaPods

After adding your dependencies into the podfile, you will be able install them to the project.

Close Xcode and in the project directory, run `pod install` to build the project:

```sh
pod install
```

Do not reopen the project in Xcode.

## .xcworkspace

From this point on, to continue working on the project, use the newly created `.xcworkspace` file to open the project in Xcode.

## Import installed dependencies

To import dependencies in swift files:

```swift
import DependencyName
```
