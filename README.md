# C++ Library Template (`mylib`)

Small C++ library project template:
```txt
- CMake (with installation and support `find_package`)
- Тесты (GoogleTest + CTest)
- Examples of use
- CI (GitHub Actions)
- Formatting settings (`.clang-format` for Google Style)
```

---

## 1. How to use this repository as a template

### 1.1. Step 1 – Delete Git history (make a “clean” project)

#### macOS / Linux

```bash
rm -rf .git
git init
git add --all
git commit -m "Initial commit"
```

#### Windows (PowerShell)

```powershell
Remove-Item -Recurse -Force .git
git init
git add --all
git commit -m "Initial commit"
```

#### Windows (cmd.exe)

```bat
rmdir /S /Q .git
git init
git add --all
git commit -m "Initial commit"
```

---

### 1.2. Step 2 - Rename `mylib` to suit your project

The template uses the name `mylib`. It is usually replaced with the name of your library, for example `awesome`:

1. Folders:
   - `include/mylib/` → `include/awesome/`
2. Namespace in code:
   - `namespace mylib { ... }` → `namespace awesome { ... }`
3. CMake Entries:
   - `project(mylib ...)` → `project(awesome ...)`
   - target `mylib` → `awesome`
   - `mylibTargets.cmake`, `mylibConfig.cmake` → `awesomeTargets.cmake`, `awesomeConfig.cmake`
   - `mylib::mylib` → `awesome::awesome`
4. In other files:
   - `README.md`, `ci.yml`, examples, tests (`mylib_tests` и т.п.)

The most convenient way is to do a global search/replace by string `mylib` in IDE (VS Code: `Ctrl+Shift+F` / `Cmd+Shift+F`).

---

## 2. Project structure

```text
├─ include/mylib/      # Public Headlines (public API)
├─ src/                # Implementation libraries
├─ tests/              # Unit tests (GoogleTest + CTest)
├─ examples/           # Examples of use
├─ cmake/              # CMake configs for find_package
├─ .github/workflows/  # CI (GitHub Actions)
└─ CMakeLists.txt      # Root CMakeLists
```

---

## 3. Build

Requirements:

```txt
- CMake ≥ 3.20
- C++ compiler with support C++20
- (preferably) Ninja
```

```bash
# Configuration
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=ON -DBUILD_EXAMPLES=ON

# Build
cmake --build build
```

---

## 4. Running tests

```bash
cd build
ctest --output-on-failure
```

---

## 5. Use as an external library

After installation:

```bash
cmake --install build --prefix /usr/local
```

In another CMake project:

```cmake
find_package(mylib CONFIG REQUIRED)

add_executable(app main.cpp)
target_link_libraries(app PRIVATE mylib::mylib)
```

We use our name instead `mylib`.