show all file in location /
```bash
find /
```

show all file in the current location
```bash
find . 
```

find all json files in the current location
```bash
find . -name "*.json"
```

## TIPS

if we don't want to see messages like  `:Permission denied` just add `2>/dev/null`
```bash
find / -name "*.ulog" 2>/dev/null
```
if we want find only files (not directory ) just add `-f`
```bash
find / -name "*json" -f 2>/dev/null
```
if only directory `-d`
```bash
find / -name "*json" -d 2>/dev/null
```
if check only new files we can add tag


move everything to /dev/null (union stderr and stdout)
```
command > /dev/null 2>&1
```