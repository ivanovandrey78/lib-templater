# mylib

[**Короткое описание проекта**]

Пример:  
*mylib — небольшая C++ библиотека, предоставляющая вспомогательные функции для X/Y/Z.*

---

## Возможности

- [Пункт 1: что умеет библиотека]
- [Пункт 2]
- [Пункт 3]

---

## Структура проекта

```text

├─ include/mylib/    # Публичные заголовки (public API)
├─ src/              # Реализация библиотеки
├─ tests/            # Юнит‑тесты (GoogleTest + CTest)
├─ examples/         # Примеры использования
├─ cmake/            # CMake-конфиги для find_package
└─ CMakeLists.txt
```

## Сборка 

Требования: 
- CMake ≥ 3.20
- C++ компилятор с поддержкой C++20
- (опционально) Ninja

```bash
# Конфигурация
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=ON -DBUILD_EXAMPLES=ON

# Сборка
cmake --build build
```

## Запуск тестов

```bash
cd build
ctest --output-on-failure
```