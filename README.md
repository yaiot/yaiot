# yaiot

Движок сценариев Умного Дома Яндекса (УДЯ), хоть и хорош, но имеет ряд ограничений. Мы строим экосистему вокруг него, чтобы добавить больше функционала минимальными услиями, оставаясь, насколько это можно, в рамках УДЯ.

## YAML-сценарии

## IFTTT-интеграция

**Проблема**: хотя сценарии умного дома и хороши, но они не позволяют совершать действия за переделами УДЯ. А иногда хочется, например, отправить сообщение в телеграм в ответ на срабатывание какого-либо датчика.
**Решение**: добавить в УДЯ возможность совершать действия во внешних системах (например, ходить в API Telegram или запускать сценарии IFTTT).
**Как это работает**: единственный способ как-то взаимодействовать с внешним миром из УДЯ — зажигать виртуальные лампочки. Наш бекенд лампочек, в свою очередь, может 

Что здесь нужно:
1. бекенд умных лампочек (по типу [ya-iot-vars](https://github.com/iliakonnov/ya-iot-vars))
	* возможно, что не лампочек, а, скажем,
2. база данных, которая хранит действие, которое нужно совершить

## Телеграм-бот
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxOTY1MjM2MCwxNjQzNzA0NzkxXX0=
-->