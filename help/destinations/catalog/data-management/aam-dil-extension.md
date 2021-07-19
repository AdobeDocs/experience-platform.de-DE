---
keywords: Audience Manager DIL-Erweiterung;Ziel-Audience Manager;dil-Erweiterung
title: Audience Manager DIL-Erweiterung
description: Die Audience Manager DIL-Erweiterung ist ein DMP-Ziel (Data Management Platform) in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 33%

---

# Audience Manager DIL-Erweiterung {#aam-dil-extension}

## Übersicht {#overview}

Dies ist die Adobe Audience Manager Data Integration Library-Erweiterung (Client-seitige Implementierung). Hinweis: Diese Erweiterung ist nicht für die Server-seitige Weiterleitung (Server-Side Forwarding, SSF) von Adobe Analytics-Daten vorgesehen. Nutzen Sie für SSF die Adobe Analytics-Erweiterung. Wichtig: Ab Version 8.0 weist DIL eine feste Abhängigkeit vom ID-Dienst [!DNL Experience Cloud], Version 3.3 oder höher, auf. Implementieren Sie sowohl [!DNL Experience Cloud] ID-Dienst als auch DIL für vollständige [!DNL Audience Manager] Datenintegrationsfunktionen.

[!DNL Audience Manager] DIL ist eine DMP-Erweiterung (Data Management Platform) in Adobe Experience Platform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Seite [Audience Manager-Erweiterung](../../../tags/extensions/web/audience-manager/overview.md) in der Experience Platform Launch-Dokumentation.

Dieses Ziel ist eine [!DNL Experience Platform Launch] -Erweiterung. Weitere Informationen zur Funktionsweise von Launch-Erweiterungen in Platform finden Sie unter [Übersicht über Experience Platform Launch-Erweiterungen](../launch-extensions/overview.md).

![Audience Manager DIL-Erweiterung](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Katalog [!DNL Destinations] für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wird Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an Ihren Organisationsadministrator, um Zugriff auf [!DNL Platform Launch] zu erhalten, und bitten Sie ihn, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die DIL-Erweiterung [!DNL Audience Manager]:

Gehen Sie in der [Platform-Oberfläche](http://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste aus. Wenn das Steuerelement **[!UICONTROL Konfigurieren]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie im Fenster **[!UICONTROL Verfügbare Launch-Eigenschaft]** die Eigenschaft [!DNL Launch] aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft in Launch erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Weitere Informationen zu Eigenschaften finden Sie im Abschnitt [Eigenschaftenseite](../../../tags/ui/administration/companies-and-properties.md#properties-page) der [!DNL Launch]-Dokumentation.

Der Workflow führt Sie zu [!DNL Launch], um die Installation abzuschließen.

Informationen zu den Konfigurationsoptionen für Erweiterungen finden Sie auf der [Seite zur Audience Manager-Erweiterung](../../../tags/extensions/web/audience-manager/overview.md) in der [!DNL Experience Launch] -Dokumentation.

Sie können die Erweiterung auch direkt in der [Adobe Experience Platform Launch-Benutzeroberfläche](https://launch.adobe.com/) installieren. Siehe [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in der [!DNL Platform Launch] -Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie direkt in [!DNL Platform Launch] Regeln dafür einrichten.

In [!DNL Platform Launch] können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignisdaten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der [!DNL Platform Launch]-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, zeigt die Platform-Benutzeroberfläche weiterhin **[!UICONTROL Installieren]** für die Erweiterung an. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Platform Launch]

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie unter [Erweiterungs-Upgrade](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der [!DNL Platform Launch] -Dokumentation.
