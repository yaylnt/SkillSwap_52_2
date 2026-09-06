# SkillSwap — платформа обмена навыками

[Demo]()

### Стек
<p align="center">
  <img src="https://skillicons.dev/icons?i=ts,react,redux,html,css,vite" alt="Skills" />
</p>

SkillSwap — одностраничное (SPA) приложение, в котором пользователи публикуют навыки двух типов: 
- “Учу” — навыки, которыми пользователь готов делиться;
- “Учусь” — навыки, которым пользователь хочет научиться.
Сервис позволяет находить взаимно подходящие пары, отправлять заявки на обмен и вести список текущих/завершённых сессий. Проект реализован с моковыми данными, без подключения к серверу.

---

## Быстрый старт

```bash
npm install
npm run dev
```

---

## Структура проекта

```
src/
├── api/                  # fetch-функции для загрузки JSON-моков
├── app/
│   ├── providers/        # StoreProvider, RouterProvider
│   └── styles/           # global.css с CSS-переменными
├── entities/             # Доменные модели: Skill, User, Request
│   ├── skill/
│   ├── user/
│   └── request/
├── features/             # Фичи: auth, skills, favorites, requests
├── pages/                # Страницы приложения
├── shared/
│   ├── hooks/            # useDebounce, useLocalStorage
│   ├── lib/              # constants, helpers
│   ├── types/            # общие TypeScript-типы
│   └── ui/               # атомарные компоненты
├── store/                # Redux store и типизированные хуки
└── widgets/              # Составные блоки: Header, SkillCard, FiltersBar

public/
└── db/
    ├── skills.json       # Добавь сюда моки навыков
    └── users.json        # Добавь сюда моки пользователей
```

---

## Моки данных

Файлы `public/db/skills.json` и `public/db/users.json` содержат моковые данные навыков и пользователей.

Структура объектов описана в `src/shared/types/index.ts`.

---

## Доступные скрипты

| Скрипт | Что делает |
|--------|------------|
| `npm run dev` | Запуск dev-сервера |
| `npm run build` | Сборка для продакшена |
| `npm run preview` | Запуск просмотра production-сборки |
| `npm run lint` | Проверка ESLint + Stylelint |
| `npm run lint:fix` | Автоисправление lint-ошибок |
| `npm run format` | Форматирование через Prettier |
| `npm run test` | Запуск тестов |
| `npm run test:watch` | Тесты в watch-режиме |
| `npm run test:coverage` | Покрытие (цель ≥ 70%) |

---

## Роутинг

Маршруты объявлены в `src/shared/lib/constants.ts` → `ROUTES`.

Lazy-загрузка настроена в `src/app/providers/RouterProvider.tsx`.

---

## План доработок

Командой реализован MVP проекта. Ниже план дальнейших доработок.

**Спринт 1**, зелёный CI.
- Починить тест и двойную запись в createSwapRequest
- Добавить @vitest/coverage-v8, включить покрытие в CI
- Прогнать npm run format, поправить отступы, переименовать usercard-elemetn.tsx
- Заменить Math.random() на useId() в Input
- Починить --modal-overlay-color, xmlns и три несуществующие переменные
**Спринт 2**, один источник правды.
- getAuthUser() из рендера UserCard и SkillCard, перевести на селекторы
- Свести загрузку users и skills к одной точке, убрать fetchUserById из SkillCard и динамический импорт из FavoritesPage
- Ключ likedSkills и имена событий забрать в constants и в экспорты requestStorage
- Починить связку профиля и авторизации
**Спринт 3**, границы слоёв.
- Перенести составные компоненты из shared в widgets, расформировать src/components/
- *Utils перенести в shared/lib/storage/
- Включить eslint-plugin-boundaries
- Вынести преобразование wantsToLearn в одну общую функцию

