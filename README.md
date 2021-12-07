# Практическое задание
```
Выполнил: Потоцкий Савелий
Группа: ФОМ-110510
Предмет: Параллельное и распределенное программирование
```

Структура проекта:
|Файл                           |Описание                                           |
|-------------------------------|---------------------------------------------------|
|README.md                      |Описание проекта в разметке Markdown               |
|src/tpe.py                     |Скрипт. Пример ThreadPoolExecutor                  |
|src/ppe.py                     |Скрипт. Пример ProcessPoolExecutor                 |
|src/create_links.py            |Скрипт для создания текстового файла с ссылками    |
|src/check_link_original.py     |Оригинальный скрипт для проверки ссылок            |
|src/check_link_workers_5.py    |Скрипт для проверки ссылок в 5 потоков             |
|src/check_link_workers_10.py   |Скрипт для проверки ссылок в 10 потоков            |
|src/check_link_workers_100.py  |Скрипт для проверки ссылок в 100 потоков           |
|src/cpu_bound_original.py      |Оригинальный скрипт для создания монет             |
|src/cpu_bound_workers_2.py     |Скрипт для создания монет в 2 потока               |
|src/cpu_bound_workers_4.py     |Скрипт для создания монет в 4 потока               |
|src/cpu_bound_workers_5.py     |Скрипт для создания монет в 5 потоков              |
|src/cpu_bound_workers_10.py    |Скрипт для создания монет в 10 потоков             |
|src/cpu_bound_workers_100.py   |Скрипт для создания монет в 100 потоков            |

## ProcessPoolExecutor
### Скорость выполнения
#### Скорость проверки ссылок и потребление ресурсов системы
|Скрипт                    |Описание              |Время выполнения (total)   |Время выполнения (user)|Время выполнения (system)|Загрузка процессора|
|--------------------------|----------------------|---------------------------|-----------------------|-------------------------|-------------------|
|check_link_original.py    |Оригинальный скрипт   |20 минут 6 секунд          |13 секунд              |2 секунды                |1%                 |
|check_link_workers_5.py   |Скрипт с 5 потоками   |13 минут 30 секунд         |28 секунд              |55 секунд                |10%                |
|check_link_workers_10.py  |Скрипт с 10 потоками  |4 минуты 30 секунд         |26 секунд              |41 секунда               |24%                |
|check_link_workers_100.py |Скрипт с 100 потоками |2 минуты 30 секунд         |22 секунды             |40 секунд                |41%                |

Описание параметров:
```
total - общее время выполнения скрипта
user  - время выполнения скрипта в пространстве пользователя
sys   - время выполнения скрипта в пространстве ядра
```

Скорость выполнения скрипта с созданием ссылок ```create_links.py```: 2 минуты 28 секунд

#### Потребление оперативной памяти
|Скрипт                    |Описание              |Потребление оперативной памяти|
|--------------------------|----------------------|------------------------------|
|check_link_original.py    |Оригинальный скрипт   |23 mb                         |
|check_link_workers_5.py   |Скрипт с 5 потоками   |630 mb                        |
|check_link_workers_10.py  |Скрипт с 10 потоками  |722 mb                        |
|check_link_workers_100.py |Скрипт с 100 потоками |827 mb                        |

#### Время выполнения
python3 create_links.py
```sh
➜  urfu-python git:(master) ✗ python3 create_links.py
100%|██████████| 100/100 [02:28<00:00,  1.48s/it]
```

time python3 check_link_original.py
```sh
➜  urfu-python git:(master) ✗ time python3 check_link_original.py
python3 check_link_original.py  13,20s user 2,6s system 1% cpu 20:06,67 total
```

time python3 check_link_workers_5.py
```sh
➜  urfu-python git:(master) ✗ time python3 check_link_workers_5.py
python3 check_link_workers_5.py  28,40s user 55s system 10% cpu 13:30,84 total
```

