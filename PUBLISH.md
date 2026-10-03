# Как выложить сайт со скачиванием игры на GitHub Pages

Сайт пока не опубликован. Всё можно загрузить вручную через браузер — без командной строки и без передачи пароля кому-либо.

## 1. Создай репозиторий

На GitHub нажми **+ → New repository**. Назови, например, `five-nights-with-tyoma`. Выбери **Public**, включи **Add README**, затем **Create repository**. Ветка должна называться `main`.

## 2. Загрузи страницу

В репозитории выбери **Add file → Upload files**. Перетащи **index.html** из этой папки `website`, затем **Commit changes** в `main`. Файл должен оказаться прямо в корне репозитория, не внутри папки `website`. CSS, скрипт и картинка уже внутри HTML: больше ничего для внешнего вида загружать не нужно. При желании добавь также пустой файл `.nojekyll`.

Не загружай `index.template.html`: это технический шаблон, в нём нет готовых данных. Нужен именно `index.html`.

## 3. Положи установщики в Releases

Кнопки сайта будут скачивать файлы из одного релиза с тегом **versions** — напиши ровно так, маленькими буквами.

1. На главной странице репозитория справа нажми **Releases → Create a new release** (либо **Draft a new release**).
2. В **Choose a tag** создай тег `versions`, цель **Target: main**.
3. Название релиза: `Все версии игры`.
4. В область **Attach binaries** перетащи файлы из родительской папки `outputs`. Точный список находится в **FILES-FOR-RELEASE.txt** рядом с этой инструкцией: APK, EXE, архивы исходников и `Soundtracks.zip`. Не переименовывай файлы. `.idsig` загружать не нужно.
5. Дождись окончания всех загрузок и нажми **Publish release**. Не оставляй его черновиком, иначе посетители не смогут скачивать.

EXE превышают лимит обычных Git-файлов; хранить установщики нужно именно в Releases. Для каждого файла релиза разрешён размер менее 2 GiB, наши файлы помещаются. Проверочные суммы всех сборок есть в `outputs/SHA256-all-versions.txt`; его можно прикрепить дополнительно.

## 4. Включи Pages

Открой **Settings → Pages → Build and deployment**:

- **Source: Deploy from a branch**
- **Branch: main**
- папка **/(root)**
- нажми **Save**

После завершения публикации там появится адрес вида `https://ТВОЙ-ЛОГИН.github.io/five-nights-with-tyoma/`. Открой его и нажми Android или Windows. На стандартном домене `github.io` страница сама определит логин и репозиторий; менять HTML вручную не требуется.

## Если скачивание выдаёт 404

Проверь: релиз опубликован, тег называется `versions`, нужный файл прикреплён, имя полностью совпадает со списком. Загрузка только `index.html` создаёт сайт, но сами установщики всё равно нужно отдельно прикрепить к релизу.

Для своего домена открой `index.html` текстовым редактором, найди `const REPOSITORY = '';` и впиши `const REPOSITORY = 'ТВОЙ-ЛОГИН/five-nights-with-tyoma';`. На обычном `github.io` это не нужно.

## Локальный просмотр

Открой `website/index.html` двойным щелчком. Кнопки используют APK/EXE из соседней папки `outputs`. Не перемещай отдельно HTML, если хочешь скачивать локальные файлы. Для публикации через GitHub переносится только HTML, а кнопки автоматически переключаются на Releases.

## Официальные инструкции GitHub

- [Публикация Pages из ветки](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Создание и редактирование релиза](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
- [Ограничения файлов релиза](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
- [Большие файлы в репозитории](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)
