# C++ Library Template (`mylib`)

Small C++ library project template:
```txt
- CMake (with installation and support `find_package`)
- Тесты (GoogleTest + CTest)
- Examples of use
- CI (GitHub Actions)
- Formatting settings (.clang-format for Google Style)
```

---

## 1. How to use this repository as a template

### 1.1. Step 1 – Delete Git history (make a “clean” project)

#### macOS / Linux

```bash
rm -rf .git
git init
```

#### Windows (PowerShell)

```powershell
Remove-Item -Recurse -Force .git
git init
```

#### Windows (cmd.exe)

```bash
rmdir /S /Q .git
git init
```

---

### 1.2. Step 2 - Rename `mylib` to suit your project

The template uses the name `mylib`. It is usually replaced with the name of your library, for example `awesome`:

1. Open your project folder in VS Code.
2. Open **global search**:
   - Windows/Linux: `Ctrl+Shift+F`  
   - macOS: `Cmd+Shift+F`
3. In the **Search** field type:
   ```text
   mylib
   ```
4. Open the Replace field:
   Click the small arrow ▾ on the left of the search field and enable `Replace`, or
   Press:
   - Windows/Linux: `Ctrl+H`
   - macOS: `Cmd+Alt+F`
5. In the Replace field type your new name: 
   ```text
   awesome
   ```
6. Make sure:
   - `Use Regular Expression` (.*) is off,
   - `Match Case` (Aa) is on (so only mylib is replaced, not Mylib, etc.).
7. Click `Replace All`
8. Also rename the file "`mylibConfig.cmake.in`":

#### macOS / Linux

```bash
mv cmake/mylibConfig.cmake.in cmake/awesomeConfig.cmake.in
```

#### Windows (PowerShell)

```powershell
Rename-Item -Path cmake/mylibConfig.cmake.in -NewName awesomeConfig.cmake.in
```

#### Windows (cmd.exe)

```bash
ren cmake\mylibConfig.cmake.in awesomeConfig.cmake.in
```

---

### 1.3. Step 3 – Add .vscode/ to .gitignore
VS Code configuration is usually considered local developer config and not tracked in Git.
Add `.vscode/` to `.gitignore` so that it is ignored in your project.

#### macOS / Linux

```bash
echo ".vscode/" >> .gitignore
echo ".editorconfig" >> .gitignore
git add .gitignore
git commit -m "chore(gitignore): add .vscode/ & editorconfig"
```

#### Windows (PowerShell)

```powershell
Add-Content .gitignore ".vscode/"
Add-Content .gitignore ".editorconfig"
git add .gitignore
git commit -m "chore(gitignore): add .vscode/ & editorconfig"
```

#### Windows (cmd.exe)

```bat
echo .vscode/>> .gitignore
echo .editorconfig>> .gitignore
git add .gitignore
git commit -m "chore(gitignore): add .vscode/ & editorconfig"
```

---

### 1.4. Step 4 – Replace README with your own & delete EXAMPLE
Current README.md describes the template. For a real project you should create your own README.

#### macOS / Linux

```bash
rm README.md
rm EXAMPLE.md

cat > README.md << 'EOF'
# Project Name

Short description of your project.

## Features

- Feature 1
- Feature 2
- Feature 3

## Build

Describe here how to build your project.

EOF

git add README.md
git commit -m "chore(readme): add project-specific README"
```

#### Windows (PowerShell)

```powershell
Remove-Item README.md
Remove-Item EXAMPLE.md

@'
# Project Name

Short description of your project.

## Features

- Feature 1
- Feature 2
- Feature 3

## Build

Describe here how to build your project.
'@ | Out-File -Encoding UTF8 README.md

git add README.md
git commit -m "chore(readme): add project-specific README"
```

#### Windows (cmd.exe)

```bat
del README.md
del EXAMPLE.md

(
echo # Project Name
echo.
echo Short description of your project.
echo.
echo ## Features
echo.
echo - Feature 1
echo - Feature 2
echo - Feature 3
echo.
echo ## Build
echo.
echo Describe here how to build your project.
) > README.md

git add README.md
git commit -m "chore(readme): add project-specific README"
```

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