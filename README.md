# play.c4elovek.online — исходники

Страница сервера SaperCraft (`/`) и страница сборки модов (`/mods/`).

Сайт отдаётся Cloudflare Worker **sapercraft-play** (static assets), кастомный домен
`play.c4elovek.online` привязан к воркеру. На этом же домене висит SRV-запись
Minecraft-сервера (playit) — поэтому привязку домена к Pages не переносим.

## Как обновить сайт

Вариант 1 (локально, инструменты уже установлены):
```
cd deploy\play-site
npx wrangler deploy -c ..\wrangler-play.toml
```

Вариант 2: Cloudflare Dashboard → Workers & Pages → sapercraft-play → Create new version → Upload assets.

## Структура
- `index.html` — главная страница play.c4elovek.online
- `mods/index.html` — страница модов (play.c4elovek.online/mods/)
- Архивы модов лежат в Releases репозитория BiographyWebsite (кнопки на странице модов ссылаются туда)
