# webr-org-gh-action

This repository serves as an example that strictly follows the [guidance](https://r-wasm.github.io/rwasm/articles/github-actions.html) for setting up a mini-CRAN repo for webR R WASM Package binaries.

If you would like to have the repository where you develop your R package build and act as a deployment repository, then see the [coatless-tutorials/webr-github-action-wasm-binaries](https://github.com/coatless-tutorials/webr-github-action-wasm-binaries) repository. 

## Setup `packages`

When trying to setup an environment for your own packages, please make sure to modify the `packages` file to contain the appropriate [package reference value supported by `pak`](https://r-lib.github.io/pkgdepends/reference/pkg_refs.html). In the case of generating [R WASM package binaries from GitHub](https://r-lib.github.io/pkgdepends/reference/pkg_refs.html#github-packages-github-), you can achieve this with: 

```
gh-username/reponame
```

Or, more formally with: 

```
github::gh-username/reponame
```

Need a [package from CRAN](https://r-lib.github.io/pkgdepends/reference/pkg_refs.html#cran-packages-cran-)? This can be specified as: 

```
pkgname
```
