---
title: Konfigurieren Ihres Datenspeichers für das Experience Platform Web SDK
description: 'Erfahren Sie, wie Sie die Datastreams konfigurieren. '
keywords: Konfiguration; Datastreams; datastreamId; edge; datastream id; Umgebungseinstellungen; edgeConfigId; identity; ID-Synchronisierung aktiviert; ID-Sync-Container-ID; Sandbox; Streaming-Inlet; Ereignis-Datensatz; Target; Client-Code; Eigenschaften-Token; Target-Umgebungs-ID; Cookie-Ziele; URL-Ziele; Analytics Settings Blockreport suite id;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 1ff52944be6e9475f57c62793b0e4c671ff8786b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Konfigurieren eines Datenspeichers

Die Konfiguration für das Adobe Experience Platform Web SDK ist auf zwei Stellen aufgeteilt. Die [configure-Befehl](configuring-the-sdk.md) im SDK steuert Elemente, die auf dem Client verarbeitet werden müssen, z. B. die `edgeDomain`. Datastreams verarbeitet alle anderen Konfigurationen für das SDK. Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, muss die `edgeConfigId` wird verwendet, um auf die serverseitige Konfiguration zu verweisen. Auf diese Weise können Sie die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

Ihre Organisation muss für diese Funktion freigeschaltet sein. Wenden Sie sich an Ihren Customer Success Manager (CSM), um auf die Zulassungsliste zu gelangen.

## Erstellen einer Datenspeicherkonfiguration

Sie können Datenspeicher in der Datenerfassungs-Benutzeroberfläche erstellen und verwalten, indem Sie **[!UICONTROL Datenspeicher]** in der linken Navigation.

![Tool-Navigation mit Datenspeichern](../images/datastreams/config.png)

>[!NOTE]
>
>Während Sie auf die [!UICONTROL Datenspeicher] -Registerkarte unabhängig davon, ob Sie die Tag-Management-Funktionen von Platform verwenden, müssen Sie über Entwicklerberechtigungen verfügen, um Datenspeicher selbst zu verwalten. Siehe [Benutzerberechtigungen](../../tags/ui/administration/user-permissions.md) in der Dokumentation zu Tags finden Sie weitere Details.

Erstellen Sie einen Datenspeicher, indem Sie auf **[!UICONTROL Neuer Datenspeicher]** im rechten oberen Bereich des Bildschirms. Nachdem Sie einen Namen und eine Beschreibung angegeben haben, werden Sie nach den Standardeinstellungen für jede Umgebung gefragt. Die verfügbaren Einstellungen werden nachfolgend beschrieben.

Beim Erstellen eines Datastreams werden drei Umgebungen automatisch mit identischen Einstellungen erstellt. Diese drei Umgebungen *dev*, *Schritt* und *prod*. Sie entsprechen den drei Standardumgebungen für Tags. Wenn Sie eine Tag-Bibliothek in einer Entwicklungsumgebung erstellen, verwendet die Bibliothek automatisch die Entwicklungsumgebung aus Ihrer Konfiguration. Sie können Einstellungen in einzelnen Umgebungen beliebig bearbeiten.

