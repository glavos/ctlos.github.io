---
layout: default
title: Glavos iso
menus:
  other:
    title: Glavos iso
    weight: 1
post_photo_path: /wiki/images/other/glavosiso.png
---

[YouTube link](https://www.youtube.com/watch?list=PLwdYMSK64DT6CCheHMbaqlOzpqfk2FTvT&v=XNpAXthDbrI) Старая версия, но многое объясняет.

Содержание
{: .text-delta }

1. TOC
{:toc}

## Создание iso образа

[YouTube link](https://www.youtube.com/watch?list=PLwdYMSK64DT6CCheHMbaqlOzpqfk2FTvT&v=XNpAXthDbrI) Старое видео, но многое объясняет.

- [Github README](https://github.com/glavos/glavosiso/blob/master/README.md) - быстрый способ

## Глубокое вмешательство

### Подготовка

Установить пакеты для сборки.

```bash
yay -S git archiso mkinitcpio-archiso --noconfirm --needed
```

Создание директории и клонирование репозитория.

```bash
mkdir ~/glavos
cd ~/glavos
git clone https://github.com/glavos/glavos_repo
```

Или ssh.

```bash
git clone git@github.com:glavos/ctlo_repo.git
```

### Сборка aur пакетов

Найти нужный пакет на сайте аур [aur.archlinux.org](https://aur.archlinux.org) и загрузить snapshot вида `*.tar.gz`.

Собираем пакеты в `build`.

```bash
mkdir ~/glavos/glavos_repo/build
cd ~/glavos/glavos_repo/build
wget https://aur.archlinux.org/cgit/aur.git/snapshot/gtk3-mushrooms.tar.gz
```

Распаковываем и собираем пакет.

```bash
tar -xvzf gtk3-mushrooms.tar.gz
cd gtk3-mushrooms
makepkg -s
```

Копируем собраные пакеты в `~/glavos/glavos_repo/x86_64`, инициализируем репозиторий. Пакеты в формате `*.pkg.tar.xz`, или `zst`.

```bash
cd ~/glavos/glavos_repo/x86_64
repo-add glavos_repo.db.tar.gz *.tar.xz
```

Или.

```bash
./update.sh --add
```

После добавления новых пакетов из aur необходимо переинициализировать репозиторий.(Удалить файлы баз данных), или запустить скрипт `update.sh` он сам все пересоздаст.

```bash
repo-add glavos_repo.db.tar.gz *.tar.xz

repo-add glavos_repo.db.tar.gz *.pkg.tar.zst
```

Или.

```bash
./update.sh --add
```

### Репозиторий iso

Клонируем репозиторий. Ветка master по умолчанию.

```bash
cd ~/glavos
git clone --depth=1 https://github.com/glavos/glavosiso
```

Добавляем пользовательский репозиторий для aur пакетов. В `/glavos/glavosiso/pacman.conf`.

```bash
[glavos_repo]
SigLevel = Optional TrustAll
Server = file:///home/fiduchi/glavos/glavos_repo/$arch
```

Закоментировать репозиторий glavos, если нужно.

```bash
#[glavos_repo]
#SigLevel = Never
#Server = https://raw.github.com/glavos/glavos_repo/dev/repo/$arch
```

### Сборка образа

Сделать скрипты исполняемыми.

```bash
cd glavosiso
chmod +x {autobuild.sh,chroot.sh,mkarchiso}
```

- Пакеты: packages.x86_64

Скрипту autobuild.sh обязательно нужно передать аргумент, любой. Я обычно отправляю `xfce_1.7.0` de/wm и версию.

```bash
sudo ./autobuild.sh xfce_1.7.0
```

Готовый образ и хэши создаются в данной директории `~/glavos/glavosiso/out`.

### Пересборка

Удалить каталоги и запустить скрипт сначала.

```bash
sudo rm -rf {out,work}
```

Или отредактировать.

```bash
nano /bin/pacstrap
```

Изменить строку, для пропуска установленных пакетов.

```bash
if ! pacman -r "$newroot" -Sy "${pacman_args[@]}"; then
```
На.
```bash
if ! pacman -r "$newroot" -Sy --needed "${pacman_args[@]}"; then
```

Удалить файлы блокировки.

```bash
sudo rm -v work/build.make_*
```

### Списки пакетов

Список установленных пакетов в системе. Подробно.

```bash
LANG=C pacman -Sl | awk '/\[installed\]$/ {print $1 "/" $2 "-" $3}' > ~/pkglist.txt

LANG=C pacman -Sl | awk '/\[installed\]$/ {print $2}' > ~/.pkglist.txt
```

Кратко.

```bash
pacman -Qqe > ~/pkglist.txt

pacman -Qqm > ~/aurlist.txt
```
