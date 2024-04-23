Для https://github.com/Timur-ux/DPP-Fight-Bees
Было написано два dockerfile для сборки образа, и docker-compose.yml для запуска контейнеров
1. ArucoDistance
Модуль, отвечающий за расчет расстояния до Aruco меток. С помощью докер теперь можно запускать программу.
У докер контейнеру есть доступ к камере и дисплею копьютера, на котором он запускается.
Отлично работает на OS Ubuntu 22.04.
Еслии возникли проблемы при связке дисплеев докера и вашей ОС, то поможет команда:
xhost +local:docker (она прописывается в консоли вашей ОС)
Возникают сложности при запуске на Windows 10 при помощи WSL:
Для подключения камер к WSL надо модифицировать ядро:
См. видео: https://www.youtube.com/watch?v=t_YnACEPmrM&t=2s&ab_channel=AgileDevArt
+ Лично у меня, камера заработала только в разрешении 320x240 и 5 FPS
Из-за этого чтобы работала камера в OpenCV приходилось прописывать следующие команды:
'''
# Capture video from camera
cap = cv2.VideoCapture(0)

# Without these settings my camera does not work
cap.set(cv2.CAP_PROP_FOURCC, cv2.VideoWriter_fourcc('M', 'J', 'P', 'G'))
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 320)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 240)
cap.set(cv2.CAP_PROP_FPS, 5)
'''
