---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Quellen-SDK; SDK
title: Konfigurationsoptionen im Quellen-SDK
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung des Sources-SDK vorbereiten müssen.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 1%

---

# Konfigurationsoptionen im Quellen-SDK

>[!IMPORTANT]
>
>Das Quellen-SDK befindet sich derzeit in der Beta-Phase und Ihr Unternehmen hat möglicherweise noch keinen Zugriff darauf. Die in dieser Dokumentation beschriebene Funktionalität kann sich ändern.

Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung des Sources-SDK vorbereiten müssen.

## Verbindungsspezifikation

Verbindungsspezifikationen geben die Connector-Eigenschaften einer Quelle zurück. Dazu gehören Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quellverbindungen sowie eine feste Verbindungs-Spezifikations-ID, die einer bestimmten Quelle zugewiesen ist. Verbindungsspezifikationen sind Mandant und IMS-Organisation agnostisch. Eine typische Verbindungsspezifikation enthält grundlegende Informationen zu einer bestimmten Quelle sowie drei verschiedene Abschnitte: `authSpec`, `sourceSpec`und `exploreSpec`.

| Spezifikationen | Beschreibung |
| --- | --- |
| `authSpec` | Die `authSpec` -Array enthält Informationen zu den Authentifizierungsparametern, die zum Verbinden einer Quelle mit Platform erforderlich sind. Jede Quelle kann mehrere verschiedene Authentifizierungstypen unterstützen. |
| `sourceSpec` | Die `sourceSpec` -Array enthält allgemeine Informationen zu einer Quelle, einschließlich Informationen zu Attributen, die zur Darstellung der Quelle in der Benutzeroberfläche erforderlich sind, Dokumentations-Links und Parametern zu Paginierung, Kopfzeile, Text und Planung. Außerdem `sourceSpec` beschreibt das Schema der Parameter, die zum Erstellen einer Quellverbindung aus einer Basisverbindung erforderlich sind und zum Erstellen einer Quellverbindung erforderlich sind. |
| `exploreSpec` | Die `exploreSpec` -Array definiert die Parameter, die zum Erkunden und Überprüfen der in Ihrer Quelle enthaltenen Objekte erforderlich sind. Die `exploreSpec` definiert auch das Antwortformat, das zurückgegeben wird, wenn Objekte untersucht und untersucht werden. |

{style=&quot;table-layout:auto&quot;}

## Werte der Verbindungsspezifikationen ausfüllen

Eine Verbindungsspezifikation kann in drei verschiedene Teile unterteilt werden: die Authentifizierungsspezifikationen, die Quellspezifikationen und die Analysespezifikationen.

In den folgenden Dokumenten finden Sie Anweisungen zum Ausfüllen der Werte der einzelnen Teile einer Verbindungsspezifikation:

* [Authentifizierungsspezifikation konfigurieren](./authspec.md)
* [Quellspezifikation konfigurieren](./sourcespec.md)
* [Konfigurieren der Discover-Spezifikation](./explorespec.md)


