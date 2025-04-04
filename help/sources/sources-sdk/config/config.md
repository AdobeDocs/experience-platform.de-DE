---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurationsoptionen in Selbstbedienungsquellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Selbstbedienungsquellen (Batch-SDK) vorbereiten müssen.
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 22%

---

# Konfigurationsoptionen in Selbstbedienungsquellen (Batch-SDK)

Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Selbstbedienungsquellen (Batch-SDK) vorbereiten müssen.

## Verbindungsspezifikation

Verbindungsspezifikationen geben die Connector-Eigenschaften einer Quelle zurück. Sie enthalten Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen und eine feste Verbindungsspezifikations-ID, die einer bestimmten Quelle zugewiesen wird. Verbindungsspezifikationen sind mandanten- und organisationsunabhängig. Eine typische Verbindungsspezifikation enthält grundlegende Informationen zu einer bestimmten Quelle sowie drei verschiedene Abschnitte: `authSpec`, `sourceSpec` und `exploreSpec`.

| Technische Daten | Beschreibung |
| --- | --- |
| `authSpec` | Das `authSpec`-Array enthält Informationen zu den Authentifizierungsparametern, die zum Verbinden einer Quelle mit Experience Platform erforderlich sind. Jede beliebige Quelle kann mehrere verschiedene Authentifizierungstypen unterstützen. |
| `sourceSpec` | Das `sourceSpec`-Array enthält allgemeine Informationen zu einer Quelle, einschließlich Informationen zu den Attributen, die erforderlich sind, um die Quelle in der Benutzeroberfläche darzustellen, zum Dokumentations-Link und zu Parametern in Bezug auf Paginierung, Kopfzeile, Hauptteil und Planung. Darüber hinaus beschreibt `sourceSpec` das Schema der Parameter, die zum Erstellen einer Quellverbindung aus einer Basisverbindung erforderlich sind und zum Erstellen einer Quellverbindung erforderlich sind. |
| `exploreSpec` | Das `exploreSpec`-Array definiert die Parameter, die zum Untersuchen und Überprüfen der in der Quelle enthaltenen Objekte erforderlich sind. Die `exploreSpec` definiert auch das Antwortformat, das zurückgegeben wird, wenn Objekte untersucht und geprüft werden. |

{style="table-layout:auto"}

## Füllen der Verbindungsspezifikationswerte

Eine Verbindungsspezifikation kann in drei verschiedene Teile unterteilt werden: die Authentifizierungsspezifikationen, die Quellspezifikationen und die Analysespezifikationen.

In den folgenden Dokumenten finden Sie Anweisungen zum Ausfüllen der Werte der einzelnen Teile einer Verbindungsspezifikation:

* [Konfigurieren Ihrer Authentifizierungsspezifikation](./authspec.md)
* [Konfigurieren Ihrer Quellspezifikation](./sourcespec.md)
* [Konfigurieren Ihrer Erkundungsspezifikation](./explorespec.md)
