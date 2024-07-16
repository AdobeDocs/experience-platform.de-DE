---
keywords: Analytics-Erweiterung;Analytics-Erweiterung;Ziel-Analyse
title: Adobe Analytics-Erweiterung
description: Die Adobe Analytics-Erweiterung ist ein Analyseziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf Adobe Exchange.
exl-id: 95b6e079-09a6-4262-bd01-11f155286aa9
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 46%

---

# Adobe Analytics-Erweiterung

## Übersicht {#overview}

Adobe Analytics ist eine branchenführende Lösung, mit der Sie Ihre Kunden besser verstehen und Ihr Geschäft mit Customer Intelligence steuern können.

Adobe Analytics ist eine Analyseerweiterung in Adobe Experience Platform. Weitere Informationen zur Erweiterungsfunktion finden Sie unter [Übersicht über die Adobe Analytics-Erweiterung](/help/tags/extensions/client/analytics/overview.md) in der Dokumentation zu Tags .

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Tagerweiterungen in Platform finden Sie in der [Übersicht über Tag-Erweiterungen](../launch-extensions/overview.md).

![Adobe Analytics-Erweiterung](../../assets/catalog/analytics/adobe-analytics/catalog.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Zielkatalog für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Tags in Platform. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an Ihren Organisationsadministrator, um Zugriff auf die Datenerfassungs-Benutzeroberfläche zu erhalten und ihn aufzufordern, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

Installieren der Adobe Analytics-Erweiterung:

Gehen Sie in der [Platform-Oberfläche](https://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste die Option **[!UICONTROL Konfigurieren]** aus. Wenn das Feld **[!UICONTROL Konfigurieren]** ausgegraut ist, verfügen Sie nicht über die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Tag-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie in der Dokumentation zu [Tags](../../../tags/ui/administration/companies-and-properties.md) .

Der Workflow leitet Sie zur Datenerfassungs-Benutzeroberfläche weiter, um die Installation abzuschließen.

Informationen zu den Konfigurationsoptionen für Erweiterungen finden Sie auf der [Adobe Analytics-Erweiterungsseite](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/implement-solutions/analytics.html) in der Tag-Dokumentation.

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Weitere Informationen finden Sie im Handbuch zum Hinzufügen einer neuen Erweiterung [](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit der Einrichtung von Regeln beginnen. In der Datenerfassungs-Benutzeroberfläche können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignisdaten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Ihre Erweiterungen finden Sie in der Tag-Dokumentation unter Überblick über [Regeln](../../../tags/ui/managing-resources/rules.md) .

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, zeigt die Benutzeroberfläche weiterhin **[!UICONTROL Installieren]** für die Erweiterung an. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie in der Anleitung zum [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tags-Dokumentation.
