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

## Certificate errors

You may encounter an error where a certificate is not trusted:

```
lftp some.site> ls
ls: Fatal error: Certificate verification: Not trusted (FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF)
```

In this case simply run the following to ignore the validation:

```
lftp some.site> set ssl:verify-certificate/FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF no
```

## Sources
* https://randyzwitch.com/mirror-ftp-lftp/
* http://root42.blogspot.com/2013/09/how-to-get-directory-recursively-with.html