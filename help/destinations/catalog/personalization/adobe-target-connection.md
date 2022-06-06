---
keywords: Zielpersonalisierung;Ziel;Ziel von Experience Platform;Adobe Target-Ziel;
title: Adobe Target-Verbindung
description: Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 12e2c1a32f08b6942d6e4aefc35a53bae8387d7e
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 39%

---

# Adobe Target-Verbindung {#adobe-target-connection}

## Übersicht {#overview}

Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.

Adobe Target ist eine Personalisierungsverbindung im Adobe Experience Platform-Zielkatalog.

## Voraussetzungen {#prerequisites}

### Datenspeicher-ID {#datastream-id}

Beim Konfigurieren der Adobe Target-Verbindung zu [Verwenden einer Datensatz-ID](#parameters), müssen Sie über die [Adobe Experience Platform Web SDK](../../../edge/home.md) implementiert.

Zum Konfigurieren der Adobe Target-Verbindung ohne Verwendung einer Datastraam-ID müssen Sie das Web SDK nicht implementieren.

>[!IMPORTANT]
>
>Bevor Sie eine [!DNL Adobe Target]-Verbindung erstellen, lesen Sie das Handbuch zur [Konfiguration von Personalisierungszielen für die Personalisierung derselben Seite und der nächsten Seite](../../ui/configure-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert. Für die Personalisierung der gleichen Seite und der nächsten Seite müssen Sie bei der Konfiguration der Adobe Target-Verbindung eine Datastraam-ID verwenden.

### Voraussetzungen in Adobe Target {#prerequisites-in-adobe-target}

Stellen Sie in Adobe Target sicher, dass Ihr Benutzer über Folgendes verfügt:

* Zugriff auf [Standardarbeitsbereich](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* Die **Genehmiger** [Rolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

Weitere Informationen zum Gewähren von Berechtigungen für [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) und [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Sie fordern alle Segmente an, die im Adobe Target-Ziel für ein einzelnes Profil zugeordnet sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anwendungsfälle {#use-cases}

**Personalisieren eines Homepage-Banners**

Ein Unternehmen, das Häuser vermietet und verkauft, möchte seine Homepage mit einem Banner personalisieren, das auf den Qualifikationen der Kundensegmente in Adobe Experience Platform basiert. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese als Kriterien zur Zielgruppenbestimmung für sein Zielgruppenangebot an Adobe Target senden.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informationen zu Datenstrom-IDs"
>abstract="Diese Option bestimmt, in welchen Datenerfassungsdatastream die Segmente einbezogen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Target-Konfiguration aktiviert ist. Um die Kantensegmentierung zu verwenden, müssen Sie eine Datastream-ID auswählen. Wenn Sie Kein auswählen, werden alle Anwendungsfälle deaktiviert, die Kantensegmentierung verwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Erfahren Sie mehr über die Auswahl von Datastreams"

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihrer Firma her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie den gewünschten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datenspeicher-ID**: Dadurch wird bestimmt, in welchen Datenerfassungsdatenstrom die Segmente einbezogen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die das Target-Ziel aktiviert ist. Siehe [Konfigurieren eines Datenspeichers](../../../edge/datastreams/overview.md#target) für detaillierte Informationen zum Konfigurieren eines Datastreams für Adobe Target.
   * **[!UICONTROL Keines]**: Wählen Sie diese Option aus, wenn Sie die Adobe Target-Personalisierung konfigurieren möchten, die Implementierung der [Experience Platform Web SDK](../../../edge/home.md). Bei Verwendung dieser Option unterstützen Segmente, die von Experience Platform nach Target exportiert werden, nur die Personalisierung der nächsten Sitzung und die Kantensegmentierung ist deaktiviert. Weiterführende Informationen finden Sie in der folgenden Tabelle.

| Kein Datenspeicher ausgewählt | Datenspeicher ausgewählt |
|---|---|
| <ul><li>[Edge-Segmentierung](../../../segmentation/ui/edge-segmentation.md) wird nicht unterstützt.</li><li>[Personalisierung auf derselben Seite und auf der nächsten Seite](../../ui/configure-personalization-destinations.md) werden nicht unterstützt.</li><li>Sie können Segmente nur für die Produktions-Sandbox für die Adobe Target-Verbindung freigeben.</li><li>Verwenden Sie zum Konfigurieren der Personalisierung der nächsten Sitzung ohne Verwendung einer Datastraam-ID die [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>Die Edge-Segmentierung funktioniert wie erwartet.</li><li>[Personalisierung auf derselben Seite und auf der nächsten Seite](../../ui/configure-personalization-destinations.md) werden unterstützt.</li><li>Die Segmentfreigabe wird für andere Sandboxes unterstützt.</li></ul> |

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Profilanfrageziele](../../ui/activate-profile-request-destinations.md).

## Exportierte Daten {#exported-data}

Adobe Target liest Profildaten aus dem Adobe Experience Platform Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).
