Создай одностраничный сайт-визитку по этому шаблону. Соблюдай указанные размеры, отступы, шрифты и расположение блоков. Сайт создаётся с филлерным (заглушечным) контентом: без реальных данных, без ссылок, с картинками-заглушками.

## 0. Цвет (прочитай первым)

Приоритетный цвет сайта задаётся пользователем. Если пользователь не указал цвет — используй жёлтый (#f2c200). Все акцентные элементы (текст-акцент, градиенты, свечения, активные состояния) строятся от этого цвета; вторичный акцент — контрастный светлый/циан. Остальное — тёмная тема.
Остановись и спроси нужный приоритетный цвет, если пользователь его не указал.

## 1. Файлы проекта

- `index.html`, `style.css`, `script.js`. Чистый HTML/CSS/JS, без фреймворков и сборки.
- Только сам сайт: без README, robots.txt, sitemap.xml, git.

## 2. Шрифты и базовая тема

- Inter (400, 500, 600, 800) — основной текст; JetBrains Mono (400, 600) — акценты, теги, код, логотип. Подключать через Google Fonts (`preconnect` + `display=swap`).
- `body`: `font-family: "Inter", system-ui, sans-serif`, `line-height: 1.6`, `overflow-x: hidden`.
- Цветовая система через CSS-переменные в `:root`:
  - `--bg` — тёмный (#070b14), `--bg-2` — тёмный второй (#0c1322)
  - `--glass` — rgba(255,255,255,0.04), `--glass-border` — rgba(255,255,255,0.08)
  - `--text` — светлый (#e6edf7), `--muted` — приглушённый (#8b97ad)
  - `--accent` — выбранный цвет, `--accent-2` — вторичный
  - `--radius: 18px`
- Фон body: базовый тёмный цвет + два радиальных градиента, один вверху-справа (`1200px 800px at 80% -10%`), второй слева в середине (`900px 600px at -10% 40%`), с прозрачностью к 55–60%.
- Глобально: `* { margin:0; padding:0; box-sizing:border-box }`, `html { scroll-behavior: smooth }`.
- Контейнер `.container`: `width: min(1120px, 92%)`, `margin: 0 auto` — вся сетка внутри него.

## 3. Порядок элементов в DOM (сверху вниз)

1. `<div class="spotlight">` — прожектор (фиксированный, за контентом).
2. `<canvas id="particles">` — частицы (фиксированный, самый нижний слой).
3. `<header class="topbar">` с навигацией.
4. `<main>`: секции #hero, #about, #skills, #projects, #plans, #contact.
5. `<footer>`.
6. Модальное окно проекта (`#projectModal`).
7. `<script>`.

## 4. Фоновые слои

- `#particles`: `position: fixed; inset: 0; z-index: -2; opacity: 0.55`. 45 частиц: символы кода/значки, размер 10–18px, opacity 0.08–0.30, скорость 0.25–0.85px/кадр вверх, небольшой горизонтальный дрейф. Шрифт JetBrains Mono, цвет — акцент с прозрачностью. Реагирует на ресайз окна.
- `.spotlight`: `position: fixed; width/height: 420px; border-radius: 50%; z-index: -1; transform: translate(-50%,-50%); pointer-events: none`. Радиальный градиент акцента от 0.16 к прозрачному на 70%. Следует за мышью с инерцией (lerp ≈ 0.12).

## 5. Шапка (`.topbar` / `.nav`)

- Sticky сверху (`top: 0; z-index: 100`), `backdrop-filter: blur(14px)`, фон тёмный с alpha 0.65, нижняя граница `1px` glass-border.
- Внутри `.container`, flex: `align-items: center; justify-content: space-between`, паддинг `0.9rem 0`.
- Логотип слева: JetBrains Mono, 600, 1.25rem, формат `{X}` где фигурные скобки — акцентного цвета.
- Меню справа (`.nav-links`): flex, `gap: 1.6rem`, `list-style: none`. Пункты: Обо мне, Навыки, Проекты, Планы, Контакты. Ссылки — muted, 0.92rem, hover → основной текст. Последний пункт (`.nav-cta`) — пилюля с рамкой `1px glass-border`, `padding: 0.4rem 1rem`, `border-radius: 999px`, hover — рамка акцент.
- На мобиле (≤900px): `gap: 1rem`, первые два пункта скрыты.

## 6. HERO (`#hero`)

- Grid `1.2fr 0.8fr`, `gap: 3rem`, `align-items: center`, `padding: 5.5rem 0 4rem`.
- **Левая колонка** (текст):
  - Eyebrow: вторичный акцент, JetBrains Mono, 0.9rem, `letter-spacing: 0.08em`, uppercase.
  - H1 (имя-заглушка): `clamp(2.4rem, 5.5vw, 3.8rem)`, weight 800, `line-height: 1.1`, градиентный текст (белый → акцент → вторичный) через `background-clip: text`.
  - H2 (подзаголовок `Я <печатающийся текст>`): `clamp(1.2rem, 2.6vw, 1.7rem)`, weight 600, muted; печатающаяся часть акцентная + мигающий курсор (animation blink 1s).
  - Лид-абзац: `margin-top: 1rem`, muted, `max-width: 52ch`.
  - Кнопки (`.hero-actions`): flex, `gap: 1rem`, `margin-top: 1.8rem`, flex-wrap. `.btn` — `padding: 0.75rem 1.6rem`, `border-radius: 999px`, weight 600, 0.95rem. Основная — градиент акцентов, белый текст, тень; ghost — рамка glass, текст основной. Hover — подъём на 3px.
  - Статистика (`.hero-stats`): flex, `gap: 2.4rem`, `margin-top: 2.6rem`. Три блока, каждый в колонку: сверху крупное число (1.6rem, вторичный акцент), снизу подпись (0.85rem, muted).
- **Правая колонка** (фото):
  - `.photo-frame`: `width: min(340px, 80%)`, `aspect-ratio: .9`, `border-radius: 30px`, рамка glass, фон — градиент акцента, `transform-style: preserve-3d`, 3D-tilt по мыши (макс 12°).
  - Внутри `<img>` — фото-заглушка (`object-fit: cover`), поверх `.photo-glow` (градиент акцента, `mix-blend-mode: overlay`).
  - Четыре плавающих бейджа (`.badge-float`): JetBrains Mono, 0.8rem, пилюли, тёмный фон alpha 0.85, рамка glass, анимация float 5s (подъём 14px). Позиции: badge-1 top 8% left -4%; badge-2 top 30% right -6%; badge-3 bottom 26% left -8%; badge-4 bottom 6% right -2%.
- На ≤900px: grid в один столбец, текст по центру, фото сверху (`order: -1`).

## 7. Секции (общий каркас)

- `.section`: `padding: 4.5rem 0`.
- `.section-title`: flex, `align-items: center`, `gap: 1rem`, 1.9rem, weight 800, `margin-bottom: 2.2rem`. Перед текстом — декоративная линия `.line`: 46×3px, `border-radius: 2px`, градиент акцентов.
- Все карточки имеют класс `.glass`: фон `--glass`, рамка `1px --glass-border`, `border-radius: var(--radius)`, `backdrop-filter: blur(10px)`, hover — рамка акцента.

## 8. ABOUT (`#about`)

- Grid `1fr 1fr`, `gap: 1.5rem`. Две карточки, паддинг `1.8rem`.
- Карточка 1: два подзаголовка h3 (1.1rem, вторичный акцент) с абзацами-заглушками (muted).
- Карточка 2: h3 + список `.about-list` (без маркеров, muted, пункты `0.35rem 0`), ниже — декоративное окно кода `.code-window`: тёмный фон (#050810), рамка glass, `border-radius: 12px`. Сверху `.code-titlebar` (три кружка — красный/жёлтый/зелёный), ниже `<pre><code>` — 3–5 строк псевдо-C# с подсветкой (ключевые слова, типы, строки) JetBrains Mono 0.82rem.
- На ≤900px: один столбец.

## 9. SKILLS (`#skills`)

- Grid `repeat(2, 1fr)`, `gap: 1.1rem`. Каждая карточка `.skill` — паддинг `1.1rem 1.4rem`.
  - Сверху `.skill-head`: flex `space-between`, 0.92rem weight 500 — название слева, процент `.skill-val` справа (JetBrains Mono, вторичный акцент).
  - Ниже `.bar` — высота 8px, `border-radius: 999px`, фон white 0.07; внутри `.bar i` — полоса, ширина 0 по умолчанию, градиент акцентов, `transition: width 1.4s cubic-bezier(0.22,1,0.36,1)`.
  - При появлении в вьюпорте: полоса достигает заданного `data-level`, а процент анимируется счётчиком до этого значения.
- Ниже — облако тегов `.tags`: flex-wrap, `gap: 0.6rem`, `margin-top: 2rem`. Каждый тег — пилюля JetBrains Mono 0.82rem, рамка glass, muted; hover — акцент.
- На ≤900px: один столбец.

## 10. PROJECTS (`#projects`)

- Две подгруппы. Перед каждой — `.category-title` (1.15rem weight 600, muted, `margin: 2.2rem 0 1.3rem`, левая граница 3px акцент, отступ слева 0.9rem).
- Сетка карточек `.projects-grid`: `repeat(2, 1fr)`, `gap: 1.5rem`.
- Карточка `.project`: паддинг `1.8rem`, flex-колонка, 3D-tilt по мыши (макс 7°, подъём 4px).
  - Сверху `.project-top`: flex `space-between` — иконка-эмодзи (2rem) слева, справа (опционально) блок `.project-links` со ссылкой-стрелкой ↗ (заменить на заглушку `#`).
  - h3 — 1.3rem.
  - Абзац-заглушка — muted 0.93rem.
  - Теги `.project-tags`: flex-wrap `gap: 0.5rem`; каждый тег JetBrains Mono 0.75rem, вторичный акцент на фоне акцента 0.08, `border-radius: 6px`.
  - Мета `.project-meta`: flex `space-between`, 0.8rem, muted, верхняя граница glass, `padding-top: 0.9rem`, прижата к низу (`margin-top: auto`).
  - У части карточек — кнопка «Подробнее» `.project-more` (пилюля, рамка glass, hover — акцент + подъём), `data-project="id"`.
- На ≤900px: один столбец.

## 11. PLANS (`#plans`)

- Вертикальный timeline: `.timeline` `padding-left: 2rem`, вертикальная линия слева (2px, градиент акцентов, opacity 0.5).
- Пункты `.timeline-item` — glass-карточки, паддинг `1.4rem 1.6rem`, `margin-bottom: 1.2rem`.
  - Слева точка `.dot` (16px, круг, акцент, свечение) — позиционирована на линии.
  - Внутри: h3 (1.08rem) + абзац-заглушка (muted 0.92rem).

## 12. CONTACT (`#contact`)

- Одна центральная `.contact-card` (glass), паддинг `2.6rem`, `text-align: center`.
- Вводный текст-заглушка (1.2rem, `margin-bottom: 1.6rem`).
- Ряд кнопок `.contact-links`: flex, `gap: 0.9rem`, по центру, flex-wrap. Все — заглушки: `mail@example.com`, `#` для соцсетей, нейтральный телефон. Стили те же `.btn` primary/ghost.

## 13. FOOTER

- По центру, muted, 0.85rem, `padding: 2.5rem 0`, верхняя граница glass, `margin-top: 3rem`.
- Текст: «Шаблон разработал Темир Баслиней». Никаких других имён.

## 14. Модальное окно проекта (`#projectModal`)

- Фиксированное, `inset: 0`, `z-index: 200`, flex-центрирование, паддинг `1.2rem`, скрыто (opacity 0, visibility hidden), открытие по классу `.open`.
- `.modal-overlay` — тёмный полупрозрачный фон (alpha 0.75) + blur 6px.
- `.modal-card` (glass): `width: min(880px, 100%)`, `max-height: 90vh`, `overflow-y: auto`, паддинг `1.6rem`, появление со сдвигом вверх и scale 0.98→1.
- Кнопка закрытия справа-сверху: круг 38px, ×, hover — красный фон и поворот 90°.
- Карусель `.carousel`: рамка `border-radius: 14px`, viewport скрывает overflow.
  - `.carousel-track` — flex, сдвиг через `translateX(-index*100%)`, `transition: transform 0.45s cubic-bezier(0.22,1,0.36,1)`.
  - Изображения: `flex: 0 0 100%`, ширина 100%, высота `min(52vh, 440px)`, `object-fit: contain` — картинки-заглушки.
  - Стрелки `.carousel-btn` (42px круг) слева/справа по центру; счётчик `.carousel-counter` вверху-слева (пилюля); точки `.carousel-dots` внизу по центру, активная — вторичный акцент scale 1.3.
  - Для одного изображения стрелки и точки скрыты.
- `.modal-info` (`margin-top: 1.3rem`): категория (0.74rem, uppercase, вторичный акцент), h3 (1.5rem), теги, блок описания `.modal-desc` (muted 0.95rem; абзацы-заглушки, список филлерных пунктов, строка стека выделена жирным).
- Управление: закрытие по overlay / Escape / крестику; стрелки ← → листают; свайп по горизонтали на тач (порог 40px).
- На ≤640px: паддинг карточки `1.1rem`, `max-height: 94vh`, высота картинок `34vh`, стрелки 36px.

## 15. Reveal-анимации

- `.reveal`: `opacity: 0; transform: translateY(28px); transition: opacity 0.7s, transform 0.7s`.
- `.reveal.visible`: `opacity: 1; transform: translateY(0)`.
- Наблюдатель с threshold 0.15; элементам задаётся ступенчатая задержка `(i % 6) * 70ms`; после появления задержку снимать (чтобы не мешать 3D-tilt).
- При `prefers-reduced-motion: reduce` — отключить анимации, `.reveal` сразу видим.

## 16. Адаптив и скроллбар

- ≤900px: hero в один столбец, about/skills/projects в один столбец, текст hero по центру.
- ≤640px: уменьшенные паддинги модалки и высота изображений.
- Скроллбар: `scrollbar-width: thin`; ползунок — градиент акцентов, трек — white 0.05.

## 17. Контент — только заглушки

- Имя — «Имя Фамилия», роль — нейтральная. Никаких реальных компаний, городов, вузов, соцсетей, телефонов.
- Все тексты — нейтральные заглушки. Навыки, проекты, планы — вымышленные.
- Изображения — нейтральные стоковые фото из интернета (прямые публичные URL, без людей), без локальных файлов.
- Ссылки: контакты и соцсети — `mail@example.com` / `#`; canonical, OG, Twitter, JSON-LD — только `https://example.com` и нейтральные значения. Якоря навигации (`#about` и т.п.) рабочие.

## 18. Проверка

- Открой `index.html` в браузере: проверь отрисовку, все анимации, карусель, модалку, адаптив.
- Поиском по файлам убедись, что нет реальных имён, доменов, телефонов и личных данных (кроме URL стоковых картинок).

## 19. Вывод

Сообщи, какие файлы созданы и как открыть сайт.
