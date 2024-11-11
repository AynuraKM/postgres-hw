## Создан новый кластер main2
> ![replica](../images/3.png)
>## С помощью команды `rm -rf /var/lib/postgresql/15/main2/*` очищаем директорию под бэкап.
>## Делаем бэкап `pg_basebackup -p 5432 -R -h 127.0.0.1 -U postgres -D ./main2`
>## Запускаем реплику `pg_ctlcluster restart 15 main2`
>## Делаем замер 
> ![4](../images/4.png)
># Вывод: Производительность в обоих случаях одинаковая