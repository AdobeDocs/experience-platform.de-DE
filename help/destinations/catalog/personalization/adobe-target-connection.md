---
keywords: Zielpersonalisierung; Bestimmungsort; Ziel der Erlebnisplattform; Adobe Target-Ziel;
title: Adobe Target-Verbindung (Beta)
description: Adobe Target ist eine Anwendung, die eine Echtzeit-, 1:1- und KI-gestützte Personalisierung und Experimentierung bei allen eingehenden Kundeninteraktionen über Websites, mobile Apps und mehr hinweg ermöglicht.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: ba27484655438df654a1e062309ddd30638f62a5
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 11%

---

# Adobe Target-Verbindung (Beta) {#adobe-target-connection}

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die Adobe Target-Verbindung in Adobe Experience Platform ist derzeit als Betaversion verfügbar. Dokumentation und Funktionalität können sich ändern.

Adobe Target ist eine Anwendung, die eine Echtzeit-, 1:1- , KI-gestützte Personalisierung und Experimentierung bei allen eingehenden Kundeninteraktionen über Websites, mobile Apps und mehr hinweg ermöglicht.

Adobe Target ist eine Personalisierungsverbindung in Adobe Experience Platform.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf dem [Adobe Experience Platform Web SDK](../../../edge/home.md). Sie müssen dieses SDK verwenden, um dieses Ziel zu verwenden.

## Exporttyp {#export-type}

**Profilanfrage** : Sie fordern alle Segmente an, die im Adobe Target-Ziel für ein einzelnes Profil zugeordnet sind.

## Anwendungsfälle {#use-cases}

**Personalisieren eines Homepage-Banners**

Ein häusliches Vermieter und Vertriebsunternehmen möchte seine Homepage mit einem Banner personalisieren, das auf den Qualifikationen der Kundensegmente in Adobe Experience Platform basiert. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese als Targeting-Kriterien für sein Target-Angebot an Adobe Target senden.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihres Unternehmens her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datastream-ID**: Dadurch wird bestimmt, in welchem Datenerfassungsdatenstrom die Segmente in die Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Zielkonfiguration aktiviert ist. Weitere Informationen finden Sie unter [Konfigurieren eines Datastreams](../../../edge/fundamentals/datastreams.md) .

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Profile und Segmente für Profilanfrageziele aktivieren](../../ui/activate-profile-request-destinations.md) .

## Exportierte Daten {#exported-data}

Adobe Target liest Profildaten aus dem Adobe Experience Platform Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