Die im SDK als `edgeConfigId` ist eine zusammengesetzte ID, die die Konfiguration und die Umgebung angibt (z. B. `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Wenn in der zusammengesetzten ID keine Umgebung vorhanden ist (z. B. `stage` im vorherigen Beispiel), wird die Produktionsumgebung verwendet.

Nachfolgend finden Sie die verfügbaren Einstellungen für jede Konfigurationsumgebung. Die meisten Abschnitte können aktiviert oder deaktiviert werden. Wenn diese Option deaktiviert ist, werden Ihre Einstellungen gespeichert, sie sind jedoch nicht aktiv.

## [!UICONTROL Drittanbieter-ID] settings

Der Abschnitt mit der Drittanbieter-ID ist der einzige Abschnitt, der immer aktiviert ist. Es stehen zwei Einstellungen zur Verfügung: &quot;[!UICONTROL Synchronisierung der Drittanbieter-ID aktiviert]&quot; und &quot;[!UICONTROL Container-ID der Drittanbieter-ID-Synchronisierung]&quot;.

![Identitätsabschnitt der Konfigurationsoberfläche](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Synchronisierung der Drittanbieter-ID aktiviert]

Steuert, ob das SDK Identitätssynchronisierungen mit Drittanbieter-Partnern durchführt.

### [!UICONTROL Container-ID der Drittanbieter-ID-Synchronisierung]

ID-Synchronisationen können in Container gruppiert werden, damit verschiedene ID-Synchronisierungen zu unterschiedlichen Zeiten ausgeführt werden können. Dadurch wird gesteuert, welcher Container mit ID-Synchronisierungen für eine bestimmte Konfigurations-ID ausgeführt wird.

## Adobe Experience Platform-Einstellungen

Mit den hier aufgeführten Einstellungen können Sie Daten an Adobe Experience Platform senden. Sie sollten diesen Abschnitt nur aktivieren, wenn Sie die Adobe Experience Platform erworben haben.

![Adobe Experience Platform-Einstellungsblock](../images/datastreams/platform-config.png)

| Feld | Beschreibung |
| --- | --- |
| [!UICONTROL Sandbox] | **(Erforderlich)** Wählen Sie die Platform-Sandbox aus, an die Sie Daten senden möchten. Sandboxes sind virtuelle Partitionen in Adobe Experience Platform, mit denen Sie Ihre Daten und Implementierungen von anderen in Ihrem Unternehmen isolieren können.<br><br>Wenn Sie einen Datastream erstellen, ohne eine Sandbox auszuwählen, können Sie auch später eine Sandbox auswählen.<br><br>Nachdem ein Datastream erstellt und eine Sandbox ausgewählt wurde, kann die Sandbox nicht mehr geändert werden. Die [!UICONTROL Sandbox] Das Auswahlfeld ist daher beim Bearbeiten eines vorhandenen Datenspeichers mit einer ausgewählten Sandbox nicht verfügbar.<br><br> Die [!UICONTROL Sandbox] Das Auswahlfeld ist daher beim Bearbeiten eines vorhandenen Datenspeichers nicht verfügbar.<br><br>Weitere Informationen zur Rolle von Sandboxes in Experience Platform finden Sie unter [Sandbox-Dokumentation](../../sandboxes/home.md). |
| [!UICONTROL Ereignis-Datensatz] | **(Erforderlich)** Wählen Sie den Platform-Datensatz aus, an den Kundenereignisdaten gestreamt werden. Dieses Schema muss [XDM ExperienceEvent-Klasse](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profildatensatz] | Wählen Sie den Platform-Datensatz aus, an den Kundenattributdaten gesendet werden. Dieses Schema muss [Klasse &quot;XDM Individual Profile&quot;](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Aktivieren Sie dieses Kontrollkästchen, um die Offer decisioning für eine Platform Web SDK-Implementierung zu aktivieren. Siehe Handbuch unter [Verwenden von Offer decisioning mit dem Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) für weitere Implementierungsdetails. Weitere Informationen zu Offer decisioning-Funktionen finden Sie im Abschnitt [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=de). |
| [!UICONTROL Edge-Segmentierung] | Aktivieren Sie dieses Kontrollkästchen, um [Kantensegmentierung](../../segmentation/ui/edge-segmentation.md) für diesen Datastream. Wenn das Platform Web SDK Daten über einen für die Kantensegmentierung aktivierten Datastream sendet, werden alle aktualisierten Segmentmitgliedschaften für das betreffende Profil in der Antwort zurückgesendet.<br><br>Diese Option kann in Kombination mit [!UICONTROL Personalisierungsziele] für [Anwendungsfälle für die Personalisierung der nächsten Seite](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalisierungsziele] | Bei Verwendung in Kombination mit dem [!UICONTROL Edge-Segmentierung] aktivieren, ermöglicht es diese Option dem Datastream, eine Verbindung zu Personalisierungsmaschinen wie Adobe Target herzustellen. Spezifische Schritte finden Sie in der Dokumentation zu Zielen unter [Konfigurieren von Personalisierungszielen](../../destinations/ui/configure-personalization-destinations.md). |

## Adobe Target-Einstellungen

Zum Konfigurieren von Adobe Target müssen Sie einen Clientcode angeben. Die anderen Felder sind optional.

![Adobe Target-Einstellungsblock](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>Die mit dem Clientcode verknüpfte Organisation muss mit der Organisation übereinstimmen, in der die Konfigurations-ID erstellt wird.

### [!UICONTROL Clientcode]

Die eindeutige ID für ein Zielkonto. Um dies zu finden, können Sie zu [!UICONTROL Adobe Target] > [!UICONTROL Einrichtung]> [!UICONTROL Implementierung] > [!UICONTROL Einstellungen bearbeiten] neben dem [!UICONTROL herunterladen] Schaltfläche für [!UICONTROL at.js] oder [!UICONTROL mbox.js]

### [!UICONTROL Eigenschafts-Token]

[!DNL Target] ermöglicht es Kunden, Berechtigungen durch die Verwendung von Eigenschaften zu steuern. Details finden Sie im [Unternehmensberechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=de) Abschnitt [!DNL Target] Dokumentation.

Das Eigenschafts-Token finden Sie unter [!UICONTROL Adobe Target] > [!UICONTROL Setup] > [!UICONTROL Eigenschaften]

### [!UICONTROL Target-Umgebungs-ID]

[Umgebungen](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) in Adobe Target können Sie Ihre Implementierung in allen Entwicklungsstadien verwalten. Diese Einstellung gibt an, welche Umgebung Sie für jede Umgebung verwenden möchten.

Adobe empfiehlt, dies für jeden Ihrer `dev`, `stage`und `prod` Datastream-Umgebungen, um die Dinge einfach zu halten. Wenn Sie jedoch bereits Adobe Target-Umgebungen definiert haben, können Sie diese verwenden.

## Adobe Audience Manager-Einstellungen

Zum Senden von Daten an Adobe Audience Manager ist nur diese Option erforderlich. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Manager-Einstellungsblock](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Cookie-Ziele aktiviert]

Ermöglicht dem SDK das Freigeben von Segmentinformationen über [Cookie-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) von [!DNL Audience Manager].

### [!UICONTROL URL-Ziele aktiviert]

Ermöglicht dem SDK das Freigeben von Segmentinformationen über [URL-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Diese werden in [!DNL Audience Manager].

## Adobe Analytics-Einstellungen

Steuert, ob Daten an Adobe Analytics gesendet werden. Weitere Informationen finden Sie unter [Übersicht über Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-Einstellungsblock](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL Report Suite-ID]

Die Report Suite finden Sie im Adobe Analytics Admin-Abschnitt unter [!UICONTROL Admin > Report Suites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in die einzelnen Report Suites kopiert.
