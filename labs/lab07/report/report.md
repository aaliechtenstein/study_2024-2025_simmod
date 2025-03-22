---
## Front matter
title: "Лабораторная работа №7"
subtitle: "Модель M|M|1|inf"
author: "Лихтенштейн Алина Алексеевна"
## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

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
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
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

Рассмотреть пример моделирования в *xcos* системы массового обслуживания типа $M|M|1|\infty$.

# Задание

1. Реализовать модель системы массового обслуживания типа $M|M|1|\infty$;
2. Построить график поступления и обработки заявок;
3. Построить график динамики размера очереди.

# Выполнение лабораторной работы

Зафиксируем начальные данные: $\lambda = 0.3, \, \mu = 0.35, \, z_0 = 6$. В меню Моделирование, Установить контекст зададим значения коэффициентов (рис. [-@fig:001]).

![Задание переменных окружения в xcos для модели](image/1.png){#fig:001 width=70%}

Суперблок, моделирующий поступление заявок, представлен на рис. [-@fig:002]. Заявки поступают в систему по пуассоновскому закону. Сначала заявка поступает в суперблок, затем идет в синхронизатор входных и выходных сигналов, происходит равномерное распределение на интервале $[0; 1]$ (также заявка идет в обработчик событий), далее идет преобразование в экспоненциальное распределение с параметром $\lambda$, затем заявка опять попадает в обработчик событий и выходит из суперблока.

![Суперблок, моделирующий поступление заявок](image/2.png){#fig:002 width=70%}

Суперблок, моделирующий процесс обработки заявок, представлен на рис. [-@fig:003]. В нем происходит обработка заявок в очереди по экспоненциальному закону.

![Суперблок, моделирующий обработку заявок](image/3.png){#fig:003 width=70%}

Готовая модель$M|M|1|\infty$ представлена на рис. [-@fig:004]. Она состоит из селектора, двух суперблоков, первоначального события на вход в суперблок, суммирования, оператора задержки (имитация очереди) и регистрирующих блоков: регистратора размера очереди и регистратора событий.

![Модель $M|M|1|\infty$ в xcos](image/4.png){#fig:004 width=70%}

Результат моделирования представлен на рис. [-@fig:005] и [-@fig:006]. График динамики размера очереди начинается со значения 6, так как мы указали $z_0 = 6$.

![Динамика размера очереди](image/5.png){#fig:005 width=70%}

![Поступление и обработка заявок](image/6.png){#fig:006 width=70%}

# Выводы

В процессе выполнения данной лабораторной работы был рассмотрен пример моделирования в *xcos* системы массового обслуживания типа $M|M|1|\infty$.

# Список литературы

 Королькова А.В., Кулябов Д.С. Моделирование информационных процессов
