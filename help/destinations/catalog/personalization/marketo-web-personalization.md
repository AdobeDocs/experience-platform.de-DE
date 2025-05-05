---
keywords: Marketo Web Personalization;Marketo Web Personalization;Marketo Web Personalization-Erweiterung;Marketo Web Personalization Extension;Marketo;Marketo
title: Marketo Web-Personalisierungserweiterung
description: Die Marketo Web Personalization-Erweiterung ist ein Personalisierungsziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf Adobe Exchange.
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 64%

---

# [!DNL Marketo Web Personalization]-Erweiterung {#marketo-web-personalization-extension}

## Übersicht {#overview}

Diese Erweiterung stellt das Skript für [!DNL Marketo's] Web-Personalization- und ContentAI-Anwendungen bereit. [!DNL Marketo] Web Personalization identifiziert und personalisiert Inhalte eindeutig anhand von Web-Besuchermerkmalen, z. B. Firmografien für anonyme Besucher und eine breite Palette von Verhaltensattributen innerhalb der [!DNL Marketo] Interaktionsplattform für bekannte Besucher. [!DNL Marketo] ContentAI enthält Funktionen für KI-gestützte Empfehlungen und Personalisierung für Web- und E-Mail-Kampagnen, die für B2B-Kunden einzigartig sind.

[!DNL Marketo Web Personalization] ist eine Personalisierungserweiterung in Adobe Experience Platform. Weitere Informationen zur Web-Personalisierung und ContentAI in Marketo finden Sie unter [Übersicht über Web-Personalization](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html?lang=de).

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Tag-Erweiterungen in Experience Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Marketo Web Personalization-Erweiterung](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im [!DNL Destinations] für alle Kunden verfügbar, die Experience Platform erworben haben.

Um diese Erweiterung verwenden zu können, müssen Sie Zugriff auf Tags in Adobe Experience Platform haben. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an den Admin Ihrer Organisation, um Zugriff auf Tags zu erhalten, und bitten Sie darum, Ihnen die Berechtigung **[!UICONTROL manage_properties]** zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Marketo Web Personalization]-Erweiterung:

Experience Platform Wechseln Sie in der [&#128279;](https://platform.adobe.com/) von zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann in der rechten Leiste die Option **[!UICONTROL Konfigurieren]** aus. Wenn das Feld **[!UICONTROL Konfigurieren]** ausgegraut ist, verfügen Sie nicht über die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie im [Eigenschaften-Seitenabschnitt](../../../tags/ui/administration/companies-and-properties.md#properties-page) der Tags-Dokumentation.

Der Workflow führt Sie durch die Schritte zum Abschließen der Installation.

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Weitere Informationen finden Sie im Abschnitt zum Thema [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in der Tag-Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit dem Einrichten von Regeln beginnen.

Sie können Regeln für Ihre installierten Erweiterungen einrichten, damit nur in bestimmten Situationen Ereignisdaten an das Erweiterungsziel gesendet werden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Tags-Dokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird in der Experience Platform-Benutzeroberfläche weiterhin &quot;**[!UICONTROL &quot;]** die Erweiterung angezeigt. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie in der Anleitung zum [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tags-Dokumentation.
