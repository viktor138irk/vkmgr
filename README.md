# vkmgr — StackWorks VK Hub

Универсальное VK Mini App для групп ВКонтакте: заявки, услуги, клиенты, статусы, Telegram-уведомления и базовая админка.

## Назначение

`vkmgr` — SaaS/Mini App для владельцев групп VK. Первая версия закрывает самую частую боль групп: заявки теряются в личке, комментариях и сообщениях. Приложение даёт группе единый мини-кабинет: услуги, форма заявки, статусы, админка и уведомления.

## Что внутри

- `frontend/` — VK Mini App на React + VKUI + VK Bridge.
- `backend/` — Node.js API на Express + SQLite.
- `docs/` — roadmap, API, схема базы.
- `infra/` — docker-compose и nginx-заготовка.
- `install.sh` — базовый установщик на VPS.

## MVP v0.1.0

- Инициализация пользователя через VK launch params.
- Подключение группы.
- Каталог услуг.
- Создание заявки клиентом.
- Админский список заявок.
- Смена статусов заявки.
- Telegram-уведомление о новой заявке.
- Базовые роли: owner, manager, client.

## Быстрый запуск backend

```bash
cd backend
cp .env.example .env
npm install
npm run dev
```

API будет доступен на `http://localhost:8080`.

## Быстрый запуск frontend

```bash
cd frontend
cp .env.example .env
npm install
npm run dev
```

Frontend будет доступен на `http://localhost:5173`.

## Установка из репозитория на VPS

```bash
git clone https://github.com/viktor138irk/vkmgr.git
cd vkmgr
sudo bash install.sh
```

Можно задать домены перед запуском:

```bash
sudo FRONTEND_DOMAIN=vk.example.com API_DOMAIN=api-vk.example.com bash install.sh
```

После установки HTTPS:

```bash
certbot --nginx -d vk.example.com -d api-vk.example.com
```

## Для VK Mini Apps

1. Создать приложение в кабинете VK-разработчика.
2. Указать URL frontend в настройках mini app.
3. В `frontend/.env` указать `VITE_API_URL`.
4. В `backend/.env` указать `VK_APP_SECRET` для проверки подписи launch params.
5. Для продакшна поставить HTTPS.

## Важно

Это стартовый MVP-скелет, не финальный SaaS. Перед боевым запуском нужно добавить полноценную проверку прав администратора группы через VK API, оплату тарифов, rate-limit, аудит действий и нормальную PostgreSQL/MySQL базу.
