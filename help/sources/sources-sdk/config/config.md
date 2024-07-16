---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurationsoptionen in Self-Serve-Quellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Self-Serve-Quellen (Batch SDK) vorbereiten müssen.
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 22%

---

# Konfigurationsoptionen in Self-Serve-Quellen (Batch-SDK)

Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Self-Serve-Quellen (Batch SDK) vorbereiten müssen.

## Verbindungsspezifikation

Verbindungsspezifikationen geben die Connector-Eigenschaften einer Quelle zurück. Dazu gehören Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quellverbindungen sowie eine feste Verbindungs-Spezifikations-ID, die einer bestimmten Quelle zugewiesen ist. Verbindungsspezifikationen sind Mandanten und Unternehmen agnostisch. Eine typische Verbindungsspezifikation enthält grundlegende Informationen zu einer bestimmten Quelle sowie drei verschiedene Abschnitte: `authSpec`, `sourceSpec` und `exploreSpec`.

| SPEKS | Beschreibung |
| --- | --- |
| `authSpec` | Das Array `authSpec` enthält Informationen zu den Authentifizierungsparametern, die zum Verbinden einer Quelle mit Platform erforderlich sind. Jede Quelle kann mehrere verschiedene Authentifizierungstypen unterstützen. |
| `sourceSpec` | Das Array `sourceSpec` enthält allgemeine Informationen zu einer Quelle, einschließlich Informationen zu Attributen, die zur Darstellung der Quelle in der Benutzeroberfläche erforderlich sind, Dokumentationslinks und Parametern zu Paginierung, Kopfzeile, Hauptteil und Planung. Außerdem beschreibt `sourceSpec` das Schema der Parameter, die zum Erstellen einer Quellverbindung aus einer Basisverbindung erforderlich sind und zum Erstellen einer Quellverbindung erforderlich sind. |
| `exploreSpec` | Das Array `exploreSpec` definiert die Parameter, die zum Erkunden und Überprüfen von Objekten benötigt werden, die in Ihrer Quelle enthalten sind. Der `exploreSpec` definiert auch das Antwortformat, das zurückgegeben wird, wenn Objekte untersucht und untersucht werden. |

{style="table-layout:auto"}

## Werte der Verbindungsspezifikationen ausfüllen

Eine Verbindungsspezifikation kann in drei verschiedene Teile unterteilt werden: die Authentifizierungsspezifikationen, die Quellspezifikationen und die Analysespezifikationen.

In den folgenden Dokumenten finden Sie Anweisungen zum Ausfüllen der Werte der einzelnen Teile einer Verbindungsspezifikation:

* [Konfigurieren Ihrer Authentifizierungsspezifikation](./authspec.md)
* [Konfigurieren Ihrer Quellspezifikation](./sourcespec.md)
* [Konfigurieren Ihrer Erkundungsspezifikation](./explorespec.md)
