# DPP-Fight-Bees
###  Ссылка на репозиторий: [https://github.com/Timur-ux/DPP-Fight-Bees](https://github.com/Timur-ux/DPP-Fight-Bees)
### Что сделано:
Написано два dockerfile для сборки образа, и docker-compose.yml для простого запуска контейнеров.

### Для запуска необходимо:
```

git clone git@github.com:JonAJ21/ArucoDocker.git
cd ArucoDocker
sudo docker compose build
sudo docker compose up

```

### Замечания:
#### ArucoDistance
У контейнера есть доступ к камере и дисплею host системы.
Отлично работает на OS Ubuntu 22.04. Но перед запуском контейнера надо дать доступ к дисплею с помощью следующей команды:
```
xhost +local:docker
```
Могут возникнуть сложности при запуске на Windows 10, используя WSL: 
1. Чтобы использовать камеры в WSL дать доступ к usb устройствам, подключенным к host ПК и модифицировать ядро.
(https://www.youtube.com/watch?v=t_YnACEPmrM&t=2s&ab_channel=AgileDevArt)
2. У меня камеры в WSL заработали только при разрешении 320x240 и 5 fps. Из-за этого для работы камеры в OpenCV приходилось писать следующий код:
```
cap = cv2.VideoCapture(0)
cap.set(cv2.CAP_PROP_FOURCC, cv2.VideoWriter_fourcc('M', 'J', 'P', 'G'))
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 320)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 240)
cap.set(cv2.CAP_PROP_FPS, 5) 
```
3.  Полностью протестировать работу ArucoDistance.py из-за непонимания процесса калибровки камер.
#### FetchingArucoMarks
1. Подключаются все библиотеки, используемые для сборки проекта. 
2. Для подключения ZeroMQ в CMake при поиске надо прописывать
```
find_package(cppzmq REQUIRED)
```
вместо
```
find_package(ZeroMQ REQUIRED)
```
Т.к. по каким-то причинам СMake не может найти библиотеку ZeroMQ с таким названием.

3. Образ не соберется.  (При компиляции появляются ошибки, связанные с vtable, вероятно из-за отсутствующей реализации методов классов). 
4. Пока не подключена библиотека boost-property_tree, т.к. она не используется в исходниках.
5. Такие же проблемы с камерой в WSL как для ArucoDistance

### Что остается сделать:
1. Проброс порта, через который к этому контейнеру можно будет обратиться
2. Дать доступ к файлу конфигурации config.json
3. Пробросить порты для брокера сообщений.
