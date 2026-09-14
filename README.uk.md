[English](README.md) | **Українська**

# Harmoniq API

REST API для платформи Harmoniq: статті, автори, збережені статті та сесії на cookies.

## Стек

- Node.js, Express 5
- MongoDB / Mongoose
- Celebrate / Joi валідація
- Cloudinary (завантаження зображень)
- bcrypt, httpOnly cookies (сесійна автентифікація)

## Запуск

```bash
cp .env.example .env
npm install
npm run dev
```

### Змінні середовища

| Змінна | Опис |
| --- | --- |
| `PORT` | Порт сервера (за замовчуванням `3000`, якщо не задано) |
| `MONGO_URL` | Рядок підключення до MongoDB |
| `NODE_ENV` | `development` або `production` |
| `CLIENT_URL` | Дозволені origin фронтенду (через кому) |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret |

## Ендпоінти

### Auth

| Метод | Шлях | Auth |
| --- | --- | --- |
| `POST` | `/auth/register` | — |
| `POST` | `/auth/login` | — |
| `POST` | `/auth/refresh` | cookies |
| `POST` | `/auth/logout` | cookies |

### Users

| Метод | Шлях | Auth |
| --- | --- | --- |
| `GET` | `/users` | — |
| `GET` | `/users/me` | так |
| `GET` | `/users/top-creators` | — |
| `GET` | `/users/:id` | — |
| `PATCH` | `/users/me/avatar` | так |
| `GET` | `/saved-articles` | так |
| `POST` | `/saved-articles/:id` | так |
| `DELETE` | `/saved-articles/:id` | так |

### Articles

| Метод | Шлях | Auth |
| --- | --- | --- |
| `GET` | `/articles` | — |
| `GET` | `/articles/:id` | — |
| `GET` | `/articles/author/:ownerId` | — |
| `POST` | `/articles` | так |
| `PATCH` | `/articles/:id` | так (власник) |
| `DELETE` | `/articles/:id` | так (власник) |

Сесії використовують httpOnly cookies: `accessToken`, `refreshToken`, `sessionId`.

## Структура проєкту

```
src/
  routes/        HTTP-маршрути
  controllers/   Обробники запитів
  models/        Mongoose-схеми
  validations/   Celebrate / Joi схеми
  middleware/    Auth, upload, помилки, logger
  services/      Auth-хелпери, Cloudinary
  db/            Підключення до MongoDB
```

## Скрипти

| Скрипт | Опис |
| --- | --- |
| `npm run dev` | Запуск з nodemon |
| `npm start` | Запуск production-сервера |
| `npm run lint` | Запуск ESLint |
| `npm run recalculate-articles` | Перерахунок `articlesAmount` для користувачів |
