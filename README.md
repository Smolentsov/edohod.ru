# edohod.ru — сайт личных автомобилей из Магнитогорска (GitHub Pages, статика)

## Состав
- `index.html` — главная: 6 карточек (2 заполненные + 4 «Скоро в продаже» с фото авто под чёрной накидкой)
- `cars/toyota-camry-1991.html` — 23 фото, характеристики, JSON-LD (Car, без VIN), FAQ, блок про разбивку цены
- `cars/renault-scenic-2001.html` — характеристики, JSON-LD с VIN (19 фото подключены)
- `contacts.html`, `soon.html`
- `llms.txt`, `llms-full.txt` — для ИИ-поисковиков
- `robots.txt` (разрешены GPTBot, ClaudeBot, PerplexityBot, YandexBot), `sitemap.xml` — для поисковых систем (ChatGPT, Gemini, Perplexity, Яндекс Нейро)
- `img/covered.jpg` — фото авто под накидкой для пустых карточек и страницы «Скоро»

## Что НЕТ намеренно (GitHub Pages не умеет серверную часть)
- Формы вопросов покупателей, email-уведомления, админ-панель, статусы «Забронировано/Продано» — всё это требует бэкенда.
  Витрина работает как есть; связь с продавцом — по телефону 8 963 0 966 966.

## Публикация на GitHub Pages
1. Создайте репозиторий `edohod.github.io` (или любой другой) и загрузите содержимое папки.
2. Settings → Pages → Source: `main` branch, `/ (root)`. Сайт будет на `https://<user>.github.io/<repo>/`.
3. DNS edohod.ru у регистратора:
   - A-запись `@` → `185.199.108.153` (и 109, 110, 111)
   - CNAME `www` → `<user>.github.io`
4. Settings → Pages → Custom domain: `edohod.ru`, включить Enforce HTTPS.
5. ЧПУ `/cars/toyota-camry-1991`: либо переименуйте файлы в `cars/toyota-camry-1991/index.html`, либо используйте `permalink`-структуру папок — GitHub Pages отдаст их по красивому адресу автоматически.

## Редактирование контента
Всё статическое: правьте HTML в любом редакторе. Цены и тексты — прямо в карточках и таблицах. JSON-LD — в `<head>` страниц автомобилей.
