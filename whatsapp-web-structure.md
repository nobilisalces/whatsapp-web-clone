# Структура сайта web.WhatsApp.com

## Общая архитектура

```
<html#whatsapp-web>
├── <head>
│   ├── 51 внешний скрипт (base64-encoded JS бандлы)
│   ├── 5 inline скриптов
│   ├── 5 блоков <style> (CSS-переменные темы light/dark)
│   ├── 3 CSS-файла (link)
│   └── Meta: viewport, manifest, OG-теги, theme-color
│
└── <body.color-refresh>
    └── div#mount_0_0_lw
        └── div#app
            └── div._aiwn.app-wrapper-web
```

## Дерево интерфейса (`#app`)

```
#app → .app-wrapper-web
├── #wa-popovers-bucket          — контейнер всплывающих окон
├── #expressions-panel-container — панель эмодзи/стикеров
│
├── div._aigs (MAIN LAYOUT — двухколоночный)
│   │
│   ├── ЛЕВАЯ ПАНЕЛЬ
│   │   ├── header [data-tab=2] — ШАПКА
│   │   │   ├── Кнопка "New chat"
│   │   │   └── Кнопка "Menu"
│   │   │
│   │   ├── div#side — БОКОВАЯ ПАНЕЛЬ
│   │   │   ├── [role=tablist] — ФИЛЬТРЫ ЧАТОВ
│   │   │   │   ├── Tab "All" (data-tab=3)
│   │   │   │   ├── Tab "Unread"
│   │   │   │   └── Tab "Favorites"
│   │   │   │
│   │   │   ├── div [data-tab=3] — ПОИСК
│   │   │   │   └── [role=textbox] "Search input textbox"
│   │   │   │
│   │   │   └── div#pane-side
│   │   │       └── div [data-tab=4, role=grid] — СПИСОК ЧАТОВ
│   │   │           └── [role=row] → [role=gridcell] (каждый чат)
│   │   │
│   │   └── БОКОВАЯ НАВИГАЦИЯ (кнопки)
│   │       ├── "Chats"
│   │       ├── "Status"
│   │       ├── "Communities"
│   │       ├── "Media"
│   │       ├── "Settings"
│   │       └── "Profile"
│   │
│   ├── ПРАВАЯ ПАНЕЛЬ (section)
│   │   ├── Кнопка "Get from App Store" [data-tab=8]
│   │   ├── Кнопка "Send document" [data-tab=8]
│   │   └── Кнопка "Add contact" [data-tab=8]
│   │
│   └── div._aig- — дополнительная область
│
└── #wds-toast-container — уведомления (тосты)
```

## Кнопки интерфейса

| Кнопка | Расположение |
|--------|-------------|
| Chats | Боковая навигация |
| Status | Боковая навигация |
| Communities | Боковая навигация |
| Media | Боковая навигация |
| Settings | Боковая навигация |
| Profile | Боковая навигация |
| New chat | Header [data-tab=2] |
| Menu | Header [data-tab=2] |
| All | Фильтры [data-tab=3] |
| Unread | Фильтры |
| Favorites | Фильтры |
| Get from App Store | Правая панель [data-tab=8] |
| Send document | Правая панель [data-tab=8] |
| Add contact | Правая панель [data-tab=8] |

## Поля ввода

| Элемент | Описание |
|---------|----------|
| `[role=textbox]` | "Search input textbox" [data-tab=3] |
| `<input>` | Скрытый input |

## Секции data-tab

| data-tab | Назначение |
|----------|-----------|
| 2 | HEADER — шапка левой панели (профиль, "New chat", "Menu") |
| 3 | SEARCH — поле поиска чатов + фильтры |
| 4 | CHAT LIST — список чатов (role=grid) |
| 8 | SIDE BUTTONS — дополнительные кнопки навигации |

## Статистика DOM

| Элемент | Кол-во |
|---------|--------|
| Всего | 583 |
| `<div>` | 172 |
| `<span>` | 88 |
| `<button>` | 16 |
| `<script>` | 106 |
| `<input>` | 1 |
| `<a>` | 1 |

## Дерево интерфейса (с открытым чатом)

```
#app → .app-wrapper-web
├── #wa-popovers-bucket
├── #expressions-panel-container
│
├── div._aigs (MAIN LAYOUT — двухколоночный)
│   │
│   ├── LEFT NAV ICON BAR (64px шириной)
│   │   ├── Chats / Status / Communities / Media / Settings / Profile
│   │
│   ├── ЛЕВАЯ ПАНЕЛЬ (._aigw, 437px)
│   │   ├── header [data-tab=2] — ШАПКА
│   │   ├── div#side (436px) — БОКОВАЯ ПАНЕЛЬ
│   │   │   ├── Фильтры: All | Unread | Favorites
│   │   │   ├── Поиск [data-tab=3]
│   │   │   └── #pane-side → Список чатов [data-tab=4, role=grid]
│   │
│   ├── ПРАВАЯ ПАНЕЛЬ — ОТКРЫТЫЙ ЧАТ (954px)
│   │   ├── RIGHT HEADER (954x64px) — имя контакта + кнопки
│   │   ├── CHAT WALLPAPER AREA — область сообщений
│   │   │   ├── Date labels ("Today", "11/12/2025")
│   │   │   ├── Outgoing bubbles (зелёные)
│   │   │   └── Incoming bubbles (белые)
│   │   └── FOOTER (954x64px) — поле ввода сообщения
│   │       ├── Кнопка "+" (вложения)
│   │       ├── Кнопка emoji
│   │       ├── INPUT FIELD BOX (930x52px, border-radius: 26px)
│   │       └── Кнопка микрофона
│
└── #wds-toast-container
```

