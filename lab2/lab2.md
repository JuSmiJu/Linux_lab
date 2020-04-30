# Отчет по лабораторной работе №2
## **Задание 1**
Тут просто показаны параметры, которые проставили (диски называются ssd3,ssd4 потому что я немного косяк и мне пришлось делать все с самого начала ХЕХ)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/1.jpg)

Вот мы начинаем настраивать нашу ОС. Изначально у нас два пустых SSD диска

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/2.png)

Выделили место под таблицу разделов, присволили sda '/boot', настроили RAID

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/7.jpg)

Дальше перешли к настройке LVM (система, позваляющая создавать логические тома)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/3.png)

Сделали разметку отделов (var, log, root)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/8.jpg)

После копирования раздела /boot с sda на sdb мы можем видеть такое дерево

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/5.png)

Результаты команд 'cat /proc/mdstat' (выводит инфу о RAID)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/6.png)

### *Микро вывод по заданию*
Мы настроили с нуля нашу систему, и перенесли данные с одного диска на другой, тем самым получили RAID1

## **Задание 2**
После удаления SSD1 у нас остается только один рабочий диск

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/9.jpg)

В настройках ВМ добавляем один новый SSD и проверем все ли нормально 'fdisk -l'. Disk /dev/sda: 6 Gib означает, что диск полностью пустой

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/10.jpg)

После копирования таблицы разделов мы видим, что свободная память уменьшилась 

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/11.jpg)

Добавили новый диск в RAID массив '--manage /dev/md0 --add /dev/sdb2' 

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/12.jpg)

Скапируем данные с sda1 на sdb1 и с sda2 на sdb2 

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/13.jpg)

После перезагрузки у нас все работает и дерево выглядит так:

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/14.jpg)

### *Микро вывод по заданию*
Мы удалили один диск, и добавили новый, для восстановления RAID массива. Скапировали данные со старого диска на новый и у нас все работает :)

## **Задание 3**
Представим, что мы такие косячные и у нас плетел опять диск

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/15(3).jpg)

Но мы такие умненькие и добавим новый диск чуть побольше объема (7,5 Gib)

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/16.jpg)

Мы скопировали данные со старого диска на новый, но /boot не перенесся

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/17.jpg)

Для того, чтобы перенести /boot на новый диск нам сначала нужно установить загрузчик и создать новый RAID массив. И если мы выведем дерево, то увидим, что /boot перешел на второй диск

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/18.jpg)

Теперь буедем настраивать LVM. Создадим на новом диске новый физ том

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/19.jpg)

Увеличим размер Volume Group system и увилим, что свободное место у md63 увеличилось, но пока var, log и root находятся на sda

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/20.jpg)

Перенесем var, log, root на новый диск 

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/21.jpg)

И если мы выведем дерево, то увидим, что все перенеслось

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/22.jpg)

В конечном счете у нас на диске sda не осталось смонтированных элементов

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/23.jpg)

Вот мы опять удлили диск, и добавили 1 SSD и 2 HDD

![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/24.jpg)

 Востановим RAID массив, скопируя таблицу разделов на новый SSD
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/25.jpg)
 
 Перенесем загрузочный раздел со старого диска на новый
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/26.jpg)
 
 Увеличим размер второго раздела
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/29.jpg)
 
 Расширим размер RAID (размер md127 увеличился)
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/30.jpg)
 
 Но разер LV не изменился, поэтому мы его сами расширим
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/31.jpg)
 
 Распределим место между разделами (Там небольшой косяк, но я его справила)
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/32.jpg)
 
 Будем переносить /var/log на HDD диски. Создадим новый RAID массив, там создадим новый PV, в нем создадим группу и дадим все свободное простанство. Проверим все с помощью lvs
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/33.jpg)
 
 Отформатируем раздел в ex4 
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/34.jpg)
 
 Перенесем данные логов со старого раздела на новые, выполним синхронизацию и увидим, что у нас все получилось
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/35.jpg)
 
 В конце мы перезагрузим нашу ВМ и убедимся, что у нас все работает. Выведем данные о системе
 
 ![](https://github.com/JuSmiJu/laba/blob/master/lab2/photo/36.jpg)
 
 #### Это было сложно, но я справилась:) Выполняя эту лаботаторную, я научилась настраивать ОС с нуля, если полетит один из дисков в RAID массиве, я теперь знаю как перенести данные с уцелевшего на новый и восстановить массив.
