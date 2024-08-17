# -101-Linux-commands-RUS-

### Основы

#### Стандарт иерархии файлов (FHS)

| Путь      | Содержимое |
|-----------|------------|
| /bin      | Исполняемые файлы (пользовательские) |
| /boot     | Статические файлы загрузчика |
| /etc      | Конфигурации хоста |
| /lib      | Общие библиотеки и модули ядра |
| /sbin     | Исполняемые файлы (системные/root) |
| /var      | Изменяемые файлы (например, журналы) |
| /usr      | Стороннее программное обеспечение |
| /proc     | Псевдо файловая система |
| /sys      | Псевдо файловая система |
| /mnt      | Точка монтирования для внутренних дисков |
| /media    | Точка монтирования для внешних дисков |
| /home     | Домашние каталоги пользователей |
| /run      | PID файлы работающих процессов |

#### Команды файловой системы

| Команда | Опции | Описание |
|---------|-------|----------|
| cd      | -     | Перейти в последний каталог |
|         | ~     | Перейти в домашний каталог |
|         | ~username | Перейти в домашний каталог указанного пользователя |
| pwd     |       | Показать текущий каталог |
| ls      |       | Показать содержимое каталога |
|         | -l    | Форматировать как список |
|         | -a    | Показать скрытые элементы (-A без . и ..) |
|         | -r    | Инвертировать порядок |
|         | -R    | Рекурсивно |
|         | -S    | Сортировать по размеру |
|         | -t    | Сортировать по дате изменения |
| mkdir   | -p    | Создать каталог с родительскими каталогами |
| cp      | -r    | Копировать каталог |
| rmdir   | -p    | Удалить каталог и пустые родительские каталоги |
| rm      | -rf   | Удалить каталог рекурсивно, -f без подтверждения |
| mv      |       | Переместить рекурсивно |
| find    | -iname pattern | Искать каталог/файл без учета регистра |
|         | -mmin n | Последнее изменение n минут назад |
|         | -mtime n | Последнее изменение n дней назад |
|         | -regex pattern | Путь соответствует шаблону |
|         | -size n[kMG] | По размеру файла (-n меньше чем; +n больше чем) |
|         | ! searchparams | Инвертировать поиск |


### Манипуляции с файлами

| Команда | Опции | Описание |
|---------|-------|----------|
| cat     | file  | Вывести содержимое файла |
| tac     | file  | Вывести содержимое файла в обратном порядке |
| sort    | file  | Вывести отсортированное содержимое файла |
| sort    | file -r -u | Вывести отсортированное содержимое файла в обратном порядке без дубликатов |
| head    | -n10 file | Вывести строки с 1 по 10 |
| tail    | -f file | Автоматически выводить новые строки |
| cut     | -f -4,7-10,12,15- file | Вывести выбранные поля (разделенные табуляцией) |
| cut     | -c -4,7-10,12,15- file | Вывести выбранные позиции символов |
| cut     | -f 2,4 -d, --output-delimiter=$'\t' file | Изменить разделитель (использовать табуляцию для вывода) |
| uniq    | file  | Скрыть последовательные идентичные строки |
| uniq    | file -c | Показать количество последовательных идентичных строк |
| uniq    | file -u | Скрыть все повторяющиеся строки, оставив только уникальные строки |
| file    | file  | Определить тип файла |
| wc      | file  | Подсчитать количество строк, слов и символов (байтов) |

## Архивирование

| Команда | Опции | Описание |
|---------|-------|----------|
| tar     | cfv archiv.tar file1 file2 | Создать архив / добавить или перезаписать содержимое |
| tar     | tfv archiv.tar | Показать содержимое |
| tar     | xf archiv.tar [-C ~/extracted] | Извлечь (и декомпрессировать) архив (в папку ~ / extracted) |
| tar     | cfvj archiv.tar.bz2 file | Создать архив с компрессией bzip2 |
| tar     | cfvz archiv.tar.gz file | Создать архив с компрессией gzip |
| tar     | cfa archiv.tar.[komp] file | Создать архив с компрессией (автоматически определяет тип по имени файла) |
| bzip2   | file1 file2 | Сжимать файлы (по отдельности) |
| bzip2   | -d file1 file2 | Распаковать файлы (по отдельности) |
| gzip    | file1 file2 | Сжимать файлы (по отдельности) |
| gzip    | -d file1 file2 | Распаковать файлы |

