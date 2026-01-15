 если нужно сделать патч из одного коммита 
 ```bash
 git format-patch -1 <хеш коммита>
```
если нужно сделать из нескольких коммитов
```bash
git format-patch <начальный-коммит-хеш>..<конечный-коммит-хеш>
```

если нужно сделать патч из не отслеживаемых файлов
```bash
git diff > uncommitted-changes.patch
```
если нужно сделать патч изменений добавленных командой `git add`, но не закомиченных файлов
```bash
git diff --cached > staged-changes.patch
```
если нужно их скомбинировать
```bash
git diff > all-changes.patch
git diff --cached >> all-changes.patch
```