---
title: Google Ads-Ziel
seo-title: Google Ads-Ziel
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
seo-description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 32%

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
>Wenn Sie Ihr erstes Ziel mit Google Ads erstellen möchten und die [ID-Synchronisierungsfunktion](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud ID-Dienst in der Vergangenheit nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder den Kundendienst, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen im Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf die Adobe Echtzeit-CDP übertragen.

## Voraussetzungen

### Vorhandenes Google Ads-Konto

Google hat alle neuen Google Ads-Integrationen mit Drittanbietern angehalten. Sie müssen über eine vorhandene Integration mit Google Ads verfügen, um die Schritte zur Whitelist im nächsten Abschnitt durchführen und ein Google Ads-Ziel in Adobe Echtzeit-CDP erstellen zu können.

### Whitelisting

>[!NOTE]
>
>Die Whitelist vor der Einrichtung Ihres ersten Google Ads-Ziels in Adobe Echtzeit-CDP obligatorisch. Vergewissern Sie sich bitte, dass die unten beschriebene Whitelist-Vorgehensweise von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das Google Ads-Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an Google wenden und Adobe bitten, sich als Datenanbieter in die Positivliste zu setzen und Ihr Konto auf die Positivliste zu setzen. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID** : Dies ist Ihre ID bei Google. Das ID-Format ist in der Regel 123-456-7890.

## Ziel erstellen

1. In **[!UICONTROL Connections > Destinations]**, select Google Ads, and select **[!UICONTROL Create destination]**.
   ![Google-Anzeigenziel verbinden](/help/rtcdp/destinations/assets/google-2-destination.png)

2. In the Create destination workflow, fill in the [!UICONTROL Basic Information] for the destination.
   ![Grundlegende Informationen Google Ads](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID mit Google Ads ein. Das ID-Format ist in der Regel 123-456-7890.

## Aktivieren von Segmenten in Google-Anzeigen

For instructions on how to activate segments to Google Ads, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

