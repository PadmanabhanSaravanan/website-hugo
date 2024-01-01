# Hugo

* A fast and flexible static site generator
* Hugo is optimized for speed and designed for flexibility. With its advanced templating system and fast asset pipelines, Hugo renders a complete site in seconds, often less.

# Prerequisites

Prerequisites for building a site with Docsy as a Hugo Module.

* **Install Hugo**

## Install Hugo

**On Linux**

```python
sudo apt-get install hugo
```

If you've already installed Hugo, check your version:

```bash
hugo version
```

If the result is `v0.109.0` or earlier, or if you don't see `Extended`, you'll need to install the latest version. You can see a complete list of Linux installation options in [Install Hugo](https://gohugo.io/getting-started/installing/#linux). The following shows you how to install Hugo from the release page:

**1.**  Go to the [Hugo releases](https://github.com/gohugoio/hugo/releases) page.

**2.**  In the most recent release, scroll down until you find a list of **Extended** versions.

**3.**  Download the latest extended version (`hugo_extended_0.1XX_Linux-64bit.tar.gz`).

**4.**  Create a new directory:

```bash
mkdir hugo
```

**5.**  Extract the files you downloaded to `hugo`.

**6.**  Switch to your new directory:

```bash
cd hugo
```

**7.**  Install Hugo:

```bash
sudo install hugo /usr/bin
```