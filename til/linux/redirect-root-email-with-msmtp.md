# Redirect root Email with msmtp

We want to have emails that normally go to `root` to be redirected to an external email address for more visibility. This assumes we have an email account on a server that will allow us to send outgoing email via SMTP.

First, we need to install some dependencies:

```
$ sudo apt-get install msmtp msmtp-mta mailutils bsd-mailx
```

* `msmtp` is an SMTP client
* `msmtp-mta` creates an alias for `sendmail`
* `mailutils` is a mail framework
* `bsd-mailx` is a command-line-mode mail user agent

In theory we should not need `bsd-mailx` since `mailutils` should facilitate use of the `mail` command, but due to apparmor issues with `mailutils` we will be using it.

Next, we need to create `/etc/msmtprc` for our mail configuration. Normally, each user might have their own config in `~/.msmtprc` but we want the system to pump everything through the same account by default:

```
$ sudo cat /etc/msmtprc
# Use defaults
defaults

# Turn of starttls, this can cause issues 
# connecting to some servers
tls_starttls off

# Turn on auth and TLS
auth on
tls  on

# By default we use the system's certs
tls_trust_file /etc/ssl/certs/ca-certificates.crt

# Define our log file
logfile /var/log/msmtp

# Dialup.world configuration
account dialupworld
host    smtp.purelymail.com
port    465
from    alerts@dialup.world
user    alerts@dialup.world
password changeme

account default: dialupworld
```

Change file permissions for `/etc/msmtprc` and create our log file:

```
$ sudo chmod 644 /etc/msmtprc
$ sudo touch /var/log/msmtp
$ sudo chown msmtp:msmtp /var/log/msmtp
$ sudo chmod 660 /var/log/msmtp
```

Now, set our mail transport agent to use `msmtp` and add an alias for the `root` user that points to an email address of our liking:

```
$ sudo cat /etc/mail.rc
set ask askcc append dot save crt
ignore Received Message-Id Resent-Message-Id Status Mail-From Return-Path Via Delivered-To
set mta=/usr/bin/msmtp
alias root root<famicoman@gmail.com>
```

## Aliases

We don't seem to need this but we can point `root` at an email of our choosing in `/etc/aliases`:

```
$ sudo cat /etc/aliases
# /etc/aliases
mailer-daemon: postmaster
postmaster: root
nobody: root
hostmaster: root
usenet: root
news: root
webmaster: root
www: root
ftp: root
abuse: root
noc: root
security: root
default: root
root: famicoman@gmail.com
```

## Testing

```
echo "Hello World" | msmtp -d bob@example.com
```

Test sending a mail to root:

```
echo "Testing msmtp from ${HOSTNAME} with mail command" | mail -s "hi root" root
```

Test sending a mail to another email address:

```
echo "Testing msmtp from ${HOSTNAME} with mail command" | mail -s "hi there" bob@example.com
```

## Sources

* https://gist.github.com/movd/7a9e3db63d076f85d16c7dcde62fe401
* https://askubuntu.com/questions/233576/msmtp-hangs-instead-of-delivering-the-message
* https://askubuntu.com/questions/878288/msmtp-cannot-write-to-var-log-msmtp-msmtp-log