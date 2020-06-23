---
title: Google Ads-Ziel
seo-title: Google Ads-Ziel
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
seo-description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
translation-type: tm+mt
source-git-commit: db2084024f7c25cb1f914f9b8da35298691fd95f
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 28%

---


# Google Ads-Ziel

## Übersicht

Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.

## Zielspezifikationen

Beachten Sie die folgenden Details, die sich speziell auf Google Ads-Ziele beziehen:

* Sie können die folgenden [Identitäten](../../identity-service/namespaces.md) an Google Ads-Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Lesen Sie die Audiencen in Google, um die Integration zu validieren und die Targeting-Größe der Audience zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Ads erstellen möchten und die [ID-Synchronisierungsfunktion](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud-ID-Dienst in der Vergangenheit nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder den Kundendienst, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf Adobe Echtzeit-CDP übertragen.

## Voraussetzungen

### Vorhandenes Google Ads-Konto

Google hat alle neuen Google Ads-Integrationen mit Drittanbietern angehalten. Sie müssen bereits über eine Integration mit Google Ads verfügen, um die zulassungsliste-Schritte im nächsten Abschnitt durchführen und ein Google Ads-Ziel in Adobe Echtzeit-CDP erstellen zu können.

### Zulassungsliste

>[!NOTE]
>
>Die zulassungsliste ist obligatorisch, bevor Sie Ihr erstes Google Ads-Ziel in der Adobe Echtzeit-CDP einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene zulassungsliste-Vorgang von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das Google Ads-Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an Google wenden, damit Adobe die Liste der zulässigen Datenanbieter erhält und Ihr Konto der zulassungsliste hinzugefügt wird. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID** : Dies ist Ihre ID bei Google. Das ID-Format ist in der Regel 123-456-7890.

## Ziel erstellen

1. In **[!UICONTROL Connections > Destinations]**, select Google Ads, and select **[!UICONTROL Create destination]**.
   ![Google-Anzeigenziel verbinden](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Geben Sie im Schritt **Einrichten** des Arbeitsablaufs zum Erstellen des Ziels die [!UICONTROL Grundinformationen] für das Ziel ein. <br>

   ![Grundlegende Informationen Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID mit Google Ads ein. Das ID-Format ist in der Regel 123-456-7890.
* **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions).

## Aktivieren von Segmenten in Google-Anzeigen

For instructions on how to activate segments to Google Ads, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

