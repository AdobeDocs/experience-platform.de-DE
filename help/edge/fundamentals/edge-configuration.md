---
title: Edge-Konfiguration
seo-title: Edge-Konfiguration für das Experience Platform Web SDK
description: 'Erfahren Sie, wie Sie das Experience Platform Edge-Netzwerk konfigurieren. '
seo-description: 'Erfahren Sie, wie Sie das Experience Platform Edge-Netzwerk konfigurieren. '
translation-type: tm+mt
source-git-commit: 2d58f7f95c6ad125e66856350aee2f29a0499061
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 3%

---


# Edge-Konfiguration

Die Konfiguration für das Adobe Experience Platform Web SDK ist an zwei Stellen aufgeteilt. Der [Befehl](configuring-the-sdk.md) &quot;configure&quot;im SDK steuert Dinge, die auf dem Client verarbeitet werden müssen, z. B. die `edgeDomain`. Die Edge-Konfiguration verarbeitet alle anderen Konfigurationen für das SDK. Wenn eine Anforderung an das Adobe Experience Platform Edge-Netzwerk gesendet wird, `edgeConfigId` wird die serverseitige Konfiguration mit dem Operator referenziert. Dadurch können Sie die Konfiguration aktualisieren, ohne Codeänderungen auf Ihrer Website vornehmen zu müssen.

## Erstellen einer Edge-Konfigurations-ID

Edge-Konfigurations-IDs können in Launch mit dem Edge-Konfigurationstool erstellt werden. Mit diesem Tool können Sie sowohl die Edge-Konfiguration als auch Umgebung in diesen Konfigurationen erstellen.

