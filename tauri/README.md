# Практикум — сборка под Windows (Tauri 2)

Локальная платформа курсов: библиотека, плеер уроков а-ля Stepik, обязательное ДЗ,
авто-зачёт уроков, импорт курсов из JSON и точка подключения AI-генерации.

Весь интерфейс — один файл `src/index.html`. Tauri оборачивает его в нативное
окно Windows и собирает установщик.

## 1. Что поставить (один раз)

1. **Microsoft C++ Build Tools** — https://visualstudio.microsoft.com/visual-cpp-build-tools/
   При установке отметьте workload «Разработка классических приложений на C++»
   (Desktop development with C++).
2. **Rust** — https://rustup.rs → скачайте `rustup-init.exe`, запустите, вариант по умолчанию (1).
   После установки перезапустите терминал.
3. **Node.js LTS** — https://nodejs.org
4. **WebView2** — на Windows 10/11 уже установлен. Если нет: https://developer.microsoft.com/microsoft-edge/webview2/

Проверка в новом терминале (PowerShell):
```
rustc --version
node --version
```

## 2. Запуск и сборка

В папке проекта:

```
npm install          # один раз — ставит Tauri CLI
npm run dev          # окно приложения в режиме разработки
npm run build        # сборка установщика
```

Первая сборка качает и компилирует Rust-зависимости — 5–15 минут.
Дальше — быстро.

Готовый установщик появится здесь:
```
src-tauri\target\release\bundle\nsis\Praktikum_1.0.0_x64-setup.exe
```
Рядом лежит и просто `praktikum.exe` (portable, без установки):
```
src-tauri\target\release\praktikum.exe
```

## 3. Где лежат данные

Прогресс и импортированные курсы хранятся в профиле WebView2 приложения:
`%APPDATA%\ru.praktikum.desktop\` — переустановка приложения их не трогает.

## 4. Подключение нейросети

Откройте `src/index.html`, найдите комментарий `// === AI HOOK ===` (в самом
низу, поиском по «AI HOOK»). Там функция `generateCourseWithAI()` и готовый
закомментированный пример запроса к Google Gemini с системным промптом под
формат курса. Раскомментируйте, подставьте название модели — кнопка
«Сгенерировать (AI)» заработает: валидация и импорт уже подключены.

После правки `index.html` просто пересоберите: `npm run build`.

## 5. Правка интерфейса

Всё в одном файле `src/index.html`: стили в <style>, логика в <script>.
Формат JSON курса описан внутри приложения — кнопка «Формат JSON».

## Структура

```
praktikum-tauri/
├─ src/index.html          ← всё приложение
├─ src-tauri/
│  ├─ tauri.conf.json      ← имя, размер окна, установщик
│  ├─ Cargo.toml           ← Rust-зависимости
│  ├─ src/                 ← минимальная нативная обвязка
│  ├─ icons/               ← иконки приложения
│  └─ capabilities/        ← разрешения окна
└─ package.json
```
