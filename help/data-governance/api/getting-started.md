---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für die DULE Policy Service-API
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 58%

---


# Handbuch zum Entwickler [!DNL Policy Service] für DUL-API

Data Usage Labeling and Enforcement (DULE) ist der Kernmechanismus von Adobe Experience Platform [!DNL Data Governance]. The DULE [!DNL Policy Service] provides a RESTful API that allows you to create and manage data usage policies to determine what marketing actions can be taken against data that has been labeled with certain data usage labels.

This document provides instructions for performing the key operations available in the [!DNL Policy Service] API. Wenn Sie es noch nicht getan haben, konsultieren Sie zunächst die [Übersicht zu Data Governance](../home.md), um sich mit dem DULE-Framework vertraut zu machen. Eine schrittweise Anleitung zum Erstellen und Erzwingen von DULE-Richtlinien finden Sie im [DULE-Richtlinien-Tutorial](../policies/create.md).

This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Policy Service] API.

## Getting started with DULE [!DNL Policy Service]

Before beginning to work with the [!DNL Policy Service], data on [!DNL Experience Platform] must have appropriate DULE labels applied. Eine genaue Anleitung zum Anwenden von Datennutzungsbezeichnungen auf Datensätze und Felder finden Sie im [Benutzerhandbuch für DULE-Bezeichnungen](../labels/user-guide.md).

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [!DNL Data Governance](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung [!DNL Experience Platform] erzwungen wird.
   * [DULE-Beschriftungen](../labels/overview.md): Datenverwendungsbeschriftungen werden auf [!DNL Experience Data Model] (XDM-)Datenfelder angewendet und geben Einschränkungen für den Zugriff auf diese Daten an.
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
* [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Lesehilfe für Beispiel-API-Aufrufe

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

## Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Data Governance], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

* Content-Type: application/json

## Kernressourcen und benutzerdefinierte Ressourcen

Within the [!DNL Policy Service] API, all policies and marketing actions are referred to as either `core` or `custom` resources.

Die `core`-Ressourcen werden von Adobe definiert und gepflegt, während `custom`-Ressourcen von einzelnen Kunden erstellt und gepflegt werden und daher nur für die IMS-Organisation sichtbar sind, die sie erstellt hat. Darum sind Auflistungs- und Nachschlagevorgänge (`GET`) die einzigen Vorgänge, die bei `core`-Ressourcen zulässig sind, während bei `custom`-Ressourcen Auflistungs-, Nachschlage- und Aktualisierungsvorgänge (`POST`, `PUT`, `PATCH` und `DELETE`) verfügbar sind.

## Richtlinienstatus

Datennutzungsrichtlinien können einen von drei möglichen Status aufweisen: `DRAFT`, `ENABLED` oder `DISABLED`.

Standardmäßig werden nur aktivierte Richtlinien (ENABLED) bei der Richtlinienbewertung berücksichtigt.

„DRAFT“-Richtlinien können bei der Richtlinienbewertung ebenfalls berücksichtigt werden, allerdings nur durch Setzen des Abfrageparameters `?includeDraft=true`. Weiterführende Informationen zur Richtlinienbewertung finden Sie am Ende dieses Dokuments im Abschnitt zur [Richtliniendurchsetzung](../enforcement/overview.md).

## Namen von Marketing-Aktionen {#marketing-actions}

Namen von Marketing-Aktionen sind eindeutige Kennungen für Marketing-Aktionen. Jede `core`-Marketing-Aktion hat einen eindeutigen Namen, der für alle IMS-Organisationen gilt. Diese Namen werden von Adobe definiert und verwaltet. Alle kundendefinierten Marketing-Aktionen (`custom`-Ressourcen) hingegen sind innerhalb Ihrer eigenen Organisation eindeutig und für andere IMS-Organisationen nicht sichtbar oder freigegeben.

Steps for working with marketing actions in the [!DNL Policy Service] API are outlined in the [Marketing Actions](#marketing-actions) section later in this document.

## Nächste Schritte

Nachdem Sie nun über die erforderlichen Kenntnisse und Anmeldedaten verfügen, können Sie fortfahren und mehr über die in diesem Entwicklerhandbuch verwendeten Beispiel-API-Aufrufe lesen:

* [Marketing-Aktionen](marketing-actions.md)
* [Richtlinien](policies.md)