---
title: Data Hygiene API-Handbuch
description: Erfahren Sie, wie Sie die gespeicherten personenbezogenen Daten Ihrer Kunden in Adobe Experience Platform programmatisch korrigieren oder löschen können.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 100%

---

# Data Hygiene API-Handbuch

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Healthcare Shield erworben haben.

Mit der Datenhygiene-API können Sie die in Adobe Experience Platform gespeicherten personenbezogenen Daten Ihrer Kundinnen und Kunden programmgesteuert korrigieren oder löschen sowie Ablaufdaten für Datensätze planen. In diesem Handbuch werden die erforderlichen Schritte zur Verwendung der API beschrieben und Links zu Endpunkt-Dokumentationen bereitgestellt.

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

## Datensatzgültigkeiten

Eine Datensatzgültigkeit ist eine zeitverzögerte Aktion zum Löschen eines Datensatzes. Beim Erstellen einer Datensatzgültigkeit geben Sie einen zukünftigen Zeitpunkt an, zu dem dieser Datensatz gelöscht werden soll. Weitere Details zur Planung von Datensatzgültigkeiten in der API finden Sie im [Handbuch für Datensatzgültigkeits-Endpunkte](./dataset-expiration.md).

## Privatkunden-Löschvorgänge

Mit der Datenhygiene-API können Sie alle Datensätze löschen, die mit einer Privatkunden-Identität in einem Datensatz oder in allen Datensätzen verknüpft sind. Sämtliche Datenhygiene-Aufgaben, die Privatkunden-Identitäten löschen, werden durch ein Konstrukt repräsentiert, das als Arbeitsauftrag bezeichnet wird. Weitere Details zur Verwendung von Arbeitsaufträgen in der API finden Sie im [Handbuch für Arbeitsauftrags-Endpunkte](./workorder.md).

## Kontingent

Ihre Organisation ist auf ein vorab festgelegtes monatliches Vorgangskontingent für jede Art von Datenhygieneoperation beschränkt, das je nach Lizenzierung variieren kann. Details zur Anzeige des aktuellen Kontingent-Status Ihrer Datenhygieneprozesse finden Sie im [Handbuch für Kontingentendpunkte](./quota.md).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datenhygiene-Anfragen mithilfe von API-Aufrufen verwalten. Informationen zum Ausführen dieser Aktionen in der Platform-Benutzeroberfläche finden Sie im [Handbuch für die Datenhygiene-Benutzeroberfläche](../ui/overview.md).
