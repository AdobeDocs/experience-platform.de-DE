---
keywords: Zielpersonalisierung;Ziel;Ziel von Experience Platform;Adobe Target-Ziel;
title: Adobe Target-Verbindung
description: Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 77%

---

# Adobe Target-Verbindung {#adobe-target-connection}

## Übersicht {#overview}

Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.

Adobe Target ist eine Personalisierungsverbindung in Adobe Experience Platform.

## Voraussetzungen {#prerequisites}

Diese Integration basiert auf dem [Adobe Experience Platform Web SDK](../../../edge/home.md). Sie müssen dieses SDK verwenden, um dieses Ziel zu verwenden.

>[!IMPORTANT]
>
>Bevor Sie eine [!DNL Adobe Target]-Verbindung erstellen, lesen Sie das Handbuch zur [Konfiguration von Personalisierungszielen für die Personalisierung derselben Seite und der nächsten Seite](../../ui/configure-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert.

## Exporttyp und Häufigkeit {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | You are requesting all the segments that are mapped in the Adobe Target destination for a single profile. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anwendungsfälle {#use-cases}

**Personalisieren eines Homepage-Banners**

Ein Unternehmen, das Häuser vermietet und verkauft, möchte seine Homepage mit einem Banner personalisieren, das auf den Qualifikationen der Kundensegmente in Adobe Experience Platform basiert. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese als Kriterien zur Zielgruppenbestimmung für sein Zielgruppenangebot an Adobe Target senden.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informationen zu Datenstrom-IDs"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatenstrom die Segmente in der Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Sie müssen einen Datenstrom konfigurieren, bevor Sie Ihr Ziel konfigurieren können."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=de" text="Erfahren Sie, wie Sie einen Datenstrom konfigurieren"

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Read the [access control overview](/help/access-control/ui/overview.md) or contact your product administrator to obtain the required permissions.

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihrer Firma her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie den gewünschten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datenspeicher-ID**: Dadurch wird bestimmt, in welchem Datenerfassungs-Datenstrom die Segmente in die Antwort auf die Seite aufgenommen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Weitere Details finden Sie unter [Konfigurieren eines Datenstroms](../../../edge/fundamentals/datastreams.md).

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Read the [access control overview](/help/access-control/ui/overview.md) or contact your product administrator to obtain the required permissions.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Profilanfrageziele](../../ui/activate-profile-request-destinations.md).

## Exportierte Daten {#exported-data}

Adobe Target liest Profildaten aus dem Adobe Experience Platform Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).
