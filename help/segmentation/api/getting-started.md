---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Segmentdienst
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# Entwicklerhandbuch für Segmentdienst

Mit der Segmentierung können Sie Segmente erstellen und Audiencen in Adobe Experience Platform aus Ihren Echtzeit-Daten zum Profil von Kunden generieren.

## Erste Schritte

Dieser Leitfaden erfordert ein Verständnis der verschiedenen Adobe Experience Platformen, die mit der Segmentierung verbunden sind.

- [Segmentierung](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Segmentierung mithilfe der API erfolgreich zu verwenden.

### Lesen von Beispiel-API-Aufrufen

Die Dokumentation zur Segmentierungsdienst-API enthält Beispiele für API-Aufrufe, die zeigen, wie Ihre Anforderungen formatiert werden. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Erforderliche Kopfzeilen

Die API-Dokumentation erfordert auch, dass Sie das [Authentifizierungstraining](../../tutorials/authentication.md) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufzurufen. Wenn Sie das Authentifizierungstraining abschließen, werden die Werte für die einzelnen erforderlichen Kopfzeilen in Experience Platform API-Aufrufen bereitgestellt, wie unten dargestellt:

- Genehmigung: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zum Arbeiten mit Sandboxen in der Experience Platform finden Sie in der Übersicht über [Sandboxen](../../sandboxes/home.md).

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

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Entwicklerhandbuch für [Segmentdefinitionen](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor festgelegte Segmentdefinitionen, um ein Audiencen-Segment zu erstellen. Mit dem `/segment/jobs` Endpunkt können Sie eine Liste von Segmentaufträgen abrufen, einen neuen Segmentauftrag erstellen, Details zu einem bestimmten Segmentauftrag abrufen oder einen bestimmten Segmentauftrag löschen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Entwicklerhandbuch für [Segmentaufträge](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche wird verwendet, um konfigurierbare Felder, die in verschiedenen Datenquellen enthalten sind, zu suchen und zu indizieren und sie in Echtzeit zurückzugeben. Informationen zum Arbeiten mit der Segmentsuche finden Sie im Handbuch für [Suchentwickler](segment-search.md)

## Nächste Schritte

Um mit dem Aufrufen mithilfe der Segmentierungs-API zu beginnen, wählen Sie eines der Unterleitfäden aus, um zu erfahren, wie bestimmte segmentierungsbezogene Endpunkte verwendet werden. Weitere Informationen zum Arbeiten mit Segmenten mithilfe der Benutzeroberfläche &quot;Platform&quot;finden Sie im Benutzerhandbuch [zur Segmentierung](../ui/overview.md).