# Blueprint Home Assistant MiButton Remote

## Описание
Управление светом в Home Assistant с помощью беспроводной кнопки Xiaomi Mi Wireless Switch (YTC4040GL) и датчика двери / движения.
Система включает и выключает свет по кнопке, датчику и таймеру, а также наблюдает за остаточным временем.

## Управление кнопкой:

одиночное нажатие: включает свет на короткое время / выключает
двойное нажатие: включает свет на среднее время или увеличивает яркость на 100%, если свет уже включен
тройное нажатие: включает свет на долгое время
четырехкратное нажатие: включает / уменьшает свет до 1% на 1 минуту
многократное: настраиваемое
удержание: добавляет / убавляет яркость

## Управление (сбработка) по датчику открытия / движения (sensor detect 1,2):
свет выключен: включает свет на короткое время
время таймера ниже time detect (в минутах) тогда сработавший датчик перезапускает таймер на короткое время
(пример: time detect=3 мин., на таймере 2 минуты, перезапустит таймер на время Short)

## АВТО Включение света , когда 1 и 2 бинарные сенсоры в состоянии /on/, а 3 бинарный сенсор /off/
(пример: удобно использовать бинарные TOD - это время суток - день/ночь, обнатный сенсор нужен для корретной работы датчиков освещенности (Светло = off).
Если первые два дали on, а третий off, то свет будет включаться по первому датчику (движения, открытия ...) 

## Выключение света по времени отсутствия движения / открытия time Inactivity (No motion)
(пример: Датички не фиксируют движения и находятся в состоянии off - в Х минутах - выключаем свет.


# Требования
Создать таймер
обеспечить 2 датчиками detect 1 и 2 (движения, открытия)
Обеспечить 3 датчиками tod 1, 2, off


бинарными сенсорами 


# Пример автоматизации
alias: Свет. Управление светом в Коридоре
description: Управление светом в Коридоре
use_blueprint:
  path: MrSnake/Light Remote MiButton.yaml
  input:
    switch: binary_sensor.soff_t1_hall_touch_2
    button: binary_sensor.soff_t1_hall_touch_2
    detect_1: binary_sensor.ble_motion_night_light
    detect_2: binary_sensor.rec_pult_button_3
    boolean_start: true
    time_detect: 1
    tod1: binary_sensor.ble_motion_night_light
    tod2: binary_sensor.tod_full_night
    todoff: light.hallway_light1
    boolean_off: false
    time_no_motion: 5
    time_short: "00:01:00"
    time_medium: "00:10:00"
    time_long: "00:30:00"
    timer: timer.svet_hallway2
    light_1: light.hallway_light2

