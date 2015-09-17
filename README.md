# versions

`versions` installs specified versions of R packages hosted on CRAN and provides
functions to list available versions and the versions of currently installed
packages. These tools can be used to help make R projects and packages more
reproducible. versions fits in the narrow gap between the
[`devtools`](https://cran.r-project.org/web/packages/devtools/index.html)
`install_version` function and the
[`checkpoint`](https://cran.r-project.org/web/packages/checkpoint/index.html)
package, using Revolution Analytics'
[MRAN snapshot server](https://mran.revolutionanalytics.com/documents/rro/reproducibility/).

### usage

You can list the versions of a package that have been on CRAN,
when they were added and whether they are available for `versions` to install.

```r
available.versions(c('checkpoint', 'devtools'))
```
```
$checkpoint
  version       date available
1  0.3.15 2015-09-15      TRUE
2  0.3.10 2015-04-27      TRUE
3   0.3.9 2015-03-17      TRUE
4   0.3.3 2014-10-10      TRUE
5   0.3.2 2014-10-01      TRUE

$devtools
   version       date available
1    1.9.1 2015-09-11      TRUE
2    1.8.0 2015-05-09      TRUE
3    1.7.0 2015-01-17      TRUE
4    1.6.1 2014-10-07      TRUE
5      1.6 2014-09-23      TRUE
6      1.5 2014-04-07     FALSE
7    1.4.1 2013-11-27     FALSE
8      1.4 2013-11-20     FALSE
9      1.3 2013-07-04     FALSE
            ...
```

You can install the version you want.

```r
install.versions('checkpoint', '0.3.9')
```

And check which version you have currently installed.

```r
installed.versions('checkpoint')
```
`[1] "0.3.9"`

You can also install the live version on CRAN on a specific date.

```r
install.dates('checkpoint', '2015-01-01')
```

#### installation

Currently the package can be installed with devtools.

```r
devtools::install_github('goldingn/versions')
```

Hopefully it'll be on CRAN soon too.


#### why?

`devtools::install_version` installs a stated package version from source files
stored on the CRAN archives. However CRAN does not store binary versions of
packages so Windows users need to have RTools installed and Windows and OSX
users get longer installation times.

`checkpoint` uses the Revolution Analytics MRAN server to install packages (from
source or binary) as they were available on a given date. It also provides a
helpful interface to detect the packages in use in a directory and install all
of those packages for a given date. `checkpoint` doesn't provide
`install.packages`-like functionality however, and that's what `versions` aims
to do, by querying MRAN.

As MRAN only goes back to 2014-09-17, `versions` can't install package from
before this date.