time python3 check_link_workers_10.py
```sh
➜  urfu-python git:(master) ✗ time python3 check_link_workers_10.py
python3 check_link_workers_10.py  26s user 41,20s system 24% cpu 4:30,88 total
```

time python3 check_link_workers_100.py
```sh
➜  urfu-python git:(master) ✗ time python3 check_link_workers_100.py
python3 check_link_workers_100.py  22,40s user 40,20s system 41% cpu 2:30,30 total
```

#### Потребление оперативной памяти
top -p ```check_link_original.py```
```sh
top - 03:49:27 up 1 day,  1:23,  2 users,  load average: 0,02, 0,04, 0,00
Tasks:   1 total,   0 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0,2 us,  0,1 sy,  0,0 ni, 99,7 id,  0,0 wa,  0,0 hi,  0,0 si,  0,0 st
MiB Mem :  11653,4 total,   9332,2 free,    949,2 used,   1372,0 buff/cache
MiB Swap:   4096,0 total,   4096,0 free,      0,0 used.  10418,1 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  10817 savalio+  20   0   24692  18216  10164 S   1,0   0,2   0:00.91 python3
```

top -p ```check_link_workers_5.py```
```sh
top - 03:51:53 up 1 day,  1:24,  2 users,  load average: 0,01, 0,03, 0,00
Tasks:   1 total,   0 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2,7 us,  5,0 sy,  0,0 ni, 89,1 id,  0,0 wa,  0,0 hi,  3,2 si,  0,0 st
MiB Mem :  11653,4 total,   8712,9 free,   1568,5 used,   1372,0 buff/cache
MiB Swap:   4096,0 total,   4096,0 free,      0,0 used.   9798,8 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  10857 savalio+  20   0 1090252 648984  10324 S  35,3   5,4   0:03.51 python3
```

top -p ```check_link_workers_10.py```
```sh
top - 03:53:21 up 1 day,  1:25,  2 users,  load average: 0,00, 0,02, 0,00
Tasks:   1 total,   0 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0,3 us,  0,3 sy,  0,0 ni, 99,2 id,  0,0 wa,  0,0 hi,  0,2 si,  0,0 st
MiB Mem :  11653,4 total,   8619,5 free,   1661,9 used,   1372,0 buff/cache
MiB Swap:   4096,0 total,   4096,0 free,      0,0 used.   9705,4 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  10910 savalio+  20   0 1477512 742264  10324 S   3,3   6,2   0:04.78 python3
```

top -p ```check_link_workers_100.py```
```sh
top - 03:54:00 up 1 day,  1:26,  2 users,  load average: 0,12, 0,05, 0,01
Tasks:   1 total,   0 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  4,3 us,  4,2 sy,  0,0 ni, 89,0 id,  0,0 wa,  0,0 hi,  2,5 si,  0,0 st
MiB Mem :  11653,4 total,   8483,4 free,   1797,8 used,   1372,3 buff/cache
MiB Swap:   4096,0 total,   4096,0 free,      0,0 used.   9569,4 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  10982 savalio+  20   0 3663408 852920  10760 S  33,3   7,1   0:10.75 python3
```

## CPU-bound
### Скорость выполнения
|Скрипт                     |Описание               |Время выполнения           |Загрузка процессора|
|---------------------------|-----------------------|---------------------------|-------------------|
|cpu_bound_original.py      |Оригинальный скрипт    |1 минута 40 секунд         |99%                |
|cpu_bound_workers_2.py     |Скрипт с 2 потоками    |52 секунды                 |128%               |
|cpu_bound_workers_4.py     |Скрипт с 4 потоками    |20 секунд                  |169%               |
|cpu_bound_workers_5.py     |Скрипт с 5 потоками    |34 секунды                 |185%               |
|cpu_bound_workers_10.py    |Скрипт с 10 потоками   |1 минута 50 секунд         |321%               |
|cpu_bound_workers_100.py   |Скрипт с 100 потоками  |42 секунды                 |278%               |

