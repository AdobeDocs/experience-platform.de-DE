---
title: Google Display & Video 360-Ziel
seo-title: Google Display & Video 360-Ziel
description: Display & Video 360, früher als DoubleClick Bid Manager bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile.
seo-description: 'Display & Video 360, früher als DoubleClick Bid Manager bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 65%

---


# [!DNL Google Display & Video 360] Ziel

## Übersicht

[!DNL Display & Video 360], früher als bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile.[!DNL DoubleClick Bid Manager]

## Zielspezifikationen

Note the following details that are specific to [!DNL Google Display & Video 360] destinations:

* Sie können die folgenden [Identitäten](../../identity-service/namespaces.md)[!DNL Google Display & Video 360] an -Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Größe des Zielgruppen-Targeting zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Display &amp; Video 360 erstellen möchten und die [ID-Synchronisierungsfunktion](https://docs.adobe.com/content/help/de-DE/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in der Vergangenheit nicht aktiviert hatten (mit Adobe Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um die ID-Synchronisierung zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf die Echtzeit-Kundendatenplattform von Adobe übertragen.

## Voraussetzungen

### Zulassungsliste

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Display & Video 360] Ziel in Adobe Echtzeit-CDP einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene Vorgang der Zulassungsliste von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Display & Video 360] Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an Google wenden und Adobe bitten, die Liste der zulässigen Datenanbieter aufzunehmen und Ihr Konto der Zulassungsliste hinzuzufügen. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an die Adobe-Kundenunterstützung oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Ihr Kontotyp**: Verwenden Sie **[!DNL Invite advertiser]**, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen, oder verwenden Sie **[!DNL Invite partner]**, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.

## Erstellen eines Ziels

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Google Display & Video 360], and select **[!UICONTROL Create destination]**.
   ![Google Display &amp; Video 360-Ziel verbinden](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Geben Sie im Schritt **Setup** des Arbeitsablaufs zum Erstellen des Ziels die [!UICONTROL Grundinformationen] für das Ziel sowie die Anwendungsfälle für das Marketing ein, die für dieses Ziel gelten sollen. <br>

   ![Grundlegende Informationen zu Google Display &amp; Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `Invite Advertiser`, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
   * Verwenden Sie `Invite Partner`, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
* **[!UICONTROL Kontokennung]**: Geben Sie Ihre **[!DNL Invite partner]**- oder **[!DNL Invite advertiser]**-Kontokennung bei Google ein. In der Regel ist dies eine sechsstellige oder siebenstellige ID.
* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions).

>[!NOTE]
>
>When setting up a [!DNL Google Display & Video 360] destination please work with your [!DNL Google Account Manager] or Adobe representative to understand which account type you have.

## Activate segments to [!DNL Google Display & Video 360]

For instructions on how to activate segments to [!DNL Google Display & Video 360], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).