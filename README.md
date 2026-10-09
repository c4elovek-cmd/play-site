# play.c4elovek.online — исходники

Страница сервера SaperCraft (`/`) и страница сборки модов (`/mods/`).

Сайт отдаётся Cloudflare Worker **sapercraft-play** (static assets), кастомный домен
`play.c4elovek.online` привязан к воркеру. На этом же домене висит SRV-запись
Minecraft-сервера (playit) — поэтому привязку домена к Pages не переносим.

## Как обновить сайт

Внести изменения в `index.html` и `mods/index.html`, затем задеплоить ассеты:

```
cd <эта папка>
$env:CLOUDFLARE_API_TOKEN = "токен с правом Account -> Workers Scripts -> Edit"
npx wrangler deploy -c wrangler-play.toml
```

Вариант без CLI: Cloudflare Dashboard → Workers & Pages → sapercraft-play →
Create new version → Upload assets.

## Структура
- `index.html` — главная страница play.c4elovek.online
- `mods/index.html` — страница модов (play.c4elovek.online/mods/)
- `wrangler-play.toml` + `deploy/play-site/` — конфиг и ассеты для деплоя
- `deploy/play-site/` — копия файлов, которая уходит в Worker (должна совпадать с `index.html` и `mods/`)

## Где лежат архивы модов

Архив собирается в **Releases этого же репозитория** (`c4elovek-cmd/play-site`),
тег `new`, файл `mods.zip`:

```
https://github.com/c4elovek-cmd/play-site/releases/download/new/mods.zip
```

Раньше ссылки вели на репозиторий `BiographyWebsite`, но он приватный, поэтому
игроки получали 404. Не возвращай ссылки на него.

## Требования к содержимому mods.zip

Набор модов в архиве должен **в точности совпадать с серверным**
(`SaperCraft\mods`). Иначе Forge покажет «Несовместимый модифицированный сервер FML».
Текущий серверный набор — 18 модов, Forge 47.4.18.
