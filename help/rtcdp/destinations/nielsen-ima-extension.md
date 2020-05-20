---
title: Nielsen IMA Handler Extension
seo-title: Nielsen IMA Handler Extension
description: Die Nielsen IMA Handler Extension ist ein Analyseziel in der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Erweiterungsfunktionalität finden Sie auf der Erweiterungsseite in Adobe Exchange.
seo-description: Die Nielsen IMA Handler Extension ist ein Analyseziel in der Adobe Echtzeit-Kundendatenplattform. Weitere Informationen zur Erweiterungsfunktionalität finden Sie auf der Erweiterungsseite in Adobe Exchange.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 5%

---


# Nielsen IMA Handler Extension {#nielsen-ima-extension}

## Übersicht {#overview}

Nielsen IMA Handler ist eine Analytics-Erweiterung in der Adobe Echtzeit-Kundendatenplattform.

Dieses Ziel ist eine Experience Platform Launch-Erweiterung. Weitere Informationen zur Funktionsweise von Starterweiterungen in Adobe Echtzeit-CDP finden Sie unter [Experience Platform Launch Extensions - Übersicht](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Nielsen IMA Handler Extension](assets/nielsen-ima-extension.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im Katalog &quot;Ziele&quot;für alle Kunden verfügbar, die Adobe Echtzeit-CDP erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Experience Platform Launch. Der Start der Experience Platform wird Adobe Experience Cloud-Kunden als eine integrierte Funktion zur Wertschöpfung angeboten. Wenden Sie sich an Ihren Unternehmensadministrator, um Zugriff auf Launch zu erhalten, und bitten Sie ihn, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Erweiterung installieren {#install-extension}

So installieren Sie die Nielsen IMA Handler-Erweiterung:

1. Wechseln Sie in der CDP-Benutzeroberfläche [von](http://platform.adobe.com/)Adobe in Echtzeit zu **[!UICONTROL Ziele > Katalog]**.
2. Wählen Sie die Erweiterung aus dem Katalog oder verwenden Sie die Suchleiste.
3. Klicken Sie auf das Ziel, um es hervorzuheben, und wählen Sie dann in der rechten Leiste die Option Erweiterung **[!UICONTROL installieren]** . Wenn das **[!UICONTROL Install Extension]** -Steuerelement ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]** . Siehe [Voraussetzungen](#prerequisites).
4. Wählen Sie im Fenster **[!UICONTROL Select available Launch property]** die Launch-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie haben auch die Möglichkeit, eine neue Eigenschaft in Launch zu erstellen. Eine Property ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie im Abschnitt [Eigenschaften](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) der Dokumentation Starten.
5. Der Arbeitsablauf führt Sie zum Starten, um die Installation abzuschließen.

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