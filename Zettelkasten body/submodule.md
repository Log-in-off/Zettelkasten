при выкачивании нового репозитория можно рекурсивно выкачать все сабмодули
```
git clone git@github.com:PX4/PX4-Autopilot.git --recurse-submodules
```

но если известно, что нужна не `main` ветка, то лучше сделать `clone` без рекурсивного выкачивания, а после перехода на нужную ветку докачать сабмодули. 
В этом случае изменения сабмодулей из прошлой ветки(`main`) не будут конфликтовать с требуемой.
```
git clone  git@github.com:PX4/PX4-Autopilot.git
cd PX4-Autopilot
git checkout v1.14.0
git submodule update --init --recursive
```

Если меняем бранч и появляются незакомиченые изменения из других сабмодулей, то можно вызывать 
```
git checkout . --recurse-submodules
```

для сабмодулей можно применять подход `foreach`
например для удаления не отслеживаемых файлов [[git_clean]]
```
git submodule foreach 'git clean -d -f'
```

так же можно пройтись по всем сабмодулям и обновить их содержимое до актуального
```
git submodule foreach 'git checkout'
```
для добавления нового сабмодуля
```
git submodule add https://name.git path/to/folder/where/it/will/be/keep
```