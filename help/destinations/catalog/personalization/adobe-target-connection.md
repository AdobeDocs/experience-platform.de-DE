---
keywords: Zielpersonalisierung;Ziel;Ziel von Experience Platform;Adobe Target-Ziel;
title: Adobe Target-Verbindung
description: Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 3b2fedf4f7b17c4fb32afb5978bfac6f618f5bc3
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 58%

---

# Adobe Target-Verbindung {#adobe-target-connection}

## Ziel-Änderungsprotokoll {#changelog}

| Veröffentlichungsmonat | Aktualisierungstyp | Beschreibung |
|---|---|---|
| Juni 2023 | Aktualisierung der Funktionen und Dokumentation | Ab Juni 2023 können Sie beim Konfigurieren einer neuen Adobe Target-Zielverbindung den Adobe Target-Arbeitsbereich auswählen, für den Sie Zielgruppen freigeben möchten. Weitere Informationen finden Sie im Abschnitt [Verbindungsparameter](#parameters). Weitere Informationen über Arbeitsbereiche finden Sie im Tutorial zum [Konfigurieren von Arbeitsbereichen](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=de) in Adobe Target. |
| Mai 2023 | Aktualisierung der Funktionen und Dokumentation | Ab Mai 2023 wird die **[!UICONTROL Adobe Target]** Verbindungsunterstützung [attributbasierte Personalisierung](../../ui/activate-edge-personalization-destinations.md#map-attributes) und ist allgemein für alle Kunden verfügbar. |

{style="table-layout:auto"}

## Übersicht {#overview}

Adobe Target ist ein Programm, das bei allen eingehenden Kundeninteraktionen über Websites, Mobile Apps usw. KI-gestützte Echtzeit-Personalisierung und Experimente ermöglicht.

Adobe Target ist eine Personalisierungsverbindung im Adobe Experience Platform-Zielkatalog.

Eine kurze Übersicht über die Konfiguration der Adobe Target-Verbindung in Experience Platform finden Sie im folgenden Video.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Voraussetzungen {#prerequisites}

### Datenspeicher-ID {#datastream-id}

Beim Konfigurieren der Adobe Target-Verbindung zu [Verwenden einer Datensatz-ID](#parameters), müssen Sie über die [Adobe Experience Platform Web SDK](../../../edge/home.md) implementiert.

Zum Konfigurieren der Adobe Target-Verbindung ohne Verwendung einer Datastraam-ID müssen Sie das Web SDK nicht implementieren.

>[!IMPORTANT]
>
>Bevor Sie eine [!DNL Adobe Target]-Verbindung erstellen, lesen Sie das Handbuch zur [Konfiguration von Personalisierungszielen für die Personalisierung derselben Seite und der nächsten Seite](../../ui/activate-edge-personalization-destinations.md). In dieser Anleitung werden die erforderlichen Konfigurationsschritte für die Anwendungsfälle der Personalisierung derselben Seite und der nächsten Seite für mehrere Experience Platform-Komponenten erläutert. Für die Personalisierung der gleichen Seite und der nächsten Seite müssen Sie bei der Konfiguration der Adobe Target-Verbindung eine Datastraam-ID verwenden.

### Voraussetzungen in Adobe Target {#prerequisites-in-adobe-target}

Stellen Sie in Adobe Target sicher, dass Ihr Benutzer über Folgendes verfügt:

* Zugriff auf [Standardarbeitsbereich](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#default-workspace);
* Die **Genehmiger** [Rolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en#roles-and-permissions).

Weitere Informationen zum Gewähren von Berechtigungen für [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=en#section_8C425E43E5DD4111BBFC734A2B7ABC80) und [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=en#roles-permissions).

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Sie fordern alle Segmente an, die im Adobe Target-Ziel für ein einzelnes Profil zugeordnet sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informationen zu Datenstrom-IDs"
>abstract="Mit dieser Option wird festgelegt, in welchen Datenerfassungs-Datenstrom die Segmente einbezogen werden. Das Dropdown-Menü enthält nur Datenströme, für die die Zielkonfiguration aktiviert ist. Um die Edge-Segmentierung zu verwenden, müssen Sie eine Datenstrom-ID auswählen. Wenn Sie „Keine“ auswählen, werden alle Anwendungsfälle deaktiviert, die die Edge-Segmentierung verwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=de#parameters" text="Weitere Informationen zur Auswahl von Datenströmen"

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Experience Platform stellt automatisch eine Verbindung zur Adobe Target-Instanz Ihrer Firma her. Es ist keine Authentifizierung erforderlich.

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Informationen zu Adobe Target-Arbeitsbereichen"
>abstract="Wählen Sie den Adobe Target-Arbeitsbereich aus, für den Zielgruppen freigegeben werden sollen. Für jede Adobe Target-Verbindung kann ein Arbeitsbereich ausgewählt werden. Nach der Aktivierung werden die Zielgruppen zum ausgewählten Arbeitsbereich weitergeleitet, während die entsprechenden Kennzeichnungen für die Datennutzung aus Experience Platform befolgt werden."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=de" text="Weitere Informationen zu Adobe Target-Arbeitsbereichen"

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **Name**: Geben Sie den gewünschten Namen für das Ziel ein.
* **Beschreibung**: Geben Sie eine Beschreibung für das Ziel ein. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden. Dieses Feld ist optional.
* **Datenspeicher-ID**: Dadurch wird bestimmt, in welchen Datenerfassungsdatenstrom die Segmente einbezogen werden. Das Dropdown-Menü zeigt nur Datensätze an, für die die Target- und Adobe Experience Platform-Dienste aktiviert sind. Siehe [Konfigurieren eines Datenspeichers](../../../edge/datastreams/configure.md#aep) für detaillierte Informationen zum Konfigurieren eines Datastreams für Adobe Experience Platform und Adobe Target.
   * **[!UICONTROL Keines]**: Wählen Sie diese Option aus, wenn Sie die Adobe Target-Personalisierung konfigurieren möchten, die Implementierung der [Experience Platform Web SDK](../../../edge/home.md). Bei Verwendung dieser Option unterstützen Segmente, die von Experience Platform nach Target exportiert werden, nur die Personalisierung der nächsten Sitzung und die Kantensegmentierung ist deaktiviert. Weiterführende Informationen finden Sie in der folgenden Tabelle.
* **Arbeitsbereich**: Adobe Target auswählen [Arbeitsbereich](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=de) für die Zielgruppen freigegeben werden. Für jede Adobe Target-Verbindung kann ein Arbeitsbereich ausgewählt werden. Bei Aktivierung werden die Zielgruppen zum ausgewählten Arbeitsbereich weitergeleitet, während die entsprechenden [Datennutzungsbezeichnungen für Experience Platformen](../../../data-governance/labels/overview.md).

| Kein Datenspeicher ausgewählt | Datenspeicher ausgewählt |
|---|---|
| <ul><li>[Edge-Segmentierung](../../../segmentation/ui/edge-segmentation.md) wird nicht unterstützt.</li><li>[Personalisierung auf derselben Seite und auf der nächsten Seite](../../ui/activate-edge-personalization-destinations.md) werden nicht unterstützt.</li><li>Sie können Segmente nur für die Adobe Target-Verbindung freigeben. *Standard-Produktions-Sandbox*.</li><li>Verwenden Sie zum Konfigurieren der Personalisierung der nächsten Sitzung ohne Verwendung einer Datastraam-ID die [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>Die Edge-Segmentierung funktioniert wie erwartet.</li><li>[Personalisierung auf derselben Seite und auf der nächsten Seite](../../ui/activate-edge-personalization-destinations.md) werden unterstützt.</li><li>Die Segmentfreigabe wird für andere Sandboxes unterstützt.</li></ul> |

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Profilanfrageziele](../../ui/activate-edge-personalization-destinations.md).

## Exportierte Daten {#exported-data}

Adobe Target liest Profildaten aus dem Adobe Experience Platform Edge Network, sodass keine Daten exportiert werden.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).
