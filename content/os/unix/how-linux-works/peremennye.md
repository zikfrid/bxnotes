---
title: Переменные
seoDescription: Переменные linux.
seoKeywords: linux, vars
date: 2018-08-05 05:00:00
---
# Переменные

## Переменные оболочки

Чтобы в *оболочке* создать *переменную* и присвоить ей значение используется знак равенства:
```bash
myvar='Hello Word'
# или
myvar=HellowWord
```

Чтобы вывести *переменную* можно использовать команду вывода в поток:
```bash
echo $myvar
```

## Переменные окружения

Чтобы сделать из *переменной оболочки* *переменную окружения* используйте команду:
```bash
export myvar
```

*Переменные окружения* можно передавать командам.
В них удобно хранить часто используемые параметры для команд.

## Командный путь

*Командный путь* - это пути, по которым оболочка ищет команды, запрашиваемые пользователем.

Пути хранятся в переменной `$PATH`.

Эту переменную можно отредактировать, например:
```bash
PATH=somedir:$PATH
# добавили свой каталог первым
```