### Управление дисками и файловыми системами

#### Общее управление дисками (без LVM)

| Команда | Опции | Описание |
|---------|-------|----------|
| fdisk   | -l | Список физических дисков и разделов |
| fdisk   | /dev/sdb | |
| fdisk   | n | Создать новый раздел |
| fdisk   | /dev/sdb | |
| fdisk   | t | |
| fdisk   | 8e | Изменить тип раздела на Linux LVM |
| mkfs.xfs | /dev/myVG/myVol | Форматировать LV в XFS |
| mkfs.ext4 | -f /dev/myVG/myVol | Форматировать LV в EXT4 (перезаписать) |
| blkid   | /dev/myVG/myVol | Показать UUID и форматирование тома |
| mount   | | Показать текущие смонтированные файловые системы |
| mount   | -t ext4 /dev/myVG/myVol /mountpoint | Смонтировать LV в /mountpoint |
| mount   | -a | Смонтировать согласно конфигурации в /etc/fstab |
| umount  | | Демонтировать файловую систему |
| umount  | /dev/myVG/myVol | Демонтировать LV из /mountpoint |
| umount  | /mountpoint | Демонтировать LV из /mountpoint |
| df      | - | Показать использование диска |
| xfs_growfs | /dev/myVG/myVol | Изменить размер файловой системы xfs |
| resize2fs | /dev/myVG/myVol | Изменить размер файловой системы ext3/4 |

### Другие команды

| Команда | Опции | Описание |
|---------|-------|----------|
| <command> | --help | Помощь по текущей команде (не стандартизировано) |
|           | -h | |
|           | -? | |
| man       | <command> | Страница руководства по команде |
| man       | -k keyword | Поиск команды по ключевому слову (или apropos) |
| alias     | | Показать алиасы |
| alias     | name='command' | Создать алиас |

### Глобы (Wildcards)

*Точка . в начале скрытых элементов игнорируется шаблонами глобов!*

| Символ | Описание |
|--------|----------|
| ?      | Любой одиночный символ |
| *      | Любая последовательность символов |
| [ac-e] | Один символ из перечисленных |
| [!ac-e] | Один символ, не входящий в перечисленные |

### Регулярные выражения (Regex)

*Bash сам по себе не поддерживает регулярные выражения. Используйте программы, такие как grep, sed, awk.*

#### Управляющие символы

| Символ | Описание |
|--------|----------|
| .      | Любой одиночный символ |
| [ac-e] | Один символ из перечисленных |
| [^ac-e] | Один символ, не входящий в перечисленные |
| ^      | Начало строки |
| $      | Конец строки |
| \d     | Цифра |
| \D     | Не цифра |
| \s     | Пробел |
| \S     | Не пробел |
| \<     | Начало слова |
| \>     | Конец слова |
| pattern? | Квантификатор 0 или 1 |
| pattern* | Квантификатор 0..n |
| pattern+ | Квантификатор 1..n |
| pattern{x} | Квантификатор ровно x |
| pattern{x,} | Квантификатор x..n |
| pattern{x,y} | Квантификатор x..y |
| pattern{,y} | Квантификатор 0..y |

### Grep

| Команда | Опции | Описание |
|---------|-------|----------|
| grep    | pattern file | Расширенные регулярные выражения |
| grep    | -E pattern file | Расширенные регулярные выражения |
| grep    | -v pattern file | Инвертировать совпадения |
| grep    | -w pattern file | Полное совпадение слова |
| grep    | -i pattern file | Игнорировать регистр |

### Перенаправление потоков

| Оператор  | Описание |
|-----------|----------|
| >         | Перезаписать файл |
| >>        | Добавить в конец файла |

#### Управляющие символы

| Символ            | Описание |
|-------------------|----------|
| > file или 1> file | Перенаправить STDOUT в файл |
| < file            | Перенаправить файл в STDIN |
| 2> file           | Перенаправить STDERR в файл |
| 2>&1              | Перенаправить STDERR в тот же поток, что и STDOUT |
| > file 2>&1       | Перенаправить STDOUT и STDERR в файл |

