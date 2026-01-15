create archive 
```bash
tar -cf archive_name.tar file_or_folder
```

create archive with compressing 
```bash
tar -czf archive_name.tar.gz file_or_folder
```

Extract files
```bash
tar -xf archive_name.tar 
```

Extract compressing  files 
```bash
tar -xzf archive_name.tar.gz
```

Functions for bashrc
```bash
# the fierst arg - name of arch, and rest of them - files and folder for compressing
compress() {
    tar -czf "$1.tar.gz" "${@:2}"
}
# the fierst arg - name of arch, the second - is option name of path to the folder or the current location
decompress() {
    tar -xzf "$1" -C "${2:-.}"
}
```