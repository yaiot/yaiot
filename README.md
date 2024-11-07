# yaiot

Движок сценариев Умного Дома Яндекса (УДЯ), хоть и хорош, но имеет ряд ограничений. Мы строим экосистему вокруг него, чтобы добавить больше функционала минимальными услиями, оставаясь, насколько это можно, в рамках УДЯ.

## YAML-сценарии

Делает @iliakonnov

При всей любви к мобильным приложениям с пятью экранами и прочим, но гораздо удобнее хранить свои сценарии как текст в YAML, а в идеале с системой контроля версий, а ещё лучше — на гитхабе с CI (но это тема следующего хакатона). Наше расширение для браузера позволяет писать сценарии в YAML-файле и с помощью одной-единственной кнопки их все добавить в Умный Дом Яндекса.

Фичи нашего YAML формата:
- позволяет удобно управлять большим количеством разных сценариев и заливать их все вместе
- умеет группировать разные устройства вместе и использовать их в сценариях
- имеет более простой формат, чем хождение через curl в приватное API Яндекса

## IFTTT-интеграция

**Проблема**: хотя сценарии умного дома и хороши, но они не позволяют совершать действия за переделами УДЯ. А иногда хочется, например, отправить сообщение в телеграм в ответ на срабатывание какого-либо датчика.
**Решение**: добавить в УДЯ возможность совершать действия во внешних системах (например, ходить в API Telegram или запускать сценарии IFTTT).
**Как это работает**: единственный способ как-то взаимодействовать с внешним миром из УДЯ — зажигать виртуальные лампочки. Наш бекенд лампочек, в свою очередь, может видеть нажатия умных лампочек и реагировать на их добавление.

Что здесь нужно:

**Бекенд:** (делает @d-tolmachev)
Бекенд обслуживает умные лампочки и реализует всю логику их срабатывания:
1. бекенд умных лампочек (по типу [ya-iot-vars](https://github.com/iliakonnov/ya-iot-vars))
	* возможно, что не лампочек, а какой-то другой [вид устройств](https://yandex.ru/dev/dialogs/smart-home/doc/ru/concepts/device-types)
2. база данных, которая хранит отображение из ID лампочки (и пользователя) в URL, который нужно будет дергать
3. когда лампочка включается из сценария, мы идем в URL

**Фронтенд:** (делает @KH9IZ)
Нужна возможность как-то это конфигурировать

1. телеграм-бот умеет в авторизацию OAuth (см. ниже), этот токен должен браться из базы данных
2. в телеграм-боте должна быть возможность управлять умными лампочками: добавлять, удалять, редактировать.
3. Это может быть реализовано через команды `/add https://...`, `/edit_XXXX https://...`, `/delete_XXXX` и команду вывода списка текущих лампочек `/list`.
4. У каждой лампочки должно быть человеческое имя (требование API Яндекса)! Открытый вопрос откуда его брать.

## Авторизация в телеграм-боте

Делает @fadyat

Чтобы телеграм-ботом можно было пользоваться, хозяин умного дома должен как-то дать нашему бекенду токен. Для этого надо понять как работает OAuth и как удобнее всего можно получать от пользователя его токен в телеграм-боте.

Документация: https://yandex.ru/dev/dialogs/smart-home/doc/ru/concepts/platform-protocol#platform-access

## Алерты на недоступность лампочек в телеграме

Делает @fadyat

Пользователь бота может подписаться на мониторинг недоступности лампочек ~~(платная фича)~~ и тогда мы будем ему в телегарм присылать сообщение о том, что устройство было потеряно.
Подписка переключается (вкл-выкл) отдельной командой бота.
Наш бекенд каждые N времени получает состояние умного дома пользователя и находит там устройства, которые в offline.

Документация: https://yandex.ru/dev/dialogs/smart-home/doc/ru/concepts/platform-device-info

## Ссылки на сценарии в телеграм-боте

Делает @DenChika

**Проблема:** хотим предоставлять возможность легко запускать сценарии умного дома из интерфейса телеграма одним кликом.
**Решение:** генерируем ссылки на телеграм-бота, которые будут запускать тот или иной сценарий
**Как это работает:** генерируем ссылки вида `t.me/Bot?start=123456` и когда кто-угодно делает боту `/start` с ID ссылки, мы запускаем привязанный к этой ссылке сценарий

Что здесь нужно:
* пользователь бота (хозяин умного дома) авторизуется через OAuth в нашем приложении. Мы получаем от Яндекса токен, который предоставляет нам доступ к умному дому пользователя, и сохраняем его в БД.
* пользователь бота смотрит на список своих сценриев в боте (например, сообщение с командами `/scenario_XXXX`) и выбирает один
* мы в ответ на это генерируем ссылку вида `t.me/Bot?start=123456`
* потом кто угодно переходит по ссылке и может запускать сценарий: мы достаем соответствующий токен из базы и запускаем соответствующий сценарий

Нужно уметь делать revoke для ссылок (список активных ссылок текущего пользователя и возможность каждую отдельно удалить).

Документация: https://yandex.ru/dev/dialogs/smart-home/doc/ru/concepts/platform-scenario
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4ODIxMzc1NSw2MTQ2MDAyMzMsMTkzND
Y5MjkzLDE2NDM3MDQ3OTFdfQ==
-->
