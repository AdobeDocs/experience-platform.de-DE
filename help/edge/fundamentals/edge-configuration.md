---
title: Edge-Konfiguration
seo-title: Edge-Konfiguration für das Web SDK der Experience Platform
description: 'Erfahren Sie, wie Sie das Experience Platform Edge Network konfigurieren. '
seo-description: 'Erfahren Sie, wie Sie das Experience Platform Edge Network konfigurieren. '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 4%

---


# Konfigurieren der Kante

Die Konfiguration für das Adobe Experience Platform [!DNL Web SDK] ist an zwei Stellen aufgeteilt. Der [Befehl](configuring-the-sdk.md) &quot;configure&quot;im SDK steuert Dinge, die auf dem Client verarbeitet werden müssen, z. B. die `edgeDomain`. Die Edge-Konfiguration verarbeitet alle anderen Konfigurationen für das SDK. Wenn eine Anforderung an das Adobe Experience Platform gesendet wird [!DNL Edge Network], `edgeConfigId` wird die serverseitige Konfiguration referenziert. Dadurch können Sie die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

## Erstellen einer Edge-Konfigurations-ID

Edge-Konfigurations-IDs können in Adobe [!DNL Launch] mit dem Edge-Konfigurationstool erstellt werden. Mit diesem Tool können Sie sowohl die Edge-Konfiguration als auch Umgebung in diesen Konfigurationen erstellen.

