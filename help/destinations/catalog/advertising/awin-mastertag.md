---
keywords: Awin Advertiser Mastertag-Erweiterung;Master-Tag-Tag;Awin;awin;AWIN
title: Awin Advertiser Mastertag-Erweiterung
description: Die Awin Advertiser Mastertag-Erweiterung ist ein Werbeziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf Adobe Exchange.
exl-id: 99a9ea40-b89f-4503-91a7-60cc8e1cd6d3
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 58%

---

# [!DNL Awin Advertiser Mastertag]-Erweiterung {#awin-mastertag-extension}

## Übersicht {#overview}

Der [!DNL MasterTag] ist eine JavaScript-Bibliothek, die alle für die Awin-Tracking-Lösung erforderlichen Funktionen enthält und bedingungslos an jede Seite der Site angehängt werden sollte, einschließlich der Bestätigungsseite, jedoch ohne Seiten, die Zahlungsinformationen anzeigen oder verarbeiten.

[!DNL Awin Advertiser Mastertag] ist eine Werbeerweiterung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Erweiterungen in Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Awin Advertiser Mastertag-Erweiterung in der Benutzeroberfläche](../../assets/catalog/advertising/awin-mastertag/catalog.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im [!DNL Destinations]-Katalog für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, müssen Sie Zugriff auf Tags in Adobe Experience Platform haben. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an den Admin Ihrer Organisation, um Zugriff auf Tags zu erhalten, und bitten Sie darum, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Awin Advertiser Mastertag]-Erweiterung:

Gehen Sie in der [Platform-Oberfläche](https://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste die Option **[!UICONTROL Konfigurieren]** aus. Wenn das Feld **[!UICONTROL Konfigurieren]** ausgegraut ist, verfügen Sie nicht über die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Tag-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie in der Dokumentation zu [Tags](../../../tags/ui/administration/companies-and-properties.md) .

Der Workflow leitet Sie zur Datenerfassungs-Benutzeroberfläche weiter, um die Installation abzuschließen.

Informationen zu den Konfigurationsoptionen und zur Installationsunterstützung von Erweiterungen finden Sie auf der [Awin Advertiser Mastertag-Seite in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Weitere Informationen finden Sie im Handbuch zum Hinzufügen einer neuen Erweiterung [](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .


## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit der Einrichtung von Regeln beginnen. In der Datenerfassungs-Benutzeroberfläche können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignisdaten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Ihre Erweiterungen finden Sie in der Tag-Dokumentation unter Überblick über [Regeln](../../../tags/ui/managing-resources/rules.md) .

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, zeigt die Benutzeroberfläche weiterhin **[!UICONTROL Installieren]** für die Erweiterung an. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie in der Anleitung zum [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tags-Dokumentation.
