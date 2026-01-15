mostly works for SATA disk

full output
```bash
sudo smartctl -A /dev/sdX
```

parsed critical information
```bash
sudo smartctl -A /dev/sda | egrep -i "Reallocated|Current Pending|Offline Uncorrectable|UDMA|Temperature|Raw Read|Power_On_Hours"

```