---
keywords: adform extension;adform
title: Erweiterung hinzufügen
seo-title: Erweiterung hinzufügen
description: Die Adobe-Erweiterung ist ein Analysenziel in der Echtzeit-Kundendatenplattform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
seo-description: Die Adobe-Erweiterung ist ein Analysenziel in der Echtzeit-Kundendatenplattform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 39%

---


# Erweiterung hinzufügen {#adform-extension}

## Übersicht {#overview}

Mit der Erweiterung &quot;Adform Website Tracking&quot;können Anzeigenkunden Adform Tracking Points mühelos über die [!DNL Experience Platform Launch] Plattform auf ihren Websites implementieren.

[!DNL Adform] ist eine Analyseerweiterung in der Echtzeit-Kundendatenplattform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)

Dieses Ziel ist eine [!DNL Adobe Experience Platform Launch] Erweiterung. For more information about how [!DNL Platform Launch] extensions work in Adobe Real-time CDP, see [Experience Platform Launch extensions overview](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Erweiterung hinzufügen](/help/rtcdp/destinations/assets/adform-extension.png)

## Voraussetzungen  {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Adobe Real-time CDP.

To use this extension, you need access to [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wird Adobe Experience Cloud-Kunden als eine zusätzliche Funktion angeboten. Contact your organization administrator to get access to [!DNL Platform Launch] and ask them to grant you the **[!UICONTROL manage_properties]** permission so you can install extensions.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die Adobe-Erweiterung:

1. In the [Adobe Real-time CDP interface](http://platform.adobe.com/), go to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.
3. Click on the destination to highlight it, then select **[!UICONTROL Configure]** in the right rail. If the **[!UICONTROL Configure]** control is greyed out, you are missing the **[!UICONTROL manage_properties]** permission. Siehe [Voraussetzungen](#prerequisites).
4. In the **[!UICONTROL Select available Launch property]** window, select the [!DNL Launch] property in which you want to install the extension. Sie können auch eine neue Eigenschaft in Launch erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Learn about properties in the [Properties page section](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/companies-and-properties.html#property-seite) of the [!DNL Launch] documentation.
5. The workflow takes you to [!DNL Launch] to complete the installation.

For information about the extension configuration options and installation support, see the [Adform page on Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html).

You can also install the extension directly in the [Adobe Experience Platform Launch interface](https://launch.adobe.com/). See [Add a new extension](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) in the [!DNL Platform Launch] documentation.


## Verwenden der Erweiterung {#how-to-use}

Once you have installed the extension, you can start setting up rules for it directly in [!DNL Platform Launch].

In [!DNL Platform Launch], you can set up rules for your installed extensions to send event data to the extension destination only in certain situations. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

You can configure, upgrade, and delete extensions in the [!DNL Platform Launch] interface.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Benutzeroberfläche der Echtzeit-Kundendatenplattform von Adobe weiterhin **[!UICONTROL Installieren]** für die Erweiterung angezeigt. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Platform Launch]

To upgrade your extension, see [Extension upgrade](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in the [!DNL Platform Launch] documentation.



