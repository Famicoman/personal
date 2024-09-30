# Monitor ECC RAM with rasdaemon

We have ECC RAM installed and want to monitor for errors. `rasdaemon` can report memory errors and we can configure it so we know which DIMM is the issue.

Install `rasdaemon`:

```
# apt install rasdaemon
```

Enable and start the service:

```
# systemctl enable rasdaemon
# systemctl start rasdaemon
```

We can verify things are running by checking the error count:

```
# ras-mc-ctl --error-count
Label                 CE      UE
mc#0csrow#2channel#0  0   0
mc#0csrow#2channel#1  0   0
mc#0csrow#3channel#1  0   0
mc#0csrow#3channel#0  0   0
```

From left to right we have EDAC path of the DIMM, correctable errors, and uncorrectable errors.

We want to label these but by default there will be no labels to map to the EDAC paths:

```
# ras-mc-ctl --print-labels
ras-mc-ctl: Error: No dimm labels for LENOVO model SHARKBAY
```

We need to know which DIMM is which so reboot the system with only one stick of RAM and check errors again:

```
# ras-mc-ctl --error-count
Label                 CE      UE
mc#0csrow#2channel#0  0   0
mc#0csrow#2channel#1  0   0
```

Now we need a new file for the label mapping in `/etc/ras/dimm_labels.d/`:

```
# cat /etc/ras/dimm_labels.d/lenovo
Vendor: LENOVO
Model: SHARKBAY
  DIMM_2:   0.0.0, 0.1.0;
  DIMM_4:   0.0.1, 0.1.1;
```

Notice that there are two entries per DIMM, mapped to mc#, row# and channel#, due to these being 128 bit wide channels. So it looks like this RAM is dual-channel and each stick has two mapped channels. DIMM numbering here corresponds to the slot it is using to make a problematic stick easily identifiable.

Motherboard Vendor/Model can be retrieved via:

```
# ras-mc-ctl --mainboard
ras-mc-ctl: mainboard: LENOVO model SHARKBAY
```

Now that the file is created we can register our new labels:

```
# ras-mc-ctl --register-labels
```

Now we can print the labels to verify the mapping and show error count again to see the new labels used:

```
# ras-mc-ctl --print-labels
LOCATION                            CONFIGURED LABEL     SYSFS CONTENTS
mc0 csrow 0 channel 0
             DIMM_2               DIMM_2
mc0 csrow 0 channel 1
             DIMM_4               DIMM_4
mc0 csrow 1 channel 0
             DIMM_2               DIMM_2
mc0 csrow 1 channel 1
             DIMM_4               DIMM_4
			 
# ras-mc-ctl --error-count
Label   CE      UE
DIMM_4  0       0
DIMM_4  0       0
DIMM_2  0       0
DIMM_2  0       0
```

Finally, enable the `ras-mc-ctl` service to have these labels registered at startup:

```
# systemctl enable ras-mc-ctl
# systemctl start ras-mc-ctl
```

## Sources
* https://www.setphaserstostun.org/posts/monitoring-ecc-memory-on-linux-with-rasdaemon/