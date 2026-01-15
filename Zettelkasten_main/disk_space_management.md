визуальное предаставление
```bash
baobab
```

быстрая статистика по занимаемому месту
```bash
df -h
```

глубокий анализ всех файлов и сортировка по размеру в заданной директории
``` bash
 sudo du -h /var/lib/docker/ | sort -h
```

копирование с правами и визуалицаией (возможно  флага -ah достаточно)
```bash
rsync -aHAX --info=progress2 library/ /mnt/raid1/immich_store/library/
```