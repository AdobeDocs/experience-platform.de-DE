---
title: Data Hygiene API-Anleitung
description: Erfahren Sie, wie Sie die gespeicherten personenbezogenen Daten Ihrer Kunden in Adobe Experience Platform programmatisch korrigieren oder löschen können.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 33%

---

# Data Hygiene API-Handbuch

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Mit der Data Hygiene API können Sie die in Adobe Experience Platform gespeicherten personenbezogenen Daten Ihrer Kunden programmatisch korrigieren oder löschen sowie TTL-Protokolle (Time-to-Live) für Datensätze planen. In diesem Handbuch werden die erforderlichen Schritte zur Verwendung der API beschrieben und Links zu endpunktspezifischeren Dokumentationen bereitgestellt.

## Erste Schritte

Sie können über den folgenden Stammpfad auf die Data Hygiene-API zugreifen: `https://platform.adobe.io/data/core/hygiene/`

In den folgenden Abschnitten werden die wichtigsten Konzepte beschrieben, die Sie kennen müssen, bevor Sie Aufrufe an die API durchführen.

### Sammeln von Werten für erforderliche Kopfzeilen

Um die Data Hygiene-API aufrufen zu können, müssen Sie zunächst Ihre Authentifizierungsdaten erfassen. Befolgen Sie die [API-Authentifizierungshandbuch](../../landing/api-authentication.md) um Werte für die einzelnen Header zu generieren, die für die Data Hygiene-API erforderlich sind, wie unten dargestellt:

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

Eine Datensatz-TTL ist eine zeitverzögerte Aktion zum Löschen eines Datensatzes. Durch Erstellen einer TTL geben Sie einen zukünftigen Zeitpunkt an, zu dem dieser Datensatz gelöscht werden soll. Siehe [Endpunktleitfaden für Datensatz-TTL](./ttl.md) für Details zur Planung von Datensatz-TTLs in der API.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datenhygiene-Anfragen mithilfe von API-Aufrufen verwalten. Informationen zum Ausführen dieser Aktionen in der Platform-Benutzeroberfläche finden Sie in der [Handbuch zur Datenhygiene](../ui/overview.md).
