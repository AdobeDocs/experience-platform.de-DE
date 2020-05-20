---
title: Adobe Target-Erweiterung
seo-title: Adobe Target-Erweiterung
description: Die Adobe-Erweiterung des Zieldatensatzes ist ein Ziel für die Personalisierung in der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Erweiterungsfunktionalität finden Sie auf der Erweiterungsseite in Adobe Exchange.
seo-description: null
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 15%

---


# Adobe Target-Erweiterung {#adobe-target-extension}

## Übersicht {#overview}

Adobe Target ist die Adobe Experience Cloud-Lösung, die Ihnen all das bietet, was Sie benötigen, um die Erlebnisse Ihrer Kunden anzupassen und zu personalisieren, sodass Sie Umsätze auf Ihren Web- und mobilen Sites, in Apps, sozialen Medien und anderen digitalen Kanälen maximieren können.

Adobe Zielgruppe ist eine Erweiterung der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Erweiterungsfunktionalität finden Sie auf der Seite mit den Erweiterungen in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100162.html).

Dieses Ziel ist eine Experience Platform Launch-Erweiterung. Weitere Informationen zur Funktionsweise von Starterweiterungen in Adobe Echtzeit-CDP finden Sie unter [Experience Platform Launch Extensions - Übersicht](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Adobe Target-Erweiterung](/help/rtcdp/destinations/assets/adobe-target-extension.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im Katalog &quot;Ziele&quot;für alle Kunden verfügbar, die Adobe Echtzeit-CDP erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Experience Platform Launch. Der Start der Experience Platform wird Adobe Experience Cloud-Kunden als eine integrierte Funktion zur Wertschöpfung angeboten. Wenden Sie sich an Ihren Unternehmensadministrator, um Zugriff auf Launch zu erhalten, und bitten Sie ihn, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Erweiterung installieren {#install-extension}

So installieren Sie die Adobe-Erweiterung des Zieldatensatzes:

1. Wechseln Sie in der CDP-Benutzeroberfläche [von](http://platform.adobe.com/)Adobe in Echtzeit zu **[!UICONTROL Ziele > Katalog]**.
2. Wählen Sie die Erweiterung aus dem Katalog oder verwenden Sie die Suchleiste.
3. Klicken Sie auf das Ziel, um es hervorzuheben, und wählen Sie dann in der rechten Leiste die Option Erweiterung **[!UICONTROL installieren]** . Wenn das **[!UICONTROL Install Extension]** -Steuerelement ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]** . Siehe [Voraussetzungen](#prerequisites).
4. Wählen Sie im Fenster **[!UICONTROL Select available Launch property]** die Launch-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie haben auch die Möglichkeit, eine neue Eigenschaft in Launch zu erstellen. Eine Property ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie im Abschnitt [Eigenschaften](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) der Dokumentation Starten.
5. Der Arbeitsablauf führt Sie zum Starten, um die Installation abzuschließen.

Informationen zu den Optionen für die Erweiterungskonfiguration finden Sie auf der Seite &quot; [Adobe-Erweiterung des Zieldatensatzes&quot;](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/target-extension/overview.html) in der Experience Launch-Dokumentation.

Sie können die Erweiterung auch direkt in der [Experience Platform Launch-Oberfläche](https://launch.adobe.com/)installieren. Siehe [Hinzufügen einer neuen Erweiterung](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) in der Dokumentation &quot;Starten&quot;.


## Verwendung der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie Beginn zum Einrichten von Regeln für diese Erweiterung direkt in Launch einrichten.

In Launch können Sie Regeln für Ihre installierten Erweiterungen einrichten, um nur in bestimmten Situationen Ereignis-Daten an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der Dokumentation zu [Regeln](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen der Erweiterung {#configure-upgrade-delete}

Sie können Erweiterungen in der Benutzeroberfläche &quot;Starten&quot;konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits auf einer Ihrer Eigenschaften installiert ist, wird in der CDP-Benutzeroberfläche von Adobe in Echtzeit weiterhin die **[!UICONTROL Installation]** für die Erweiterung angezeigt. Starten Sie den Installationsarbeitsablauf, wie unter [Install extension](#install-extension) beschrieben, um zum Starten und Konfigurieren oder Löschen Ihrer Erweiterung zu gelangen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie unter [Extension-Aktualisierung](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in der Dokumentation Starten.