#### Время выполнения
time python3 cpu_bound_original.py
```sh
➜  urfu-python git:(master) ✗ time python3 cpu_bound_original.py
74423225562650041312300170970113131209039395861867 13113fe3bac6e7932a84be15daf00000
78138172162358727934152966672983355057834855559146 844d046af859ccee045b2dccb0400000
11883748626334330146885373773083414850372274317559 46d8b1975071a7e6dcf8929c79000000
46492724803931749239582807805961983933863683784614 4810a57fbffbb69563df67820bc00000
python3 cpu_bound_original.py  100,97s user 0,02s system 99% cpu 1:40,99 total
```

time python3 cpu_bound_workers_2.py
```sh
➜  urfu-python git:(master) ✗ time python3 cpu_bound_workers_2.py
76708917560096757037302428338733040715148185870172 5b12848d967f4850fac20ccd75a00000
57426170887149887365060905627578417571215709356238 f3d37558ccae46a6921fea2a41200000
26030898069907412916155323619241044811063934444637 ddef169c311935a1fd371680c8100000
47748341349189175560866729083168500237916885487734 1b694c6012f9e94251151f62dc000000
python3 cpu_bound_workers_2.py  68,00s user 0,02s system 128% cpu 52,745 total
```

time python3 cpu_bound_workers_4.py
```sh
➜  urfu-python git:(master) ✗ time python3 cpu_bound_workers_4.py
24070950331917384447270518636850155045498505415356 386a19c7637bd0bb303a360ebd900000
31734023993144854352752769480493848520723591823689 3515772604895c09fa84afcb21800000
96330793686991723387757283044942282101218952759140 8abab119a98a743e72461af2dff00000
65434396038454910651895696765728024197679707409300 73688b7d58d47b53cde9c48cc2300000
python3 cpu_bound_workers_4.py  34,93s user 0,02s system 169% cpu 20,592 total
```

time python3 cpu_bound_workers_5.py
```sh
➜  urfu-python git:(master) ✗ time python3 cpu_bound_workers_5.py
54080430552522238152679346613878285315045620791440 6bb50bbb6120a9311b99a8fec7a00000
88941087107383480707164440004718863409911969570557 16af81f3552490035853a6c756300000
34316102602067864976288744165255240311821562807928 aaad69433c1017293c355c653a600000
75886859368298821923118861741237405929546837214010 5252bc3c6e42638c44722e76d2a00000
python3 cpu_bound_workers_5.py  64,07s user 0,05s system 185% cpu 34,649 total
```

time python3 cpu_bound_workers_10.py
```sh
➜  urfu-python git:(master) ✗ time python3 cpu_bound_workers_10.py
83476063119009189426785335699400999047644305236988 3e68ac4e870b257a4cd7447434000000
36866113071182518162273910125579558996958349773534 b8b95d9ca06142b8397518e996a00000
42262889970252102310267938716825445590735699116587 f970379425038df919c7dacfc5100000
82925745199201683103941986630739671274202650564462 e8d813fce86b6f6dbc4c717374b00000
python3 cpu_bound_workers_10.py  352,37s user 0,10s system 321% cpu 1:49,58 total
```

time python3 cpu_bound_workers_100.py
```sh
➜  urfu-python git:(master) ✗ time python3 cpu_bound_workers_100.py
55058255388371854692631454958255261964408575673543 6e347c39d2ba8d0fda65081797f00000
87135191563600731837071011414069174456259492765011 39351db84f0906101b07ee516d100000
39330218151764654514345705621386825984454088757776 0ca6fb87533c0b4dfc23eb8619600000
45662512025733602333864487147825403216278697712477 51bc8f0be9c3dbc19a37cbafb4000000
python3 cpu_bound_workers_100.py  119,12s user 0,04s system 278% cpu 42,712 total
```