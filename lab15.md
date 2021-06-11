---
# Front matter
lang: ru-RU
title: "отчёта по лабораторной работе 15"
subtitle: "Операционные системы"
author: "Алхатиб Осама"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Отчет по лабораторной работе №15

----

### Средства, применяемые при разработке программного обеспечения в ОС типа UNIX/Linux

----

## Российский Университет Дружбы Народов

### Факультет Физико-Математических и Естественных Наук

*Дисциплина: Операционные системы*

Студент: Алхатиб Осама

Группа: НПИбд-02-20

2021г.

---

## Цель работы
Приобретение практических навыков работы с именованными каналами.

---

Ход работы
1,2,3. Работают 2 клиента, передают время раз в 5 и 4 секунды, сервер работает 20 секунд

![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/1.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/2.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/3.png)
**Сервер отключается и файл не существует, закрывая клиенты**
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/4.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/5.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/6.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/7.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/8.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/9.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/10.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/11.png)
![](https://raw.githubusercontent.com/osamakhateb/lab15/main/image/12.png)

---

## Вывод
В результате работы , я приобрел практические навыки работы с именованными каналами

---

####    ***Контрольные вопросы***
1. Именованные каналы отличаются от неименованных наличием идентификатора канала, 
который представлен как специальный файл (соответственно имя именованного канала —
это имя файла).
2. Для создания неименованного канала используется системный вызов pipe. Массив из
двух целых чисел является выходным параметром этого системного вызова.
3. Вы можете создавать именованные каналы из командной строки и внутри программы. С 
давних времен программой создания их в командной строке была команда: mknod - $ mknod 
имя_файла , однако команды mknod нет в списке команд X/Open, поэтому она включена не во 
все UNIX-подобные системы. Предпочтительнее применять в командной строке - $ mkfifo 
имя_файла.
4. int read(int pipe_fd, void *area, int cnt);
Int write(int pipe_fd, void *area, int cnt);
Первый аргумент этих вызовов - дескриптор канала, второй - указатель на область памяти, с 
которой происходит обмен, третий - количество байт. Оба вызова возвращают число 
переданных байт (или -1 - при ошибке).
5. int mkfifo (const char *pathname, mode_t mode); Первый параметр — имя файла, 
идентифицирующего канал, второй параметр маска прав доступа к файлу. Вызов функции 
mkfifo() создаёт файл канала (с именем, заданным макросом FIFO_NAME): 
mkfifo(FIFO_NAME, 0600);
6. При чтении меньшего числа байтов, чем находится в канале, возвращается требуемое 
число байтов, остаток сохраняется для последующих чтений. При чтении большего числа 
байтов, чем находится в канале или FIFO возвращается доступное число байтов.
7. При записи большего числа байтов, чем это позволяет канал или FIFO, вызов write(2) 
блокируется до освобождения требуемого места. При этом атомарность операции не 
гарантируется. Если процесс пытается записать данные в канал, не открытый ни одним 
процессом на чтение, процессу генерируется сигнал. Запись числа байтов, меньшего емкости 
канала или FIFO, гарантированно атомарно. Это означает, что в случае, когда несколько 
процессов одновременно записывают в канал, порции данных от этих процессов не 
перемешиваются.
8. В общем случае возможна многонаправленная работа процессов с каналом, т.е. возможна 
ситуация, когда с одним и тем же каналом взаимодействуют два и более процесса, и каждый из взаимодействующих каналов пишет и читает информацию в канал. Но традиционной 
схемой организации работы с каналом является однонаправленная организация, когда канал 
связывает два, в большинстве случаев, или несколько взаимодействующих процесса, каждый 
из которых может либо читать, либо писать в канал.
9. Write - Функция записывает length байтов из буфера buffer в файл, определенный 
дескриптором файла fd. Эта операция чисто 'двоичная' и без буферизации. Реализуется как 
непосредственный вызов DOS. С помощью функции write мы посылаем сообщение клиенту 
или серверу.
10. Строковая функция strerror - функция языков C/C++, транслирующая код ошибки, 
который обычно хранится в глобальной переменной errno, в сообщение об ошибке, понятном 
человеку. Ошибки эти возникают при вызове функций стандартных Си-библиотек.
Возвращенный указатель ссылается на статическую строку с ошибкой, которая не должна 
быть изменена программой. Дальнейшие вызовы функции strerror перезапишут содержание 
этой строки. Интерпретированные сообщения об ошибках могут различаться, это зависит от 
платформы и компилятора