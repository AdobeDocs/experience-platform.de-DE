---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele
title: E-Mail-Marketing-Ziele – Übersicht
type: Tutorial
description: E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 9d2e98c834eddcacf67de7caafef4717e38d80f8
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 39%

---

# E-Mail-Marketing-Ziele – Übersicht {#email-marketing-destinations}

## Übersicht {#overview}

E-Mail-Dienstanbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-Mail-Kampagnen. Adobe Experience Platform lässt sich mit ESPs integrieren, indem es Ihnen ermöglicht, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

Platform exportiert Ihre Segmente als `.csv` -Dateien und stellt sie an Ihrem gewünschten Speicherort bereit. Planen Sie Ihren Datenimport in Ihre E-Mail-Marketing-Plattform vom Speicherort, der unter aktiviert ist. [!DNL Platform]. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Weitere Informationen finden Sie in den Artikeln zu den einzelnen Zielen .

## Unterstützte E-Mail-Marketing-Ziele {#supported-destinations}

Adobe Experience Platform unterstützt die folgenden E-Mail-Marketing-Ziele:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Mit einem neuen E-Mail-Marketing-Ziel verbinden {#connect-destination}

Um für Ihre Kampagnen Segmente an E-Mail-Marketing-Ziele zu senden, muss Platform zunächst eine Verbindung zum Ziel herstellen. Siehe [Tutorial zur Zielerstellung](../../ui/connect-destination.md) für detaillierte Informationen zur Einrichtung eines neuen Ziels.

## Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele {#best-practices}

### Identitätsauswahl {#identity}

Adobe empfiehlt, eine eindeutige Kennung aus der [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Dies ist das Feld, aus dem Ihre Benutzeridentitäten abgeleitet werden. In der Regel besteht das Feld aus der E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle finden Sie die gängigsten eindeutigen Kennungen und deren XDM-Feld im Schema.

| Eindeutige Kennung | XDM-Feld im einheitlichen Schema |
|----------------- | ---------------------------|
| E-Mail-Adresse | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Treueprogramm-Kennung | `Customer-defined XDM field` |

### Andere Zielattribute

Wählen Sie in der Schemafeldauswahl die anderen Felder aus, die Sie an das E-Mail-Ziel exportieren möchten. Zu den empfohlenen Optionen gehören:

| Schema | XDM-Feld |
|------ | ---------|
| Vorname | `person.name.firstName` |
| Nachname | `person.name.lastName` |
| Telefon | `mobilePhone.number` |
| Adresse Ort | `homeAddress.city` |
| Adresse Bundesland | `homeAddress.stateProvince` |
| Adresse Postleitzahl | `homeAddress.postalCode` |
| Geburtstag | `person.birthDayAndMonth` |
| Segmentmitgliedschaft | `segmentMembership.status` |

## Importieren von Daten aus Ihrem Speicherort in das Ziel {#import-data-into-destination}

Lesen Sie die einzelnen Artikel zu E-Mail-Marketing-Zielen , um zu erfahren, wie Sie Daten von Ihrem Speicherort in Ziele importieren:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce-Marketing Cloud](salesforce-marketing-cloud.md)

## Segmente für E-Mail-Marketing-Ziele aktivieren {#activate}

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md).

## Weitere Ressourcen

* [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md)
* [Erstellen von E-Mail-Marketing-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](../../api/connect-activate-batch-destinations.md)
