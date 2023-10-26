---
title: Anhang zum Sandbox Tooling API
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Sandbox Tooling-API.
source-git-commit: e4e89c5250885bef177ba0d678629261a361a66d
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---


# Anhang zum Sandbox-API-Handbuch

Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit dem [!DNL Sandbox] API.

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
| `jobType` | Der Auftragstyp. Dieser Wert kann NEW, RESUME und ROLLBACK lauten. |
| `jobStatus` | Der Status des Auftrags. Dieser Wert kann &quot;Ausstehend&quot;, &quot;IN_PROGRESS&quot;, &quot;SUCCESS&quot;, &quot;FEHLGESCHLAGEN&quot;und &quot;ABGEBROCHEN&quot;sein. |
| `requestType` | Der Typ der Anforderung. Dieser Wert kann EXPORT, IMPORT und COPY sein. |
| `expiryPeriod ` | Dieser vom Benutzer angegebene Zeitraum definiert das Ablaufdatum des Pakets (in Tagen) ab der Veröffentlichung des Pakets. Dieser Wert darf nicht negativ sein. Der Standardwert beträgt 90 Tage ab dem Zeitpunkt, zu dem die Update- oder Publish-API aufgerufen wird. |
