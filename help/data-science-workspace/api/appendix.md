---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen
solution: Experience Platform
title: Handbuch zur Sensei Machine Learning API - Anhang
topic-legacy: Developer guide
description: Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der Sensei Machine Learning-API.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 7%

---

# [!DNL Sensei Machine Learning] Anhang zum API-Handbuch

Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der [!DNL Sensei Machine Learning] API.

## Abfrageparameter für den Asset-Abruf {#query}

Die [!DNL Sensei Machine Learning] API unterstützt Abfrageparameter beim Abrufen von Assets. Die verfügbaren Abfrageparameter und ihre Verwendung werden in der folgenden Tabelle beschrieben:

| Abfrageparameter | Beschreibung | Standardwert |
| --------------- | ----------- | ------- |
| `start` | Gibt den Startindex für die Paginierung an. | `start=0` |
| `limit` | Gibt die maximale Anzahl der zurückzugebenden Ergebnisse an. | `limit=25` |
| `orderby` | Gibt die Eigenschaften an, die für die Sortierung in Prioritätsreihenfolge verwendet werden sollen. Einen Bindestrich (**-**) vor einem Eigenschaftsnamen, der in absteigender Reihenfolge sortiert werden soll, andernfalls werden die Ergebnisse in aufsteigender Reihenfolge sortiert. | `orderby=created` |
| `property` | Gibt den Vergleichsausdruck an, den ein Objekt erfüllen muss, damit es zurückgegeben werden kann. | `property=deleted==false` |

>[!NOTE]
>
>Bei Kombination mehrerer Abfrageparameter müssen diese durch kaufmännische Und-Zeichen (**&amp;**).

## Python-CPU- und GPU-Konfigurationen {#cpu-gpu-config}

Python Engines haben die Möglichkeit, für Trainings- oder Scoring-Zwecke zwischen einer CPU oder einer GPU zu wählen und wird in einer [MLInstance](./mlinstances.md) als Aufgabenspezifikation (`tasks.specification`).

Im Folgenden finden Sie eine Beispielkonfiguration, die angibt, wie eine CPU für Schulungen und eine GPU für Scoring verwendet wird:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>Die Werte von `cpus` und `gpus` gibt nicht die Anzahl der CPUs oder GPUs an, sondern die Anzahl der physischen Computer. Diese Werte sind zumutbar `"1"` und löst andernfalls eine Ausnahme aus.

## PySpark- und Spark-Ressourcenkonfigurationen {#resource-config}

Spark Engines haben die Möglichkeit, Rechenressourcen für Trainings- und Scoring-Zwecke zu ändern. Diese Ressourcen werden in der folgenden Tabelle beschrieben:

| Ressource | Beschreibung | Typ |
| -------- | ----------- | ---- |
| driverMemory | Speicher für Treiber in Megabyte | int |
| driverCores | Anzahl der vom Fahrer verwendeten Kerne | int |
| executorMemory | Speicher für Executor in Megabyte | int |
| executorCores | Anzahl der vom Executor verwendeten Kerne | int |
| numExecutors | Anzahl der Executor | int |

Ressourcen können auf einer [MLInstance](./mlinstances.md) als (A) individuelle Trainings- oder Scoring-Parameter oder (B) innerhalb eines zusätzlichen Spezifikations-Objekts (`specification`). Beispielsweise sind die folgenden Ressourcenkonfigurationen für Training und Scoring identisch:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
