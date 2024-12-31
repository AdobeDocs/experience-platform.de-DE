---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;Sandbox;Sandbox;Sandboxes;Sandboxes;Sandboxes
solution: Experience Platform
title: Sandbox-API-Handbuch - Anhang
description: Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit der Sandbox-API.
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# Sandbox-API-Handbuch - Anhang

Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit der [!DNL Sandbox]-API.

## Verwenden von Abfrageparametern {#query}

Die [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) unterstützt die Verwendung von Abfrageparametern zum Seiten- und Filtern von Ergebnissen beim Auflisten von Sandboxes.

>[!NOTE]
>
>Die Abfrageparameter `limit` und `offset` müssen zusammen angegeben werden. Wenn Sie nur einen angeben, gibt die API einen Fehler zurück. Wenn Sie „Keine“ angeben, ist die standardmäßige Begrenzung 50 und der Versatz 0.

| Parameter | Beschreibung |
| --- | --- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden sollen. |
| `offset` | Die Anzahl der Entitäten vom ersten Datensatz bis zum Start (Offset) der Antwortliste. |
