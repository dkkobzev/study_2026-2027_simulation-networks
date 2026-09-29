---
## Front matter
title: Лабораторная работа
subtitle: Номер 3
author: "Кобзев Д. К."

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: /home/dkkobzev/pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
    - spelling=modern
    - babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: Liberation Serif
romanfont: Liberation Serif
sansfont: Liberation Sans
monofont: Liberation Mono
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9

## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Целью данной работы является знакомство с инструментом для измерения пропускной способности сети в режиме реального времени — iPerf3, а также получение навыков проведения воспроизводимого эксперимента по измерению пропускной способности моделируемой сети в среде Mininet.

# Выполнение лабораторной работы

В каталоге /work/lab_iperf3 для работы над проектом создаем подкаталог lab_iperf3_topo и копируем в него файл с примером скрипта mininet/examples/emptynet.py, описывающего стандартную простую топологию сети mininet.
Запускаем скрипт создания топологии lab_iperf3_topo.py.
После отработки скрипта смотрим элементы топологии и завершаем работу mininet(Рис. 1.1).

![Создание простейшей топологии сети](image/1.png){height=60%}

Вносим в скрипт lab_iperf3_topo.py изменение, позволяющее вывести на экран информацию о обоих хостах.
Проверяем корректность отработки изменённого скрипта (Рис. 1.2).

![Информация о хостах](image/2.png){height=60%}

Делаем копию скрипта lab_iperf3_topo.py.
В начале скрипта lab_iperf3_topo2.py добавляем записи об импорте классов CPULimitedHost и TCLink.
Изменяем строку описания сети, указав на использование ограничения производительности и изоляции.
Изменяем функцию задания параметров виртуального хоста h1, указав, что ему будет выделено 50% от общих ресурсов процессора системы. Аналогичным образом для хоста h2 задаем долю выделения ресурсов процессора в 45%. 
Изменяем функцию параметров соединения между хостом h1 и коммутатором s3 (Рис. 1.3), (Рис. 1.4).

![lab_iperf3_topo2.py](image/3.png){height=60%}

![Скрипт с функциями ограничения производительности и изоляции](image/4.png){height=60%}

Строим графики по проводимому эксперименту. Делаем копию скрипта lab_iperf3_topo2.py и поместите его в подкаталог iperf (Рис. 1.5).

![Копия скрипта lab_iperf3_topo2.py](image/5.png){height=60%}

Изменяем код в скрипте lab_iperf3.py так, чтобы:
– на хостах не было ограничения по использованию ресурсов процессора;
– каналы между хостами и коммутатором были по 100 Мбит/с с задержкой 75 мс, без потерь, без использования ограничителей пропускнойспособности и максимального размера очереди.
– После функции старта сети описываем запуск на хосте h2 сервера iPerf3, а на хосте h1 запуск с задержкой в 10 секунд клиента iPerf3 с экспортом результатов в JSON-файл, комментируем строки, отвечающие за запуск CLI-интерфейса (Рис. 1.6).

![lab_iperf3.py](image/6.png){height=60%}

Запускаем на отработку скрипт lab_iperf3.py.
Строим графики из получившегося JSON-файла.
Создаем Makefile для проведения всего эксперимента (Рис. 1.7).

![Построение графиков](image/7.png){height=60%}

В Makefile прописываем запуск скрипта эксперимента, построение графиков и очистку каталога от результатов.
Проверяем корректность отработки Makefile.
Завершаем соединение с виртуальной машиной mininet и выключите её (Рис. 1.8).

![Makefile](image/8.png){height=60%}

# Выводы

В результате выполнения лабораторной работы я был знакомлен с инструментом для измерения пропускной способности сети в режиме реального времени — iPerf3, а также получил навыки проведения воспроизводимого эксперимента по измерению пропускной способности моделируемой сети в среде Mininet.

# Список литературы{.unnumbered}
