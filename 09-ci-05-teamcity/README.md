# Домашнее задание к занятию 11 «Teamcity» - Иванов Дмитрий (fops-13)

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).


Подготовлены виртуальные машины:
<img src="img/09_05_1.png">

Первоначальная настройка teamcity-server:
<img src="img/09_05_3.png">

Авторизованный агент:
<img src="img/09_05_2.png">

Форк репозитория example-teamcity:
```url
https://github.com/dmlorren/example-teamcity
```

Отредактирован инвентарный файл:
<img src="img/09_05_4.png">

Запуск осуществляется через плейбук:
```
ansible-playbook site.yml -i inventory/cicd/hosts.yml
```

## Основная часть

1. Создайте новый проект в teamcity на основе fork.
<img src="img/09_05_5.png">

2. Сделайте autodetect конфигурации.
<img src="img/09_05_6.png">

3. Сохраните необходимые шаги, запустите первую сборку master.
<img src="img/09_05_7.png">

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.
<img src="img/09_05_8.png">

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.
<img src="img/09_05_9.png">

6. В pom.xml необходимо поменять ссылки на репозиторий и nexus. Идём в форкнутый нам репозиторий и прямо в гите редактируем ip.
<img src="img/09_05_10.png">

7. Запустите сборку по master (через кнопку run), убедитесь, что всё прошло успешно и артефакт появился в nexus.
   
7.1 Предварительно в два наших шага (Maven и Maven2) нужно зайти и выбрать settings.xml и сохранить.
<img src="img/09_05_11.png">

7.2 Заходим на сервер с нексусом и проверяем, что артефакты загрузились.
<img src="img/09_05_12.png">

8. Мигрируйте `build configuration` в репозиторий.
Предварительно, нужно проверить, что авторизация в git будет идти через токен, а не через http, иначе будет ошибка.
<img src="img/09_05_13.png">

В репозиторий загрузка прошла успешно.
<img src="img/09_05_14.png">

9.  Создайте отдельную ветку `feature/add_reply` в репозитории.
<img src="img/09_05_15.png">

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.
11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.
<img src="img/09_05_16.png">
<img src="img/09_05_17.png">

12. Сделайте push всех изменений в новую ветку репозитория.
```
git checkout -b feature/add_reply
git push origin feature/add_reply
```
<img src="img/09_05_18.png">

13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
<img src="img/09_05_19.png">

14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
```
git checkout master
git merge feature/add_reply
git push https://github.com/dmlorren/example-teamcity master
```

15.  Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
У нас в нексусе уже есть артефакты от прошлых шагов, просто добавим в pom.xml новую версию (было 0.0.2 стало 1.0.0)

16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
<img src="img/09_05_20.png">

18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.

Ссылки:
https://github.com/dmlorren/example-teamcity

https://github.com/dmlorren/mnt-homeworks/blob/MNT-video/09-ci-05-teamcity/README.md

---