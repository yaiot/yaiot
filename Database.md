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

CREATE TABLE scen(
	user_id Int64 PRIMARY KEY,
	token String
);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxNDEyOTYyNV19
-->