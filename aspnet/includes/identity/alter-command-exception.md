> Некоторые команды не поддерживаются, если приложение использует SQLite в качестве хранилища данных удостоверений. Из-за ограничений в ядре СУБД `Alter` команды вызовут следующее исключение:
>
> "System. NotSupportedException: SQLite не поддерживает эту операцию миграции". 
>
> В качестве обходного решения выполните Code First миграции для базы данных, чтобы изменить таблицы.
