---
layout: default
title: Установка и настройка репозиториев glavos
menus:
  install:
    title: Репозиторий glavos
    weight: 4
---

Содержание
{: .text-delta }

1. TOC
{:toc}

## Добавление ключа 1

> Удалить все упомянания glavos_repo из `/etc/pacman.conf`.

```bash
sudo nano /etc/pacman.conf

[glavos_repo]
Server = https://github.com/glavos/$repo/raw/master/$arch
...
```

### Установка

- Скачать и запустить скрипт.
- Автоматически установит запись в `/etc/pacman.conf`.
- Установит необходимые ключи.

```bash
curl -LO git.io/strap.sh

sudo sh strap.sh
```

## Добавление ключа 2

Данный способ немного сложнее.

```bash
# инициализация gpg
pacman-key --init

pacman -Sy wget && wget git.io/glavos.gpg
pacman-key --add glavos.gpg
# или с key сервера
pacman-key --recv-keys 98F76D97B786E6A3
```

### Проверить отпечаток

```bash
pacman-key --finger 98F76D97B786E6A3
```

### Подписываем ключ

```bash
pacman-key --lsign-key 98F76D97B786E6A3
# список
pacman-key --list-keys
```

### Обновляем ключи

```bash
pacman-key --populate
# up key server
pacman-key --refresh-keys
```

### Сортируем зеркала reflector

```bash
pacman -S reflector

reflector --verbose -a1 -f10 -l70 -p https -p http --sort rate --save /etc/pacman.d/mirrorlist
```

### Устанавливаем зеркала

```bash
nano /etc/pacman.conf

[glavos_repo]
Server = https://github.com/glavos/$repo/raw/master/$arch
Server = https://osdn.net/projects/glavos/storage/$repo/$arch
Server = https://cvc.keybase.pub/$repo
```

## Glavos aur

Можете воспользоваться [Glavos aur](https://dev.glavos.ru/glavos-aur) репозиторием, пакетов не так много, но он содержит последнии версии пакетов.

```bash
nano /etc/pacman.conf

[glavos-aur]
SigLevel = Optional TrustAll
Server = https://dev.glavos.ru/glavos-aur
```

> Если Вы заметите какие-либо проблемы в репозиториях, сообщите в [Telegram Chat](https://telegram.me/glavos).
