---
title: Bing Ads Universal Ereignis Tracking (UET)-Erweiterung
seo-title: Bing Ads Universal Ereignis Tracking (UET)-Erweiterung
description: Die Erweiterung Bing Ads Universal Ereignis Tracking (UET) ist ein Werbeziel in der Adobe Echtzeit-Kundendatenplattform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Erweiterungsseite in Adobe Exchange.
seo-description: null
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 42%

---


# [!DNL Bing Ads Universal Event Tracking] (UET) Erweiterung {#bing-ads-extension}

## Übersicht {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET) [!DNL Experience Platform Launch] ist eine nützliche Methode, um zu verfolgen, was passiert, wenn jemand auf Ihre Suchanzeige geklickt hat. Durch Verwendung eines einzelnen UET-Tags zur Aufzeichnung der Kundenaktivitäten auf Ihrer Website können Sie diese Daten nutzen, um Konversionen oder Audiencen der Zielgruppe mithilfe von Remarketing-Listen zu verfolgen.

[!DNL Bing Ads Universal Event Tracking] (UET) ist eine Werbeerweiterung in der Adobe Echtzeit-Kundendatenplattform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Erweiterungsseite in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Dieses Ziel ist eine [!DNL Experience Platform Launch] Erweiterung. For more information about how [!DNL Launch] extensions work in Adobe Real-time CDP, see [Experience Platform Launch extensions overview](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Bing Ads Extension](assets/bing-extension.png)


## Voraussetzungen {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Adobe Real-time CDP.

To use this extension, you need access to [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wird Adobe Experience Cloud-Kunden als zusätzliche, nützliche Funktion angeboten. Contact your organization administrator to get access to [!DNL Launch] and ask them to grant you the **[!UICONTROL manage_properties]** permission so you can install extensions.

## Erweiterung installieren {#install-extension}

To install the [!DNL Bing Ads Universal Event Tracking] (UET) extension:

1. Wechseln Sie in der [Benutzeroberfläche der Adobe Echtzeit-Kundendatenplattform](http://platform.adobe.com/) zu **[!UICONTROL Ziele > Katalog]**.
2. Wählen Sie die Erweiterung aus dem Katalog oder verwenden Sie die Suchleiste.
3. Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste **[!UICONTROL Erweiterung installieren]**. Wenn das Steuerelement **[!UICONTROL Erweiterung installieren]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).
4. In the **[!UICONTROL Select available Launch property]** window, select the [!DNL Launch] property in which you want to install the extension. You also have the option of creating a new property in [!DNL Launch]. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Learn about properties in the [Properties page section](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/companies-and-properties.html#Property-Seite) of the [!DNL Launch] documentation.
5. The workflow takes you to [!DNL Launch] to complete the installation.

Informationen zu den Erweiterungskonfigurationsoptionen und zur Installationsunterstützung finden Sie auf der Seite [Bing Ads Universal Ereignis Tracking (UET) in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Sie können die Erweiterung auch direkt in der [Experience Platform Launch-Benutzeroberfläche](https://launch.adobe.com/) installieren. See [Add a new extension](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) in the [!DNL Launch] documentation.


## So verwenden Sie die Erweiterung {#how-to-use}

Once you have installed the extension, you can start setting up rules for it directly in [!DNL Launch].

In [!DNL Launch], you can set up rules for your installed extensions to send event data to the extension destination only in certain situations. Weiterführende Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Dokumentation zu Regeln](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Erweiterung konfigurieren, aktualisieren und löschen {#configure-upgrade-delete}

You can configure, upgrade, and delete extensions in the [!DNL Launch] interface.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Benutzeroberfläche der Adobe Echtzeit-Kundendatenplattform weiterhin **[!UICONTROL Installieren]** für die Erweiterung angezeigt. Starten Sie den Installationsvorgang, wie unter [Erweiterung installieren](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Launch]

To upgrade your extension, see [Extension upgrade](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in the [!DNL Launch] documentation.
