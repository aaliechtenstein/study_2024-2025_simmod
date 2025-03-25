---
## Front matter
lang: ru-RU
title: Лабораторная работа №8
subtitle: Модель TCP/AQM
author:
  - Лихтенштейн А.А.
institute:
  - Российский университет дружбы народов, Москва, Россия

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="60%"}

  * Лихтенштейн Алина Алексеевна
  * студентка
  * Российский университет дружбы народов
  * 1132229533@pfur.ru
  * <https://aaliechtenstein.github.io/ru/>

:::
::: {.column width="25%"}

:::
::::::::::::::

## Цель работы

Реализовать модель TCP/AQM в xcos и OpenModelica.

## Задание

1. Построить модель TCP/AQM в xcos;
2. Построить графики динамики изменения размера TCP окна $W(t)$ и размера очереди $Q(t)$;
3. Построить модель TCP/AQM в OpenModelica;

## Реализация в xcos

![Установка контекста](image/1.png){#fig:001 width=70%}

## Реализация в xcos

![Модель TCP/AQM в xcos](image/2.png){#fig:002 width=70%}

## Реализация в xcos

![Динамика изменения размера TCP окна W (t) и размера очереди Q(t)](image/3.png){#fig:003 width=70%}

## Реализация в xcos

![Фазовый портрет (W, Q)](image/4.png){#fig:004 width=70%}

## Реализация в xcos

![Динамика изменения размера TCP окна W (t) и размера очереди Q(t) при С = 0.9](image/5.png){#fig:005 width=70%}

## Реализация в xcos

![Фазовый портрет (W, Q) при С = 0.9](image/6.png){#fig:006 width=70%}

## Реализация модели в OpenModelica

```
parameter Real N=1;
parameter Real R=1;
parameter Real K=5.3;
parameter Real C=1;

Real W(start=0.1);
Real Q(start=1);

equation

der(W)= 1/R - W*delay(W, R)/(2*R)*K*delay(Q, R);
der(Q)= if (Q==0) then max(N*W/R-C,0) else (N*W/R-C);
```

## Реализация модели в OpenModelica

![Динамика изменения размера TCP окна W (t) и размера очереди Q(t). OpenModelica](image/7.png){#fig:007 width=70%}

## Реализация модели в OpenModelica

![Фазовый портрет (W, Q). OpenModelica](image/8.png){#fig:008 width=70%}

## Выводы

В процессе выполнения данной лабораторной работы была реализована модель TCP/AQM в xcos и OpenModelica.

## Список литературы

Королькова А.В., Кулябов Д.С. Моделирование информационных процессов
