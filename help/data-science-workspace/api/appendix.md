---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Anhang
topic: Developer guide
translation-type: tm+mt
source-git-commit: 2940f69d193ff8a4ec6ad4a58813b5426201ef45
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 4%

---


# Anhang

Die folgenden Abschnitte enthalten Referenzinformationen zu verschiedenen Funktionen der Sensei Machine Learning API.

## Abfragen-Parameter für den Asset-Abruf {#query}

Die Sensei Machine Learning API unterstützt Abfragen beim Abrufen von Assets. Die verfügbaren Parameter für die Abfrage und ihre Verwendung werden in der folgenden Tabelle beschrieben:

| Abfrageparameter | Beschreibung | Standardwert |
| --------------- | ----------- | ------- |
| `start` | Gibt den Startindex für die Paginierung an. | `start=0` |
| `limit` | Gibt die maximale Anzahl der zurückzugebenden Ergebnisse an. | `limit=25` |
| `orderby` | Gibt die Eigenschaften an, die für die Sortierung in der Reihenfolge der Priorität verwendet werden sollen. Fügen Sie vor dem Namen einer Eigenschaft einen Bindestrich (**-**) ein, der in absteigender Reihenfolge sortiert werden soll. Andernfalls werden die Ergebnisse in aufsteigender Reihenfolge sortiert. | `orderby=created` |
| `property` | Gibt den Vergleichs-Ausdruck an, den ein Objekt erfüllen muss, um zurückgegeben zu werden. | `property=deleted==false` |

>[!NOTE] Beim Kombinieren mehrerer Abfragen müssen diese durch das kaufmännische Und (**&amp;**) getrennt werden.

## Python CPU- und GPU-Konfigurationen {#cpu-gpu-config}

Python Engines haben die Möglichkeit, entweder eine CPU oder eine GPU zu Trainings- oder Scoring-Zwecken zu wählen und wird auf einer [MLInstanz](./mlinstances.md) als Aufgabe-Spezifikation (`tasks.specification`) definiert.

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

>[!NOTE] Die Werte `cpus` und `gpus` nicht die Anzahl der CPUs oder GPUs, sondern die Anzahl der physischen Maschinen. Diese Werte sind zulässig `"1"` und werden andernfalls eine Ausnahme auslösen.

## Ressourcenkonfigurationen von PySpark und Spark {#resource-config}

Spark Engines haben die Möglichkeit, zu Schulungs- und Bewertungszwecken Computerressourcen zu ändern. Diese Ressourcen werden in der folgenden Tabelle beschrieben:

| Ressource | Beschreibung | Typ |
| -------- | ----------- | ---- |
| driverMemory | Speicher für Treiber in Megabyte | int |
| driverCores | Anzahl der vom Fahrer verwendeten Kerne | int |
| executeMemory | Speicher für Führungskräfte in Megabyte | int |
| executeCores | Anzahl der vom Prüfer verwendeten Kerne | int |
| numExecutors | Anzahl der Führungskräfte | int |

Ressourcen können auf einer [MLInstanz](./mlinstances.md) entweder als (A) individuelle Trainings- oder Scoring-Parameter oder (B) innerhalb eines zusätzlichen Specification-Objekts (`specification`) angegeben werden. Beispielsweise sind die folgenden Ressourcenkonfigurationen für Schulung und Bewertung gleich:

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
