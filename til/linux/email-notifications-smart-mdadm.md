# Email Notifications via SMART and mdadm

We want email notifications on hard drive SMART health and RAID health. This assumes we have already [redirected root email with msmtp](redirect-root-email-with-msmtp.md).

To get our RAID health, we need to set `MAILADDR` and `MAILFROM` in the `mdadm.conf`. Note that using `root` as the `MAILADDR` value does not properly redirect mail via any existing alias so an explicit address needs to be specified.

```
$  sudo cat /etc/mdadm/mdadm.conf
...
# instruct the monitoring daemon where to send mail alerts
MAILADDR famicoman@gmail.com
MAILFROM alerts@dialup.world
```

We can test the notification with the following:

```
$ sudo mdadm --monitor --scan --test -1
```

For SMART health, we can leverage `smartd`, so we edit `/etc/smartd.conf` and comment out every existing line but add the following:

```
$ sudo cat /etc/smartd.conf
...
/dev/sdb -a -o on -S on -s (S/../../1/06|L/../15/./07) -m root
/dev/sdc -a -o on -S on -s (S/../../1/06|L/../15/./07) -m root
```

* `-a` checks for SMART Health Status failed, usage attributes failure, changes in prefailure and usage attributes, error and selftest logs, and pending sector and uncorrectable counts as non-zero
* `-o on` enables automatic offline tests
* `-S on` enables attribute autosave
* `-s` starts a self-test based on regular expression
* `S/../../1/06` schedules a short test every Monday at 6AM
* `L/../15/./07` schedules a long test the 15th of every month at 7AM
* `-m root` sends a warning email to `root`

Then restart the `smartd` service:

```
$ sudo systemctl restart smartd
```

To test, we need to append `-M test` to the lines in the configuration. On restart `smartd` will send test emails:

```
$ sudo cat /etc/smartd.conf
...
/dev/sdb -a -o on -S on -s (S/../../1/06|L/../15/./07) -m root -M test
/dev/sdc -a -o on -S on -s (S/../../1/06|L/../15/./07) -m root -M test
$ sudo systemctl restart smartd
```

## Sources

* https://pieterbakker.com/set-mdadm-to-send-e-mail-notifications/
* https://www.suse.com/support/kb/doc/?id=000016716
* https://ubuntuforums.org/archive/index.php/t-1185134.html
* https://dustymabe.com/2012/01/29/monitor-raid-arrays-and-get-e-mail-alerts-using-mdadm/
* https://dan.langille.org/2018/11/04/using-smartd-to-automatically-run-tests-on-your-drives/
* https://gist.github.com/jimeh/7f4f1da81df100a00425
* https://linuxconfig.org/how-to-configure-smartd-and-be-notified-of-hard-disk-problems-via-email