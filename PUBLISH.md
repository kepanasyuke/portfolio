# Публикация сайта на GitHub Pages

Сайт — статика, сборка не нужна. Всё содержимое папки `site/` и есть сайт:

```
site/
  index.html                179 КБ
  PUBLISH.md                этот файл
  assets/portrait.jpg       78 КБ
  assets/media-manifest.json
  assets/media/<slug>/      скриншоты, GIF, видео — 83 файла, 27,2 МБ
```

Вес папки целиком — **27,2 МБ** (лимит GitHub на файл — 100 МБ, на один push — 2 ГБ,
так что медиа проходят с большим запасом). Самые крупные файлы:
`assets/media/mirro/demo.mp4` 9,3 МБ, `assets/media/fumiklea/banking.webm` 5,0 МБ,
`assets/media/eight-projects/hero.gif` 1,3 МБ.

`index.html` вырос до 179 КБ (184273 байт), потому что иконки технологий вшиты в файл как inline-SVG
спрайт: 54 иконки, внешних запросов за ними нет, сайт работает и офлайн.

## Вариант A. Отдельный репозиторий `portfolio` (рекомендую)

Адрес получится `https://kepanasyuke.github.io/portfolio/`.

```powershell
cd C:\Users\Admin\Documents\MultiTool\HomeChats\Chat-74\site

git init
git add index.html assets
git commit -m "Личный сайт-портфолио: программист, 19 проектов, 25 языков"
git branch -M main
git remote add origin https://github.com/kepanasyuke/portfolio.git
git push -u origin main
```

Затем в GitHub: **Settings → Pages → Build and deployment**:
- Source: `Deploy from a branch`
- Branch: `main`, папка `/ (root)`
- Save → через 1–2 минуты сайт откроется по адресу выше.

## Вариант B. Корневой адрес `kepanasyuke.github.io`

Если создать репозиторий с именем ровно `kepanasyuke.github.io`, сайт ляжет на `https://kepanasyuke.github.io/` без всякого пути. Шаги те же, только `git remote add origin https://github.com/kepanasyuke/kepanasyuke.github.io.git`.

## Вариант C. Репозиторий уже существует

Положить всё содержимое `site/` в папку `docs/` и в Pages выбрать Branch `main`, папка `/docs`.

## Что проверить после публикации

1. Открывается портрет в шапке (`assets/portrait.jpg` рядом с `index.html` — регистр букв важен).
2. Фильтры («Все 25», «Backend и приложения», «Данные», «Тестирование», «Обучение», «Разное») переключают карточки.
3. Все 25 карточек на месте, ссылки «Код» и «Сайт» ведут на `github.com/kepanasyuke`.
4. Картинки и гифки в карточках видны (15 блоков с медиа), два видео запускаются по клику и показывают постер, а не чёрный прямоугольник.
5. Страница на телефоне: меню и карточки не вылезают за экран по горизонтали.
6. Адрес сайта добавлен в профиль: **github.com/settings/profile → Website** — он подсветится в профиле.
7. Ссылка на сайт в резюме: в `cv-kristina-panasyuk.docx` / `.pdf` в блоке контактов.

## Обновление

Правки в `index.html` → `git add index.html` → `git commit -m "обновление"` → `git push`.
Pages пересобирается автоматически.

Новые медиа: положить файл в `assets/media/<slug>/`, дописать путь в `assets/media-manifest.json`
и в карточку `index.html`, затем `git add assets index.html`.
