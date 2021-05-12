---
title: Konfigurieren Sie Ihr Datastream für das Web SDK der Experience Platform
description: 'Erfahren Sie, wie Sie die Datenströme konfigurieren. '
keywords: configuration;datastreams;datastreamId;edge;edge-Konfigurations-ID;Umgebung-Einstellungen;edgeConfigId;identity;id-Synchronisierung aktiviert;ID-Container-ID;Sandbox;Streaming-Inlet;Ereignis-Datensatz;Zielgruppe;Client-Code;Property-Token;Zielgruppe-Umgebung-ID;Cookie-Ziele;URL-Ziele;Analytics-Einstellungen Blocker-Report Suite
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 5642fa155d487982f01d25fa765bb36ad5c3bb21
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---


# Konfigurieren eines Datenspeichers

Die Konfiguration für das Adobe Experience Platform Web SDK ist an zwei Stellen aufgeteilt. Der Befehl [configure](configuring-the-sdk.md) im SDK steuert Elemente, die auf dem Client verarbeitet werden müssen, wie z. B. `edgeDomain`. Datastreams behandeln alle anderen Konfigurationen für das SDK. Wenn eine Anforderung an das Adobe Experience Platform Edge Network gesendet wird, wird `edgeConfigId` verwendet, um auf die serverseitige Konfiguration zu verweisen. Dadurch können Sie die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

Ihre Organisation muss für diese Funktion freigeschaltet sein. Wenden Sie sich an Ihren Customer Success Manager (CSM), um die Zulassungsliste aufzurufen.

## Erstellen einer Datenasterkonfiguration

Datastreams können mit dem Datastream-Konfigurationstool in Adobe [!DNL Experience Platform Launch] erstellt werden.

![datastreams-Tool-Navigation](../../assets/datastreams_config.png)

>[!NOTE]
>
>Das Konfigurationstool &quot;datastreams&quot;steht Kunden auf der Zulassungsliste unabhängig davon zur Verfügung, ob sie [!DNL Experience Platform Launch] als Tag-Manager verwenden. Darüber hinaus benötigen Benutzer Entwicklungsberechtigungen in [!DNL Experience Platform Launch]. Weitere Informationen finden Sie im Artikel [Benutzerberechtigungen](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/user-permissions.html) in der [!DNL Experience Platform Launch]-Dokumentation.

Erstellen Sie einen Datastream, indem Sie oben rechts im Bildschirm auf **[!UICONTROL Neuer Datensatz]** klicken. Nachdem Sie einen Namen und eine Beschreibung angegeben haben, werden Sie nach den Standardeinstellungen für jede Umgebung gefragt. Die verfügbaren Einstellungen sind nachfolgend beschrieben.

Beim Erstellen eines Datastreams werden automatisch drei Umgebung mit identischen Einstellungen erstellt. Diese drei Umgebung sind *dev*, *stage* und *prod*. Sie entsprechen den drei Standardeinstellungen in [!DNL Experience Platform Launch]. Wenn Sie eine [!DNL Experience Platform Launch]-Bibliothek zu einer dev-Umgebung erstellen, verwendet die Bibliothek automatisch die dev-Umgebung Ihrer Konfiguration. Sie können die Einstellungen in den einzelnen Umgebung beliebig bearbeiten.

