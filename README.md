# Hugo

## Table of Content

* [**Introduction to Hugo**](#introduction-to-hugo)
* [**Prerequisites**](#prerequisites)
* [**Detailed Setup instructions**](#detailed-setup-instructions)
* [**Adding Content**](#adding-content)
* [**Previews and Deployment**](#previews-and-deployment)
* [**Host on GitHub Pages**](#host-on-github-pages)
* [**Reference**](#reference)

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
hugo mod get github.com/google/docsy@v0.8.0
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

## Adding Content

**Content root directory**

* You add content for your site under the content root directory of your Hugo site project - either `content/` or a language-specific root like `content/en/`.
* The files in your content root directory are typically grouped in subdirectories corresponding to your site’s sections and templates, which we’ll look at in Content sections and templates.

**Custom sections**

* If you’ve copied the example site and don’t want to use one of the provided content sections, just delete the appropriate content subdirectory. 
* Similarly, if you want to add a top-level section, just add a new subdirectory, though you’ll need to specify the layout or content type explicitly in the frontmatter of each page if you want to use any existing Docsy template other than the default one. 
* For example, if you create a new directory `content/en/amazing` and want one or more pages in that custom section to use Docsy’s docs template, you add type: docs to the frontmatter of each page:

  ```
  ---
  title: "My amazing new section"
  weight: 1
  type: docs
  description: >
    A special section with a docs layout.  
  ---
  ```

**Page frontmatter**

* Each page file in a Hugo site has metadata frontmatter that tells Hugo about the page. You specify page frontmatter in TOML, YAML, or JSON (our example site and this site use YAML). Use the frontmatter to specify the page title, description, creation date, link title, template, menu weighting, and even any resources such as images used by the page. You can see a complete list of possible page frontmatter in [Front Matter](https://gohugo.io/content-management/front-matter/).

  ```
  ---
  title: "Adding Content"
  linkTitle: "Adding Content"
  weight: 1
  description: >
    Add different types of content to your Docsy site.  
  ---
  ```

## Previews and Deployment

**Serving your site locally**

Depending on your deployment choice you may want to serve your site locally during development to preview content changes. To serve your site locally:

* Ensure you have an up to date local copy of your site files cloned from your repo.
* Ensure you have the tools described in [Prerequisites and installation](#prerequisites) installed on your local machine, including `postcss-cli` (you’ll need it to generate the site resources the first time you run the server).
* Run the hugo server command in your site root. By default your site will be available at `http://localhost:1313`.

## Host on GitHub Pages

GitHub provides free and fast static hosting over SSL for personal, organization, or project pages directly from a GitHub repository via its GitHub Pages service and automating development workflows and build with GitHub Actions.

**Prerequisites**

1. Create a GitHub account
2. Install Git
3. Create a Hugo site and test it locally with `hugo server`.

[Create a GitHub account](https://github.com/signup)

[Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

[Create a Hugo site](/getting-started/quick-start/)

### Types of sites

* **There are three types of GitHub Pages sites:** project, user, and organization. 
* Project sites are connected to a specific project hosted on GitHub. User and organization sites are connected to a specific account on GitHub.com.

> See the [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites) to understand the requirements for repository ownership and naming.

### Procedure

**Step 1:** Create a GitHub repository.

**Step 2:** Push your local repository to GitHub.

**Step 3:** Visit your GitHub repository. From the main menu choose **Settings**&nbsp;>&nbsp;**Pages**. In the center of your screen you will see this:

![screen capture](image/gh-pages-1.png)

**Step 4:** Change the **Source** to `GitHub Actions`. The change is immediate; you do not have to press a Save button.

![screen capture](image/gh-pages-2.png)

**Step 5:** Create an empty file in your local repository.

```text
.github/workflows/hugo.yaml
```

**Step 6:** Copy and paste the YAML below into the file you created. Change the branch name and Hugo version as needed.

```python
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.121.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Install Dart Sass
        run: sudo snap install dart-sass
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v3
```

**Step 7:** Commit the change to your local repository with a commit message of something like "Add workflow", and push to GitHub.

**Step 8:** From GitHub's main menu, choose **Actions**. You will see something like this:

![screen capture](image/gh-pages-3.png)

**Step 9:** When GitHub has finished building and deploying your site, the color of the status indicator will change to green.

![screen capture](image/gh-pages-4.png)

**Step 10:** Click on the commit message as shown above. You will see this:

![screen capture](image/gh-pages-5.png)

Under the deploy step, you will see a link to your live site.

In the future, whenever you push a change from your local repository, GitHub will rebuild your site and deploy the changes.

## Reference

* [**Docsy Documentation**](https://www.docsy.dev/docs/)
* [**Host on Github**](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
* [**Hugo Documentation**](https://gohugo.io/documentation/)
* [**Docsy Github**](https://github.com/google/docsy)
* [**Hugo docsy theme**](https://themes.gohugo.io/themes/docsy/)