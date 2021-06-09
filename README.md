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

## Room for improvement: proxies

With the increasing enforcement of encrypted protocols, generic caching proxies become less and less viable. One way out of this is to let the client manage the caching itself. DlCache currently does this on a per-user-x-host level. Having looked at Sonatype Nexus, there is the possibility of simple uploads to the Nexus instance's raw host repository format in order to provide intranet caching. That would be a useful extension (idea: use "dlcache_server" env variable similar to "http_proxy").

    curl -v -u admin:pwd --upload-file debian-10.9.0-amd64-netinst.iso http://nas:8081/repository/dlcache/a/b/c/a.iso
