---
title: Google-Ziel
seo-title: Google-Ziel
description: Die Echtzeit-Kundendatenplattform von Adobe ist mit Google integriert, damit Sie Ihre Daten in DV360, Google Ad Manager, Google AdWords und Google AdX ausführen und aktivieren können.
seo-description: Die Echtzeit-Kundendatenplattform von Adobe ist mit Google integriert, damit Sie Ihre Daten in DV360, Google Ad Manager, Google AdWords und Google AdX ausführen und aktivieren können.
translation-type: ht
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google-Ziel

## Übersicht

Die Echtzeit-Kundendatenplattform von Adobe ist mit Google integriert, damit Sie Ihre Daten in DV360, Google Ad Manager, Google AdWords Display und Google AdX ausführen und aktivieren können.

## Zielspezifikationen

Beachten Sie folgende Details, die speziell für Google-Ziele gelten:

* Sie können folgende [Identitäten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) an Google-Ziele senden: **Google Cookie ID, IDFA, GAID**.
* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Echtzeit-Kundendatenplattform von Adobe umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und eine Datenabnahme zu verstehen.

## Voraussetzungen

### Whitelisting

Bevor Sie das Google-Ziel in der Echtzeit-Kundendatenplattform von Adobe verbinden, müssen Sie sich an Google wenden und darum bitten, Ihr Konto auf die Whitelist zu setzen. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Kontokennung**: Dies ist die Adobe-Kontokennung bei Google. Wenden Sie sich an den Adobe Support, um diese Kennung zu erhalten.
* **Kundenkennung**: Dies ist die Adobe-Kundenkonto-Kennung bei Google. Wenden Sie sich an den Adobe Support, um diese Kennung zu erhalten.
* **Partnerkennung**: Dies ist Ihre dreistellige Partnerkennung bei Google.
* **Netzwerkkennung**: Dies ist Ihr Konto bei Google.
* **Zielgruppenverknüpfungskennung**: Dies ist Ihr Konto bei Google.
* Ihr Kontotyp. Dabei kann es sich um **Advertiser einladen**, **Partner einladen**, **DFP**, **AdWords** oder **AdX** handeln.


## Ziel verbinden

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option „Google“ und dann **[!UICONTROL Ziel erstellen]**.
   ![Google-Ziel verbinden](/help/rtcdp/destinations/assets/google-destination.png)

2. Geben Sie im Zielverbindungsassistenten die grundlegenden Informationen für das Ziel ein.
   ![Google-Basisinformationen ](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Name**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **Beschreibung**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **Kontotyp**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `Invite advertiser` für Google DV360.
   * Verwenden Sie `Invite partner` für Google DV360.
   * Verwenden Sie `DFP by Google` für Google Ad Manager.
   * Verwenden Sie `AdWords` für Google AdWords Display.
   * Verwenden Sie `AdX buyer` für Google AdX.
* **Kontokennung**: Geben Sie Ihre Google-Kontokennung ein.

>[!NOTE]
>
>Wenden Sie sich zum Einrichten eines Google-Ziels an Ihren Google-Kundenbetreuer oder Adobe-Support-Mitarbeiter, um zu verstehen, zu welchem Produkttyp Ihr Konto gehört. Wenden Sie sich bei Google DV360 an Ihren Google-Kundenbetreuer, um zu verstehen, zu welchem Produkttyp Ihr Konto gehört. 

## Segmente für Google aktivieren

Anweisungen zum Aktivieren von Segmenten für Google finden Sie unter [Daten für Ziele aktivieren](/help/rtcdp/destinations/activate-destinations.md).