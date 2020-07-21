---
title: Google Ads-Ziel
seo-title: Google Ads-Ziel
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
seo-description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 43%

---


# [!DNL Google Ads] Ziel

## Übersicht

[!DNL Google Ads], früher bekannt als [!DNL Google AdWords], ist ein Online-Werbedienst, der es Unternehmen ermöglicht, per Klick Werbung über textbasierte Suchvorgänge, grafische Displays, [!DNL YouTube] Videos und mobile In-App-Displays hinweg zu bezahlen.

## Zielspezifikationen

Note the following details that are specific to [!DNL Google Ads] destinations:

* Sie können die folgenden [Identitäten](../../identity-service/namespaces.md)[!DNL Google Ads] an -Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Activated audiences are created programmatically in the [!DNL Google] platform.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße der Audience zu verstehen.

>[!IMPORTANT]
>
>If you are looking to create your first destination with [!DNL Google Ads] and have not enabled the [ID sync functionality](https://docs.adobe.com/content/help/de-DE/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in the past (with Audience Manager or other applications), please reach out to Adobe Consulting or Customer Care to enable ID syncs. Wenn Sie zuvor Google-Integrationen im Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, an die Echtzeit-Kundendatenplattform von Adobe übertragen.

## Voraussetzungen

### Vorhandenes [!DNL Google Ads] Konto

[!DNL Google] hat alle neuen [!DNL Google Ads] Integrationen mit Drittanbietern angehalten. You must have an existing integration with [!DNL Google Ads] in order to be able to perform the allow list steps in the next section and to create a [!DNL Google Ads] destination in Adobe Real-time CDP.

### Zulassungsliste

>[!NOTE]
>
>Die Zulassungsliste ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ads] Ziel in Adobe Echtzeit-CDP einrichten. Please ensure the allow list process described below has been completed by [!DNL Google] before creating a destination.

Bevor Sie das [!DNL Google Ads] [!DNL Google] Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an Adobe wenden, um die Liste der zulässigen Datenanbieter aufzunehmen und Ihr Konto der Zulassungsliste hinzuzufügen. Contact [!DNL Google] and provide the following information:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei [!DNL Google]. Wenden Sie sich an die Kundenunterstützung von Adobe oder Ihren Adobe-Support-Mitarbeiter, um diese Kennung zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei [!DNL Google]. Wenden Sie sich an die Adobe-Kundenunterstützung oder Ihren Adobe-Support-Mitarbeiter, um die Kennung zu erhalten.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID** : Dies ist Ihre ID mit [!DNL Google]. Das Format der Kennung lautet in der Regel 123-456-7890.

## Ziel erstellen

1. In **[!UICONTROL Connections > Destinations]**, select [!DNL Google Ads], and select **[!UICONTROL Create destination]**.
   ![Google Ads-Ziel verbinden](/help/rtcdp/destinations/assets/google-2-destination.png)

2. In the **Setup** step of the create destination workflow, fill in the [!UICONTROL Basic Information] for the destination. <br>

   ![Google Ads-Basisinformationen ](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID ein [!DNL Google Ads]. Das Format der Kennung lautet in der Regel 123-456-7890.
* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions).

## Activate segments to [!DNL Google Ads]

For instructions on how to activate segments to [!DNL Google Ads], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

