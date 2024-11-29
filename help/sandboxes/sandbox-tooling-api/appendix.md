---
title: Anhang zum Sandbox Tooling API
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Sandbox Tooling-API.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 2%

---

# Anhang zum Sandbox-API-Handbuch

Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der [!DNL Sandbox]-API.

## Verwenden von Abfrageparametern {#query}

Die Sandbox Tooling-API unterstützt die Verwendung von Abfrageparametern zum Paginieren und Filtern von Ergebnissen bei der Auflistung von Paketen.

>[!NOTE]
>
>Die `limit` kann einzeln übergeben und gestartet werden.

| Parameter | Beschreibung |
| --- | --- |
| `limit` | Die maximale Anzahl von Datensätzen, die in der Antwort zurückgegeben werden. Der Standardwert ist 20. |
| `start` | Der Beginn, an dem eine untergeordnete Liste von Elementen beginnen soll. |
| `targetSandbox` | Stellt den Namen der Sandbox dar, in die Sie Ihre Artefakte importieren möchten. |
| `jobType` | Der Auftragstyp. Dieser Wert kann `NEW`, `RESUME` oder `ROLLBACK` sein. |
| `jobStatus` | Der Status des Auftrags. Dieser Wert kann `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` oder `CANCELLED` sein. |
| `requestType` | Der Typ der Anforderung. Dieser Wert kann `EXPORT`, `IMPORT` oder `COPY` sein. |
| `expiryPeriod` | Dieser vom Benutzer angegebene Zeitraum definiert das Ablaufdatum des Pakets (in Tagen) ab der Veröffentlichung des Pakets. Dieser Wert darf nicht negativ sein. Der Standardwert beträgt 90 Tage ab dem Zeitpunkt, zu dem die Update- oder Publish-API aufgerufen wird. |
| `packageType` | Der Pakettyp. Dieser Wert kann `PARTIAL` oder `FULL` sein. |
| `status` | Der Status des Pakets. Dieser Wert kann `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` oder `PUBLISH_FAILED` sein. |
