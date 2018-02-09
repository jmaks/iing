iing
====

iing — нода для idec-сетей нового поколения.

Нода поддерживает следующие стандарты и расширения:
  * метод /e;
  * метод /m;
  * метод /u/e (включая сокращённый индекс);
  * метод /u/m;
  * метод /u/point;
  * метод /x/c;
  * метод /list.txt;
  * метод /blacklist.txt;
  * метод /x/features;
  * метод /x/file;
  * метод /x/small-echolist;
  * метод /x/caesium (возвращает список эхоконференций в формате конфига для клиента caesium);
  * метод /f/e;
  * метод /f/f;
  * метод /f/p;
  * новый формат цитирования (с подстановкой имени или инициалов);
  * имена эхоконференций без индекса (точка в имени по прежнему обязательна);

При каждом запуске нода проверяет наличие всех необходимых директорий и файлов и, в случае отсутствия каких-либо позиций, создаёт их.

Конфигурирование
----------------

Пример файла конфигурации находится в iing.def.cfg и копируется в iing.cfg в случае отсутствия последнего. Формат файла очень простой: первое слово является ключом, в вся остальная строка — значением. Все строки, первые слова которых не являются ключевыми игнорируются при разборе.

Список ключей:
  * nodename: имя ноды, которое будет проставляться в поле адреса и отображаться в заголовке веб-интерфейса;
  * nodedsc: строчка-описание ноды;
  * nodeurl: URL ноды для использования в RSS;
  * echo: эхоконференция; данный параметр является составным: первое слово значения является названием эхоконференции, а остальная строка — её описанием;
  * fecho: файлэхоконференция; параметр задаётся аналогично параметру echo;
  * webinterface: включение/отключение веб-интерфейса ноды. Если параметр выставлен в 1 или не задан, то веб-интерфейс доступен. Во всех остальных случаях, он выключен;
  * background: имена графических файлов в директории lib/, разделённые запятой, которые будут выставляться в качестве фона страницы;
  * norobots: не имеет параметров; запрещает индексацию роботам поисковых систем;
  * registration: не имеет параметров; разрешает регистрацию поинтов через веб-интерфейс;
  * nosubscription: при наличии данного ключевого слова подписки в веб-интерфейсе не работают и список конференций берётся напрямую из конфига ноды.

Фетчинг
-------

В директории tools/ есть фетчер. Для его работы необходимы конфигурационные файлы схожего с файлом конфигурации ноды формата.

Список ключей:
  * node: адрес ноды для взаимодействия со слешем в конце (для php-ноды он будет представлять собой что-то вроде http://node.example/ii-point.php?q=/);
  * echo: название эхоконференции (без описания);
  * fecho: название файлэхоконференции (без описания);
  * auth: строка авторизации (необходима для файлэх).

Фетчер необходимо вызывать из корневой директории iing с указанием файла конфигурации в качестве параметра. Например,

  $ ./fetcher.py -f ./mira.cfg

points.txt
----------

Формат файла, в котором хранится информация о поинтах следуюший:

hash:authstr:username:point, где

  * hash: хеш из логина и пароля для веб-интерфейса (см. функцию hsh(str) из points.py);
  * authstr: строка авторизации для работы клиента;
  * username: имя поинта;
  * point: номер поинта.

Номер поинта может быть произвольным. Это учитывается при автоматической подстановке номера и скрипт исключает коллизии.

Для добавления поинта можно зайти на веб-интерфейс ноды и зарегистрироваться при включенном параметре registration или запустить points.py

  $ ./points.py -u <username> -p <password>

Так же в points.txt имеется возможность устанавливать флаги для поинтов. Делается это добавлением пятого столбца к записи с перечислением флагов через запятую. На данный момент нода поддерживает только флаг "OP", включающий в веб-интерфейсе для этого поинта возможность удаления и помещения в чёрный список сообщение одной кнопкой.
