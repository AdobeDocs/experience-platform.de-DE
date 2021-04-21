---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Sensei Machine Learning API - Handbuch
topic-legacy: Developer guide
description: Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der Sensei Machine Learning API.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 7%

---

# [!DNL Sensei Machine Learning] API-Handbuch

Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der [!DNL Sensei Machine Learning]-API.

## Abfragen-Parameter für den Asset-Abruf {#query}

Die API [!DNL Sensei Machine Learning] unterstützt Abfragen beim Abrufen von Assets. Die verfügbaren Parameter für die Abfrage und ihre Verwendung werden in der folgenden Tabelle beschrieben:

| Abfrageparameter | Beschreibung | Standardwert |
| --------------- | ----------- | ------- |
| `start` | Gibt den Startindex für die Paginierung an. | `start=0` |
| `limit` | Gibt die maximale Anzahl der zurückzugebenden Ergebnisse an. | `limit=25` |
| `orderby` | Gibt die Eigenschaften an, die für die Sortierung in der Reihenfolge der Priorität verwendet werden sollen. Fügen Sie vor dem Eigenschaftsnamen einen Bindestrich (**-**) ein, der in absteigender Reihenfolge sortiert werden soll. Andernfalls werden die Ergebnisse in aufsteigender Reihenfolge sortiert. | `orderby=created` |
| `property` | Gibt den Vergleichs-Ausdruck an, den ein Objekt erfüllen muss, um zurückgegeben zu werden. | `property=deleted==false` |

>[!NOTE]
>
>Beim Kombinieren mehrerer Abfrage-Parameter müssen diese durch ein kaufmännisches Und (**&amp;**) getrennt werden.

## Python CPU- und GPU-Konfigurationen {#cpu-gpu-config}

Python Engines haben die Möglichkeit, entweder eine CPU oder eine GPU zu Trainings- oder Scoring-Zwecken zu wählen und wird auf einer [MLInstance](./mlinstances.md) als Aufgabe-Spezifikation (`tasks.specification`) definiert.

Die folgende Beispielkonfiguration gibt die Verwendung einer CPU für Schulungen und einer GPU für die Bewertung an:

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

Spark Engines haben die Möglichkeit, zu Schulungs- und Bewertungszwecken Computerressourcen zu ändern. Diese Ressourcen werden in der folgenden Tabelle beschrieben:

| Ressource | Beschreibung | Typ |
| -------- | ----------- | ---- |
| driverMemory | Speicher für Treiber in Megabyte | int |
| driverCores | Anzahl der vom Fahrer verwendeten Kerne | int |
| executorMemory | Speicher für Führungskräfte in Megabyte | int |
| executorCores | Anzahl der vom Executor verwendeten Kerne | int |
| numExecutors | Anzahl der Führungskräfte | int |

Ressourcen können auf einer [MLInstance](./mlinstances.md) entweder als (A) individuelle Schulungs- oder Bewertungsparameter oder (B) als zusätzliches Spezifikationsobjekt (`specification`) angegeben werden. Beispielsweise sind die folgenden Ressourcenkonfigurationen für Schulung und Bewertung gleich:

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
