---
title: Google-Ziel
seo-title: Google-Ziel
description: Adobe Echtzeit-CDP ist mit Google integriert, damit Sie Ihre Daten in DV360, Google Ad Manager, Google AdWords und Google AdX ausführen und aktivieren können.
seo-description: Adobe Echtzeit-CDP ist mit Google integriert, damit Sie Ihre Daten in DV360, Google Ad Manager, Google AdWords und Google AdX ausführen und aktivieren können.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google-Ziel

## Übersicht

Adobe Echtzeit-CDP ist mit Google integriert, damit Sie Ihre Daten in DV360, Google Ad Manager, Google AdWords Display und Google AdX ausführen und aktivieren können.

## Zielspezifikationen

Beachten Sie die folgenden Details, die für Google-Ziele spezifisch sind:

* Sie können die folgenden [Identitäten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) an Google-Ziele senden: **Google Cookie-ID, IDFA, GAID**.
* Aktivierte Zielgruppen werden programmgesteuert auf der Google-Plattform erstellt.
* Adobe Echtzeit-CDP enthält derzeit keine Messungsmetrik zur Validierung einer erfolgreichen Aktivierung. Lesen Sie die Zielgruppenzählungen in Google, um die Integration zu validieren und Daten-Dropdown zu verstehen.

## Voraussetzungen

### Whitelisting

Bevor Sie das Google-Ziel in der Adobe Echtzeit-CDP verbinden, müssen Sie sich an Google wenden und um die Whitelist Ihres Kontos bitten. Wenden Sie sich an Google und geben Sie die folgenden Informationen ein:

* **Konto-ID** : dies ist die Adobe-Konto-ID für Google. Wenden Sie sich an den Adobe Support, um diese ID zu erhalten.
* **Kunden-ID** : dies ist die Adobe-Kundenkonto-ID bei Google. Wenden Sie sich an den Adobe Support, um diese ID zu erhalten.
* **Partner-ID** : Dies ist Ihre dreistellige Partner-ID mit Google;
* **Netzwerk-ID** : dies ist Ihr Konto bei Google;
* **Zielgruppen-Link-ID** : dies ist Ihr Konto bei Google;
* Ihr Kontotyp. Dies könnte **Einladungs-Advertiser**, **Einladungspartner**, **DFP**, **AdWords**, **AdX** sein.


## Ziel verbinden

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** Google und dann Ziel **[!UICONTROL erstellen]**.
   ![Google-Ziel verbinden](/help/rtcdp/destinations/assets/google-destination.png)

2. Geben Sie im Verbindungsziel-Assistenten die grundlegenden Informationen für das Ziel ein.
   ![Basisinformationen Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Name**: Geben Sie den bevorzugten Namen für dieses Ziel ein.
* **Beschreibung**: Optional. Sie können beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **Kontotyp**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwendung `Invite advertiser` für Google DV360
   * Verwendung `Invite partner` für Google DV360
   * Verwendung `DFP by Google` für Google Ad Manager
   * Verwendung `AdWords` für Google AdWords-Anzeige
   * Verwendung `AdX buyer` für Google AdX
* **Konto-ID**: Geben Sie Ihre Konto-ID bei Google ein.

>[!NOTE]
>
>Wenden Sie sich beim Einrichten eines Google-Ziels an Ihren Google-Kundenbetreuer oder Adobe-Kundenbetreuer, um zu verstehen, unter welchen Produkttyp Ihr Konto fällt. Bei Google DV360 fragen Sie bitte Ihren Google-Kundenbetreuer, unter welchen Produkttyp Ihr Konto fällt. 

## Aktivieren von Segmenten bei Google

Anweisungen zum Aktivieren von Segmenten in Google finden Sie unter Daten in Ziele [aktivieren](/help/rtcdp/destinations/activate-destinations.md).