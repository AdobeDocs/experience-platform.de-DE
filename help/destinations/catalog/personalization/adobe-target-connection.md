---
keywords: Zielpersonalisierung; Bestimmungsort; Ziel der Erlebnisplattform; Adobe Target-Ziel;
title: Adobe Target-Verbindung
description: Adobe Target ist eine Anwendung, die Echtzeit-KI-gestützte Personalisierungs- und Experimentierungsfunktionen für alle eingehenden Kundeninteraktionen über Websites, mobile Apps und mehr hinweg bietet.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: a990e829c8ba034f31b883360495513f3f5b4cfc
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 8%

---

# Adobe Target-Verbindung {#adobe-target-connection}

## Übersicht {#overview}

Adobe Target ist eine Anwendung, die Echtzeit-KI-gestützte Personalisierungs- und Experimentierungsfunktionen für alle eingehenden Kundeninteraktionen über Websites, mobile Apps und mehr hinweg bietet.

Adobe Target ist eine Personalisierungsverbindung in Adobe Experience Platform.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf der [Adobe Experience Platform Web SDK](../../../edge/home.md). Sie müssen dieses SDK verwenden, um dieses Ziel zu verwenden.

>[!IMPORTANT]
>
>Vor der Erstellung [!DNL Adobe Target] Verbindung, lesen Sie die Anleitung zum [Personalisierungsziele für die Personalisierung der gleichen Seite und der nächsten Seite konfigurieren](../../ui/configure-personalization-destinations.md). In diesem Handbuch werden die erforderlichen Konfigurationsschritte für die Personalisierungsfälle der gleichen Experience Platform und der nächsten Seite für mehrere Seitenkomponenten erläutert.

## Exporttyp {#export-type}

**Profilanfrage** - Sie fordern alle Segmente an, die im Adobe Target-Ziel für ein einzelnes Profil zugeordnet sind.

## Anwendungsfälle {#use-cases}

**Personalisieren eines Homepage-Banners**

Ein häusliches Vermieter und Vertriebsunternehmen möchte seine Homepage mit einem Banner personalisieren, das auf den Qualifikationen der Kundensegmente in Adobe Experience Platform basiert. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese als Targeting-Kriterien für sein Target-Angebot an Adobe Target senden.

## Mit Ziel verbinden {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Über Datastream-IDs"
>abstract="Diese Option bestimmt, in welchem Datenerfassungsdatenstrom die Segmente in die Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Zielkonfiguration aktiviert ist. Sie müssen einen Datastream konfigurieren, bevor Sie Ihr Ziel konfigurieren können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Erfahren Sie, wie Sie einen Datastream konfigurieren."

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihres Unternehmens her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datenspeicher-ID**: Dadurch wird bestimmt, in welchem Datenerfassungsdatenstrom die Segmente in die Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Zielkonfiguration aktiviert ist. Siehe [Konfigurieren eines Datastreams](../../../edge/fundamentals/datastreams.md) für weitere Details.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Lesen [Profile und Segmente für Profilanforderungsziele aktivieren](../../ui/activate-profile-request-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Adobe Target liest Profildaten aus dem Adobe Experience Platform Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, lesen Sie die [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
