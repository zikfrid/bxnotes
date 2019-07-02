---
title: Права доступа
seoDescription: Устройство прав в системе Linux. Изменение прав командой chmod, описание команды umask, типы пользователей и режимы доступа.
seoKeywords: linux, chmod, umask
date: 2018-08-05 10:00:00
---
# Права доступа

## Просмотр прав доступа

Команда:
```bash
ls -l
```

### Формат:
```
-rw-r--r-- 1 user somegroup 18 Aug 5 00:58 index.html
```

### Описание формата:

- |	rw- |	r-- |	r--
--- | --- | --- | ---
Режим файла, определяет тип файла:<br>`-` обычный файл,<br>`d` каталог | Права владельца файла | Права группы владельца | остальные (общие права)

### Права доступа

Символ | Значение
--- | ---
`r` | чтение 
`w` | запись 
`x` | Файл является исполняемым (можно запустить как программу).<br>Для каталога это означает доступ к файлам внутри данного каталога. `s` | setuid, файл запускается как будто его запускает указанный пользователь. 
`–` | Ничего не обозначает.

### Просмотра группы текущего пользователя:
```bash
groups
```

## Изменение прав доступа

### Шаблон команды: 
```bash
chmod go+w-r file 
# для групп пользователя и остальных добавить право чтения и удалить право записи на файл file
```

Сначала нужно указать для каких групп должны действовать изменения, затем какие права добавить или убрать и имя файла.

### Типы пользователей

Символ | Описание
--- | ---
u | владелец файла 
g | группа владельца 
o | другие 
a | все (или ugo)

### Операторы

Символ | Описание 
--- | ---
+ | добавить определенные права 
- | удалить определенные права 
= | установить определенные права

## Абсолютное изменение прав

При данном способе устанавливаются все биты доступа:
```bash
chmod 644 file
```

`644` означает:
+ `6` для владельца (в двоичной форме *110*)
+ `4` для группы владельца (в двоичной форме *100*)
+ `4` для остальных (в двоичной форме *100*)

Двоичная маска применяется к шаблону `rwx` и таким образом получаем: 

+ `rw` для владельца,
+ `r` для группы
+ `r` для остальных

### Популярные значения прав:

Права	| Описание | Применение
--- | --- | ---
644 (-rw--r--r-) | Владелец имеет право чтения и записи, группа владельца и остальные только чтнеие	| Файлы
600 (-rw-------) | Владелец имеет право чтения и записи, группа владельца и остальные ничего не могут	| Файлы
755 (-rwxr-xr-x) | У владельца чтение, запись и запуск, группа владельца и остальные чтение и запись	| Каталоги, команды
700 (-rwx------) | У владельца полные права, группа владельца и остальные нет прав	| Каталоги, команды
711 (-rwx--x--x) |У владельца полные права, группа владельца и остальные могут только запускать	| Каталоги

## umask

Команда `umask` позволяет настроить шаблон доступа для вновь создаваемых файлов и каталогов. Чтобы новые права применились по умолчанию в следующих сеансах, нужно поместить команду `umask` с указанием режима в один из файлов запуска системы.

Команда `umask` показывает какие биты доступа нужно сбросить у вновь создаваемых файлов и каталогов. Например, после выполнения команды `umask 174` новые файлы будут создаваться с правами -rw-----w- 602, а новые каталоги правами drw-----wx 603. То есть, в правах владельца будет сброшен бит `x`, в группе владельца будут сброшены все биты, а у остальных будет сброшен бит `r`.