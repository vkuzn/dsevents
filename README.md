# Дополнительное задание

## Описание

Требуется разработать программу dsevents, которая принимает на вход описание 
модели распределённой системы (РС) и выводит список событий. В зависимости от 
указанных параметров, программа должна выводить соответствующий список событий.

Параметры программы:
1) past <EventID>, выводит множество событий прошлого для указанного события;
2) future <EveentID>, выводит множество событи будущего;
3) concurrent <EventID>, выводит множество параллельных событий.

Описание модели РС представляет собой JSON-файл следующей структуры:
1) Processes - массив структур, описывающих процессы. 
   Процесс описывается одним полем ID - ид-р процесса;
2) Channels - массив структур, описывающих каналы взаимодействия.
   Канал описывается полями "ID" - ид-р канала, 
   From - ид-р процесса отправителя,
   To - ид-р процесса получателя;
3) Messages - массив структур, описывающих пересылаемые сообщения.
   Сообщение описывается одним полем ID - ид-р сообщения;
4) Events - массив структур, описывающих события.
   Событие описывается полями ID - ид-р события,
   ProcessID - ид-р процесса, в котором происходит событие,
   Seq - порядковый номер среди других событий процесса,
   ChannelID - ид-р канала взаимодействия,
   MessageID - ид-р пересылаемого сообщения,
   ChannelID и MessageID имеют значение null для внутренних событий.

Ввод и вывод осуществляется через стандартные потоки Input/Output.
Разработка: язык C#, платформа .Net Core 3.1

## Пример

Файл model.json содержит пример описания модели распределённой системы (рис. 1).

![alt Рисунок 1](https://github.com/vkuzn/dsevents/blob/master/diagram.gif?raw=true)

Запуск программы

$ dsevents past e2_3 < model.json
e1_1 e1_2 e2_1 e2_2

$ dsevents future e2_3 < model.json
e2_4 e1_4

$ dsevents concurrent e2_3 < model.json
e3_1 e2_2 e1_3
