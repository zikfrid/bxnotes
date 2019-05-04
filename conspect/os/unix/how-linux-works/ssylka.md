---
layout: post.njk
tags: [post, postInConspect:how-linux-works]
conspect: how-linux-works
section: os
subject: unix
title: Ссылка
seoDescription: Что такое символическая ссылка. Создание и использование символических ссылок в Linux.
seoKeywords: linux, symlink
date: 2018-08-05 11:00:00
---
# Ссылка

## Что такое символмческая ссылка

Символическая ссылка — это файл, который указывает на другой файл, каталог или символическую ссылку. Символическая ссылка не обязательно должна указывать на существующий объект.

Символическая ссылка имеет тип `l` в описании:
```
lrwxrwxrwx 1 ruser users 11 Feb 27 13:52 somedir -> /home/origdir
```

## Создание символической ссылки

Чтобы создать символическую ссылку, используйте команду:
```bash
ln -s path linkname 
# если не указать атрибут -s будет создана жесткая ссылка
```

## Редактирование и удаление символической ссылки

При редактировании символической ссылки будет модифицирован файл, на который она указывает. 

При удалении ссылки файл останется. 

При удалении файла, ссылка будет указывать на несуществующий файл.