### Чтение и редактирование текста

#### Less

| Команда          | Описание |
|------------------|----------|
| q                | Выйти |
| R                | Обновить содержимое |
| F                | Автоматическая прокрутка |
| g number         | Перейти к строке |
| m lowercaseLetter | Отметить строку |
| ' lowercaseLetter | Перейти к отметке |
| /pattern         | Искать вперед |
| ?pattern         | Искать назад |
| n                | Следующий результат поиска |
| N                | Предыдущий результат поиска |
| ESC u            | Убрать выделение поиска |

### VI/VIM Редактирование

*Чтобы выйти из режима редактирования, нажмите ESC.*

| Команда | Описание |
|---------|----------|
| i       | Вставить перед курсором |
| a       | Вставить после курсора |
| A       | Вставить в конец строки |
| o       | Новая строка ниже |
| O       | Новая строка выше |
| u       | Отменить |
| .       | Повторить последнюю команду |
| yy      | Копировать строку |
| 5yy     | Копировать 5 строк |
| p       | Вставить ниже |
| P       | Вставить выше |
| x       | Удалить символ |
| 5x      | Удалить 5 символов |
| dd      | Удалить строку |
| 5dd     | Удалить 5 строк |
| :10,20d | Удалить строки с 10 по 20 |
| d0      | Удалить до начала строки |
| d$      | Удалить до конца строки |

### Навигация

*Передвигайтесь, как обычно, с помощью стрелок, клавиш Home, End, Pg Up, Pg Dn.*

| Команда | Описание |
|---------|----------|
| 5G      | Перейти на строку 5 |
| H       | Перейти в начало экрана |
| M       | Перейти в середину экрана |
| L       | Перейти в конец экрана |
| 5w      | Перейти на 5 слов вперед |
| 5b      | Перейти на 5 слов назад |

### Другие команды

| Команда     | Описание |
|-------------|----------|
| /foo        | Искать вперед |
| ?foo        | Искать назад |
| n           | Повторить поиск |
| :w          | Сохранить |
| :q          | Закрыть |
| :wq         | Сохранить и закрыть |
| :q!         | Закрыть без сохранения |
| :!command   | Выполнить команду bash |
| :r foo      | Прочитать файл foo в этот файл |

### Управление пользователями и группами

#### UID

| UID     | Тип           |
|---------|---------------|
| <1000   | системная учетная запись |
| >1000   | пользовательская учетная запись |

#### База данных пользователей

*Информация о пользователях без паролей хранится в /etc/passwd.*

| username | PW | UID | GID | GECOS | HOME | SHELL |
|----------|----|-----|-----|-------|------|-------|
| hfict    | x  | 1000| 1000|       | /home/hfict | /bin/bash |

#### База данных групп

*Информация о группах с членами вторичных групп хранится в /etc/group. Основные члены групп идентифицируются по GID в базе данных пользователей.*

| groupname | PW | GID | Users |
|-----------|----|-----|-------|
| wheel     | x  | 10  | hfict,user2 |

### База данных паролей

*Хэшированные пароли пользователей хранятся в /etc/shadow. Шифрование паролей настраивается в /etc/login.defs.*

| username | PW       | Последнее изменение пароля | Минимум | Максимум | Предупреждение | Неактивность | Истечение срока |
|----------|----------|----------------------------|---------|----------|----------------|--------------|-----------------|
| hfict    | [hash]   | 17803                      | 0       | 99999    | 7              |              |                 |

#### PW (Пароль):

- `[hash]` - Зашифрованный текст пароля
- `![hash]` - Аккаунт заблокирован
- `!!` или `*` - Аккаунт заблокирован, пароль не установлен

### Команды

