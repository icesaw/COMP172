# NT8
### Техническое задание для написания индикатора на платформу Ninjatrader 8 
> ТЗ пока в разработке - ловлю возможные баги, настройки будут меняться не будут
#### Описание
Индикатор  представляет из себя "облегченный" фильтр кластеров обьема, т.е. мне не нужно рисовать весь кластерный график и каждый Cluster Profile в каждой свече, только фильтр обьемов в барах, не нужны ни вертикальный обьем ни гистограмы. 

#### Требования
- Индикатор должен исправно работать на последней версии Ninjatrader 8 (на 1.12.2019)
- Индикатор должен поставляться файлами с расширением .cs (сорцы), а не dll - это необходимо для последующей доработки индикатора в случае непредвиденных обстоятельств (несовместимость с клиентом, новая версия клиента Ninjatrader и проч. - а связь с разработчиком пропадет)
- Минимум графики - никаких обводок кластеров, градиентов и проч, чем меньше графики будет - тем лучше - и тем меньше будет нагрузка на клиент (будет грузиться история минимум 100 дней) - иначе Ninjatrader просто повиснет.
 - Индикатор должен работать на любом типе графика (Time, Tick, Volume - это набор минимум для требований)
 - В индикаторе должно быть минимум 5 фильтров - это нужно для того чтобы каждый раз не грузить индикатор по новой
 - Сам кластерный график не нужен вообще, нужны исключительно фильтры ценовых кластеров обьема по количеству баров по оси Y
 - После оплаты возможен исключительно фикс багов - доработка индикатора уже по договоренности.
 - Индикатор сугубо для личного пользования, поэтому надеюсь он не попадет в паблик, благодарю за понимание.
 
#### Описание индикатора

##### Пример окна настроек фильтра кластера

| Описание настроек для каждого фильтра | Значения |
| - | - |
| Filter On/Off | True/False | 
| Text | True/False |
| Font Color | |
| Volume | равно или больше 1 | 
| Color | | Цвет кластера |
| Opacity | 0-100 | 
| Bars Gap | равно или больше 0| 
| Alert | True/False |
| Sound | alert.wav |


> Пояснения к настройкам

- On/Off - Включение/выключение фильтра  (значения true/false)

- Text  - Включение/выключение текста цифрового значения всего суммированного кластера (значения true/false)

- Font Color - цвет текста (если включен)

- Volume - минимальный обьем который должен быть в кластере

- Color - Цвет кластера

- Opacity - Прозрачность кластера (от 0 до 100)

- Bars Gap (в барах) - Минимально допустимый гэп по количеству баров между рядом стоящими барами по цене Y для создания ценового кластера - если Bars Gap равен нулю то считает только бары подряд, если Bars Gap равен 1 то считает кластер с гэпом в 1 бар по оси Y - например 3 бара подряд 1 гэп + 2 бара подряд + все оставшиеся бары подряд по оси Y.

- Alert - Включение\Выключение алерта на прохождение Volume по условиям выше (значения true/false)

- Sound - звук алерта

Примерный внешний вид на NT7 (индикатор с ошибкой - кластера накладываются один на другой + не на всех барах подряд а только фиксированное количество баров или меньше)

http://prntscr.com/q5p0x3
http://prntscr.com/q5p1d7
http://prntscr.com/q5p1os

> Примечание

При наложении кластеров одного фильтра один на другой - их обьемы суммируются (за вычетом тех что наложились) и рисуется один кластер с общим обьемом. При наложении кластеров разных фильтров - кластера накладываются один на другой.

Т.к. фильтрует только объёмы по горизонтали, то высота кластера составит 1 тик.
