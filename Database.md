# База данных

Цели:
1. Хранить токены доступа к Умному Дому
2. Хранить созданные /start? ссылки запуска сценариев
3. Хранить состояние подписки на алерты (вкл/выкл)
4. Хранить созданные виртуальные лампочки

```sql
CREATE TABLE tokens(
	user_id Int64 PRIMARY KEY,
	token String
);

CREATE TABLE scenarios(
	id STRING PRIMARY KEY,  -- нужен генератор случайных строк
	user_id Int64,     -- см. tokens
	scenario_id Int64  -- айдишник в УДЯ
);

CREATE TABLE alerts(
	user_id Int64 PRIMARY KEY,
);

CREATE TABLE hooks(
	id UUID PRIMARY KEY,
	user_id Int64,  -- см. tokens
	scenario_id
);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUxMDg2NDkzNF19
-->