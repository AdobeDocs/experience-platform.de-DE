---
keywords: Awin Advertiser mastertag extension;mastertag tag;Awin;awin;AWIN
title: Awin Advertiser Mastertag-Erweiterung
description: Die Awin Advertiser Mastertag Extension ist ein Werbeziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 27%

---


# [!DNL Awin Advertiser Mastertag]-Erweiterung {#awin-mastertag-extension}

## Übersicht {#overview}

Die [!DNL MasterTag] ist eine JavaScript-Bibliothek, die alle für die Awin-Tracking-Lösung erforderlichen Funktionen enthält und bedingungslos an jede Seite der Site angehängt werden sollte, einschließlich der Bestätigungsseite, jedoch ohne jede Seite, die Zahlungsinformationen anzeigt oder verarbeitet.

[!DNL Awin Advertiser Mastertag] ist eine Werbeverlängerung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Dieses Ziel ist eine [!DNL Experience Platform Launch]-Erweiterung. Weitere Informationen zur Funktionsweise von Starterweiterungen in der Plattform finden Sie unter [Übersicht über Experience Platform Launch-Erweiterungen](../launch-extensions/overview.md).

![Awin Advertiser Mastertag-Erweiterung in der Benutzeroberfläche](../../assets/catalog/advertising/awin-mastertag/catalog.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Katalog [!DNL Destinations] für alle Kunden verfügbar, die Platform gekauft haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wird Adobe Experience Cloud-Kunden als eine zusätzliche Funktion angeboten. Wenden Sie sich an Ihren Unternehmensadministrator, um Zugriff auf [!DNL Platform Launch] zu erhalten, und bitten Sie ihn, Ihnen die **[!UICONTROL manage_properties]**-Berechtigung zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die Erweiterung [!DNL Awin Advertiser Mastertag]:

Wechseln Sie in der [Plattform-Schnittstelle](http://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es hervorzuheben, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste aus. Wenn das Steuerelement **[!UICONTROL Configure]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie im Fenster **[!UICONTROL Verfügbare Platform launch-Eigenschaft]** auswählen die [!DNL Platform Launch]-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie haben auch die Möglichkeit, eine neue Eigenschaft in [!DNL Platform Launch] zu erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Weitere Informationen zu Eigenschaften finden Sie im Abschnitt [Seite &quot;Eigenschaften&quot;der [!DNL Launch]-Dokumentation.](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)

Der Arbeitsablauf führt Sie zu [!DNL Platform Launch], um die Installation abzuschließen.

Informationen zu den Konfigurationsoptionen und zur Installationsunterstützung von Erweiterungen finden Sie auf der [Awin Advertiser Mastertag-Seite in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Sie können die Erweiterung auch direkt in der [Adobe Experience Platform Launch-Schnittstelle](https://launch.adobe.com/) installieren. Siehe [Hinzufügen einer neuen Erweiterung](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) in der [!DNL Platform Launch]-Dokumentation.


## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie Beginn zum Einrichten von Regeln für diese Erweiterung direkt in [!DNL Platform Launch] erstellen.

Unter [!DNL Platform Launch] können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignis-Daten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der [!DNL Platform Launch]-Schnittstelle konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits auf einer Ihrer Eigenschaften installiert ist, zeigt die Plattform-Benutzeroberfläche für die Erweiterung weiterhin **[!UICONTROL Install]** an. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Platform Launch]

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie unter [Extension-Aktualisierung](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in der [!DNL Platform Launch]-Dokumentation.
