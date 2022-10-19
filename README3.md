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

1. Написание скрипта, реализующего перемещение игрового объекта EnergyShield влед за указателем мыши:
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

2. Работа над графическоим интерфейсом:
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


3. Создала новый проект из шаблона 3D-Core.
4. Импортировала asset Dragon for Boss Monster в проект через Project Manager.
5. Скопировала анимацию FlyIdle, создала AnimationController.
6. Создала сферу, поменяла ее параметры и добавила материал. Добавила ей RigidBody, сохранила как префаб DragonEgg.
7. Изменила положение камеры.
8. Создала игровой скрипт для перемещения дракона

```py
 public class EnemyDragon : MonoBehaviour{
 
 public GameObject dragonEggPrefab;
 public float speed = 1;
 public float timeBetweenEggDrops = 1f;
 public float leftRightDistance = 10f;
 public float chanceDirection = 0.1f;

void Update(){

  Vector3 pos = transform.position;
  pos.x += speed * Time.deltaTime;
  transform.position = pos;

  if (pos.x < -leftRightDistance){
      speed = Mathf.Abs(speed);
    } 
  else if (pos.x > leftRightDistance){
      speed = -Mathf.Abs(speed);
    }
}

private void FixedUpdate() {
  if (Random.value < chanceDirection){
     speed *= -1;
   }
}

```
![Lab_2-SampleScene-Windows_-Mac_-Linux-Unity-2021 3 11f1-Personal_-_DX11_-2022-10-15-16-48-56_Trim](https://user-images.githubusercontent.com/85516001/195998188-8b2a6cc9-567d-419e-9acf-6af387b55e47.gif)

7. Написала функцию DropEgg, скачала asset Fire & Spell для визуального оформления.
```py
void Start(){
   Invoke("DropEgg", 2f);
}
  
void DropEgg(){
  Vector3 myVector = new Vector3(0.0f, 5.0f, 0.0f);
  GameObject egg = Instantiate<GameObject>(dragonEggPrefab);
  egg.transform.position = transform.position + myVector;
  Invoke("DropEgg", timeBetweenEggDrops);
}
 ```
![image](https://user-images.githubusercontent.com/85516001/195998280-8676a530-95a7-4ed9-88b3-1d83a1ae180c.png)


8. Написала скрипт для генерации EnergyShield:
```py
public class DragonPicker : MonoBehaviour{

  public GameObject energyShieldprefab;
  public int numEnergyShield = 3;
  public float energyShieldBottomY = -6f;
  public float energyShieldRadius = -1.5f;
  
void Start(){

 for (int i = 1; i < numEnergyShield; i++){
    GameObject tShieldGo = Instantiate<GameObject>(energyShieldprefab);
    tShieldGo.transform.position = new Vector3(0, energyShieldBottomY, 0);
    tShieldGo.transform.localScale = new Vector3(1*i, 1*i, 1*i);
  }
}
```

Итоговый результат:
![Lab_2-SampleScene-Windows_-Mac_-Linux-Unity-2021 3 11f1-Personal-_DX11_-2022-10-15-17-29-39_Trim](https://user-images.githubusercontent.com/85516001/195998828-35881dff-8337-4706-8b98-1b71640b5173.gif)




## Задание 2
### В проект, выполненный в предыдущем задании, добавить систему проверки того, что SDK подключен (доступен в режиме онлайн и отвечает на запросы);

1. Собранный проект на WebGL.
![image](https://user-images.githubusercontent.com/85516001/195998458-8ccd396c-c06b-4174-83e0-5152ad5b02b5.png)

2. Проект запущен на localhost:
![image](https://user-images.githubusercontent.com/85516001/195998517-8008dacf-e9b1-4670-914f-e1a760e6765e.png)

3. Яндекс Игры Dragon Picker:
![image](https://user-images.githubusercontent.com/85516001/195998541-6b2fe295-db3f-42b2-9f28-cdcb3c8f9776.png)



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
