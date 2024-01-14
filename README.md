# GitHub Action for an Org webR WASM R Package Repository

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

## Setup Github Pages on the Repository

1. Click on the **Settings** tab for the repository
2. Under "Code and automation", select the **Pages** menu item.
3. Under the "Source" option select **GitHub Action** from the drop down.
4. In the "Custom Domain" settings, make sure that **Enforce HTTPS** is checked.

![Example configuration of GitHub Pages](figures/github-pages-configuration-for-org-repository.png)

## Trigger a build

The R WASM Package binaries are either built by updating/committing files in the repository or by manually triggering a workflow deploy.

You can trigger a workflow deploy by:

1. Go to the **Actions** tab of the repository
2. Selecting the **Build and deploy wasm R package repository** workflow
3. Clicking on **Run workflow** dropdown
4. Pressing the **Run workflow** button.

![Example of triggering a manual deployment of the repository](figures/github-pages-trigger-cran-repo-build.png)

## Usage inside webR

Inside of a webR session, you can access the built binaries by using the
repository’s GitHub Pages URL, e.g.

```
https://gh-username.github.io/repo-name
```

This can be set either using `options()` or specifying the location in
each `webr::install()` call.

The easiest is probably to define the location webR should search for in
`options()`.

``` r
# Run once at the start of the session
options(
  repos = c("https://gh-username.github.io/repo-name", 
            "https://repo.r-wasm.org/")
)

# Call
webr::install("pkgname")
```

Otherwise, you can specify it each time:

``` r
webr::install("pkgname", "https://gh-username.github.io/repo-name")
```

<div>

> **Important**
>
> Please make sure the repository’s [GitHub Pages website is available
> over
> `HTTPS`](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https#enforcing-https-for-your-github-pages-site)
> not `HTTP` (notice the lack of an `s`). You can verify this option was
> selected by:
>
> 1.  Going to the repository’s **Settings** page
> 2.  Selecting **Pages** under **Code and automation**
> 3.  Checking the **Enforce HTTPS** button.
>
> Otherwise, you will receive the error message of:
>
>     Warning: unable to access index for repository http://gh-username.github.io/repo-name/bin/emscripten/contrib/4.3

</div>

## Verify

Go to the [webR REPL Editor](https://webr.r-wasm.org/v0.2.2/) (pinned to
v0.2.2) and run the following:

``` r
# Check if package `{drawr}` is installed
"drawr" %in% installed.packages()[,"Package"]
# Install the binary from a repository
webr::install(
  "drawr", 
  repos = "https://tutorials.thecoatlessprofessor.com/webr-org-gh-action/"
)
# Check to see if the function works
mat_2x2 <- matrix(1:4, nrow = 2)
drawr::draw_matrix(mat_2x2, show_cell_indices = TRUE)
# View help documentation
?drawr::draw_matrix
```

You should receive:

![Screenshot of the webR REPL editor showing how to download from
repository outside of repo.r-wasm.org an R package
binary](figures/webr-repl-example-workflow.png)
