# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил:
- Лысиков Дмитрий Александрович
- РИ-220948

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Цель работы
Научиться работать с даннами из  Google Sheets с помощью Python и передавать их в Unity.

### Задание 1
### Выберите одну из компьютерных игр, приведите скриншот её геймплея и краткое описание концепта игры. Выберите одну из игровых переменных в игре (ресурсы, внутри игровая валюта, здоровье персонажей и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.

### Игра: "Marvel's Spider-Man PlayStation 4"
![1670809462_276-1669580109-936558060](https://github.com/DmitryLysikov/ANALIZDAN2/assets/129677338/cf7166e1-29b3-4d18-ae2d-4b527c30bec8)


Ход работы:
- Кратко описать концепт игры, выбрать игровую переменную, описать её характеристики и роль в игре и построить экономическую модель игры.

Описание концепта игры.
- "Marvel's Spider-Man PlayStation 4" - это игра, в которой игроки играют за главного героя Питера Паркера, который должен защитить свой город от супер-злодеев, которые пытаются захватить город. Игроки могут управлять своим персонажем, выбирать атаки и использовать способности, чтобы уничтожать врагов и защищать свой город.Tакже включает в себя различные сюжетные события и квесты, которые игроки могут выполнять, чтобы пройти уровни и достичь своих целей.

Рассмотрим одну из игровых переменных в игре.
- Игровая валюта (жетоны "спайдера"). Основной ресурс в игре.
  
- Валюта может использоваться для:
  основной ресурс для создания костюмов, модификаций и гаджетов.

- Жетоны рюкзака. Эти жетоны откроются вам одними из самых первых. По всему городу наш Человек-паук разбросал 55 рюкзаков с памятными предметами.

- Жетоны достопримечательностей. Самый простой вид жетонов, который только можно придумать. Всего есть 50 достопримечательностей, все они отмечены на карте. Вам нужно сделать фотографию каждого из них. 

- Жетоны преступлений. Еще одни жетоны, доступные Питеру практически с самого начала игры. Вы получите их, расправляясь с бандитами и другими асоциальными элементами на улицах Манхэттена.
- Научные жетоны в Spider-Man можно получить целыми тремя способами. Первый и самый очевидный - выполнить все дополнительные задачи в лаборатории Октавиуса.
- Жетоны испытаний. Эти жетоны - одни из самых ценных в Spider-Man. Берегите их и не тратьте просто так. Разблокируются они ближе к середине игры вместе с испытаниями Бригадира.
- Жетоны баз. Еще один вид жетонов, которые достаточно долго выбивать. К концу игры вам будет доступно четыре вида баз: тайники Фикса, лагеря заключенных, склады "Демонов" и блокпосты "Соболя".

Схема экономической модели в игре.
Игровая валюта занимает очень важную роль в модели, поэтому я расположил её в центре.
![amp_poster](https://github.com/DmitryLysikov/ANALIZDAN2/assets/129677338/16113a6e-bdc6-4526-a636-77ad8478117e)



### Задание 2
### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в выбранной игре (в качестве таких переменных может выступать игровая валюта, ресурсы, здоровье и т.д.). Средствами google-sheets визуализируйте данные в google-таблице (постройте график, диаграмму и пр.) для наглядного представления выбранной игровой величины.

Ход работы:
- Настроить доступ к google-таблице по api, написать код генерации данных с помощью Python, используя gspread. 
- Передать данные в таблицу, построить график и диаграмму, используя переданные данные.

```py
import gspread
import numpy as np
gc = gspread.service_account(filename='unityanalizdan-f39f64e89140.json')
sh = gc.open("Unity")
price = np.random.randint(0, 100, 11)
mon = list(range(1,11))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        tempInf = price[i-1]
        tempInf = str(tempInf)
        tempInf = tempInf.replace('.',',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(price[i-1]))
        sh.sheet1.update(('C' + str(i)), str(tempInf))
        print(tempInf)
```
![Снимок экрана 2023-11-10 010147](https://github.com/DmitryLysikov/ANALIZDAN2/assets/129677338/f3d5409c-087a-4abb-ac02-d8f6a6e4e79b)



### Задание 3
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.

Ход работы:
- Создать ключ API для передачи данных из google-таблицы в Unity.
- Создать новый 3D проект на Unity, добавить необходимые звуковые файлы.
- Написать скрипт для воспроизведения звуков, в зависимости от значения в таблице.


```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;
using System;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    void Update()
    {
        if (!dataSet.ContainsKey("Mon_" + i.ToString())) return;

        if (dataSet["Mon_" + i.ToString()] > 0 & statusStart == false)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log("Покупка костюма: +" + dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] < 0 & statusStart == false)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log("Покупка модификации: " + dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 15 & statusStart == false)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log("Покупка гаджета: " + dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get(
            "https://sheets.googleapis.com/v4/spreadsheets/1cY1tcBfyk_0_Dw7KC-Ss8yxl0i3GmMu3qQDhc37nxTo/values/A1%3AZ100?key=AIzaSyBEgxE3l_WGN1wikRFOgYmk5_I94rRCrzo");

        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add("Mon_" + selectRow[0], float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```
![Снимок экрана 2023-11-10 012950](https://github.com/DmitryLysikov/ANALIZDAN2/assets/129677338/b602589b-61d4-4b3f-9312-7a4ad5e1a7ae)




## Выводы

Я узнал как передавать данные в гугл таблицу, используя язык Python, а также как считывать данные из таблицы и затем написать код в Unity, который будет обрабатывать таблицу.
Также я вспомнил как создавать диаграммы в Google таблице и вспомнил синтаксис Python.

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
