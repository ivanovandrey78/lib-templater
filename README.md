
# C++ Library Template (`mylib`)

Шаблон небольшого C++‑проекта‑библиотеки:
```txt
- CMake (с установкой и поддержкой `find_package`)
- Тесты (GoogleTest + CTest)
- Примеры использования
- CI (GitHub Actions)
- Настройка форматирования (`.clang-format` под Google Style)
```

---

## 1. Как использовать этот репозиторий как шаблон

### 1.1. Шаг 1 — клонировать шаблон

```bash
git clone https://github.com/you/mylib-template.git myproject
cd myproject
```

---

### 1.2. Шаг 2 — удалить историю Git (сделать “чистый” проект)

#### macOS / Linux

```bash
rm -rf .git
```

#### Windows (PowerShell)

```powershell
Remove-Item -Recurse -Force .git
```

#### Windows (cmd.exe)

```bat
rmdir /S /Q .git
```

---

### 1.3. Шаг 3 — создать новый репозиторий и первый коммит

В той же директории (`myproject`):

```bash
git init
git add .
git commit -m "Initial commit"
```

---

### 1.4. Шаг 4 — переименовать `mylib` под свой проект

В шаблоне используется имя `mylib`. Обычно его заменяют на имя своей библиотеки, например `awesome`:

1. Папки:
   - `include/mylib/` → `include/awesome/`
2. Неймспейс в коде:
   - `namespace mylib { ... }` → `namespace awesome { ... }`
3. Вхождения в CMake:
   - `project(mylib ...)` → `project(awesome ...)`
   - таргет `mylib` → `awesome`
   - `mylibTargets.cmake`, `mylibConfig.cmake` → `awesomeTargets.cmake`, `awesomeConfig.cmake`
   - `mylib::mylib` → `awesome::awesome`
4. В других файлах:
   - `README.md`, `ci.yml`, примеры, тесты (`mylib_tests` и т.п.)

Удобнее всего сделать глобальный поиск/замену по строке `mylib` в редакторе (VS Code: `Ctrl+Shift+F` / `Cmd+Shift+F`).

---

## 2. Структура проекта

```text
├─ include/mylib/      # Публичные заголовки (public API)
├─ src/                # Реализация библиотеки
├─ tests/              # Юнит‑тесты (GoogleTest + CTest)
├─ examples/           # Примеры использования
├─ cmake/              # CMake-конфиги для find_package
├─ .github/workflows/  # CI (GitHub Actions)
└─ CMakeLists.txt      # Корневой CMakeLists
```

---

## 3. Сборка

Требования:

```txt
- CMake ≥ 3.20
- C++ компилятор с поддержкой C++20
- (желательно) Ninja
```

```bash
# Configuration
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=ON -DBUILD_EXAMPLES=ON

# Build
cmake --build build
```

---

## 4. Запуск тестов

```bash
cd build
ctest --output-on-failure
```

---

## 5. Примеры

После сборки:

```bash
./build/examples/mylib_example_basic
```

(Путь/имя бинарника могут отличаться на Windows: `build\examples\mylib_example_basic.exe`.)

---

## 6. Использование как внешней библиотеки

После установки:

```bash
cmake --install build --prefix /usr/local
```

В другом CMake‑проекте:

```cmake
find_package(mylib CONFIG REQUIRED)

add_executable(app main.cpp)
target_link_libraries(app PRIVATE mylib::mylib)
```

Используем своё имя вместо `mylib`.