---

## Стили элементов

### Body / App

| Свойство | Значение |
|----------|---------|
| Background | `rgb(219, 216, 212)` / `#DBD8D4` |
| Color | `rgb(10, 10, 10)` / `#0A0A0A` |
| Font | `400 16px/16px "Segoe UI", "Helvetica Neue", Helvetica` |
| Viewport | 1456x1057px |

### Left Nav Icon Bar

| Свойство | Значение |
|----------|---------|
| Width | 64px |
| Background | `rgb(247, 245, 243)` / `#F7F5F3` |

### Left Panel Header [data-tab=2]

| Свойство | Значение |
|----------|---------|
| Background | `rgb(247, 245, 243)` / `#F7F5F3` |
| Color | `rgb(10, 10, 10)` |
| Font | `400 16px/16px` |

### Sidebar (#side)

| Свойство | Значение |
|----------|---------|
| Background | `rgb(255, 255, 255)` / `#FFFFFF` |
| Width | 436px |
| Height | 993px |

### Filter Tabs (All / Unread / Favorites)

| Свойство | Значение |
|----------|---------|
| Background (active) | `rgb(217, 253, 211)` / `#D9FDD3` |
| Color (active) | `rgb(21, 96, 62)` / `#15603E` |
| Font | `400 13.3px/normal` |
| Padding | `0 12px` |
| Border-radius | `9999px` (pill) |
| Size | 44x32px |

### Search Input

| Свойство | Значение |
|----------|---------|
| Background | transparent |
| Color | `rgb(10, 10, 10)` |
| Font | `400 15px/20px` |

### Chat List Item

| Свойство | Значение |
|----------|---------|
| Font (name) | `400 17px/21px` |
| Font (preview) | `400 14px/20px` |
| Font (time) | `400 12px/16px` |
| Color (preview) | `rgba(0, 0, 0, 0.6)` |
| Color (time) | `rgba(0, 0, 0, 0.6)` |

### Right Header (открытый чат)

| Свойство | Значение |
|----------|---------|
| Background | `rgb(255, 255, 255)` / `#FFFFFF` |
| Size | 954x64px |
| Padding | `10px 16px` |

### Contact Name (в хедере чата)

| Свойство | Значение |
|----------|---------|
| Color | `rgb(10, 10, 10)` |
| Font | `400 16px/21px` |

### Subtitle ("Message yourself")

| Свойство | Значение |
|----------|---------|
| Color | `rgba(0, 0, 0, 0.6)` |
| Font | `400 13px/20px` |

### Chat Wallpaper Area

| Свойство | Значение |
|----------|---------|
| Background | `rgb(239, 233, 224)` / `#EFE9E0` |
| Foreground pattern | `#E5DBCD` |

### Outgoing Message Bubble (исходящее)

| Свойство | Значение |
|----------|---------|
| Background | `rgb(217, 253, 211)` / `#D9FDD3` |
| Color | `rgb(10, 10, 10)` |
| Font (bubble) | `400 14.2px/19px` |
| Font (text) | `400 14px/20px` |
| Border-radius | `7.5px 0px 7.5px 7.5px` |

### Incoming Message Bubble (входящее)

| Свойство | Значение |
|----------|---------|
| Background | `rgb(255, 255, 255)` / `#FFFFFF` |
| Border-radius | `0px 7.5px 7.5px 7.5px` |

### Date Label ("Today")

| Свойство | Значение |
|----------|---------|
| Color | `rgba(0, 0, 0, 0.6)` |
| Font | `545 12px/16px` |

### Timestamp

| Свойство | Значение |
|----------|---------|
| Color | `rgba(0, 0, 0, 0.6)` |
| Font | `400 12px/16px` |

### Footer (Input Area)

| Свойство | Значение |
|----------|---------|
| Size | 954x64px |
| Background | transparent |

### Message Input Box

| Свойство | Значение |
|----------|---------|
| Background | `rgb(255, 255, 255)` / `#FFFFFF` |
| Font | `400 15px/20px` |
| Padding | `5px` |
| Border-radius | `26px` (pill) |
| Size | 930x52px |
| Placeholder | "Type a message" |

---

## WDS Design System Tokens (CSS Variables)

### Акцентные цвета

