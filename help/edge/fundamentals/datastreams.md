---
title: Konfigurieren Ihres Datenspeichers für das Experience Platform Web SDK
description: 'Erfahren Sie, wie Sie die Datenströme konfigurieren. '
keywords: Konfiguration; Datastreams; datastreamId; edge; datastream id; Umgebungseinstellungen; edgeConfigId; identity; ID-Synchronisierung aktiviert; ID-Sync-Container-ID; Sandbox; Streaming-Inlet; Ereignis-Datensatz; Target; Client-Code; Eigenschaften-Token; Target-Umgebungs-ID; Cookie-Ziele; URL-Ziele; Analytics Settings Blockreport suite id;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---


# Konfigurieren eines Datenspeichers

Die Konfiguration für das Adobe Experience Platform Web SDK ist auf zwei Stellen aufgeteilt. Der Befehl [configure](configuring-the-sdk.md) im SDK steuert Elemente, die auf dem Client verarbeitet werden müssen, z. B. `edgeDomain`. Datastreams verarbeitet alle anderen Konfigurationen für das SDK. Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, wird `edgeConfigId` verwendet, um auf die serverseitige Konfiguration zu verweisen. Auf diese Weise können Sie die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

Ihre Organisation muss für diese Funktion freigeschaltet sein. Wenden Sie sich an Ihren Customer Success Manager (CSM), um auf die Zulassungsliste zu gelangen.

## Erstellen einer Datenspeicherkonfiguration

Datenspeicher können in der Datenerfassungs-Benutzeroberfläche mithilfe des Konfigurationstools Datastream erstellt werden.

![Tool-Navigation mit Datenspeichern](../images/datastreams/config.png)

>[!NOTE]
>
>Das Konfigurationswerkzeug für Datenspeicher steht Kunden auf der Zulassungsliste zur Verfügung, unabhängig davon, ob sie Platform als Tag-Manager verwenden. Darüber hinaus benötigen Benutzer Entwicklungsberechtigungen. Weitere Informationen finden Sie im Artikel [Benutzerberechtigungen](../../tags/ui/administration/user-permissions.md) in der Tag-Dokumentation.

Erstellen Sie einen Datastream, indem Sie oben rechts im Bildschirm auf **[!UICONTROL Neuer Datastream]** klicken. Nachdem Sie einen Namen und eine Beschreibung angegeben haben, werden Sie nach den Standardeinstellungen für jede Umgebung gefragt. Die verfügbaren Einstellungen werden nachfolgend beschrieben.

Beim Erstellen eines Datastreams werden drei Umgebungen automatisch mit identischen Einstellungen erstellt. Diese drei Umgebungen sind *dev*, *stage* und *prod*. Sie entsprechen den drei Standardumgebungen für Tags. Wenn Sie eine Tag-Bibliothek in einer Entwicklungsumgebung erstellen, verwendet die Bibliothek automatisch die Entwicklungsumgebung aus Ihrer Konfiguration. Sie können Einstellungen in einzelnen Umgebungen beliebig bearbeiten.

