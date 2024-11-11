## 1. Создана схема `College` и в ней таблица `Students` с полем `ID`
## 2. С помощью команды `SELECT pg_size_pretty(pg_total_relation_size('college.students'));` просматриваем размер файла таблицы с 1млн строк
>![size1](../images/hw3-size1.png)
## 3. С помощью команды `SELECT schemaname, relname, n_dead_tup FROM pg_stat_all_tables WHERE relid='college.students'::regclass \gx` смотрим количество мертвых строк в таблице после 5-и разового обновления
>![amount](../images/hw3-dead-tup-1.png)
## С помощью команды `SELECT schemaname, relname, last_autovacuum FROM pg_stat_user_tables WHERE schemaname = 'college' AND relname = 'students';` проверяем время запуска автовакуума
>![vacuum1](../images/hw3-last-v1.png)
## 5. Снова обновляем все строчки и проверяем размер таблицы 
>![1](../images/hw3-size2.png)
## 6. С помощью команды `ALTER TABLE college.students SET (autovacuum_enabled = false);` отключаем автовакуум
## 7. Размер файла после 10-и кратного обновления всех строк:
>![2](../images/hw3-size3.png)
>
># Результат:
> 5 из 10 циклов попали в ячейки, они были почизены автовакуумом, но не удалены, а оставшиеся циклы увеличили тпблицу, выделением новых страничек, и поэтому размер таблицы увеличился