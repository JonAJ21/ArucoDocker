# Извлечение ARUCO меток с видеопотока

В данном модуле реализовано извлечение aruco меток с видеопотока. В дальнейшем идентификаторы меток передаются на  сервер для дальнейшей обработки.

- Язык программирования: C++
- Подключаемые библиотеки: opencv, boost-property_tree, zeroMQ

## Настройка

Настройка модуля происходит через файл config.json, который должен располагаться в одной директории с исполняемым файлом.

Параметры настройки:

### Сервер для отправки

```json
"Server" : {
    "IP" : IP adress,
    "port" : Port
}
```
