***Задание 1***

    Сложите исходники приложения в Github:

    1.Скачайте с FTP файлы проекта. Предлагаем использовать для этого клиент Filezilla
        FTP ADDRESS: 178.154.213.194
        Логин: techuser
        Пароль: techuser
    2. Склонируйте созданный репозиторий sausage-store на свою рабочую станцию.

Инициализируем Git-репозиторий:
```bash
git init
```

[//]: # (Клонироуем репозиторий :)

[//]: # (```bash)

[//]: # (git clone git@github.com:EgorSinitsyn/sausage-store.git)

[//]: # (```)

Добавляем файлы в отслеживание:
```bash
git add .
```

Коммитим изменения:
```bash
git commit -m "Создание репозитория"
``` 

Команды в помощь:
$ git log — есть коммит, который добавляет файлы
$ git diff — пустота
$ git status — nothing to commit, working tree clean





***Задание 2*** 

    В репозиторий попали файлы настройки /.idea/ и /.vscode/ от других разработчиков. Вам нужно удалить их из проекта.
        1.Заберите последнюю версию main из удалённого репозитория к себе.
        2.Добавьте директории /.idea/ и /.vscode/ в .gitignore.
        3.Удалите  /.idea/ и /.vscode/ из проекта.
        4.Удалите /.idea/ и /.vscode/ из Git-индекса.
        5.Сохраните изменения в удалённом Git-репозитории.

Добавяю директории /.idea/ и /.vscode/ в .gitignore.
```bash
nano .gitignore
```

Удаляю  /.idea/ и /.vscode/ из проекта.
```bash
rm -r .vscode/
rm -r .idea/
```

Удаляю /.idea/ и /.vscode/ из Git-индекса.
```bash
git rm -r --cached .idea/
git rm -r --cached .vscode/
```

Сохраняю изменения в удалённом Git-репозитории.
```bash
git add .gitignore
git rm --cached .gitignore
git commit -m "Удаление лишних файлов /.idea/ и /.vscode/"
git push git@github.com:EgorSinitsyn/sausage-store.git
#git push --set-upstream git@github.com:EgorSinitsyn/sausage-store.git main
```





***Задание 3***

    История изменений в репозитории разрослась до нечитаемого уровня. 
    Необходимо изучить, какие последние коммиты можно укомплектовать в один коммит и объединить
        1. Заберите последнюю версию main к себе.
        2. Посмотрите на историю коммитов ветки main.
        3. Объедините 4 последних изменений в один коммит.
        4. Сохраните изменения в удалённом Git-репозитории.
        5. Отправьте на проверку в бот.
        6. После успешной проверки удалите файлы

История коммитов ветки main.
```bash
git log
```

Объединение 4 последних изменений в один коммит.
```bash
git rebase -i HEAD~4
git rebase --continuqe
```
pick 5860c54 adding 1additional com
squash 497bb9f adding 2additional com
squash 0182f52 rebase -i
squash 6e326ea 4

```bash
touch test.py
nano test.py
```

```bash
git add .
git commit -m "Добавление test.py"
git push git@github.com:EgorSinitsyn/sausage-store.git
```





***Задание 4***

    Приложение перестало работать. Точное время коллапса — 1 коммит назад.
    Вам нужно откатить эти изменения в ветке main.
        1.Заберите последнюю версию main к себе.
        2.Откатите ветку main на 1 коммит назад. Не поломайте взаимодействие разработчиков с Git, а то в следующий раз они не помогут с приложением. Это значит, что изменения должны быть отдельным коммитом, без перезаписи истории изменений.
        3. Запушьте изменения.
        4.Отправьте задание на проверку в бот.

Откатываю ветку main на 1 коммит назад:
```bash
git revert HEAD
git diff
```

Добавляю .gitignore в игнорируемые файлы:
```bash
nano gitignore
```
Добавляю в файл .gitignore следующие строки:
.gitignore

Проверяю статус:
```bash
git status
```

Git-add
```bash
git add .
```

got commit
```bash
git commit -m "Добавление файла .gitignore"
```

git push
```bash
git push git@github.com:EgorSinitsyn/sausage-store.git
```





***Задание 5***

    Нужно включить в релиз зелёную кнопку. Но только её одну. Для этого посмотрите, какие изменения есть в ветке new_button, 
    и заберите из неё файл green_button.xml в main.
        1. Заберите все изменения из удалённого Git-репозитория к себе, в том числе и новые ветки.
        2. Переключитесь на ветку new_button.
        3. Найдите коммит, создающий файл green_button.xml.
        4. Слейте только этот коммит с веткой main, другие коммиты и файлы не нужны.
        5. Удалите ветку new_button.
        6. Запушьте изменения и отправьте на проверку в бот.

Создаю новую ветку new_button:
```bash
git checkout -b new_button
```

Проверяю ветку, в которой работаю:
```bash
git branch
```

Добавляю файл green_button.xml в ветку new_button:
```bash
git add green_button.xml
```

Коммитим изменения:
```bash
git commit -m "Добавил файл green_button.xml"
```

Для разнообразия создадим файл с red_button.xml:
```bash
git add red_button.xml
```

Коммитим изменения:
```bash
git commit -m "Добавил файл red_button.xml"
```

Теперь хочу коммит с green_button.xml перенести в ветку main:
```bash
git checkout main
git cherry-pick 1ec952d1d4a78fdf40269638f53f1eb7af835608
git commit -m "Влил файл green_button.xml в ветку main"
git push git@github.com:EgorSinitsyn/sausage-store.git
```

Удаляю ветку new_button:
```bash
git branch -d new_button
```

```bash
git branch
```





***Задание 6***

    Поправьте отступ в шаблоне сайта. Отступ задаётся по адресу: frontend/src/app/app.component.css. 
    Нужно изменить padding-top: 65px; на padding-top: 70px;.
        1. Создайте отдельную ветку и внесите изменения, которые решат задачу. Название ветки задайте на своё усмотрение.
        2. Запушьте изменения и создайте Pull Request.
        3. Отправьте Pull Request на проверку, чтобы получить апрув и влить изменения в main.

Создаю новую ветку fix_padding:
```bash
git checkout -b fix_padding
```

Исправляю изменения в файле frontend/src/app/app.component.css. 
```bash
nano frontend/src/app/app.component.css
```

Коммитим изменения:
```bash
git add frontend/src/app/app.component.css
git commit -m "Изменение отступа padding-top в файле app.component.css"
```

Заливаем изменение в мейн:
```bash
git checkout main
git cherry-pick 9b049232309dd1bafa2954ec70e281260b9d249f
git push git@github.com:EgorSinitsyn/sausage-store.git
```

Удаляем ветку fix_padding:
```bash
git branch -d fix_padding
```





***Задание 7***

    Измените название сосиски «Русская» на «Еврейская». Список доступных для заказа сосисок задаётся в 
    backend/src/main/java/com/yandex/practicum/devops/SausageApplication.java.
        1. Заберите последнюю версию main к себе.
        2. Создайте новую ветку, имя выберите на свой вкус.
        3. Внесите изменения, чтобы «починить» название сосиски.
        4. Запушьте изменения и создайте Pull Request.
        5. Тем временем один из разработчиков поправил имя этой сосиски без задачи, прямо в ветке main.
        6. Посмотрите в свой Pull Request. Из-за изменений в main появились конфликты.
        7. Заберите в свою ветку изменения из main и разрешите появившиеся конфликты.
        8. Запушьте изменения и отправьте Pull Request на проверку.

Создаю новую ветку jew_sausage:
```bash
git checkout -b jew_sausage
```

Исправляю изменения в файле backend/src/main/java/com/yandex/practicum/devops/SausageApplication.java. 
```bash
nano backend/src/main/java/com/yandex/practicum/devops/SausageApplication.java
```

Коммитим изменения:
```bash
git add backend/src/main/java/com/yandex/practicum/devops/SausageApplication.java
git commit -m "Изменение названия сосиски Русская на Еврейская"
```

Пушим изменения в отдельную ветку:
```bash
git push origin jew_sausage
```

Создаю Pull Request в интерфейсе Гитхаб: https://github.com/EgorSinitsyn/sausage-store/compare/main...jew_sausage
и отправляю на проверку.

[//]: # (Сливаем изменения из jew_sausage в main)

[//]: # (```bash)

[//]: # (git checkout main)

[//]: # (git merge jew_sausage)

[//]: # (git push origin main)

[//]: # (```)

Удаляем ветку:
```bash
git branch -d jew_sausage
```





***Финальные правки:***
```bash
git add.
git commit -m "Финальные правки"
git push git@github.com:EgorSinitsyn/sausage-store.git
```