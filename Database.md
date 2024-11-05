# База данных

Цели:
1. Хранить токены доступа к Умному Дому (используется практически всеми)
2. Хранить созданные /start? ссылки запуска сценариев
3. Хранить состояние подписки на алерты (вкл/выкл)
4. Хранить созданные виртуальные лампочки

```sql
CREATE TABLE tokens(
	user_id Int64 PRIMARY KEY,  -- будет много поиска
	token String
);

CREATE TABLE scenarios(
	id STRING PRIMARY KEY,  -- нужен генератор случайных строк
	user_id Int64,     -- по этому полю будет поиск в редакторе
	scenario_id Int64  -- айдишник в УДЯ
);

CREATE TABLE alerts( -- тупо exists
	user_id Int64 PRIMARY KEY
);

CREATE TABLE hooks(
	lamp_id UUID PRIMARY KEY,  -- виртуальная лампочка
	user_id Int64,  -- по этому полю будет поиск в редакторе
	name String,    -- человеческое имя лампочки
	url String      -- сюда делаем запрос когда лампочка зажигается
);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTg4NzUwNTQsMjAwNDE0ODgzN119
-->