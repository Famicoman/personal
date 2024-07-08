# Mirror an FTP site/directories with lftp

There is an FTP site that we want to mirror directories from, and continue downloads if they get interrupted

Install `lftp`:

```
# apt install lftp
```

FTP to the site:

```
$ lftp ftp://some.site
```

Change to out local download directory:

```
lftp some.site> lcd /mnt/storage/downloads
```

Mirror a directory:

```
lftp some.site> mirror -c --verbose some_directory
```

## Sources
* https://randyzwitch.com/mirror-ftp-lftp/
* http://root42.blogspot.com/2013/09/how-to-get-directory-recursively-with.html