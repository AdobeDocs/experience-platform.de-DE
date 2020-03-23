---
title: Google Display & Video 360-Ziel
seo-title: Google Display & Video 360-Ziel
description: Display & Video 360, früher DoubleClick Bid Manager genannt, ist ein Tool zum Ausführen von Retargeting und Audience zielgerichteter digitaler Campaign in den Lagerbestandsquellen Display, Video und Mobil.
seo-description: 'Display & Video 360, früher DoubleClick Bid Manager genannt, ist ein Tool zum Ausführen von Retargeting und Audience zielgerichteter digitaler Campaign in den Lagerbestandsquellen Display, Video und Mobil. '
translation-type: tm+mt
source-git-commit: 810028edc662a7f52484e37cf0fbdfafe5db650f

---


# Google Display &amp; Video 360-Ziel

## Übersicht

Display &amp; Video 360, früher DoubleClick Bid Manager genannt, ist ein Tool zum Ausführen von Retargeting und Audience zielgerichteter digitaler Campaign in den Lagerbestandsquellen Display, Video und Mobil.

## Zielspezifikationen

Beachten Sie die folgenden Details, die speziell für Google Display &amp; Video 360-Ziele gelten:

* Sie können die folgenden [Identitäten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) an Google Display &amp; Video 360-Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Lesen Sie die Audiencen in Google, um die Integration zu validieren und die Targeting-Größe der Audience zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Display &amp; Video 360 erstellen möchten und die [ID-Synchronisierungsfunktion](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) in der Vergangenheit (mit Adobe Audience Manager oder anderen Anwendungen) nicht aktiviert haben, wenden Sie sich an Adobe Consulting oder den Kundendienst, um die ID-Synchronisierung zu aktivieren. Wenn Sie zuvor Google-Integrationen im Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf die Adobe Echtzeit-CDP übertragen.

## Voraussetzungen

### Whitelisting

>[!NOTE]
>
>Die Whitelist obligatorisch, bevor Sie Ihr erstes Google Display &amp; Video 360-Ziel in Adobe Echtzeit-CDP einrichten. Vergewissern Sie sich bitte, dass die unten beschriebene Whitelist-Vorgehensweise von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das Google Display &amp; Video 360-Ziel in der Adobe Echtzeit-CDP erstellen, müssen Sie sich an Google wenden und um die Zulassung von Adobe als Datenanbieter und die Positivliste Ihres Kontos bitten. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Ihr Kontotyp**: Verwenden Sie **[!DNL Invite advertiser]** diese Option, um Audiencen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto freizugeben, oder **[!DNL Invite partner]** um zuzulassen, dass Audiencen für alle Marken in Ihrem Display &amp; Video 360-Konto freigegeben werden.

## Ziel erstellen

1. Wählen Sie **[!UICONTROL Connections > Destinations]** in &quot;Google Display &amp; Video 360&quot;die Option **[!UICONTROL Create destination]**.
   ![Google Display &amp; Video 360-Ziel verbinden](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Geben Sie im Assistenten zum Erstellen des Ziels die grundlegenden Informationen für das Ziel ein.
   ![Grundlegende Informationen Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **Name**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **Beschreibung**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **Kontotyp**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie diese Option, `Invite Advertiser` um Audiencen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto freizugeben.
   * Verwenden Sie diese Option, `Invite Partner` um die Freigabe von Audiencen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
* **Konto-ID**: Geben Sie Ihre **[!DNL Invite partner]** Konto-ID oder Ihre **[!DNL Invite advertiser]** Konto-ID bei Google ein. Normalerweise ist dies eine sechsstellige oder siebenstellige ID.

>[!NOTE]
>
>Wenden Sie sich bei der Einrichtung eines Google Display &amp; Video 360-Ziels an Ihren Google-Kundenbetreuer oder Adobe-Kundenbetreuer, um zu verstehen, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten für Google Display &amp; Video 360

For instructions on how to activate segments to Google Display &amp; Video 360, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).