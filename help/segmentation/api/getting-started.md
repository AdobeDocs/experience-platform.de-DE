---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 40%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Mit dem Segmentierungsdienst für Adobe Experience Platformen können Sie Segmente erstellen und Audiencen in Adobe Experience Platform aus Ihren [!DNL Real-time Customer Profile] Daten generieren.

The developer guide requires a working understanding of the various Experience Platform services involved with using [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Sandbox-Umgebungen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen für die Entwicklung und Erweiterung von Anwendungen für digitale Erlebnisse unterteilen.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lesehilfe für Beispiel-API-Aufrufe

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung in Experience Platform.

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufrufen zu können. Wenn Sie das Authentifizierungs-Tutorial absolvieren, erhalten Sie die Werte für jede der erforderlichen Kopfzeilen in Experience Platform-API-Aufrufen, wie unten dargestellt:

- Autorisierung: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md). -->

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profil zu welchen Audiencen gehören. Mit dem `/segment/definitions` Endpunkt können Sie eine Liste von Segmentdefinitionen abrufen, eine neue Segmentdefinition erstellen, Details zu einer bestimmten Segmentdefinition abrufen, eine bestimmte Segmentdefinition löschen oder Details einer bestimmten Segmentdefinition überschreiben.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor festgelegte Segmentdefinitionen, um ein Zielgruppensegment zu erstellen. Sie können den `/segment/jobs`-Endpunkt verwenden, um eine Liste von Segmentaufträgen abzurufen, einen neuen Segmentauftrag zu erstellen, Details zu einem bestimmten Segmentauftrag abzurufen oder einen bestimmten Segmentauftrag zu löschen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Entwicklerhandbuch für Segmentaufträge](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche wird verwendet, um konfigurierbare Felder, die in verschiedenen Datenquellen enthalten sind, zu suchen und zu indizieren und sie in Echtzeit zurückzugeben. Informationen zum Arbeiten mit der Segmentsuche finden Sie im Handbuch für [Suchentwickler](segment-search.md)

## Nächste Schritte

Um Aufrufe mithilfe der [!DNL Segmentation Service] API durchzuführen, wählen Sie eine der verfügbaren Endpunkthandbücher entweder über die linke Navigation oder im [Entwicklerhandbuch aus](./overview.md)