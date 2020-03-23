---
title: Ziel von Google Ad Manager
seo-title: Ziel von Google Ad Manager
description: 'Google Ad Manager, früher DoubleClick für Herausgeber oder DoubleClick AdX, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Anzeigen auf ihren Websites, über Videos und in mobilen Apps zu verwalten. '
seo-description: 'Google Ad Manager, früher DoubleClick für Herausgeber oder DoubleClick AdX, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Anzeigen auf ihren Websites, über Videos und in mobilen Apps zu verwalten. '
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Ziel von Google Ad Manager

## Übersicht

Google Ad Manager, früher DoubleClick für Herausgeber oder DoubleClick AdX, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Anzeigen auf ihren Websites, über Videos und in mobilen Apps zu verwalten.

## Zielspezifikationen

Beachten Sie die folgenden Details, die sich speziell auf Google Ad Manager-Ziele beziehen:

* Sie können die folgenden [Identitäten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) an Google Ad Manager-Ziele senden: **Google-Cookie-ID, IDFA, GAID, Roku-IDs, Microsoft-IDs, Amazon Fire TV-IDs**.
* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Lesen Sie die Audiencen in Google, um die Integration zu validieren und die Targeting-Größe der Audience zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Ad Manager erstellen möchten und die [ID-Synchronisierungsfunktion](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) im Experience Cloud ID-Dienst in der Vergangenheit nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder den Kundendienst, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen im Audience Manager eingerichtet haben, werden die ID-Synchronisierungen, die Sie eingerichtet haben, auf die Adobe Echtzeit-CDP übertragen.

## Voraussetzungen

### Whitelisting

>[!NOTE]
>
>Die Whitelist vor der Einrichtung Ihres ersten Google Ad Manager-Ziels in Adobe Echtzeit-CDP obligatorisch. Vergewissern Sie sich bitte, dass die unten beschriebene Whitelist-Vorgehensweise von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das Google Ad Manager-Ziel in Adobe Echtzeit-CDP erstellen, müssen Sie sich an Google wenden und Adobe bitten, sich als Datenanbieter in die Positivliste zu setzen und Ihr Konto auf die Positivliste zu setzen. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an den Adobe-Kundendienst oder Ihren Adobe-Kundenbetreuer, um diese ID zu erhalten.
* **Netzwerk-ID** : dies ist Ihr Konto bei Google Ad Manager
* **Audience Link-ID** : dies ist Ihr Konto bei Google Ad Manager
* Ihr Kontotyp. **DFP von Google** oder **AdX-Käufer**.

## Ziel erstellen

1. In **[!UICONTROL Connections > Destinations]**, select Google Ad Manager, and select **[!UICONTROL Create destination]**.
   ![Google Ad Manager-Ziel verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Geben Sie im Assistenten zum Erstellen des Ziels die grundlegenden Informationen für das Ziel ein.
   ![Grundlegende Informationen Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **Name**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **Beschreibung**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **Kontotyp**: Wählen Sie je nach Konto bei Google eine Option aus:
   * DoubleClick `DFP by Google` für Herausgeber verwenden
   * Verwenden Sie `AdX buyer` für Google AdX.
* **Kontokennung**: Geben Sie Ihre Google-Kontokennung ein. Dies kann Ihre Netzwerk-ID oder Ihre Audience Link-ID sein. Normalerweise ist dies eine achtstellige ID.

>[!NOTE]
>
>Wenden Sie sich beim Einrichten eines Google Ad Manager-Ziels an Ihren Google-Kundenbetreuer oder Adobe-Kundenbetreuer, um zu verstehen, welchen Kontotyp Sie haben.

## Aktivieren von Segmenten in Google Ad Manager

For instructions on how to activate segments to Google Ad Manager, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).