---
keywords: Experience Platform; Startseite; beliebte Themen; API; Sandbox; Sandbox; Sandboxes; Sandboxes
solution: Experience Platform
title: Anhang zum Sandbox-API-Handbuch
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Sandbox-API.
topic-legacy: developer guide
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# Anhang zum Sandbox-API-Handbuch

Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit dem [!DNL Sandbox] API.

## Verwenden von Abfrageparametern {#query}

Die [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) unterstützt die Verwendung von Abfrageparametern zur Seite und Filterung von Ergebnissen bei der Auflistung von Sandboxes.

>[!NOTE]
>
>Die `limit` und `offset` -Abfrageparameter müssen zusammen angegeben werden. Wenn Sie nur eine angeben, gibt die API einen Fehler zurück. Wenn Sie &quot;Keine&quot;angeben, ist die Standardbegrenzung 50 und der Versatz 0.

| Parameter | Beschreibung |
| --- | --- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden. |
| `offset` | Die Anzahl der Entitäten aus dem ersten Datensatz, aus dem die Antwortliste gestartet (versetzt) werden soll. |
