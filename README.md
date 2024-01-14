# webr-org-gh-action

This repository serves as an example that strictly follows the [guidance](https://r-wasm.github.io/rwasm/articles/github-actions.html) for setting up a mini-CRAN repo for webR R WASM Package binaries.

This repository is part of a series of repositories exploring the topic.

- **[Org-focused webR/WASM Package Repository without a `{pkgdown}` website (Preferred)](https://github.com/coatless-tutorials/webr-org-gh-action)  [This repository]**
- [Unified GitHub Action Deployment using artifacts of R WASM Package binaries and {pkgdown} website](https://github.com/coatless-tutorials/webr-unified-gh-workflow)
- [Separate GitHub Action Deployment onto `gh-pages` branch of R WASM Package binaries and {pkgdown} website](https://github.com/coatless-tutorials/webr-github-action-wasm-binaries)

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

So, the example `packages` file contains three lines where 2 are dedicate to install a package on GitHub as well as CRAN and the last line is an empty line:

```
coatless-rpkg/drawr
visualize

```

**Note:** Not leaving an empty line will result in a warning message during the "Retrieve packages from `./packages` file" step.

```
Warning message:
In readLines("./packages") : incomplete final line found on './packages'
```