![Edge-Konfigurationstool](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Das Edge-Konfigurationstool steht Kunden auf der Zulassungsliste unabhängig davon zur Verfügung, ob sie [!DNL Launch] als Tag-Manager arbeiten. Darüber hinaus benötigen Benutzer Entwicklungsberechtigungen in [!DNL Launch]. Weitere Informationen finden Sie im Artikel [Benutzerberechtigungen](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/user-permissions.html) in der [!DNL Launch] Dokumentation.

Sie können eine Edge-Konfiguration erstellen, indem Sie im oberen rechten Bereich des Bildschirms auf **[!UICONTROL Neue Edge-Konfiguration]** klicken. Nachdem Sie einen Namen und eine Beschreibung angegeben haben, werden Sie nach den Standardeinstellungen für jede Umgebung gefragt.

### Standardeinstellungen für Umgebung

Mit diesen Standardeinstellungen werden die ersten drei Umgebung mit identischen Einstellungen erstellt. Diese drei Umgebung sind *dev*, *stage* und *prod*. Sie entsprechen den drei Standardeinstellungen in [!DNL Launch]. Wenn Sie eine [!DNL Launch] Bibliothek zu einer dev-Umgebung erstellen, verwendet die Bibliothek automatisch die dev-Umgebung Ihrer Konfiguration. Sie können die Einstellungen in den einzelnen Umgebung beliebig bearbeiten.

Die im SDK verwendete ID `edgeConfigId` ist eine Composite-ID, die die Konfiguration und die Umgebung angibt. Wenn keine Umgebung vorhanden ist, wird die Umgebung der Produktion verwendet.

### Einstellungen für Umgebung

Nachfolgend sind alle Einstellungen aufgeführt, die für eine Umgebung verfügbar sind. Die meisten Abschnitte können aktiviert oder deaktiviert werden. Wenn diese Option deaktiviert ist, werden Ihre Einstellungen gespeichert, sind aber nicht aktiv.

#### [!UICONTROL Identität]

Der Identitätsabschnitt ist der einzige Abschnitt, der immer aktiviert ist. Es stehen zwei Einstellungen zur Verfügung: &quot;[!UICONTROL ID-Synchronisierungen aktiviert]&quot;und &quot;[!UICONTROL ID-Synchronisierungs-Container-ID]&quot;.

![Identitätsabschnitt der Konfigurationsoberfläche](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID-Synchronisierung aktiviert]

Steuert, ob das SDK Identitätssynchronisierungen mit Drittanbieter-Partnern ausführt.

##### [!UICONTROL ID-Synchronisierungs-Container-ID]

ID-Synchronisierungen können in Container gruppiert werden, damit verschiedene ID-Synchronisierungen zu unterschiedlichen Zeiten ausgeführt werden können. Dadurch wird gesteuert, welcher Container von ID-Synchronisierungen für eine bestimmte Konfigurations-ID ausgeführt wird.

#### Adobe Experience Platform

Mit den hier aufgeführten Einstellungen können Sie Daten an das Adobe Experience Platform senden. Sie sollten diesen Abschnitt nur aktivieren, wenn Sie das Adobe Experience Platform erworben haben.

![Adobe Experience Platform-Einstellungsblock](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Sandboxen sind Standorte in der Adobe Experience Platform, an denen Kunden ihre Daten und Implementierungen voneinander isolieren können. Weitere Informationen zur Funktionsweise finden Sie in der [Sandbox-Dokumentation](../../sandboxes/home.md).

##### [!UICONTROL Streaming-Inlet]

Ein Streaming-Einlass ist eine HTTP-Quelle im Adobe Experience Platform. Diese werden auf der Registerkarte &quot;[!UICONTROL Quellen]&quot;im Adobe Experience Platform als HTTP-API erstellt.

##### [!UICONTROL Ereignis DataSet]

Edge-Konfigurationen unterstützen das Senden von Daten an Datasets mit einem Schema der Klasse [!UICONTROL Experience Ereignis].

#### Adobe Target

Zum Konfigurieren von Adobe Target müssen Sie einen Clientcode angeben. Die anderen Felder sind optional.

![Adobe Target-Einstellungsblock](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>Die mit dem Clientcode verknüpfte Organisation muss mit der Organisation übereinstimmen, in der die Konfigurations-ID erstellt wird.

##### [!UICONTROL Clientcode]

Die eindeutige ID für ein Zielgruppen-Konto. Um dies zu finden, navigieren Sie zu [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementierung] > [!UICONTROL Bearbeitungseinstellungen] neben der Schaltfläche zum [!UICONTROL Herunterladen]  [!UICONTROL für entwederat.jsodermbox.js]

##### [!UICONTROL Eigenschafts-Token]

[!DNL Target] ermöglicht es Kunden, Berechtigungen über die Verwendung von Eigenschaften zu steuern. Details finden Sie im Abschnitt [Enterprise Permissions](https://docs.adobe.com/content/help/de-DE/target/using/administer/manage-users/enterprise/properties-overview.html) in der [!DNL Target] Dokumentation.

Das Eigenschafts-Token finden Sie unter [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

##### [!UICONTROL Zielgruppe-Umgebung-ID]

[Umgebung](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) in Adobe Target unterstützen Sie bei der Verwaltung Ihrer Implementierung in allen Entwicklungsstadien. Diese Einstellung gibt an, welche Umgebung Sie für jede Umgebung verwenden möchten.

Adobe empfiehlt, diese Einstellung für jede Ihrer `dev`-, `stage`- und `prod` Edge-Umgebung anders festzulegen, um die Arbeit zu vereinfachen. Wenn Sie jedoch bereits Adobe Target-Umgebung definiert haben, können Sie diese verwenden.

#### Adobe Audience Manager

Alles, was zum Senden von Daten an Adobe Audience Manager erforderlich ist, ist, diesen Abschnitt zu aktivieren. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience Einstellungsblock verwalten](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie-Ziele aktiviert]

Ermöglicht dem SDK die Freigabe von Segmentinformationen über [Cookie-Ziele](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) von [!DNL Audience Manager].

##### [!UICONTROL URL-Ziele aktiviert]

Ermöglicht dem SDK die Freigabe von Segmentinformationen über [URL-Ziele](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Diese werden in konfiguriert [!DNL Audience Manager].

#### Adobe Analytics

Steuert, ob Daten an Adobe Analytics gesendet werden. Weitere Details finden Sie in der [Analytics-Übersicht](../solution-specific/analytics/analytics-overview.md).

![Adobe Analytics-Einstellungsblock](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite-ID]

Die Report Suite finden Sie im Adobe Analytics Admin-Abschnitt unter [!UICONTROL Admin > Report Suites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in die einzelnen Report Suites kopiert.
