---
layout: default
title: Установка Glavos Linux
menus:
  install:
    title: Установка
    weight: 1
image: /assets/img/programming.svg
post_video: dOn_rHMZGxY
---

## Содержание
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Запись ISO

Для записи образа на USB накопитель потребуется установочный ISO образ, который можно скачать по ссылке [Скачать Glavos Linux](/get).

> Перед началом записи образа, отформатируйте USB накопитель в FAT32, например, используя gparted. Проверьте контрольные суммы.

## Проверка ISO образа

Файлы с контрольными суммами всегда находятся рядом с iso, в [зеркалах загрузки](/get) и имеют расширение файла `.txt`. Внутри файла хеш, который и нужно сравнить.

Проверка контрольных сумм в Windows.

Чтобы проверить контрольные суммы в Windows используйте следующую утилиту [MD5 & SHA Checksum Utility](http://raylin.wordpress.com/downloads/md5-sha-1-checksum-utility/).

Проверка контрольных сумм в Linux.

Проверка MD5.

```bash
md5sum glavos_xfce_1.0.0_20181102.iso
```

Проверка SHA256.

```bash
sha256sum glavos_xfce_1.0.0_20181102.iso
```

GPG.

```bash
sudo pacman -S gnupg
```

Импорт ключа и проверка образа.

```bash
gpg --keyserver keys.gnupg.net --recv-keys 98F76D97B786E6A3
gpg --verify glavos_xfce_1.0.0_20181102.iso.sig glavos_xfce_1.0.0_20181102.iso
```

Подробнее о [GnuPG](/wiki/other/gnupg).

На этом проверка образа закончена. Выше были приведены несколько способов проверки, можете использовать любой, или все сразу.

## Программы для записи

Для записи образа в **Linux** потребуется для начала отформатировать Ваш USB накопитель. Сделать это можно следующей командой.

```bash
sudo mkfs.vfat /dev/sdX -I
```

Далее записываем скачанный ранее образ используя утилиту **dd**.

```bash
sudo dd bs=4M if=glavos.iso of=/dev/sdX status=progress && sync
```

Кросплатформенные инструменты для записи образов (Linux, Windows).

- [Etcher](https://etcher.io/)

Для записи образа в **Windows** рекомендуется использовать программу [Rufus](https://rufus.akeo.ie/).

> При записи образа в программе Rufus выбирайте режим записи ISO в dd.

## Установка

После успешной записи образа и его загрузки на Вашем устройстве Вы увидите в самом начале раздел выбора языка интерфейса. Выбирайте тот, который Вам удобен. В данном примере будет использоваться русский язык.

> Если вы используете образ с xfce, то у вас присутствует выбор метода установки.

- Online: открывается раздел выбора других окружений и доп. программ, обязательно требуется включенный интернет.
- Offline: произойдет установка того, что вы видите в текущий момент, простая распаковка, интернет не нужен.

![Glavos step 1](/wiki/images/install/install-glavos/1.png)

На следующем шаге Вам требуется указать Ваше примерное местоположение для установки и выбора временной зоны.

![Glavos step 2](/wiki/images/install/install-glavos/2.png)

> Раскладка **ru,us** по **alt+shift**.

![Glavos step 3](/wiki/images/install/install-glavos/3.png)

После выбора раскладки Вам требуется разметить диск вручную либо оставить всё как есть.

![Glavos step 4](/wiki/images/install/install-glavos/4.png)

После завершения переразметки диска Вам нужно создать пользователя, выбрать желаемый пароль.

![Glavos step 5](/wiki/images/install/install-glavos/5.png)

Проверяем данные, можно вернуться и исправить, если что-то не так. Если всё верно - нажимайте "**Установить**".

![Glavos step 6](/wiki/images/install/install-glavos/6.png)

Дождитесь конца установки.

![Glavos step 7](/wiki/images/install/install-glavos/7.png)

Готово! Теперь Вы можете перезагрузить Ваше устройство.

![Glavos step 8](/wiki/images/install/install-glavos/8.png)

Выбор в меню GRUB.

![Glavos step 9](/wiki/images/install/install-glavos/9.png)

Менеджер входа (используется LightDm), в правом верхнем углу можно выбрать сессию, если присутствуют другие Окружения (DE), или Оконные менеджеры (WM). На данном скриншоте XFCE, она единственная и по умолчанию ничего можно не выбирать.

![Glavos step 10](/wiki/images/install/install-glavos/10.png)

Вот и все! Отдельная благодарность за скриншоты пользователю **breadandbutter** с nnm-club.me

![Glavos step 11](/wiki/images/install/install-glavos/11.png)
