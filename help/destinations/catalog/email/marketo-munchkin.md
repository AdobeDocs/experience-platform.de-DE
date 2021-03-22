---
keywords: Marketo Munchkin;marketo munchkin;Marketo Munchkin extension;marketo munchkin extension;marketo;Marketo
title: Marketo Munchkin-Erweiterung
description: Die Marketo-Munchkin-Erweiterung ist ein Personalisierungsziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 19%

---


# [!DNL Marketo Munchkin]-Erweiterung {#marketo-munchkin-extension}

## Übersicht {#overview}

Von der Interessentenverwaltung bis hin zum kontenbasierten Marketing vereinfacht [!DNL Marketo Engagement Platform], wie Sie die Interaktion mit Kunden und Potenzieller Kunden in jeder Phase ihrer Erfahrung planen, organisieren und messen.

[!DNL Marketo’s Munchkin] JavaScript ermöglicht die Verfolgung von Seitenbesuchen und Klicks auf Ihre  [!DNL Marketo] Landingpages und externen Webseiten durch Endbenutzer.

[!DNL Marketo Munchkin] ist eine E-Mail-Erweiterung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html).

Dieses Ziel ist eine Adobe Experience Platform Launch-Erweiterung. Weitere Informationen zur Funktionsweise von Platform launch-Erweiterungen in Platform finden Sie unter [Übersicht über Adobe Experience Platform Launch-Erweiterungen](../launch-extensions/overview.md).

![Marketo Munchkin-Erweiterung](../../assets/catalog/email/marketo-munchkin/catalog.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im Katalog [!DNL Destinations] für alle Kunden verfügbar, die Platform gekauft haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Adobe Experience Platform Launch.  Platform Launch ist für Adobe Experience Cloud-Kunden als integrierte, Mehrwert bietende Funktion verfügbar. Wenden Sie sich an Ihren Unternehmensadministrator, um Zugriff auf Platform launch zu erhalten, und bitten Sie ihn, Ihnen die **[!UICONTROL manage_properties]**-Berechtigung zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die Erweiterung [!DNL Marketo Munchkin]:

Wechseln Sie in der [Plattform-Schnittstelle](http://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es hervorzuheben, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste aus. Wenn das Steuerelement **[!UICONTROL Configure]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie im Fenster **[!UICONTROL Verfügbare Platform launch-Eigenschaft]** auswählen die Platform launch-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie haben auch die Möglichkeit, eine neue Eigenschaft im Platform launch zu erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Weitere Informationen zu den Eigenschaften finden Sie im Abschnitt [Eigenschaftenseite](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) der Platform launch-Dokumentation.

Der Arbeitsablauf führt Sie zum Platform launch, um die Installation abzuschließen.

Informationen zu den Erweiterungskonfigurationsoptionen und der Installationsunterstützung finden Sie auf der Seite [Marketo Munchkin unter Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html).

Sie können die Erweiterung auch direkt in der [Adobe Experience Platform Launch-Schnittstelle](https://launch.adobe.com/) installieren. Siehe [Hinzufügen einer neuen Erweiterung](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) in der Platform launch-Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie Beginn zum Einrichten von Regeln für diese direkt in Platform launch verwenden.

Unter Platform launch können Sie Regeln für Ihre installierten Erweiterungen einrichten, um nur in bestimmten Situationen Ereignis-Daten an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Platform launch-Oberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits auf einer Ihrer Eigenschaften installiert ist, zeigt die Plattform-Benutzeroberfläche für die Erweiterung weiterhin **[!UICONTROL Install]** an. Starten Sie den Installationsarbeitsablauf wie unter [Erweiterung installieren](#install-extension) beschrieben, um zum Platform launch zu gelangen und Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie unter [Extension-Aktualisierung](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in der Platform launch-Dokumentation.