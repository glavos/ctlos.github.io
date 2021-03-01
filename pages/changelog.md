---
layout: page
title: Лог Изменений
description: История измененя Glavos, релизы
permalink: /wiki/changelog/
comments: false
edit: false
---

Подпишись, чтобы быть в кусе новостей.

- Группа в VK: [vk.com/glavos](https://vk.com/glavos)
- Telegram канал: [t.me/glavos_info](https://telegram.me/glavos_info)
- Подпишись на: [RSS](https://glavos.github.io/wiki/feed.xml)

> Последние и наиболее актуальные версии представлены на странице загрузки [glavos.github.io/get](/get).

Пройдите [небольшой опрос](https://forms.gle/qzAUa6R4fShf3xSw7).

## Контакты

[Свяжитесь с нами](/wiki/#контакты), если у Вас есть предложения, или пожелания.

## Поддержи проект

- [Donate](/donat/).

<div class="changelog">
	{% for change in site.posts %}
		<div class="changelog_item">
			<h2>{{ change.title }}</h2>
			<p><span class="text-small">{{ change.date | date_to_string }}</span> <span class="badge {{ change.type }}">{{ change.type }}</span></p>
			{{ change.content }}
		</div>
	{% endfor %}
</div>
