---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen;
solution: Experience Platform
title: Handbuch zur API für maschinelles Lernen in Sensei - Anhang
description: Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der Sensei-API für maschinelles Lernen.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# [!DNL Sensei Machine Learning]-API-Handbuch - Anhang

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der [!DNL Sensei Machine Learning]-API.

## Abfrageparameter für den Asset-Abruf {#query}

Die [!DNL Sensei Machine Learning]-API unterstützt Abfrageparameter beim Abrufen von Assets. Die verfügbaren Abfrageparameter und deren Verwendung werden in der folgenden Tabelle beschrieben:

| Abfrageparameter | Beschreibung | Standardwert |
| --------------- | ----------- | ------- |
| `start` | Gibt den Startindex für die Paginierung an. | `start=0` |
| `limit` | Gibt die maximale Anzahl der zurückzugebenden Ergebnisse an. | `limit=25` |
| `orderby` | Gibt die Eigenschaften an, die für die Sortierung nach Priorität verwendet werden sollen. Fügen Sie vor einem Eigenschaftsnamen einen Bindestrich (**-**) ein, um in absteigender Reihenfolge zu sortieren. Andernfalls werden die Ergebnisse in aufsteigender Reihenfolge sortiert. | `orderby=created` |
| `property` | Gibt den Vergleichsausdruck an, den ein Objekt erfüllen muss, damit er zurückgegeben wird. | `property=deleted==false` |

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen sie durch kaufmännische Und-Zeichen getrennt werden (**&amp;**).

## Python CPU- und GPU-Konfigurationen {#cpu-gpu-config}

Python-Engines haben die Möglichkeit, für Trainings- oder Scoring-Zwecke entweder zwischen einer CPU oder einer GPU zu wählen, und wird in einer [MLInstance](./mlinstances.md) als Aufgabenspezifikation (`tasks.specification`) definiert.

Im Folgenden finden Sie eine Beispielkonfiguration, die die Verwendung einer CPU für das Training und einer GPU für die Bewertung angibt:

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
>Die Werte von `cpus` und `gpus` geben nicht die Anzahl der CPUs oder GPUs an, sondern die Anzahl der physischen Computer. Diese Werte sind zulässig `"1"` und lösen andernfalls eine Ausnahme aus.

## PySpark- und Spark-Ressourcenkonfigurationen {#resource-config}

Spark-Engines haben die Möglichkeit, Rechenressourcen für Trainings- und Scoring-Zwecke zu ändern. Diese Ressourcen werden in der folgenden Tabelle beschrieben:

| Ressource | Beschreibung | Typ |
| -------- | ----------- | ---- |
| driverMemory | Speicher für Treiber in Megabyte | int |
| driverCores | Anzahl der vom Treiber verwendeten Kerne | int |
| executorMemory | Speicher für Executor in Megabyte | int |
| executorCores | Anzahl der vom Executor verwendeten Kerne | int |
| numExecutors | Anzahl der Executors | int |

Ressourcen können in einer [MLInstance](./mlinstances.md) entweder als (A) einzelne Trainings- oder Scoring-Parameter oder (B) in einem zusätzlichen Spezifikationsobjekt (`specification`) angegeben werden. Beispielsweise sind die folgenden Ressourcenkonfigurationen für Training und Bewertung identisch:

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