![Edge-Konfigurationstool](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Das Edge-Konfigurationstool steht Kunden mit der Liste &quot;Zulassen&quot;zur Verfügung, unabhängig davon, ob sie Launch als Tag-Manager verwenden. Außerdem benötigen Benutzer beim Start Entwicklungsberechtigungen. Weitere Informationen finden Sie im Artikel [Benutzerberechtigungen](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/user-permissions.html) in der Dokumentation zum Starten.

Sie können eine Edge-Konfiguration erstellen, indem Sie oben rechts im Bildschirm auf **[UICONTROL New Edge Configuration]** klicken. Nachdem Sie einen Namen und eine Beschreibung angegeben haben, werden Sie nach den Standardeinstellungen für jede Umgebung gefragt.

### Standardeinstellungen für Umgebung

Mit diesen Standardeinstellungen werden die ersten drei Umgebung mit identischen Einstellungen erstellt. Diese drei Umgebung sind dev, stage und prod. Sie entsprechen den drei Standardeinstellungen in &quot;Start&quot;. Wenn Sie eine Startbibliothek für eine dev-Umgebung erstellen, verwendet die Bibliothek automatisch die dev-Umgebung aus Ihrer Konfiguration. Sie können die Einstellungen in den einzelnen Umgebung beliebig bearbeiten.

Die im SDK verwendete ID `edgeConfigId` ist eine Composite-ID, die die Konfiguration und die Umgebung angibt. Wenn keine Umgebung vorhanden ist, wird die Umgebung der Produktion verwendet.

### Einstellungen für Umgebung

Nachfolgend sind alle Einstellungen aufgeführt, die für eine Umgebung verfügbar sind. Die meisten Abschnitte können aktiviert oder deaktiviert werden. Wenn diese Option deaktiviert ist, werden Ihre Einstellungen gespeichert, sind aber nicht aktiv.

#### [!UICONTROL Identität]

Der Identitätsabschnitt ist der einzige Abschnitt, der immer aktiviert ist. Es stehen zwei Einstellungen zur Verfügung: ID-Synchronisierungen aktiviert und ID-Synchronisierungs-Container-ID.

![Identitätsabschnitt der Konfigurationsoberfläche](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID-Synchronisierung aktiviert]

Steuert, ob das SDK Identitätssynchronisierungen mit Drittanbieter-Partnern ausführt.

##### [!UICONTROL ID-Synchronisierungs-Container-ID]

ID-Synchronisierungen können in Container gruppiert werden, damit verschiedene ID-Synchronisierungen zu unterschiedlichen Zeiten ausgeführt werden können. Dadurch wird gesteuert, welcher Container von ID-Synchronisierungen für eine bestimmte Konfigurations-ID ausgeführt wird.

#### Adobe Experience Platform

Mit den hier aufgeführten Einstellungen können Sie Daten an die Adobe Experience Platform senden. Sie sollten diesen Abschnitt nur aktivieren, wenn Sie die Adobe Experience Platform erworben haben.

![Einstellungsblock für Adobe Experience Platform](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Sandboxes sind Orte in der Adobe Experience Platform, an denen Kunden ihre Daten und Implementierungen voneinander isolieren können. Weitere Informationen zur Funktionsweise finden Sie in der [Sandbox-Dokumentation](../../sandboxes/home.md).

##### [!UICONTROL Streaming-Inlet]

Ein Streaming-Einlass ist eine HTTP-Quelle in der Adobe Experience Platform. Diese werden auf der Registerkarte &quot; [!UICONTROL Quellen] &quot;in der Adobe Experience Platform als HTTP-API erstellt.

##### [!UICONTROL Ereignis DataSet]

Edge-Konfigurationen unterstützen das Senden von Daten an Datasets mit einem Schema der Klasse [!UICONTROL Experience Ereignis].

#### Adobe Target

Zum Konfigurieren von Adobe Zielgruppe müssen Sie einen Clientcode angeben. Die anderen Felder sind optional.

![Einstellungsblock für Adobe Zielgruppe](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>Die mit dem Clientcode verknüpfte Organisation muss mit der Organisation übereinstimmen, in der die Konfigurations-ID erstellt wird.

##### [!UICONTROL Clientcode]

Die eindeutige ID für ein Zielgruppen-Konto. Dazu navigieren Sie zu [!UICONTROL Adobe Zielgruppe] > [!UICONTROL Setup]> [!UICONTROL Implementierung] > [!UICONTROL Bearbeitungseinstellungen] neben der Schaltfläche zum [!UICONTROL Herunterladen]  [!UICONTROL für entwederat.jsodermbox.js]

##### [!UICONTROL Eigenschafts-Token]

Mit der Zielgruppe können Kunden Berechtigungen mithilfe von Eigenschaften steuern. Einzelheiten finden Sie im Abschnitt [Enterprise Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) in der Dokumentation zur Zielgruppe.

Das Eigenschafts-Token befindet sich in [!UICONTROL Adobe Zielgruppe] > [!UICONTROL Setup] > [UICONTROL-Eigenschaften]

##### [!UICONTROL Zielgruppe-Umgebung-ID]

[Umgebung](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) in Adobe Zielgruppe helfen Ihnen, Ihre Implementierung in allen Entwicklungsstadien zu verwalten. Diese Einstellung gibt an, welche Umgebung Sie für jede Umgebung verwenden möchten.

Adobe empfiehlt, diese Einstellung für jede Ihrer `dev`-, `stage`- und `prod` Edge-Konfigurationseinstellungen unterschiedlich festzulegen, um die Arbeit zu vereinfachen. Wenn Sie jedoch bereits [!UICONTROL Adobe Zielgruppe-Umgebung] definiert haben, können Sie diese verwenden.

#### Adobe Audience Manager

Zum Senden von Daten an Adobe Audience Manager müssen Sie diesen Abschnitt nur aktivieren. Die anderen Einstellungen sind optional, werden jedoch empfohlen.

![Adobe Audience - Einstellungsblock verwalten](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie-Ziele aktiviert]

Ermöglicht dem SDK, Segmentinformationen über [Cookie-Ziele](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) von Audience Manager freizugeben.

##### [!UICONTROL URL-Ziele aktiviert]

Ermöglicht dem SDK die Freigabe von Segmentinformationen über [URL-Ziele](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Diese werden im Audience Manager konfiguriert.

#### Adobe Analytics

Steuert, ob Daten an Adobe Analytics gesendet werden. Weitere Details finden Sie in der [Analytics-Übersicht](../solution-specific/analytics/analytics-overview.md).

![Adobe Analytics-Einstellungsblock](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite-ID]

Die Report Suite finden Sie im Adobe Analytics Admin-Abschnitt unter [!UICONTROL Admin > Report Suites]. Wenn mehrere Report Suites angegeben sind, werden die Daten in die einzelnen Report Suites kopiert.
