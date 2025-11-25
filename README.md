# OTUS. ML-Basic. Git, Shell

## Часть 1. Терминал

### Навигация и просмотр

```bash
pwd                  # текущая директория
ls                   # содержимое папки
ls -la               # подробный список с скрытыми файлами
cd folder            # перейти в папку
cd ..                # на уровень выше
cd ~                 # домашняя директория
cd -                 # вернуться в предыдущую папку
```

### Работа с файлами и папками

```bash
mkdir folder         # создать папку
mkdir -p a/b/c       # создать вложенные папки
touch file.txt       # создать пустой файл
rm file.txt          # удалить файл
rm -r folder         # удалить папку с содержимым
cp file.txt copy.txt # копировать
mv file.txt new.txt  # переименовать/переместить
```

### Просмотр и редактирование

```bash
cat file.txt              # вывести содержимое
head -n 10 file.txt       # первые 10 строк
tail -n 10 file.txt       # последние 10 строк
echo "text"               # вывести текст
echo "text" > file.txt    # записать в файл (перезапись)
echo "text" >> file.txt   # дописать в файл
```

### Полезное

```bash
clear                # очистить экран
history              # история команд
ctrl + c             # прервать выполнение
ctrl + r             # поиск по истории
tab                  # автодополнение
```

### Создание и активация виртуального окружения Python

```bash
python3 -m venv .venv        # создать виртуальное окружение
source .venv/bin/activate    # активировать (Linux/Mac)
.venv\Scripts\activate       # активировать (Windows)
which python3                # проверить путь к интерпретатору
pip install package_name     # установить пакет
deactivate                   # деактивировать
```

---

## Часть 2. Git — основы

### Настройка

```bash
# глобальные настройки
git config --global user.name "Name"
git config --global user.email "email@example.com"

# локальные настройки
git config --local user.name "Name"
git config --local user.email "email@example.com"

# проверить настройки
git config --local --list
```

### Создание репозитория

```bash
git init             # создать репозиторий в текущей папке
git clone <url>      # клонировать существующий
```

### Базовый цикл работы

```bash
git status                      # состояние репозитория
git add file.txt                # добавить файл в индекс
git add .                       # добавить все файлы в индекс
git commit -m "commit message"  # зафиксировать изменения
git log                         # история коммитов
git log --oneline               # компактная история
```

### .gitignore

```
# файл .gitignore
*.pyc
__pycache__/
.env
.venv/
.idea/
.DS_Store
```

---

## Часть 3. Ветки

### Работа с ветками

```bash
git branch                    # список веток
git branch feature            # создать ветку
git checkout feature          # переключиться
git checkout -b feature-2     # создать и переключиться
git switch -c feature-2       # создать и переключиться (новый синтаксис)
git switch main               # переключиться на главную ветку
git branch -D feature-2       # удалить ветку
```

### Merge — слияние веток

```bash
git checkout -b feature
# ... работаем в feature ...
git checkout main
git merge feature           # слить feature в main
```

### Rebase — перебазирование

```bash
git checkout -b feature-2
# ... работаем в feature-2 ...
git checkout main
# ... работаем в main, добавляем коммиты в main ...
git checkout feature-2
git rebase main             # перенести коммиты feature-2 на вершину main
```

Разница: merge сохраняет историю разветвления, rebase делает линейную историю.

### Reset — отмена коммитов

```bash
git reset --soft HEAD~1     # отменить коммит, изменения в индексе
git reset --mixed HEAD~1    # отменить коммит, изменения в рабочей директории
git reset --hard HEAD~1     # отменить коммит и изменения полностью
```

### Другие способы отмены

```bash
git restore file.txt            # отменить изменения в файле
git restore --staged file.txt   # убрать из индекса
```

---

## Часть 4. GitHub

### SSH vs HTTPS

HTTPS — проще, но каждый раз вводить логин/пароль (или токен).

SSH — настроить один раз:
```bash
ssh-keygen -t ed25519 -C "email@example.com"
# добавить публичный ключ в GitHub Settings -> SSH Keys
```

### Связь с удаленным репозиторием

```bash
git remote add origin <url>     # добавить удаленный репозиторий
git remote -v                   # список удаленных репозиториев
git remote remove origin        # удалить связь
```

### Push, Pull, Fetch, Pull Request

```bash
git push origin main                # первый пуш (устанавливает upstream)
git switch -c feature               # создать и переключиться на новую ветку
# ... работаем в новой ветке ...
git push origin feature             # запушить ветку
# ... создаем Pull Request ...
git switch main                     # переключиться на главную ветку
git fetch                           # только получить (без слияния)
git pull origin main                # получить и слить изменения из удаленного репозитория в текущую ветку
```

### Работа с чужим репозиторием

```bash
git clone <url>                 # клонировать
git pull origin main            # обновить из оригинала
```

---

## Часть 5. Git в VS Code

### Source Control панель (Ctrl+Shift+G)

- Видны измененные файлы
- `+` — stage (git add)
- Поле ввода — commit message
- Галочка — commit

### Встроенные возможности

- Просмотр diff при клике на файл
- Кнопки Sync, Push, Pull в статус-баре
- Разрешение конфликтов с подсветкой
- AI autocomplete commit messages

### Полезные команды (Ctrl+Shift+P)

- Git: Clone
- Git: Checkout to...
- Git: Create Branch

---

## Шпаргалка

| Команда | Действие |
|---------|----------|
| `git init` | Создать репозиторий |
| `git clone <url>` | Клонировать |
| `git status` | Состояние |
| `git add .` | Добавить все |
| `git commit -m "msg"` | Коммит |
| `git log --oneline` | История |
| `git branch name` | Создать ветку |
| `git checkout name` | Переключиться |
| `git merge name` | Слить |
| `git rebase name` | Перебазировать |
| `git reset --soft HEAD~1` | Отменить коммит |
| `git push origin <branch>` | Отправить |
| `git pull origin <branch>` | Получить |
| `git fetch origin <branch>` | Получить |
| `git switch -c <branch>` | Создать и переключиться |
| `git switch <branch>` | Переключиться |
| `git branch -D <branch>` | Удалить ветку |
| `git branch` | Список веток |
---