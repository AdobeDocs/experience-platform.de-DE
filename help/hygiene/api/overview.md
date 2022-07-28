---
title: Data Hygiene API-Handbuch
description: Erfahren Sie, wie Sie die gespeicherten personenbezogenen Daten Ihrer Kunden in Adobe Experience Platform programmatisch korrigieren oder löschen können.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 94%

---

# Data Hygiene API-Handbuch

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die den Gesundheitsschild erworben haben.

Mit der Data Hygiene API können Sie die in Adobe Experience Platform gespeicherten personenbezogenen Daten Ihrer Kunden programmgesteuert korrigieren oder löschen sowie TTL-Protokolle (Time-to-Live) für Datensätze planen. In diesem Handbuch werden die erforderlichen Schritte zur Verwendung der API beschrieben und Links zu Endpunkt-Dokumentationen bereitgestellt.

## Erste Schritte

Sie können über den folgenden Stammpfad auf die Data Hygiene API zugreifen: `https://platform.adobe.io/data/core/hygiene/`

Im nachfolgenden Abschnitt erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die API durchführen.

### Sammeln von Werten für erforderliche Kopfzeilen

Um die Data Hygiene-API aufrufen zu können, müssen Sie zunächst Ihre Authentifizierungsdaten erfassen. Folgen Sie den Schritten im [API-Authentifizierungs-Handbuch](../../landing/api-authentication.md), um wie unten dargestellt Werte für die einzelnen Kopfzeilen zu generieren, die für die Data Hygiene API erforderlich sind:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* `Content-Type: application/json`

### Lesen von Beispiel-API-Aufrufen

In diesem Dokument wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/api-guide.md#sample-api) in den Ersten Schritten für Experience Platform-APIs.

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## Time to Live (TTL) für Datensätze

Eine Datensatz-TTL ist eine zeitverzögerte Aktion zum Löschen eines Datensatzes. Beim Erstellen einer TTL geben Sie einen zukünftigen Zeitpunkt an, zu dem dieser Datensatz gelöscht werden soll. Weitere Informationen zur Planung von Datensatz-TTLs in der API finden Sie im [Handbuch für Datensatz-TTL-Endpunkte](./ttl.md).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datenhygiene-Anfragen mithilfe von API-Aufrufen verwalten. Informationen zum Ausführen dieser Aktionen in der Platform-Benutzeroberfläche finden Sie im [Handbuch für die Datenhygiene-Benutzeroberfläche](../ui/overview.md).
