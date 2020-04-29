# Отчет по лабораторной работе №2
## **Задание 1**
Тут просто показаны параметры, которые проставили (диски называются ssd3,ssd4 потому что я немного косяк и мне пришлось делать все с самого начала ХЕХ)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/1.jpg)

Вот мы начинаем настраивать нашу ОС. Изначально у нас два пустых SSD диска

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/2.png)

Выделили место под таблицу разделов, присволили sda /boot, настроили RAID

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/7.jpg)

Дальше перешли к настройке LVM (система, позваляющая создавать логические тома)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/3.png)

Сделали разметку отделов (var, log, root)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/8.jpg)

После копирования раздела /boot с sda на sdb мы можем видеть такое дерево

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/5.png)

Результаты команд cat /proc/mdstat (выводит инфу о RAID)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/6.png)

### *Микро вывод по заданию*
Мы настроили с нуля нашу систему, и перенесли данне с одного диска на другой, тем самым получили RAID1

## **Задание 2**
