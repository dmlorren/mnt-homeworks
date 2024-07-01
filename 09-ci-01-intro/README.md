# Домашнее задание к занятию 7 «Жизненный цикл ПО» - Иванов Дмитрий (fops-13)

## Подготовка к выполнению

1. Получить бесплатную версию Jira - https://www.atlassian.com/ru/software/jira/work-management/free (скопируйте ссылку в адресную строку). Вы можете воспользоваться любым(в том числе бесплатным vpn сервисом) если сайт у вас недоступен. Кроме того вы можете скачать [docker образ](https://hub.docker.com/r/atlassian/jira-software/#) и запустить на своем хосте self-managed версию jira.
2. Настроить её для своей команды разработки.
3. Создать доски Kanban и Scrum.
4. [Дополнительные инструкции от разработчика Jira](https://support.atlassian.com/jira-cloud-administration/docs/import-and-export-issue-workflows/).

## Основная часть

Необходимо создать собственные workflow для двух типов задач: bug и остальные типы задач. Задачи типа bug должны проходить жизненный цикл:

1. Open -> On reproduce.
2. On reproduce -> Open, Done reproduce.
3. Done reproduce -> On fix.
4. On fix -> On reproduce, Done fix.
5. Done fix -> On test.
6. On test -> On fix, Done.
7. Done -> Closed, Open.

Остальные задачи должны проходить по упрощённому workflow:

1. Open -> On develop.
2. On develop -> Open, Done develop.
3. Done develop -> On test.
4. On test -> On develop, Done.
5. Done -> Closed, Open.

**Что нужно сделать**

1. Создайте задачу с типом bug, попытайтесь провести его по всему workflow до Done. 
1. Создайте задачу с типом epic, к ней привяжите несколько задач с типом task, проведите их по всему workflow до Done. 
1. При проведении обеих задач по статусам используйте kanban. 
1. Верните задачи в статус Open.
1. Перейдите в Scrum, запланируйте новый спринт, состоящий из задач эпика и одного бага, стартуйте спринт, проведите задачи до состояния Closed. Закройте спринт.
2. Если всё отработалось в рамках ожидания — выгрузите схемы workflow для импорта в XML. Файлы с workflow и скриншоты workflow приложите к решению задания.

## Решение задачи:
1. Создали workflow для типа задачи bug и назначил схему на бизнес процесс и применили к проекту
<img src="img/CI09_01.png">

2. Протянули созданную багу по всему workflow
<img src="img/CI09_111.png">
<img src="img/CI09_02.png">

3. Создали workflow для остальных типов задач, назначили схему на бизнес процесс и применили к проекту
<img src="img/CI09_02.png">
4. Создали задачу epic прикрепили таски, провели по новому workflow
<img src="img/CI09_04.png">
<img src="img/CI09_05.png">
5. Создали скрам в нашем проекте из бэклога прокинули задачи, прогнали через статусы, спринт завершён успешно.
<img src="img/CI09_06.png">
<img src="img/CI09_07.png">

### Экспортированные xml:
[all_requests_except_bug.xml](https://github.com/dmlorren/mnt-homeworks/blob/MNT-video/09-ci-01-intro/xml/all_requests_except_bug.xml)
[workflow_for_bug.xml](https://github.com/dmlorren/mnt-homeworks/blob/MNT-video/09-ci-01-intro/xml/workflow_for_bug.xml)

---

