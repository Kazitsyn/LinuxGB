## Урок 4. Скрипты Bash

### Задание:

- Написать скрипт  очистки директорий. На вход принимает путь к директории. Если директория существует, то удаляет в ней все файлы с расширениями .bak, .tmp, .backup. Если директории нет, то выводит ошибку.

```bash
#!/bin/bash

if [ $# -eq 0 ]; then
  echo "Usage: $0 <directory_path>"
  exit 1
fi

if [ ! -d "$1" ]; then
  echo "Error: Directory '$1' not found"
  exit 1
fi

echo "Cleaning directory '$1'..."

find "$1" -type f \( -name "*.bak" -o -name "*.tmp" -o -name "*.backup" \) -delete

echo "Done."
```

- Создать скрипт ownersort.sh, который в заданной папке копирует файлы в директории, названные по имени владельца каждого файла. Учтите, что файл должен принадлежать соответствующему владельцу.


```bash
#!/bin/bash

if [ $# -eq 0 ]; then
  echo "Usage: $0 <directory_path>"
  exit 1
fi

if [ ! -d "$1" ]; then
  echo "Error: Directory '$1' not found"
  exit 1
fi

echo "Sorting files in directory '$1' by owner..."

for file in "$1"/*; do
  if [ -f "$file" ]; then
    owner=$(stat -c '%U' "$file")
    if [ ! -d "$1/$owner" ]; then
      mkdir "$1/$owner"
    fi
    cp "$file" "$1/$owner"
  fi
done

echo "Done."
```