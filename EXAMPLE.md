# Quick bootstrap (Windows, PowerShell)

Open **PowerShell** in the project root and run this script  
(click the “Copy” button in the top-right corner of the block):

```powershell
Remove-Item -Recurse -Force .git
git init

Add-Content .gitignore ".vscode/"
Add-Content .gitignore ".editorconfig"
git add .gitignore
git commit -m "chore(gitignore): add .vscode/ & editorconfig"

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