Die im SDK als `edgeConfigId` verwendete ID ist eine Composite-ID, die die Konfiguration und die Umgebung angibt (z. B. `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Wenn keine Umgebung in der Composite-ID vorhanden ist (im vorherigen Beispiel `stage`), wird die Umgebung &quot;Produktion&quot;verwendet.

Nachfolgend finden Sie die verfügbaren Einstellungen für jede Konfigurationsdatei. Die meisten Abschnitte können aktiviert oder deaktiviert werden. Wenn diese Option deaktiviert ist, werden Ihre Einstellungen gespeichert, sind aber nicht aktiv.

## [!UICONTROL IDS-] Einstellungen von Drittanbietern

Der Drittanbieter-ID-Abschnitt ist der einzige Abschnitt, der immer aktiviert ist. Es stehen zwei Einstellungen zur Verfügung: &quot;[!UICONTROL Synchronisierung der Drittanbieter-ID aktiviert]&quot;und &quot;[!UICONTROL Container-ID-Synchronisierung mit Drittanbieter-ID]&quot;.

![Identitätsabschnitt der Konfigurationsoberfläche](../../assets/edge_configuration_identity.png)

### [!UICONTROL Synchronisierung von Drittanbieter-IDs aktiviert]

Steuert, ob das SDK Identitätssynchronisierungen mit Drittanbieter-Partnern ausführt.

### [!UICONTROL Container-ID für Synchronisierung mit Drittanbieter-ID]

ID-Synchronisierungen können in Container gruppiert werden, damit verschiedene ID-Synchronisierungen zu unterschiedlichen Zeiten ausgeführt werden können. Dadurch wird gesteuert, welcher Container von ID-Synchronisierungen für eine bestimmte Konfigurations-ID ausgeführt wird.

## Adobe Experience Platform-Einstellungen

Mit den hier aufgeführten Einstellungen können Sie Daten an Adobe Experience Platform senden. Sie sollten diesen Abschnitt nur aktivieren, wenn Sie das Adobe Experience Platform erworben haben.

![Adobe Experience Platform-Einstellungsblock](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Sandboxen sind Standorte in Adobe Experience Platform, an denen Kunden ihre Daten und Implementierungen voneinander isolieren können. Weitere Informationen zur Funktionsweise finden Sie in der [Sandbox-Dokumentation](../../sandboxes/home.md).

### [!UICONTROL Streaming-Inlet]

Ein Streaming-Einlass ist eine HTTP-Quelle in Adobe Experience Platform. Diese werden auf der Registerkarte &quot;[!UICONTROL Quellen]&quot;im Adobe Experience Platform als HTTP-API erstellt.

### [!UICONTROL Ereignis DataSet]

Datastreams unterstützen das Senden von Daten an Datasets mit einem Schema der Klasse [!UICONTROL Erlebnis-Ereignis].

## Adobe Target-Einstellungen

Zum Konfigurieren von Adobe Target müssen Sie einen Clientcode angeben. Die anderen Felder sind optional.

![Adobe Target-Einstellungsblock](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>Die mit dem Clientcode verknüpfte Organisation muss mit der Organisation übereinstimmen, in der die Konfigurations-ID erstellt wird.

### [!UICONTROL Clientcode]

Die eindeutige ID für ein Zielgruppen-Konto. Um dies zu finden, navigieren Sie zu [!UICONTROL Adobe Target] > [!UICONTROL Setup] [!UICONTROL Implementierung] > [!UICONTROL Bearbeitungseinstellungen] neben der Schaltfläche [!UICONTROL Download] für [!UICONTROL at.js] oder &lt;a11 2/>mbox.js][!UICONTROL 

### [!UICONTROL Eigenschafts-Token]

[!DNL Target] ermöglicht es Kunden, Berechtigungen über die Verwendung von Eigenschaften zu steuern. Details finden Sie im Abschnitt [Enterprise Permissions](https://docs.adobe.com/content/help/de-DE/target/using/administer/manage-users/enterprise/properties-overview.html) der [!DNL Target]-Dokumentation.

Das Eigenschafts-Token finden Sie unter [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Eigenschaften]

### [!UICONTROL Zielgruppe-Umgebung-ID]

[Mit ](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Umgebungen in Adobe Target können Sie Ihre Implementierung in allen Entwicklungsstadien verwalten. Diese Einstellung gibt an, welche Umgebung Sie für jede Umgebung verwenden möchten.

Adobe empfiehlt, dies für jede Ihrer `dev`-, `stage`- und `prod`-Datastraam-Umgebung anders festzulegen, um die Dinge zu vereinfachen. Wenn Sie jedoch bereits Adobe Target-Umgebung definiert haben, können Sie diese verwenden.

## Adobe Audience Manager-Einstellungen

Alles, was zum Senden von Daten an Adobe Audience Manager erforderlich ist, ist, diesen Abschnitt zu aktivieren. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Einstellungsblock verwalten](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie-Ziele aktiviert]

Ermöglicht dem SDK, Segmentinformationen über [Cookie-Ziele](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) von [!DNL Audience Manager] freizugeben.

### [!UICONTROL URL-Ziele aktiviert]

Ermöglicht dem SDK, Segmentinformationen über [URL-Ziele](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) freizugeben. Diese werden in [!DNL Audience Manager] konfiguriert.

## Adobe Analytics-Einstellungen

Steuert, ob Daten an Adobe Analytics gesendet werden. Weitere Details finden Sie unter [Analytics-Übersicht](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics-Einstellungsblock](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite-ID]

Die Report Suite finden Sie im Abschnitt &quot;Adobe Analytics Admin&quot;unter [!UICONTROL Admin > ReportSuites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in die einzelnen Report Suites kopiert.
