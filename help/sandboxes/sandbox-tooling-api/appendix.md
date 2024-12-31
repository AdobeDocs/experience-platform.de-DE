---
title: Handbuch zur Sandbox-Tooling-API - Anhang
description: Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit der Sandbox-Tooling-API.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# Sandbox-API-Handbuch - Anhang

Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit der [!DNL Sandbox]-API.

## Verwenden von Abfrageparametern {#query}

Die Sandbox-Tooling-API unterstützt die Verwendung von Abfrageparametern zur Paginierung und Filterung der Ergebnisse beim Auflisten von Paketen.

>[!NOTE]
>
>Die `limit` kann einzeln übergeben und gestartet werden.

| Parameter | Beschreibung |
| --- | --- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden sollen. Der Standardwert ist 20. |
| `start` | Der Beginn, an dem eine Teilmenge von Elementen beginnen soll. |
| `targetSandbox` | Stellt den Sandbox-Namen dar, in den Sie Ihre Artefakte importieren möchten. |
| `jobType` | Die Art des Auftrags. Dieser Wert kann `NEW`, `RESUME` oder `ROLLBACK` sein. |
| `jobStatus` | Der Status des Vorgangs. Dieser Wert kann `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` oder `CANCELLED` sein. |
| `requestType` | Der Typ der Anfrage. Dieser Wert kann `EXPORT`, `IMPORT` oder `COPY` sein. |
| `expiryPeriod` | Dieser benutzerdefinierte Zeitraum definiert das Paketablaufdatum (in Tagen) ab dem Zeitpunkt der Veröffentlichung des Pakets. Dieser Wert sollte nicht negativ sein. Der Standardwert liegt bei 90 Tagen ab dem Zeitpunkt, zu dem die Update- oder Publish-API aufgerufen wird. |
| `packageType` | Der Pakettyp. Dieser Wert kann `PARTIAL` oder `FULL` sein. |
| `status` | Der Status des Pakets. Dieser Wert kann `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` oder `PUBLISH_FAILED` sein. |
