---
keywords: livefyre;livefyre extension
title: Adobe Livefyre-Erweiterung
seo-title: Adobe Livefyre-Erweiterung
description: Die Adobe Livefyre-Erweiterung ist ein Social-Media-Ziel in der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
seo-description: Die Adobe Livefyre-Erweiterung ist ein Social-Media-Ziel in der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
translation-type: tm+mt
source-git-commit: 164c51e543d5eba11e4756723f3fecd84ec48f59
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 56%

---


# Adobe Livefyre-Erweiterung {#adobe-livefyre-extension}

## Übersicht {#overview}

Mit Adobe Livefyre können Sie einen konstanten Fluss von anwendergenerierten Inhalten auf Ihrer Website erkunden, organisieren und veröffentlichen, um für authentische und hochpersonalisierte Erlebnisse zu sorgen.

Adobe Livefyre ist eine Social-Media-Erweiterung in der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100464.html).

Dieses Ziel ist eine [!DNL Experience Platform Launch] Erweiterung. For more information about how [!DNL Launch] extensions work in Adobe Real-time CDP, see [Experience Platform Launch extensions overview](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Adobe Livefyre-Erweiterung](/help/rtcdp/destinations/assets/adobe-livefyre-extension.png)


## Voraussetzungen  {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Adobe Real-time CDP.

To use this extension, you need access to [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wird Adobe Experience Cloud-Kunden als eine zusätzliche Funktion angeboten. Contact your organization administrator to get access to [!DNL Launch] and ask them to grant you the **[!UICONTROL manage_properties]** permission so you can install extensions.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die Adobe Livefyre-Erweiterung:

1. In the [Adobe Real-time CDP interface](http://platform.adobe.com/), go to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.
3. Click on the destination to highlight it, then select **[!UICONTROL Configure]** in the right rail. If the **[!UICONTROL Configure]** control is greyed out, you are missing the **[!UICONTROL manage_properties]** permission. Siehe [Voraussetzungen](#prerequisites).
4. In the **[!UICONTROL Select available Launch property]** window, select the [!DNL Launch] property in which you want to install the extension. You also have the option of creating a new property in [!DNL Launch]. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Learn about properties in the [Properties page section](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/companies-and-properties.html#property-seite) of the [!DNL Launch] documentation.
5. The workflow takes you to [!DNL Launch] to complete the installation.

Informationen zu den Konfigurationsoptionen für Erweiterungen und zur Installationsunterstützung finden Sie auf der [Seite zu Adobe Livefyre in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100464.html).

Sie können die Erweiterung auch direkt in der [Benutzeroberfläche von Experience Platform Launch](https://launch.adobe.com/) installieren. See [Add a new extension](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) in the [!DNL Launch] documentation.


## Verwenden der Erweiterung {#how-to-use}

Once you have installed the extension, you can start setting up rules for it directly in [!DNL Launch].

In [!DNL Launch], you can set up rules for your installed extensions to send event data to the extension destination only in certain situations. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

You can configure, upgrade, and delete extensions in the [!DNL Launch] interface.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Benutzeroberfläche der Echtzeit-Kundendatenplattform von Adobe weiterhin **[!UICONTROL Installieren]** für die Erweiterung angezeigt. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Launch]

To upgrade your extension, see [Extension upgrade](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in the [!DNL Launch] documentation.