| Команда   | Параметр | Описание |
|-----------|----------|----------|
| id        | username | Показать ID и группы пользователя |
| who       |          | Показать вошедших пользователей |
| last      |          | Показать последние входы |
| lastb     |          | Показать последние неудачные входы |
| sudo      | -u user command | Выполнить команду с правами пользователя (по умолчанию root) |
| sudo      | -i или su -  | Shell с правами root |
| su        |          | Shell как root (non-login shell) |
| su        | -        | Shell как root (login shell) |
| su        | - user   | Shell как пользователь |
| useradd   | -u 2101 -g primarygroup -c comment username | Создать пользователя (без -g, будет создана новая группа) |
| usermod   | -G group1, group2 | Определить (перезаписать) вторичные группы |
| usermod   | -ag group, group2 | Добавить вторичные группы |
| usermod   | -l username | Изменить имя пользователя |
| usermod   | -L        | Заблокировать аккаунт |
| usermod   | -U        | Разблокировать аккаунт |
| usermod   | -s shellpath | Изменить shell |
| userdel   | -r username | Удалить пользователя, включая домашнюю директорию и почтовый ящик |
| passwd    | username | Изменить пароль (интерактивно) |
| groupadd  | groupname | Создать группу (опционально установить GID с -g) |
| groupdel  | groupname | Удалить группу |

### Разрешения файловой системы

Разрешения могут быть установлены для:

- Пользователя (владельца)
- Группы (владельца)
- Прочих

Только root может изменить пользователя. Пользователь может изменить группу.

#### Основные разрешения (Добавьте двоичные флаги для комбинирования):

| Символ | Двоичный флаг | Разрешение |
|--------|---------------|------------|
| r      | 4             | чтение     |
| w      | 2             | запись     |
| x      | 1             | выполнение |

#### Расширенные разрешения (ставятся перед основными разрешениями: chmod 1777 shared):

| Символ | Двоичный флаг | Имя         | Описание |
|--------|---------------|-------------|----------|
| t / T  | 1             | Sticky Bit  | Другие не могут удалять содержимое (применимо только к каталогам) |
| s / S  | 2             | SGID-Bit    | Файл: запуск с разрешениями группы <br> Каталог: новые элементы наследуют группу |
| s / S  | 4             | SUID-Bit    | Файл запускается с разрешениями пользователя (применимо только к файлам) |

#### Дополнительная информация

- Расширенные разрешения заменяют `x` при использовании `ls -l`. Малые буквы, если `x` установлено, большие буквы, если `x` не установлено.
- Разрешение на чтение каталога позволяет видеть сам каталог, но не его содержимое. Используйте разрешение на выполнение, чтобы показать содержимое.

### Команды

| Команда | Опции | Описание |
|---------|-------|----------|
| chmod   | -R [uog] dirname | Установить разрешения рекурсивно с использованием двоичных флагов |
| chmod   | +[suog] filename | Добавить разрешения с использованием двоичных флагов |
| chmod   | -[suog] filename | Удалить разрешения с использованием двоичных флагов |
| chmod   | u+x filename | Добавить разрешение на выполнение для пользователя |
| chmod   | g+wx filename | Добавить разрешения на запись и выполнение для группы |
| chmod   | o-r filename | Удалить разрешение на чтение для прочих |
| chown   | -R user:group filename | Изменить владельца (пользователя и группу) рекурсивно |
| chown   | user filename | Изменить владельца (пользователя) |
| chown   | :group filename | Изменить владельца (группу) |
| chgroup | group filename | Изменить владельца (группу) |

### SSH

*Конфигурация SSH выполняется в /etc/ssh/sshd_config.*

*Перезагрузите службу SSH с помощью `systemctl reload sshd`, чтобы применить изменения!*

*Параметры DenyUsers, AllowUsers, DenyGroups, AllowGroups взаимно исключают друг друга и применяются в порядке, указанном выше.*

| Конфигурация      | Опция                | Описание |
|-------------------|----------------------|----------|
| PermitRootLogin   | no                   | Запретить root вход через SSH |
|                   | yes                  | Разрешить root вход через SSH |
|                   | without-password     | Разрешить только с аутентификацией по ключу (private/public key auth) |
| AllowUsers        | user1 user2          | Разрешить только пользователям user1 и user2 |
| DenyUsers         | user1 user2          | Разрешить всем пользователям, кроме user1 и user2 |
| AllowGroups       | group1 group2        | Разрешить только пользователям из указанных групп |
| DenyGroups        | group1 group2        | Разрешить всем пользователям, кроме тех, кто в указанных группах |

### Cronjobs

#### Crontab

Задания cron настраиваются в файлах crontab. Не редактируйте эти файлы напрямую. Используйте `crontab -e`. Это выполняет все необходимые действия для активации задания cron после сохранения отредактированного crontab. Расположения файлов следующие:

