---
keywords: bing; Anzeigen-Ereignisverfolgung; Ereignisverfolgung; UET; UET-Erweiterung
title: Erweiterung für Bing Ads Universal Event Tracking (UET)
description: Die Bing Ads Universal Event Tracking (UET)-Erweiterung ist ein Werbeziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf Adobe Exchange.
exl-id: f2fc4d1f-01b0-4813-902c-9a3c30a8fa78
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 53%

---

# [!DNL Bing Ads Universal Event Tracking] (UET)-Erweiterung {#bing-ads-extension}

## Übersicht {#overview}

Die [!DNL Bing Ads Universal Event Tracking] (UET)-Tag-Erweiterung ist eine nützliche Methode, um zu verfolgen, was passiert, wenn jemand auf Ihre Suchanzeige geklickt hat. Wenn Sie mit einem einzelnen UET-Tag aufzeichnen, was Kunden auf Ihrer Website tun, können Sie diese Daten nutzen, um Konversionen zu verfolgen oder Zielgruppen mithilfe von Remarketing-Listen anzusprechen.

[!DNL Bing Ads Universal Event Tracking] (UET) ist eine Werbeerweiterung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Tags-Erweiterungen in Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Bing Ads-Erweiterung](../../assets/catalog/advertising/bing-ads/catalog.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im [!DNL Destinations]-Katalog für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, müssen Sie Zugriff auf Tags in Adobe Experience Platform haben. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an den Admin Ihrer Organisation, um Zugriff auf Tags zu erhalten, und bitten Sie darum, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Bing Ads Universal Event Tracking] (UET)-Erweiterung:

Gehen Sie in der [Platform-Oberfläche](https://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste die Option **[!UICONTROL Konfigurieren]** aus. Wenn das Feld **[!UICONTROL Konfigurieren]** ausgegraut ist, verfügen Sie nicht über die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Tag-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu den Eigenschaften in [Tag-Dokumentation](../../../tags/ui/administration/companies-and-properties.md).

Der Workflow leitet Sie zur Datenerfassungs-Benutzeroberfläche weiter, um die Installation abzuschließen.

Informationen zu den Konfigurationsoptionen für Erweiterungen und zur Installationsunterstützung finden Sie in der [Bing Ads Universal Event Tracking (UET)-Seite auf Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Siehe Handbuch unter [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) für weitere Informationen.


## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit dem Einrichten von Regeln beginnen. In der Datenerfassungs-Benutzeroberfläche können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignisdaten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der Übersicht unter [Regeln](../../../tags/ui/managing-resources/rules.md) in der Tag-Dokumentation.

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird die Benutzeroberfläche weiterhin angezeigt **[!UICONTROL Installieren]** für die Erweiterung. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie in der Anleitung zum [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tags-Dokumentation.
