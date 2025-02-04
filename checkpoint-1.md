# Стереокабачки - чекпоинт 1
## Задача: 
Стереозрение по двум камерам для определения геометрии объекта  
<img width="792" alt="image" src="https://github.com/user-attachments/assets/f152cee4-5afb-4c9e-a23c-5cadc47013c2">

## Команда

**Александр Смехнов** - Fullstack/CV/DL/PM  
**Айдар Рахматуллин** - CV/DL/MLE  
**Богдан Заволович** - MLE/Fullstack  
**Денис Кустов** - DL/Backend/MLE  
**Вячеслав Бендик** - CV/Backend  

github org: https://github.com/stereo-zucchini

## Что сделано сейчас
Мы искали инфу по решению подобных кейсов, нашли подходы как с классическим CV, так и с DL.

Найденные решения и источники:
http://vision.deis.unibo.it/~smatt/Seminars/StereoVision.pdf
[https://medium.com/@satya15july_11937/depth-estimation-from-stereo-images-using-deep-learning-314952b8eaf9](https://medium.com/@satya15july_11937/depth-estimation-from-stereo-images-using-deep-learning-314952b8eaf9)

## Потенциальное техническое решение:

1. Нам требуется сделать feature matching между двумя изображениями  
![image](https://github.com/user-attachments/assets/95417a8f-d4d1-4811-9184-1c615892a42a)
2. Затем используя информацию о положении объекта и камер рассчитываем дистанцию до замэтченных точек  
![image](https://github.com/user-attachments/assets/18831435-0613-4297-83dd-1078766fbe29)

## Продуктовое решение
1. Модель для построения карты глубины
2. Веб сервис с АПИ для процессинга изображений и операций с ними
3. Фронтенд для загрузки фото и операций со стороны человека

## Схема АПИ

0. По эндпоинту `/add_frame` загружаются кадры с камер про объект съемки, кадры сохраняются в хранилище.
1. По эндпоинту `/process_frame` запускается поиск карты глубины для фрейма(потенциально работает постоянный воркер)
2. По эндпоинту `/get_frame` получается карта глубины для фрейма и другая инфа

## Сценарий использования
0. Кадры с камер загружаются пользователем через веб приложение(потенциально в автоматическом режиме)
1. Пользователь может запустить поиск карты глубины(задача добавляется в очередь)
2. Пользователь может просмотреть информацию по фрейму(оба изображения и карту глубины)
3. В веб приложении есть визуализация depth image с инструментами измерений расстояний между точками 
