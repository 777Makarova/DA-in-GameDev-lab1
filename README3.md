# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
Интеграция интерфейса пользователя в разрабатываемое интерактивное приложение.

## Задание 1
### Используя видео-материалы практических работ 1-2 повторить реализацию игровых механик.

Ход работы: 

1. Реализация механизма ловли объектов

Написание скрипта, реализующего перемещение игрового объекта EnergyShield влед за указателем мыши:
```py
public class EnergyShield : MonoBehaviour
{
    void Update()
    {
        Vector3 mousePos2D = Input.mousePosition;
        mousePos2D.z = -Camera.main.transform.position.z;
        Vector3 mousePos3D = Camera.main.ScreenToWorldPoint(mousePos2D);
        Vector3 pos = this.transform.position;
        pos.x = mousePos3D.x;
        this.transform.position = pos;
        
    }
}
```
![Lab_2 - SampleScene - WebGL - Unity 2021 3 11f1 Personal _DX11_ 2022-10-19 14-28-07_Trim](https://user-images.githubusercontent.com/85516001/196681678-8748a98c-7a77-4248-9ba6-b0347b518b48.gif)


Добавление метода OnCollisionEnter, позволюящего реализовать ловлю объектов Dragon Eggs, и Canvas:
```py
 private void OnCollisionEnter(Collision coll) {
        GameObject Collided = coll.gameObject;
        if (Collided.tag == "Dragon Egg"){
            Destroy(Collided);
        }
    }
```
![Lab_2 - SampleScene - WebGL - Unity 2021 3 11f1 Personal_ _DX11_ 2022-10-19 14-40-18_Trim](https://user-images.githubusercontent.com/85516001/196682113-f0dcbbb9-3324-45f2-a6ab-76cf2692db23.gif)

2. Реализация графического интерфейса с добавлением счетчика очков:
2.1. Реализация функционала для отображения счетчика очков путем дополнения метода OnCollisionEnter. Написание метода Start и добавление библиотеки TMPro:
```py
using TMPro;

public class EnergyShield : MonoBehaviour
{
    public TextMeshProUGUI scoreGT;
     void Start()
    {
        GameObject scoreGO = GameObject.Find ("Score");
        scoreGT = scoreGO.GetComponent<TextMeshProUGUI>();
        scoreGT.text = "0";
    }

 private void OnCollisionEnter(Collision coll) {
        GameObject Collided = coll.gameObject;
        if (Collided.tag == "Dragon Egg"){
            Destroy(Collided);
        }
        int score = int.Parse(scoreGT.text);
        score += 1;
        scoreGT.text = score.ToString();
    }
 ```
 ![Lab_2 - SampleScene - WebGL - Unity 2021 3 11f1 Personal_ _DX11_ 2022-10-19 14-58-59_Trim](https://user-images.githubusercontent.com/85516001/196685029-6c7ab501-aedc-447c-93f9-622c13b3964e.gif)

2.2. В скрипт DragonEgg добавим условие, которое будет перезапускать сцену при ловле объекта:
```py
void Update()
    {
        if (transform.position.y < bottomY){
            Destroy(this.gameObject);
            DragonPicker apScript = Camera.main.GetComponent<DragonPicker>();
            apScript.DragonEggDestroyed();
        }       
    }
  
```
2.3. Также допишем скрипт файл Dragon Picker, добавим метод, к которому обращались в скрипте DragonEgg:
```py
public void DragonEggDestroyed(){
     GameObject[] tDragonEggArray = GameObject.FindGameObjectsWithTag("Dragon Egg");
     foreach (GameObject tGO in tDragonEggArray){
         Destroy(tGO);
     }
    }
```

![Lab_2 - SampleScene - WebGL - Unity 2021 3 11f1 Personal_ _DX11_ 2022-10-19 15-18-07](https://user-images.githubusercontent.com/85516001/196689089-4adf5370-2907-418e-b75c-cec098f09e6f.gif)


## Задание 2
### Используя видео-материалы практических работ 3-4 повторить реализацию игровых механик;

3. Уменьшение жизни. Добавление текстур

## Задание 3

## Выводы

В ходе лабораторной работы я cоздала интерактивное приложение и изучила принципы интеграции в него игровых сервисов.

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