Die im SDK als `edgeConfigId` verwendete ID ist eine zusammengesetzte ID, die die Konfiguration und die Umgebung angibt (z. B. `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Wenn in der zusammengesetzten ID keine Umgebung vorhanden ist (im vorherigen Beispiel z. B. `stage` ), wird die Produktionsumgebung verwendet.

Nachfolgend finden Sie die verfügbaren Einstellungen für jede Konfigurationsumgebung. Die meisten Abschnitte können aktiviert oder deaktiviert werden. Wenn diese Option deaktiviert ist, werden Ihre Einstellungen gespeichert, sie sind jedoch nicht aktiv.

## [!UICONTROL IDSettings ] von Drittanbietern

Der Abschnitt mit der Drittanbieter-ID ist der einzige Abschnitt, der immer aktiviert ist. Es stehen zwei Einstellungen zur Verfügung: &quot;[!UICONTROL Synchronisation der Drittanbieter-ID aktiviert]&quot;und &quot;[!UICONTROL Container-ID der Drittanbieter-ID]&quot;.

![Identitätsabschnitt der Konfigurationsoberfläche](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Synchronisierung der Drittanbieter-ID aktiviert]

Steuert, ob das SDK Identitätssynchronisierungen mit Drittanbieter-Partnern durchführt.

### [!UICONTROL Container-ID der Drittanbieter-ID-Synchronisierung]

ID-Synchronisationen können in Container gruppiert werden, damit verschiedene ID-Synchronisierungen zu unterschiedlichen Zeiten ausgeführt werden können. Dadurch wird gesteuert, welcher Container mit ID-Synchronisierungen für eine bestimmte Konfigurations-ID ausgeführt wird.

## Adobe Experience Platform-Einstellungen

Mit den hier aufgeführten Einstellungen können Sie Daten an Adobe Experience Platform senden. Sie sollten diesen Abschnitt nur aktivieren, wenn Sie die Adobe Experience Platform erworben haben.

![Adobe Experience Platform-Einstellungsblock](../images/datastreams/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Sandboxes sind Orte in Adobe Experience Platform, die es Kunden ermöglichen, ihre Daten und Implementierungen voneinander zu isolieren. Weitere Informationen zur Funktionsweise finden Sie in der [Sandboxes-Dokumentation](../../sandboxes/home.md).

### [!UICONTROL Streaming-Inlet]

Ein Streaming-Inlet ist eine HTTP-Quelle in Adobe Experience Platform. Diese werden auf der Registerkarte &quot;[!UICONTROL Quellen]&quot;in der Adobe Experience Platform als HTTP-API erstellt.

### [!UICONTROL Ereignis-Datensatz]

Datastreams unterstützen das Senden von Daten an Datensätze mit einem Schema der Klasse [!UICONTROL Erlebnisereignis].

## Adobe Target-Einstellungen

Zum Konfigurieren von Adobe Target müssen Sie einen Clientcode angeben. Die anderen Felder sind optional.

![Adobe Target-Einstellungsblock](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>Die mit dem Clientcode verknüpfte Organisation muss mit der Organisation übereinstimmen, in der die Konfigurations-ID erstellt wird.

### [!UICONTROL Clientcode]

Die eindeutige ID für ein Zielkonto. Um dies zu finden, navigieren Sie zu [!UICONTROL Adobe Target] > [!UICONTROL Setup] [!UICONTROL Implementierung] > [!UICONTROL Bearbeitungseinstellungen] neben der Schaltfläche [!UICONTROL Download] für [!UICONTROL at.js] oder &lt;a1 2/>mbox.js][!UICONTROL 

### [!UICONTROL Eigenschafts-Token]

[!DNL Target] ermöglicht es Kunden, Berechtigungen durch die Verwendung von Eigenschaften zu steuern. Details finden Sie im Abschnitt [Unternehmensberechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=de) der [!DNL Target] -Dokumentation.

Das Eigenschafts-Token finden Sie unter [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Eigenschaften]

### [!UICONTROL Target-Umgebungs-ID]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Mit Umgebungen in Adobe Target können Sie Ihre Implementierung in allen Entwicklungsstadien verwalten. Diese Einstellung gibt an, welche Umgebung Sie für jede Umgebung verwenden möchten.

Adobe empfiehlt, diese Einstellung für jede Ihrer `dev`-, `stage`- und `prod`-Datastream-Umgebungen unterschiedlich festzulegen, um die Dinge einfach zu halten. Wenn Sie jedoch bereits Adobe Target-Umgebungen definiert haben, können Sie diese verwenden.

## Adobe Audience Manager-Einstellungen

Zum Senden von Daten an Adobe Audience Manager ist nur diese Option erforderlich. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Manager-Einstellungsblock](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Cookie-Ziele aktiviert]

Ermöglicht dem SDK das Freigeben von Segmentinformationen über [Cookie-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) von [!DNL Audience Manager].

### [!UICONTROL URL-Ziele aktiviert]

Ermöglicht dem SDK das Freigeben von Segmentinformationen über [URL-Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Diese sind in [!DNL Audience Manager] konfiguriert.

## Adobe Analytics-Einstellungen

Steuert, ob Daten an Adobe Analytics gesendet werden. Weitere Informationen finden Sie unter [Analytics-Übersicht](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-Einstellungsblock](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL Report Suite-ID]

Die Report Suite finden Sie im Adobe Analytics Admin-Abschnitt unter [!UICONTROL Admin > Report Suites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in die einzelnen Report Suites kopiert.
