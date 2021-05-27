---
keywords: Experience Platform; Startseite; beliebte Themen; API; Sandbox; Sandbox; Sandboxes; Sandboxes
solution: Experience Platform
title: Anhang zum Sandbox-API-Handbuch
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Sandbox-API.
topic-legacy: developer guide
source-git-commit: e4067f79e9da106fe2d2a86fa0024c2e5fe5d0ba
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 10%

---

# Anhang zum Sandbox-API-Handbuch

Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der [!DNL Sandbox]-API.

## Verwenden von Abfrageparametern {#query}

Die [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) unterstützt die Verwendung von Abfrageparametern zur Seite und Filterung von Ergebnissen bei der Auflistung von Sandboxes.

>[!NOTE]
>
>Die Abfrageparameter `limit` und `offset` müssen zusammen angegeben werden. Wenn Sie nur eine angeben, gibt die API einen Fehler zurück. Wenn Sie &quot;Keine&quot;angeben, ist die Standardbegrenzung 50 und der Versatz 0.

| Parameter | Beschreibung |
| --- | --- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden. |
| `offset` | Die Anzahl der Entitäten aus dem ersten Datensatz, aus dem die Antwortliste gestartet (versetzt) werden soll. |
