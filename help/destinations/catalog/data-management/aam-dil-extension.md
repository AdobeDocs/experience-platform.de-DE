---
keywords: Audience Manager DIL-Erweiterung;Ziel-Audience Manager;dil-Erweiterung
title: Audience Manager DIL-Erweiterung
description: Die Audience Manager DIL-Erweiterung ist ein DMP-Ziel (Data Management Platform) in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 20%

---

# Audience Manager DIL-Erweiterung {#aam-dil-extension}

## Übersicht {#overview}

Dies ist die Adobe Audience Manager Data Integration Library-Erweiterung (Client-seitige Implementierung). Hinweis: Diese Erweiterung ist nicht für die Server-seitige Weiterleitung (Server-Side Forwarding, SSF) von Adobe Analytics-Daten vorgesehen. Nutzen Sie für SSF die Adobe Analytics-Erweiterung. Wichtig: Ab Version 8.0 weist DIL eine feste Abhängigkeit vom ID-Dienst [!DNL Experience Cloud], Version 3.3 oder höher, auf. Implementieren Sie sowohl [!DNL Experience Cloud] ID-Dienst als auch DIL für vollständige [!DNL Audience Manager] Datenintegrationsfunktionen.

[!DNL Audience Manager] DIL ist eine DMP-Erweiterung (Data Management Platform) in Adobe Experience Platform. Weitere Informationen zur Erweiterungsfunktion finden Sie auf der [Seite zur Audience Manager-Erweiterung](../../../tags/extensions/web/audience-manager/overview.md) in der Tag-Dokumentation.

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Erweiterungen in Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Audience Manager DIL-Erweiterung](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Katalog [!DNL Destinations] für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Tags in Adobe Experience Platform. Tags werden Adobe Experience Cloud-Kunden als zusätzliche, Mehrwert bietende Funktion angeboten. Wenden Sie sich an Ihren Organisationsadministrator, um Zugriff auf Tags zu erhalten, und bitten Sie ihn, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die DIL-Erweiterung [!DNL Audience Manager]:

Gehen Sie in der [Platform-Oberfläche](http://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste aus. Wenn das Steuerelement **[!UICONTROL Konfigurieren]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie in der [Tag-Dokumentation](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Der Workflow führt Sie durch die Schritte zum Abschluss der Installation.

Informationen zu den Konfigurationsoptionen für Erweiterungen finden Sie auf der [Seite zur Audience Manager-Erweiterung](../../../tags/extensions/web/audience-manager/overview.md) in der Tag-Dokumentation.

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Weitere Informationen finden Sie im Handbuch zu [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit der Einrichtung von Regeln beginnen. In der Datenerfassungs-Benutzeroberfläche können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignisdaten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Ihre Erweiterungen finden Sie in der Tag-Dokumentation unter [rules](../../../tags/ui/managing-resources/rules.md) .

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, zeigt die Benutzeroberfläche weiterhin **[!UICONTROL Installieren]** für die Erweiterung an. Starten Sie den Installations-Workflow wie unter [Installieren der Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie im Handbuch zum [Prozess für Erweiterungs-Upgrades](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tag-Dokumentation.
