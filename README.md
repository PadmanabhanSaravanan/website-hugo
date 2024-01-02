# Hugo

## Table of Content

* [**Introduction to Hugo**](#introduction-to-hugo)
* [**Prerequisites**](#prerequisites)
* [**Detailed Setup instructions**](#detailed-setup-instructions)

## Introduction to Hugo

* A fast and flexible static site generator
* Hugo is optimized for speed and designed for flexibility. With its advanced templating system and fast asset pipelines, Hugo renders a complete site in seconds, often less.

## Prerequisites

Prerequisites for building a site with Docsy as a Hugo Module.

* [**Install Hugo**](#install-hugo)
* [**Install Go language**](#install-go-language)
* [**Install Git VCS client**](#install-git-vcs-client)
* [**Install PostCSS**](#install-postcss)

### Install Hugo

**On Windows**


* **Chocolatey:**

  Chocolatey is a free and open-source package manager for Windows. To install the extended edition of Hugo:

  ```python
  choco install hugo-extended
  ```

* **Scoop:**

  Scoop is a free and open-source package manager for Windows. To install the extended edition of Hugo:
  
  ```python
  scoop install hugo-extended
  ```

* **Winget**

  Winget is Microsoft’s official free and open-source package manager for Windows. To install the extended edition of Hugo:
  
  ```python
  winget install Hugo.Hugo.Extended
  ```

**On Linux**

```python
sudo apt-get install hugo
```

If you've already installed Hugo, check your version:

```bash
hugo version
```

If the result is `v0.109.0` or earlier, or if you don't see `Extended`, you'll need to install the latest version. You can see a complete list of Linux installation options in [Install Hugo](https://gohugo.io/getting-started/installing/#linux). The following shows you how to install Hugo from the release page:

* Go to the [Hugo releases](https://github.com/gohugoio/hugo/releases) page.

* In the most recent release, scroll down until you find a list of **Extended** versions.

* Download the latest extended version (`hugo_extended_0.1XX_Linux-64bit.tar.gz`).

* Create a new directory:

  ```bash
  mkdir hugo
  ```

* Extract the files you downloaded to `hugo`.

* Switch to your new directory:

  ```bash
  cd hugo
  ```

* Install Hugo:

  ```bash
  sudo install hugo /usr/bin
  ```

### Install Go language

Hugo's commands for module management require that the Go programming language is installed on your system. Check whether `go` is already installed:

```console
$ go version
go version go1.21.4
```

Ensure that you are using version 1.12 or higher.

If the `go` language is not installed on your system yet or if you need to upgrade, go to the [download area](https://go.dev/dl/) of the Go website, choose the installer for your system architecture and execute it. Afterwards, check for a successful installation.


### Install Git VCS client

Hugo's commands for module management require that the `git` client is installed on your system. Check whether `git` is already present in your system:

```console
$ git version
git version 2.42.1
```

If no `git` client is installed on your system yet, go to the [Git website](https://git-scm.com/), download the installer for your system architecture and execute it. Afterwards, check for a successful installation.

### Install PostCSS

To build or update your site's CSS resources, you also need [`PostCSS`](https://postcss.org/) to create the final assets. If you need to install it, you must have a recent version of [NodeJS](https://nodejs.org/en/) installed on your machine so you can use `npm`, the Node package manager. By default `npm` installs tools under the directory where you run [`npm install`](https://docs.npmjs.com/cli/v6/commands/npm-install#description):

```bash
npm install -D autoprefixer
npm install -D postcss-cli
```

Starting in [version 8 of `postcss-cli`](https://github.com/postcss/postcss-cli/blob/master/CHANGELOG.md), you must also separately install `postcss`:

```bash
npm install -D postcss
```

Note that versions of `PostCSS` later than 5.0.1 will not load `autoprefixer` if installed [globally](https://flaviocopes.com/npm-packages-local-global/), you must use a local install.


## Detailed Setup instructions

Specifying the [Docsy theme](https://github.com/google/docsy) as Hugo Module for your minimal site gives you all the theme-y goodness, but you'll need to specify your own site structure.

* [**Create your new skeleton project**](#create-your-new-skeleton-project)
* [**Import the Docsy theme module as a dependency of your site**](#import-the-docsy-theme-module-as-a-dependency-of-your-site)
* [**Add theme module configuration settings**](#add-theme-module-configuration-settings)
* [**Preview your site**](#preview-your-site)

### Create your new skeleton project

To create a new Hugo site project and then add the Docs theme as a submodule, run the following commands from your project's root directory.

```bash
hugo new site my-new-site
cd  my-new-site
```

This will create a minimal site structure, containing the folders `archetypes`, `content`, `data`, `layouts`, `static`, and `themes` and a configuration file (default: `hugo.toml`).

* In Hugo 0.110.0 the default config base filename was changed to `hugo.toml`.
* If you are using hugo 0.110 or above, consider renaming your `config.toml` to `hugo.toml`!

### Import the Docsy theme module as a dependency of your site

Only sites that are Hugo Modules themselves can import other modules. To turn your site into a Hugo Module, run the following commands in your newly created site directory:

```bash
hugo mod init github.com/me/my-new-site
```

This creates two new files, `go.mod` for the module definitions and `go.sum` which holds the checksums for module verification.

Next declare the Docsy theme module as a dependency for your site.

```bash
hugo mod get github.com/google/docsy@v{{% param "version" %}}
```

This command adds the `docsy` theme module to your definition file `go.mod`.

### Add theme module configuration settings

Add the settings in the following snippet at the end of your site's [configuration file] (default: `hugo.toml`) and save the file.

```configuration
[module]
  proxy = "direct"
  # uncomment line below for temporary local development of module
  # replacements = "github.com/google/docsy -> ../../docsy"
  [module.hugoVersion]
    extended = true
    min = "0.73.0"
  [[module.imports]]
    path = "github.com/google/docsy"
    disable = false
```

### Preview your site

To build and preview your site locally:

```bash
hugo server
```

By default, your site will be available at [http://localhost:1313](http://localhost:1313/).