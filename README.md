<div align="center">

# ✦ Praktikum · Практикум

**Локальная платформа учебных курсов с генерацией уроков через нейросеть.**
Уроки, задания и обязательное ДЗ — из одного JSON-файла. Работает офлайн.

<!-- Замените ссылки ниже на реальные после первого релиза -->
[Скачать для Windows](../../releases) · [Формат курса](#-формат-курса) · [English](#-english)

![Интерфейс библиотеки](docs/screenshot-library.png)

</div>

---

## ✦ Что это

Praktikum — это программа для обучения в стиле Stepik, которая работает целиком
на вашем компьютере. Курсы можно **сгенерировать нейросетью** (по вашему
API-ключу), **написать вручную** в простом JSON или **импортировать** готовые.
Прохождение уроков отмечается автоматически и подсвечивается созвездием шагов.

## ✦ Скриншоты

![Урок с созвездием шагов](docs/screenshot-lesson.png)
![Генерация курса нейросетью](docs/screenshot-generate.png)


## ✦ Возможности

- **Плеер уроков** в стиле Stepik: модули, уроки, пошаговые задания.
- **Три типа шагов:** теория (Markdown с кодом), тест (одиночный/множественный выбор), ответ текстом (точное совпадение / число / вхождение).
- **Обязательное ДЗ** в конце каждого урока — без него урок не засчитывается.
- **Авто-зачёт** урока при прохождении всех шагов + возможность снять отметку вручную.
- **Генерация курсов ИИ** через любой OpenAI-совместимый API: DeepSeek, OpenAI, Gemini, OpenRouter, локальная Ollama. Курс собирается по частям с проверкой формата.
- **Язык интерфейса и курсов:** русский, English, 简体中文.
- **Импорт / экспорт** курсов в JSON, строгая валидация структуры.
- **Локально и приватно:** данные и API-ключ хранятся только на вашем устройстве.

## ✦ Быстрый старт

### Вариант 1 — просто открыть (без установки)
Скачайте `index.html` и откройте его в браузере. Всё работает сразу.
> Для надёжного сохранения прогресса запускайте через локальный сервер:
> `python -m http.server`, затем откройте `http://localhost:8000`.

### Вариант 2 — приложение для Windows
Скачайте портативную сборку из [Releases](../../releases), распакуйте и запустите
`Praktikum.exe`. Установка не требуется.

### Вариант 3 — собрать нативное приложение (Tauri, ~10 МБ)
См. папку [`tauri/`](tauri) и инструкцию в её README.

## ✦ Подключение нейросети

1. Откройте **«✦ Сгенерировать (AI)»**.
2. Выберите провайдера (по умолчанию — DeepSeek) или впишите свой Base URL и модель.
3. Вставьте API-ключ, укажите тему, уровень, объём и язык курса.
4. Нажмите **«Сгенерировать»** — курс появится в библиотеке.

Ключ хранится только локально и отправляется напрямую провайдеру. Пресеты
редактируемы: если имя модели изменится, впишите актуальное вручную.

## ✦ Формат курса

Курс — это один JSON-объект. Минимальный пример:

```json
{
  "title": "Название курса",
  "description": "Короткое описание",
  "modules": [{
    "title": "Модуль 1",
    "lessons": [{
      "title": "Урок 1",
      "steps": [
        { "type": "text", "content": "### Заголовок\nТекст в **Markdown**." },
        { "type": "quiz", "question": "2 + 2 = ?", "options": ["3","4","5"], "correct": [1], "explanation": "Почему так" },
        { "type": "input", "question": "Столица Франции?", "answer": "Париж", "match": "exact" }
      ],
      "homework": [
        { "type": "quiz", "question": "Обязательное ДЗ", "options": ["да","нет"], "correct": [0] }
      ]
    }]
  }]
}
```

| Поле | Описание |
|---|---|
| `type: "text"` | Теория; `content` — Markdown (заголовки, списки, `код`, блоки ` ``` `) |
| `type: "quiz"` | `options` — варианты, `correct` — индексы верных (с нуля), несколько = мультивыбор; `explanation` — пояснение |
| `type: "input"` | `answer` (или `answers[]`), `match`: `exact` / `contains` / `number` (+ `tolerance`) |
| `homework` | Массив шагов quiz/input; обязателен для авто-зачёта урока |

Кнопка **«Формат JSON»** внутри приложения показывает эту же справку.
Готовые курсы можно складывать в папку [`courses/`](courses).

## ✦ Технологии

Чистый HTML/CSS/JS в одном файле, без сборки и зависимостей в рантайме.
Десктоп-версии — обёртки Tauri (Rust) или Electron. Хранение — localStorage.

## ✦ Как помочь проекту

Идеи, баги и правки приветствуются — см. [CONTRIBUTING.md](CONTRIBUTING.md).
Особенно рады улучшениям перевода на 简体中文 и новым курсам в `courses/`.

## ✦ Лицензия

[MIT](LICENSE) — используйте свободно.

---

<a name="-english"></a>

## ✦ English

**Praktikum** is a local, offline learning platform in the spirit of Stepik.
Generate courses with AI (your own API key), write them by hand in simple JSON,
or import ready-made ones. Lesson progress is tracked automatically and lights
up as a constellation.

**Features:** Stepik-style lesson player · three step types (theory / quiz /
text answer) · mandatory homework per lesson · auto-completion · AI generation
via any OpenAI-compatible API (DeepSeek, OpenAI, Gemini, OpenRouter, Ollama) ·
UI & course languages: Russian, English, Simplified Chinese · JSON import/export
with validation · fully local and private.

**Quick start:** download `index.html` and open it in a browser, or grab the
portable Windows build from [Releases](../../releases). To connect AI, open
"Generate (AI)", pick a provider, paste your API key, and describe the course.

Licensed under [MIT](LICENSE).
