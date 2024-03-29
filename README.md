# Домашнее задание к занятию «Резервное копирование» Белобородов Юрий

### Цель задания
В результате выполнения этого задания вы научитесь:
1. Настраивать регулярные задачи на резервное копирование (полная зеркальная копия)
2. Настраивать инкрементное резервное копирование с помощью rsync


### Чеклист готовности к домашнему заданию

1. Установлена операционная система Ubuntu на виртуальную машину и имеется доступ к терминалу
2. Сделан клон этой виртуальной машины с другим IP адресом


### Задание 1
- Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию `/tmp/backup`
- Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
- Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
- На проверку направить скриншот с командой и результатом ее выполнения

Ответ:

Команда rsync
```
rsync -av --delete --exclude '.*' /home /tmp/backup
```

Результат

![1-1_commandrsync.png](https://github.com/Zikin18/SYS-25_10.03/blob/master/1-1_commandrsync.png)


### Задание 2
- Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
- Резервная копия должна быть полностью зеркальной
- Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции
- Резервная копия размещается локально, в директории `/tmp/backup`
- На проверку направить файл crontab и скриншот с результатом работы утилиты.

Ответ:

Скрипт
```
#!/bin/sh
rsync -av --delete --exclude '.*' /home /tmp/backup >> /var/log/crontab.log

```

Содержимое crontab после добавления скрипта

![2-1_crontab.png](https://github.com/Zikin18/SYS-25_10.03/blob/master/2-1_crontab.png)

Проверка скрипта и отображение результатов работы

`tail /var/log/crontab.log`

![2-2_log_result.png](https://github.com/Zikin18/SYS-25_10.03/blob/master/2-2_log_result.png)