| Токен | Значение | Назначение |
|-------|---------|-----------|
| `--WDS-accent` | `#1DAA61` | Основной зелёный |
| `--WDS-accent-deemphasized` | `#D9FDD3` | Светло-зелёный (bubble, tab active) |
| `--WDS-accent-emphasized` | `#15603E` | Тёмно-зелёный (текст на accent) |

### Фоны

| Токен | Значение | Назначение |
|-------|---------|-----------|
| `--WDS-app-wash` | `#DBD8D4` | Фон приложения |
| `--WDS-background-wash-plain` | `#FFFFFF` | Основной фон панелей |
| `--WDS-background-wash-inset` | `#F7F5F3` | Фон вложенных областей |
| `--WDS-background-elevated-wash-plain` | `#FFFFFF` | Приподнятый фон |
| `--WDS-background-elevated-wash-inset` | `#F7F5F3` | Вложенный приподнятый |
| `--WDS-background-dimmer` | `rgba(0,0,0,.6)` | Затемнение (overlay) |

### Поверхности

| Токен | Значение | Назначение |
|-------|---------|-----------|
| `--WDS-surface-default` | `#FFFFFF` | По умолчанию |
| `--WDS-surface-emphasized` | `#F7F5F3` | Выделенная |
| `--WDS-surface-highlight` | `rgba(194,189,184,.15)` | Подсветка (hover) |
| `--WDS-surface-pressed` | `rgba(17,27,33,.2)` | Нажатие |
| `--WDS-surface-inverse` | `#20272B` | Инвертированная |
| `--WDS-components-surface-nav-bar` | `#FFFFFF` | Навигационная панель |

### Текст / контент

| Токен | Значение | Назначение |
|-------|---------|-----------|
| `--WDS-content-default` | `#0A1014` | Основной текст |
| `--WDS-content-deemphasized` | `#5B6368` | Вторичный текст |
| `--WDS-content-disabled` | `#B3B9BD` | Неактивный |
| `--WDS-content-inverse` | `#FFFFFF` | Инвертированный |
| `--WDS-content-on-accent` | `#FFFFFF` | На акценте |
| `--WDS-content-action-default` | `#0A1014` | Действие |
| `--WDS-content-action-emphasized` | `#1B8755` | Акцентное действие |
| `--WDS-content-external-link` | `#0063CB` | Внешние ссылки |
| `--WDS-content-read` | `#007BFC` | Прочитано (синие галочки) |

### Разделители

| Токен | Значение |
|-------|---------|
| `--WDS-lines-divider` | `rgba(17,27,33,.1)` |

### Чат (системные)

| Токен | Значение | Назначение |
|-------|---------|-----------|
| `--WDS-systems-chat-background-wallpaper` | `#EFE9E0` | Фон области чата |
| `--WDS-systems-chat-foreground-wallpaper` | `#E5DBCD` | Паттерн обоев |
| `--WDS-systems-chat-surface-composer` | `#FFFFFF` | Фон поля ввода |
| `--WDS-systems-chat-surface-tray` | `#F7F5F3` | Панель вложений |

### Пузыри сообщений

| Токен | Значение | Назначение |
|-------|---------|-----------|
| `--WDS-systems-bubble-surface-outgoing` | `#D9FDD3` | Исходящее (зелёный) |
| `--WDS-systems-bubble-surface-incoming` | `#FFFFFF` | Входящее (белый) |
| `--WDS-systems-bubble-surface-system` | `rgba(255,255,255,.9)` | Системное |
| `--WDS-systems-bubble-surface-business` | `#D5FDED` | Бизнес |
| `--WDS-systems-bubble-surface-e2e` | `#FFF0D4` | E2E уведомление |
| `--WDS-systems-bubble-surface-overlay` | `rgba(194,189,184,.15)` | Оверлей |
| `--WDS-systems-bubble-content-deemphasized` | `rgba(17,27,33,.5)` | Вторичный текст в bubble |
| `--WDS-systems-bubble-content-e2e` | `#5B6368` | E2E текст |
| `--WDS-systems-status-seen` | `#C2BDB8` | Статус "просмотрено" |

### Шрифт

```
font-family: "SF Pro Text", "SF Pro Icons", system, -apple-system, "Segoe UI", "Helvetica Neue", Helvetica, "Lucida Grande", Arial, sans-serif
```

---

## Ключевые особенности

- **React SPA** — всё рендерится в `#app`, используется React-подобный mount (`#mount_0_0_lw`)
- **CSS-классы обфусцированы** — большинство классов хешированы (`x78zum5`, `xdt5ytf`), значимые начинаются с `_ai` (`_aiwn`, `_aigs`, `_aigw`)
- **data-tab атрибуты** — основной способ идентификации секций (2=header, 3=search, 4=chat list, 8=side buttons)
- **WDS (WhatsApp Design System)** — полная система дизайн-токенов через CSS-переменные `--WDS-*`
- **Темы** — поддержка light/dark mode через CSS-переменные
