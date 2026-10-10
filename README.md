# edohod.ru — сайт личных автомобилей из Магнитогорска

## Состав
- `index.html` — главная: 4 карточки (2 активные + 2 заглушки «Скоро»)
- `cars/toyota-camry-1991.html` — страница Camry с 23 фото, JSON-LD (Car, без VIN), FAQ, блок про разбивку цены, чат-форма вопросов
- `cars/renault-scenic-2001.html` — страница Scenic (фото пока нет — используется силуэт-заглушка; замените на реальные фото, положив их в `img/scenic/`)
- `contacts.html`, `soon.html`
- `llms.txt`, `llms-full.txt` — для ИИ-поисковиков (ChatGPT, Gemini, Perplexity, Яндекс Нейро)
- `img/` — фотографии
- `style.css`, встроенный JS (админка, водяной знак, заглушка «Продано», антиспам-формы через localStorage)

## Админка (демо, front-end только)
- Скрытая кнопка в футере (точка справа) → пароль: `edohod2026`
- Меняет статус: В продаже / Забронировано (водяной знак с датой) / Продано (заглушка)
- **Важно:** состояние хранится в localStorage конкретного браузера — это демонстрация логики. Для реальной работы нужен бэкенд (см. ниже).

## Деплой статики + DNS edohod.ru
1. Залейте папку на любой статический хостинг: GitHub Pages, Netlify, Vercel, Cloudflare Pages, reg.ru.
2. В панели регистратора домена edohod.ru создайте записи:
   - Тип A: `@` → IP хостинга (или CNAME `@` → адрес хостинга, если поддерживает)
   - CNAME: `www` → `edohod.ru`
3. На хостинге подключите домен edohod.ru и включите HTTPS (Let's Encrypt).
4. ЧПУ вида `/cars/toyota-camry-1991`: на Netlify/Vercel используйте редиректы
   (`/cars/:slug` → `/cars/:slug.html`), на Apache — .htaccess с `RewriteRule ^cars/([a-z0-9-]+)$ cars/$1.html`.

## Что нужно для продакшена (бэкенд)
Статический сайт не умеет: хранить вопросы в БД, слать email, настоящий антиспам по IP, загружать фото, общий для всех посетителей статус «Продано». Минимальный вариант:
- Netlify/Vercel Functions или простой VPS + Node/Express + SQLite/Postgres
- Таблицы: `cars (slug, status, reserve_until, price, description)`, `questions (car_slug, text, ip, created_at)`, `answers (question_id, text)`
- Антиспам: при вставке вопроса проверять `SELECT count(*) FROM questions WHERE ip=? AND created_at > now()-interval '1 hour'`
- Email: SMTP через nodemailer / Resend / SendGrid → впишите ваш email в конфиг
- Загрузка фото: multer/S3 → папка `img/<slug>/`
Фронт из этого архива подключается к API без изменения дизайна.
