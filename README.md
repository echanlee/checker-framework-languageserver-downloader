# Checker Framework Language Server Downloader

## Overview

This downloader can be used by other plugins that wish to use the [Checker
Framework Language
Server](https://github.com/eisopux/checker-framework-languageserver) and the
[Checker Framework](https://github.com/typetools/checker-framework) to download
the latest versions of them, so the actual plugins for editors/IDEs can focus
more on editor-specific functions.


## Arguments

Note: when setting the organization/repo of the Checker Framework Language
Server, it is required that **the targeted repository makes releases containing
the distribution zip file of the Checker Framework and a jar file of the
CF Language Server**.

### dest

Required. This is a path to a folder that will be used to store the downloaded
files.

### checkerframework_org

This specifies from which GitHub organization to download the Checker Framework.
The default is `typetools`.

### checkerframework_repo

This specifies from which GitHub repository under `checkerframework_org` to
download the Checker Framework. The default is `checker-framework`.

Combined with `checkerframework_org`, the default Checker Framework is
`typetools/checker-framework`.

### languageserver_org

This specifies from which GitHub organization to download the CF Language
Server. The default is `eisopux`.

### languageserver_repo

This specifies from which GitHub repository under `languageserver_org` to
download the CF Language Server. The default is
`checker-framework-languageserver`.

Combined with `languageserver_org`, the default CF Language Server is
`eisopux/checker-framework-languageserver`.


## Example

Download the default Checker Framework and CF Language Server:

```
java \
    -jar checker-framework-languageserver-downloader.jar \
    -dest /some/env/
```

Download the eisop version of the Checker Framework and the default CF Language
Server:

```
java \
    -jar checker-framework-languageserver-downloader.jar \
    -dest /some/env/ \
    -checkerframework_org eisop
```


## Development notes

To build the project, run

```shell
./gradlew shadowJar
```

and then `checker-framework-languageserver-downloader-all.jar` will be generated
under `build/libs`.

To format the source code, run `$ ./gradlew spotlessApply`.

When adding a new downloader for some new dependency, please inherit
`BaseDownloader` and overwrite methods that you wish to change. We assume that
the dependency can be downloaded as a release asset from GitHub, and by default
the first file will be downloaded.

After this, add arguments to `DownloaderMain`, and instantiate/call your new
class there.
