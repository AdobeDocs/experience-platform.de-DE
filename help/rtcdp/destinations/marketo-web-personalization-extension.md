---
title: Marketo Web Personalization-Erweiterung
seo-title: Marketo Web Personalization-Erweiterung
description: Die Marketo Web Personalization-Erweiterung ist ein Personalisierungsziel in der Adobe Echtzeit-Kundendatenplattform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Erweiterungsseite in Adobe Exchange.
seo-description: Die Marketo Web Personalization-Erweiterung ist ein Personalisierungsziel in der Adobe Echtzeit-Kundendatenplattform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Erweiterungsseite in Adobe Exchange.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 94%

---


# [!DNL Marketo Web Personalization] Erweiterung {#marketo-web-personalization-extension}

## Übersicht {#overview}

This extension deploys the script for [!DNL Marketo’s] Web Personalization and ContentAI applications. [!DNL Marketo] Web Personalization identifiziert und personalisiert Inhalte für Web-Besucher-Eigenschaften auf eindeutige Weise, z. B. durch firmographische Daten für anonyme Besucher und eine breite Palette von Verhaltensattributen innerhalb der Engagement Platform für bekannte Besucher. [!DNL Marketo] [!DNL Marketo] ContentAI enthält Funktionen für KI-gestützte Empfehlungen und Personalisierung für Web- und E-Mail-Kampagnen, die für B2B-Kunden einzigartig sind.

[!DNL Marketo Web Personalization] ist eine Personalisierungs-Erweiterung in der Adobe Echtzeit-Kundendatenplattform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Erweiterungsseite in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

Dieses Ziel ist eine Experience Platform Launch-Erweiterung. Weiterführende Informationen zur Funktionsweise von Launch-Erweiterungen in der Adobe Echtzeit-Kundendatenplattform finden Sie unter [Übersicht zu Experience Platform Launch-Erweiterungen](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Marketo Web Personalization-Erweiterung](assets/marketo-web-personalization-extension.png)

## Voraussetzungen {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Adobe Real-time CDP.

Um die Erweiterung verwenden zu können, benötigen Sie Zugriff auf Experience Platform Launch. Experience Platform Launch ist für Adobe Experience Cloud-Kunden als inbegriffene, Mehrwert bietende Funktion verfügbar. Wenden Sie sich an den Administrator Ihrer Organisation, um Zugriff auf Launch zu erhalten, und bitten Sie ihn, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Erweiterung installieren {#install-extension}

So installieren Sie die [!DNL Marketo Web Personalization] Erweiterung:

1. Wechseln Sie in der [Benutzeroberfläche der Adobe Echtzeit-Kundendatenplattform](http://platform.adobe.com/) zu **[!UICONTROL Ziele > Katalog]**.
2. Wählen Sie die Erweiterung aus dem Katalog oder verwenden Sie die Suchleiste.
3. Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste **[!UICONTROL Erweiterung installieren]**. Wenn das Steuerelement **[!UICONTROL Erweiterung installieren]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).
4. Wählen Sie im Fenster **[!UICONTROL Verfügbare Launch-Eigenschaft auswählen]** die Launch-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Außerdem haben Sie die Möglichkeit, in Launch eine neue Eigenschaft zu erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie im Abschnitt [Eigenschaftenseite](https://docs.adobe.com/content/help/de-DE/launch/using/reference/admin/companies-and-properties.html#Property-Seite) der Launch-Dokumentation.
5. Der Workflow führt Sie zu Launch, wo Sie die Installation abschließen können.

Informationen zu den Konfigurationsoptionen für Erweiterungen und zur Installationsunterstützung finden Sie auf der [Seite zur Marketo Web Personalization-Erweiterung in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

Sie können die Erweiterung auch direkt in der [Experience Platform Launch-Benutzeroberfläche](https://launch.adobe.com/) installieren. Siehe [Hinzufügen einer neuen Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) in der Launch-Dokumentation.

## So verwenden Sie die Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie direkt in Launch mit dem Einrichten von Regeln für diese Erweiterung beginnen.

In Launch können Sie Regeln für Ihre installierten Erweiterungen einrichten, um nur in bestimmten Situationen Ereignisdaten an das Erweiterungsziel zu senden. Weiterführende Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Dokumentation zu Regeln](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Erweiterung konfigurieren, aktualisieren und löschen {#configure-upgrade-delete}

Sie können Erweiterungen in der Launch-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Benutzeroberfläche der Adobe Echtzeit-Kundendatenplattform weiterhin **[!UICONTROL Installieren]** für die Erweiterung angezeigt. Starten Sie den Installationsvorgang, wie unter [Erweiterung installieren](#install-extension) beschrieben, um zu Launch zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Upgraden Ihrer Erweiterung finden Sie in der Launch-Dokumentation unter [Erweiterungs-Upgrade](https://docs.adobe.com/content/help/de-DE/launch/using/reference/manage-resources/extensions/extension-upgrade.html).