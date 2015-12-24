### Современные проблемы информатики и вычислительной техники. Лабораторная 2.

##### Для утилиты lftp создать профиль apparmor, позволяющий ей исправно функционировать в рамках минимально необходимых и достаточных ограничений в операционной системе

Сначала я пошёл по такому пути:

* 0) Установить нужные пакеты;
* 1) Создать пусотой профиль в /etc/apparmor.d/;
* 2) Подгрузить профиль: sudo apparmor_parser -r /etc/apparmor.d/usr.bin.lftp;
* 3) Профиль в режим "жалобы":
sudo aa-complain /usr/bin/lftp;
* 4) Открываем программу и делаем то что всегда, качаем файлы и т.д.;
* 5) После этого aa-logprof-ом вписать все правила которые он предлагает.

Результат меня не устроил и я решил strace-ом смотреть к каким файлам нужен доступ. Сначала по одному файлу вписывал в правило а потом стал искать в каталоге abstractions по содержимому.
Довольно скоро появился [вот этот файл](https://github.com/dmitryunterov/modernprobs-lab2/blob/master/usr.bin.lftp).

Проведённые тесты показывают, что правило работает (За предоставленный для тестирования ftp-сервер спасибо Стасу Габенову):

![Скриншот с пруфами](https://github.com/dmitryunterov/modernprobs-lab2/blob/master/screenshot.png)






