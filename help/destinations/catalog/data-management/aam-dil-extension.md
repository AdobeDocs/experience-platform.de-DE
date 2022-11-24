---
keywords: Audience Manager DIL-Erweiterung;Ziel-Audience Manager;dil-Erweiterung
title: Audience Manager DIL-Erweiterung
description: Die Audience Manager DIL-Erweiterung ist ein DMP-Ziel (Data Management Platform) in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 24%

---

# Audience Manager DIL-Erweiterung {#aam-dil-extension}

## Übersicht {#overview}

Dies ist die Adobe Audience Manager Data Integration Library-Erweiterung (Client-seitige Implementierung). Hinweis: Diese Erweiterung ist nicht für die Server-seitige Weiterleitung (Server-Side Forwarding, SSF) von Adobe Analytics-Daten vorgesehen. Nutzen Sie für SSF die Adobe Analytics-Erweiterung. Wichtig: Ab Version 8.0 weist DIL eine starke Abhängigkeit von der [!DNL Experience Cloud] ID-Dienst, Version 3.3 oder höher. Implementieren Sie beide [!DNL Experience Cloud] ID-Dienst und DIL [!DNL Audience Manager] Datenintegrationsfunktionen.

[!DNL Audience Manager] DIL ist eine DMP-Erweiterung (Data Management Platform) in Adobe Experience Platform. Weitere Informationen zur Erweiterungsfunktion finden Sie unter [Audience Manager-Erweiterungsseite](../../../tags/extensions/client/audience-manager/overview.md) in der Tag-Dokumentation.

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Erweiterungen in Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Audience Manager DIL-Erweiterung](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Abschnitt [!DNL Destinations] Katalog für alle Kunden, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Tags in Adobe Experience Platform. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an Ihren Organisationsadministrator, um Zugriff auf Tags zu erhalten, und bitten Sie ihn, Ihnen die **[!UICONTROL manage_properties]** -Berechtigung, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Audience Manager] DIL-Erweiterung:

Gehen Sie in der [Platform-Oberfläche](https://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste. Wenn die Variable **[!UICONTROL Konfigurieren]** Kontrolle ausgegraut ist, fehlt die **[!UICONTROL manage_properties]** Berechtigung. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu den Eigenschaften in [Tag-Dokumentation](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Der Workflow führt Sie durch die Schritte zum Abschluss der Installation.

Informationen zu den Konfigurationsoptionen für Erweiterungen finden Sie unter [Audience Manager-Erweiterungsseite](../../../tags/extensions/client/audience-manager/overview.md) in der Tag-Dokumentation.

Sie können die Erweiterung auch direkt im [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/). Siehe Handbuch unter [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) für weitere Informationen.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit der Einrichtung von Regeln beginnen. In der Datenerfassungs-Benutzeroberfläche können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignisdaten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der Übersicht unter [Regeln](../../../tags/ui/managing-resources/rules.md) in der Tag-Dokumentation.

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird die Benutzeroberfläche weiterhin angezeigt **[!UICONTROL Installieren]** für die Erweiterung. Starten Sie den Installations-Workflow wie unter [Installieren der Erweiterung](#install-extension) , um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie im Handbuch im [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tag-Dokumentation.
