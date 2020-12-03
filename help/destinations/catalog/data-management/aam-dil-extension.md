---
keywords: Audience Manager DIL extension;destination audience manager;dil extension
title: Audience Manager DIL-Erweiterung
seo-title: Audience Manager DIL-Erweiterung
description: Die Audience Manager DIL-Erweiterung ist ein Data Management Platform (DMP)-Ziel in der Echtzeit-Kundendatenplattform von Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
seo-description: Die Audience Manager DIL-Erweiterung ist ein Data Management Platform (DMP)-Ziel in der Echtzeit-Kundendatenplattform von Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 45%

---


# Audience Manager DIL-Erweiterung {#aam-dil-extension}

## Übersicht {#overview}

Dies ist die Adobe Audience Manager Data Integration Library-Erweiterung (Client-seitige Implementierung). Hinweis: Diese Erweiterung ist nicht für die Server-seitige Weiterleitung (Server-Side Forwarding, SSF) von Adobe Analytics-Daten vorgesehen. Nutzen Sie für SSF die Adobe Analytics-Erweiterung. Important: Starting with version 8.0, DIL has a hard dependency on the [!DNL Experience Cloud] ID Service, version 3.3 or higher. Please implement both [!DNL Experience Cloud] ID Service and DIL for full [!DNL Audience Manager] data integration capabilities.

[!DNL Audience Manager] DIL ist eine Data Management Platform (DMP)-Erweiterung in der Echtzeit-Kundendatenplattform von Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Seite [Audience Manager-Erweiterung](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) in der Experience Platform Launch-Dokumentation.

Dieses Ziel ist eine [!DNL Experience Platform Launch] Erweiterung. Weitere Informationen zur Funktionsweise von Launch-Erweiterungen in der Echtzeit-Kundendatenplattform von finden Sie unter [Experience Platform Launch-Erweiterungen – Übersicht](../launch-extensions/overview.md).

![Audience Manager DIL-Erweiterung](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Voraussetzungen  {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Real-time CDP.

To use this extension, you need access to [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wird Adobe Experience Cloud-Kunden als eine zusätzliche Funktion angeboten. Contact your organization administrator to get access to [!DNL Platform Launch] and ask them to grant you the **[!UICONTROL manage_properties]** permission so you can install extensions.

## Installieren einer Erweiterung {#install-extension}

To install the [!DNL Audience Manager] DIL extension:

In the [Real-time CDP interface](http://platform.adobe.com/), go to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Click on the destination to highlight it, then select **[!UICONTROL Configure]** in the right rail. If the **[!UICONTROL Configure]** control is greyed out, you are missing the **[!UICONTROL manage_properties]** permission. Siehe [Voraussetzungen](#prerequisites).

In the **[!UICONTROL Select available Launch property]** window, select the [!DNL Launch] property in which you want to install the extension. Sie können auch eine neue Eigenschaft in Launch erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Learn about properties in the [Properties page section](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) of the [!DNL Launch] documentation.

The workflow takes you to [!DNL Launch] to complete the installation.

For information about the extension configuration options, see the [Audience Manager extension page](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) in [!DNL Experience Launch] documentation.

You can also install the extension directly in the [Adobe Experience Platform Launch interface](https://launch.adobe.com/). See [Add a new extension](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) in the [!DNL Platform Launch] documentation.

## Verwenden der Erweiterung {#how-to-use}

Once you have installed the extension, you can start setting up rules for it directly in [!DNL Platform Launch].

In [!DNL Platform Launch], you can set up rules for your installed extensions to send event data to the extension destination only in certain situations. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

You can configure, upgrade, and delete extensions in the [!DNL Platform Launch] interface.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Benutzeroberfläche der Echtzeit-Kundendatenplattform von weiterhin **[!UICONTROL Installieren]** für die Erweiterung angezeigt. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Platform Launch]

To upgrade your extension, see [Extension upgrade](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in the [!DNL Platform Launch] documentation.



