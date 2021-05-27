# dlcache

A simple file-backed download cache for NodeJS, CMake and Java:

* NodeJS: [dlcache-nodejs](//github.com/jjYBdx4IL/dlcache-nodejs)
* CMake: [dlcache-cmake](//github.com/jjYBdx4IL/dlcache-cmake)
* Java: https://github.com/jjYBdx4IL/misc/blob/master/io-utils/src/main/java/com/github/jjYBdx4IL/utils/io/DlCache.java

## Windows

Files are being stored under:

    %LOCALAPPDATA%\dlcache

## Others OSes

Files are being stored under:

    $HOME/.cache/dlcache

## Generic Behavior

You can set the environment variable `DLCACHEDIR` to set a specific root cache directory.

The actual location of the downloaded and cached file inside the root cache directory is computed from the given URL of the file:

    $relpath = $url.replace(/[^A-Za-z0-9/.-]/, "_")
    $ROOTDIR + / + $relpath

For example:

    C:\Users\work\AppData\Local\dlcache\https_\archive.apache.org\dist\lucene\solr\8.8.2\solr-8.8.2.zip

Files only get stored under the final location name after a successful checksum verification.


