# yaiot

Движок сценариев Умного Дома Яндекса (УДЯ), хоть и хорош, но имеет ряд ограничений. Мы строим \косистему вокруг него, чтобы добавить больше функционала минимальными услиями, оставаясь, насколько это можно, в рамках УДЯ.

## YAML-сценарии

## IFTTT-интеграция

**Проблема**: хотя сценарии умного дома и хороши, но они не позволяют совершать действия за переделами УДЯ. А иногда хочется, например, отправить сообщение в телеграм в ответ на срабатывание какого-либо датчика.
**Решение**: добавить в УДЯ возможность совершать действия во внешних системах (например, ходить в API Telegram или запускать сценарии IFTTT).
**Как это работает**: единственный способ как-то взаимодействовать с внешним миром из УДЯ — зажигать виртуальные лампочки. Наш бекенд лампочек, в свою очередь, может

## Телеграм-бот
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODIxNDAzOTMsMTY0MzcwNDc5MV19
-->