- `/var/spool/cron/username` — пользовательские crontab
- `/etc/crontab` — системный crontab

Формат файлов следующий (пользовательские crontab не имеют столбца `user-name`):

Пример определения задания:

```
.---------------- minute (0 - 59 | */5 [каждые 5 минут])
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) ИЛИ jan,feb,mar,apr ...
|  |  |  |  .---- day of week (0 - 6) (Воскресенье=0 или 7) ИЛИ sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  * user-name  команда для выполнения
```

#### Команды

| Команда                            | Описание |
|------------------------------------|----------|
| rpm -q cronie                      | Проверить, установлен ли пакет |
| systemctl status crond.service     | Проверить, запущена ли служба |
| crontab -l                         | Показать текущий crontab пользователя |
| crontab -e                         | Редактировать текущий crontab пользователя |
| crontab -e -u username             | Редактировать crontab конкретного пользователя |
| crontab -r                         | Удалить текущий crontab пользователя |

### Каталоги для скриптов

Скрипты, находящиеся в одном из следующих каталогов, будут выполняться с интервалом, указанным в названии каталога:

- /etc/cron.hourly - Выполняются ежечасно
- /etc/cron.daily - Выполняются ежедневно
- /etc/cron.weekly - Выполняются еженедельно
- /etc/cron.monthly - Выполняются ежемесячно

### Разрешение / Запрещение использования

Добавьте имена пользователей по одному на строку в следующие файлы:

- /etc/cron.allow - Белый список
- /etc/cron.deny - Черный список

Если ни один из файлов не существует, то всем пользователям разрешено использование.

### Логи и результаты

- Выполнение cron задач логируется в /var/log/cron.
- Результаты отправляются на почту пользователя /var/spool/mail/username.

### Управление пакетами

#### RPM

| Команда            | Описание |
|--------------------|----------|
| rpm -i rpmfile\|rpmurl | Установить пакет |
| rpm -e packagename | Удалить пакет |
| rpm -q packagename | Проверить, установлен ли пакет |
| rpm -ql packagename | Список файлов в пакете |
| rpm -qa           | Список всех установленных пакетов |
| rpm -qf /path/to/file | Получить пакет, который установил файл |
| rpm -qf $(which <exe>) | Получить пакет, который установил исполняемый файл |
| rpm -V packagename | Проверить установленный пакет |

#### YUM

*YUM настраивается в /etc/yum.conf*

