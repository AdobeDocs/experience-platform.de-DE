---
keywords: beemray,beemray-Erweiterung
title: Beemray-Erweiterung
description: Die Beemray-Erweiterung ist ein Personalisierungsziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
exl-id: 5bb639f5-42b5-48ae-a3e9-7585595ab925
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 37%

---

# [!DNL Beemray]-Erweiterung  {#beemray-extension}

## Übersicht {#overview}

[!DNL Beemray] hilft Ihnen mit situativem Kontext bei der Beschleunigung Ihres Produkts. So können Sie Einblicke gewinnen, neue Erlebnisse entwickeln, Interaktionen fördern und Momente kreieren, auf die es ankommt. Beemray automatisiert mithilfe von maschinellem Lernen kontextbezogene Kenntnisse. Beemray stellt eine Verbindung zu Adobe Experience Cloud und Ihren anderen technischen Partnern her. Alles findet in Echtzeit statt. Mit dieser Erweiterung wird das [!DNL Beemray]-SDK auf Ihrer Site installiert.

Beemray ist eine Personalisierungserweiterung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

Dieses Ziel ist eine [!DNL Adobe Experience Platform Launch] -Erweiterung. Weitere Informationen zur Funktionsweise von [!DNL Platform Launch]-Erweiterungen in Platform finden Sie unter [Übersicht über Experience Platform Launch-Erweiterungen](../launch-extensions/overview.md).

![Beemray-Erweiterung](../../assets/catalog/personalization/beemray/catalog.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Katalog [!DNL Destinations] für alle Kunden verfügbar, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wird Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an Ihren Organisationsadministrator, um Zugriff auf [!DNL Platform Launch] zu erhalten, und bitten Sie ihn, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Beemray]-Erweiterung:

Gehen Sie in der [Platform-Oberfläche](http://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste aus. Wenn das Steuerelement **[!UICONTROL Konfigurieren]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie im Fenster **[!UICONTROL Verfügbare Platform launch-Eigenschaft]** die Eigenschaft [!DNL Platform Launch] aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft in [!DNL Platform Launch] erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Weitere Informationen zu Eigenschaften finden Sie im Abschnitt [Eigenschaftenseite](../../../tags/ui/administration/companies-and-properties.md#properties-page) der [!DNL Launch]-Dokumentation.

Der Workflow führt Sie zu [!DNL Platform Launch], um die Installation abzuschließen.

Informationen zu den Konfigurationsoptionen für Erweiterungen und zur Installationsunterstützung finden Sie auf der [Beemray-Seite in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

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
