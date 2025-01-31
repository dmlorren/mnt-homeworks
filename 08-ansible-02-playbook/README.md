# Домашнее задание к занятию 2 «Работа с Playbook» - Иванов Дмитрий (fops-13)

## Подготовка к выполнению

1. * Необязательно. Изучите, что такое [ClickHouse](https://www.youtube.com/watch?v=fjTNS2zkeBs) и [Vector](https://www.youtube.com/watch?v=CgEhyffisLY).
2. Создайте свой публичный репозиторий на GitHub с произвольным именем или используйте старый.
3. Скачайте [Playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.
4. Подготовьте хосты в соответствии с группами из предподготовленного playbook.

## Основная часть

1. Подготовьте свой inventory-файл `prod.yml`.
2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает [vector](https://vector.dev). Конфигурация vector должна деплоиться через template файл jinja2. От вас не требуется использовать все возможности шаблонизатора, просто вставьте стандартный конфиг в template файл. Информация по шаблонам по [ссылке](https://www.dmosk.ru/instruktions.php?object=ansible-nginx-install). не забудьте сделать handler на перезапуск vector в случае изменения конфигурации!
3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.
4. Tasks должны: скачать дистрибутив нужной версии, выполнить распаковку в выбранную директорию, установить vector.
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.
6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги. Пример качественной документации ansible playbook по [ссылке](https://github.com/opensearch-project/ansible-playbook). Так же приложите скриншоты выполнения заданий №5-8
10. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-02-playbook` на фиксирующий коммит, в ответ предоставьте ссылку на него.


## Решение задачи 1

### Итоговый резльтат:
<img src="img/playbook_01.png">

1. Конфигурирование выполнялось в yandex cloud, под установку clickhouse и vector поднята дополнительная vm на debian (c vm1 (ansible) на vm2 проброшен id_rsa.pub в ~/.ssh/authorized_keys).
2. Для подключению по ssh использовал серые ip-адреса, так ноды всё равно находятся в одной подсети.
<img src="img/playbook_02.png">
3. Playbook устанавливает сервисы clickhouse и vector (ориентированные на deb) используя переменные описанные в group_vars и создаёт БД с именем logs.

пример команды запуска:
```bash
ansible-playbook -i inventory/myprod.yml playbook/clikhouse_vektor_install.yml 
```

создан необходимый тег:
```bash
git tag -a 08-ansible-02-playbook 8fe737638d4392655520b217fdcc3633cf4062bd -m "add tag"
git push origin --tags 
```

---