*Репозитории настраиваются в /etc/yum.repos.d/*

*Лог находится в /var/log/yum.log*

| Команда                        | Описание |
|--------------------------------|----------|
| yum install packagename [-y]   | Установить пакет (-y для автоматического подтверждения) |
| yum remove packagename         | Удалить пакет |
| yum update                     | Обновить все установленные пакеты |
| yum update packagename         | Обновить определенный пакет |
| yum update pattern*            | Обновить пакеты, используя шаблон |
| yum info packagename           | Получить подробную информацию о пакете |
| yum list packagename           | Список установленных и доступных пакетов |
| yum search searchstring        | Поиск пакета (по имени и описанию) |
| yum search all searchstring    | Поиск пакета (по всем сведениям) |
| yum deplist packagename        | Список зависимостей пакета |
| yum reinstall packagename      | Переустановить (поврежденный) пакет |
| yumdownloader --resolve packagename | Загрузить RPM пакет с зависимостями |


### Навигация по директориям

- cd - изменить рабочий каталог
- ls - показать содержимое каталога
- dir - список каталогов в колонках
- pwd - показать имя рабочего каталога
- tree - показать подкаталоги в виде дерева

### Команды для работы с файлами

- cat/tac - объединять и печатать файлы
- diff/sdiff - сравнивать файлы построчно
- find - искать файлы
- grep - поиск по шаблону в файле
- head - отображать первые строки файла
- locate - находить файлы и каталоги
- stat - отображать статус файла
- tail - отображать последние строки файла
- uniq - показывать или фильтровать повторяющиеся строки в файле

### Манипуляции с файлами и каталогами

| Команда  | Описание |
|----------|----------|
| awk      | Язык сканирования и обработки по шаблону |
| chmod    | Изменить разрешения |
| chown    | Изменить владельца и группу файла |
| cp       | Копировать файлы и каталоги |
| cut      | Удалить секции из файлов |
| mkdir    | Создать новый каталог |
| mv       | Переместить файлы и каталоги |
| nano     | Текстовый редактор |
| rm       | Удалить файлы и каталоги |
| rmdir    | Удалить каталог |
| paste    | Объединить соответствующие или последовательные строки файлов |
| rsync    | Удаленное копирование файлов |
| scp      | Безопасное копирование |
| basename | Удалить информацию о каталоге и суффиксы из пути к файлу |
| sed      | Инструмент для преобразования текста |
| sort     | Сортировать или объединять строки файлов |
| split    | Разделить файл на части |
| touch    | Изменить время доступа и модификации файла |
| vim      | Текстовый редактор |

### Инструменты архивирования и сжатия

| Команда | Описание |
|---------|----------|
| bzip2   | Блок-сортировочный компрессор файлов |
| gzip    | Инструмент сжатия |
| gunzip  | Инструмент распаковки |
| tar     | Создание, извлечение и манипуляция архивами |
| zip     | Упаковать и сжать файлы |
| unzip   | Просмотр, тестирование, извлечение сжатых ZIP файлов |

### Системные команды

| Команда       | Описание |
|---------------|----------|
| crontab       | Поддержка индивидуальных таблиц, используемых для управления демоном cron |
| df            | Отображение свободного места на диске |
| du            | Отображение статистики использования диска |
| free          | Показ информации о использовании памяти |
| hostname      | Установка или вывод имени текущего хоста системы |
| hostnamectl   | Изменение настроек имени хоста |
| ionice        | Получение/установка приоритета ввода-вывода процесса |
| iostat        | Статистика ввода-вывода |
| kill          | Завершение или посылка сигнала процессу по id |
| killall       | Завершение процессов по имени |
| lsblk         | Отображение блочных и loop-устройств |
| lsof          | Показ открытых файлов |
| mpstat        | Статистика CPU |
| ncdu          | Использование диска на основе curses |
| ps            | Показ состояния процессов |
| pstree        | Показ процессов в виде дерева |
| reboot        | Перезапуск системы |
| service       | Запуск init-скрипта |
| shutdown      | Закрытие системы в указанное время |
| top/htop      | Показ информации о процессах |
| uname         | Печать информации о операционной системе |
| useradd       | Добавление/обновление учетных записей пользователей |
| userdel       | Удаление учетной записи пользователя |
| usermod       | Изменение свойств пользователя |
| vmstat        | Статистика виртуальной памяти |
| whereis       | Поиск программ |

### Сетевые команды

| Команда    | Описание |
|------------|----------|
| dig        | Утилита для поиска DNS |
| ifconfig   | Настройка параметров сетевого интерфейса |
| ip         | Выполнение задач сетевого администрирования |
| iptable    | Настройка IPv4 межсетевого экрана |
| lscpu      | Отображение информации о архитектуре CPU |
| netstat    | Показ состояния сети |
| ping       | Проверка сетевой связи |
| whois      | Информация о доменных именах и сетевых номерах |

### Управление пакетами

| Команда | Описание |
|---------|----------|
| apt     | Управление пакетами Debian |
| rpm     | Менеджер пакетов RPM (RedHat) |
| yum     | Менеджер пакетов для RedHat Linux |

### Приложения

| Команда   | Описание |
|-----------|----------|
| bc        | базовый калькулятор |
| cal       | отображает календарь |
| cmatrix   | вход в "Матрицу" |
| curl      | передача данных на сервер или с сервера |
| echo      | отображает интерпретированные аргументы |
| factor    | выводит простые множители чисел |
| printf    | форматированный вывод |
| sl        | запускает паровоз через ваш терминал |
| wget      | неинтерактивная загрузка веб-файлов |
| xargs     | создает списки аргументов и выполняет утилиту |
| yes       | выводит непрерывный поток |
| banner    | пишет строки ASCII-символов большими буквами на стандартный вывод |
| aplay     | командная строка для воспроизведения аудиофайлов |
| spd-say   | воспроизводит данный текст как звук с командной строки |

