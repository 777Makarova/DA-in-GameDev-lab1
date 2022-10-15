# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Макарова Татьяна Сергеевна
- Институт опережающих технологий ДГТУ "Школа Икс", 4 курс
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
1. Создать новый проект из шаблона 3D-Core.
2. Проверить, что настроена интеграция редактора Unity и Visual Studio Code.
3. Создать объект Plane;
4. Создать объект Cube;
5. Создать объект Sphere;
6. Установить компонент Sphere Collider для объекта Sphere;
7. Настроить Sphere Collider в роли триггера;
8. Объект куб перекрасить в красный цвет;
9. Добавить кубу симуляцию физики, при этом куб не должен проваливаться под Plane;
10. Написать скрипт, который будет выводить в консоль сообщение о том, что объект Sphere столкнулся с объектом Cube;
11. При столкновении Cube должен менять свой цвет на зелёный, а при завершения столкновения обратно на красный.

Ход работы:
<img width="1080" alt="2022-10-15" src="https://user-images.githubusercontent.com/85516001/195996040-cb8fc1eb-1a63-4f76-b5e1-ad8095203970.png">
![Lab_1-SampleScene-Windows_-Mac_-Linux-Unity-2021 3 11f1-Personal_-_DX11_-2022-10-15-19-07-59](https://user-images.githubusercontent.com/85516001/195996663-07ddf1a8-6f03-489b-b385-8186977f3074.gif)


```py
 private void OnCollisionEnter(Collision other) {
        Debug.Log("Совершено столкновение с: " + other.gameObject.name);
        if (other.gameObject.name == "Cube"){
            other.gameObject.GetComponent<Renderer>().material.SetColor("_Color", Color.green);
        }
    }

    private void OnCollisionExit(Collision other) {
         Debug.Log("Завершено столкновение с: " + other.gameObject.name);
        if (other.gameObject.name == "Cube"){
            other.gameObject.GetComponent<Renderer>().material.SetColor("_Color", Color.red);
        }
```


#Show the effect of a scatter plot
plt.scatter(x,y)

```


## Задание 2
### Продемонстрируйте на сцене в Unity следующее: 
Что произойдёт с координатами объекта, если он перестанет быть дочерним?
Ход работы:
Координаты дочернего объекта зависят от координат родительского объекта (это можно видеть на скрине ниже) - его позиционирование в пространстве выстраивается от родительского объекта. Как только объект перестанет быть дочерним, его координаты рассчитываются относительно точки начала координат. С перемещением объекта координаты не меняются, но как только зависимость исчезает, они начинают меняться.

есть зависимость:
![image](https://user-images.githubusercontent.com/85516001/195996835-6888072e-75e7-4b46-8ef1-aaaef86dd9fd.png)

нет зависимости:
![image](https://user-images.githubusercontent.com/85516001/195997019-440824f2-1b8f-40e6-b271-d6b8555b2bea.png)


Создайте три различных примера работы компонента RigidBody:
Три примера работы RigidBody: IsKinematic, UseGravity и без них. Возьмем объект Куб и рассмотрим на его примере: 
- IsKinematic - объект не реагирует на физическое воздействие;
- UseGravity - на объект действует гравитация; 
- без всего - обычное твердое дело.
![Lab_1-SampleScene-Windows_-Mac_-Linux-Unity-2021 3 11f1-Personal_-_DX11_-2022-10-15-19-22-10](https://user-images.githubusercontent.com/85516001/195997357-2c0ea6b1-1900-4be2-a2ac-9661de0853ad.gif)



## Задание 3
### Реализуйте на сцене генерацию n кубиков. Число n вводится пользователем после старта сцены.

## Выводы

В ходе лабораторной работы я познакомилась с основными функциями Unity и взаимодействием с объектами внутри редактора.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
