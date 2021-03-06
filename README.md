## Терминология
* Экспорт -- выгрузка на сайте или телефоне, содержащая транзакции с неполным набором полей
* Дамп -- выгрузка через API синхронизации, если указать serverTime=0
* Дифф -- наше сообщение, отправленное в API синхронизации
* Дельта -- изменения, полученные через API синхронизации

## Подготовка
* Запчасти
	* Взять транзакции из основной базы, залить в тестовую, собрать грабли
	* Удалить всё с тестового аккаунта (в том числе счета и категории)
	* Скачать дамп с тестового аккаунта, проверить, что всё удалилось
	* Залить на тестовый аккаунт счета и категории
	* Залить на тестовый аккаунт одну транзакцию, созданную вручную
	* Залить на тестовый аккаунт сразу несколько транзакций, созданных собственноручно
	* Удалить категории со слэшом и запятыми
	* Приклеивание id-шника к счёту
	* Приклеивание id-шника к категории
	* Приклеивание id-шника к категории со слешами
	* Получение списка id-шников к категории со слэшами и запятыми (категории могут иметь слеш, а могут не иметь)

* Скрипт прочистки категорий
	* Применить наработки на основной базе

* Скрипт заливки транзакций
	* На вход получает экспорт и дамп со счетами и категориями
	* Для каждой строки экспорта генерирует транзакцию для диффа
	* Если что-то идёт не так, делать raise Exception("Beda!!!")
	* Отправляем

	* Сделать D-дамп и применить на основной базе
	* Если что, у нас есть все данные и набор инструментов, чтобы всё восстановить

## Заметки
При заливке дампа нужно не плодить дубли

Формулировка задачи от 31.10

* уметь удалять всё
* уметь заливать из трёх источников (csv телефон, csv сайт, dump)
	* не создавать дубли, в т.ч. мерчантов, категорий, счетов
	* заливаем только те категории, которые есть в транзакциях этого дампа и их родителей - возможно, этого хватит, 
	если нет - надо разбираться, как при заливке привести в порядок категории со слешами и запятыми.
* уметь получать дамп

## TODO
* проверить на тестовом аккаунте заливку дампа с него же через tdfin (не будет ли дублей где-либо, нет ли проблем с неизменяемыми сущностями, не меняется ли после этого дамп)
* доделать нужную склейку дублей из csv
* сделать единый инструмент заливки
* залить данные в тестовую базу и разобраться, нужно ли при заливке дампа преобразовывать категории со слэшами