**English** | [Українська](README.uk.md)

# Harmoniq API

REST API for the Harmoniq platform: articles, authors, saved articles, and cookie-based sessions.

## Stack

- Node.js, Express 5
- MongoDB / Mongoose
- Celebrate / Joi validation
- Cloudinary (image uploads)
- bcrypt, httpOnly cookies (session auth)

## Getting started

```bash
cp .env.example .env
npm install
npm run dev
```

### Environment variables

| Variable | Description |
| --- | --- |
| `PORT` | Server port (default `3000` if unset) |
| `MONGO_URL` | MongoDB connection string |
| `NODE_ENV` | `development` or `production` |
| `CLIENT_URL` | Allowed frontend origin(s), comma-separated |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret |

## Endpoints

### Auth

| Method | Path | Auth |
| --- | --- | --- |
| `POST` | `/auth/register` | — |
| `POST` | `/auth/login` | — |
| `POST` | `/auth/refresh` | cookies |
| `POST` | `/auth/logout` | cookies |

### Users

| Method | Path | Auth |
| --- | --- | --- |
| `GET` | `/users` | — |
| `GET` | `/users/me` | yes |
| `GET` | `/users/top-creators` | — |
| `GET` | `/users/:id` | — |
| `PATCH` | `/users/me/avatar` | yes |
| `GET` | `/saved-articles` | yes |
| `POST` | `/saved-articles/:id` | yes |
| `DELETE` | `/saved-articles/:id` | yes |

### Articles

| Method | Path | Auth |
| --- | --- | --- |
| `GET` | `/articles` | — |
| `GET` | `/articles/:id` | — |
| `GET` | `/articles/author/:ownerId` | — |
| `POST` | `/articles` | yes |
| `PATCH` | `/articles/:id` | yes (owner) |
| `DELETE` | `/articles/:id` | yes (owner) |

Sessions use httpOnly cookies: `accessToken`, `refreshToken`, `sessionId`.

## Project structure

```
src/
  routes/        HTTP routes
  controllers/   Request handlers
  models/        Mongoose schemas
  validations/   Celebrate / Joi schemas
  middleware/    Auth, upload, errors, logger
  services/      Auth helpers, Cloudinary
  db/            MongoDB connection
```

## Scripts

| Script | Description |
| --- | --- |
| `npm run dev` | Start with nodemon |
| `npm start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run recalculate-articles` | Recalculate `articlesAmount` per user |
