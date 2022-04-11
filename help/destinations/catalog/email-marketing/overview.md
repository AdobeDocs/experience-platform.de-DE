---
keywords: Email;e-mail;E-Mail;E-Mail-Ziele
title: E-Mail-Marketing-Ziele – Übersicht
type: Tutorial
description: E-Mail-Service-Anbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-E-Mail-Kampagnen.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 9d2e98c834eddcacf67de7caafef4717e38d80f8
workflow-type: ht
source-wordcount: '387'
ht-degree: 100%

---

# E-Mail-Marketing-Ziele – Übersicht {#email-marketing-destinations}

## Übersicht {#overview}

E-Mail-Service-Anbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-E-Mail-Kampagnen. Adobe Experience Platform lässt sich mit ESPs integrieren und ermöglicht es Ihnen, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

Platform exportiert Ihre Segmente als `.csv`-Dateien und stellt sie an Ihrem gewünschten Speicherort bereit. Planen Sie den Datenimport in Ihre E-Mail-Marketing-Plattform vom Speicherort, der in [!DNL Platform] aktiviert ist. Das Verfahren zum Importieren von Daten ist je nach Partner unterschiedlich. Weiterführende Informationen finden Sie in den Artikeln zu den einzelnen Zielen.

## Unterstützte E-Mail-Marketing-Ziele {#supported-destinations}

Adobe Experience Platform unterstützt die folgenden E-Mail-Marketing-Ziele:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Verbinden mit einem neuen E-Mail-Marketing-Ziel {#connect-destination}

Damit Segmente an E-Mail-Marketing-Ziele für Ihre Kampagnen gesendet werden können, muss Platform zunächst eine Verbindung zum Ziel herstellen. Siehe [Tutorial zur Zielerstellung](../../ui/connect-destination.md) für detaillierte Informationen zur Einrichtung eines neuen Ziels.

## Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele {#best-practices}

### Identitätsauswahl {#identity}

Adobe empfiehlt die Auswahl einer eindeutigen Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Dies ist das Feld, in dem Ihre Benutzeridentitäten verschlüsselt werden. In der Regel enthält das Feld die E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle sehen Sie die gängigsten eindeutigen Kennungen und deren XDM-Feld im Schema.

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
| Segmentzugehörigkeit | `segmentMembership.status` |

## Importieren von Daten aus Ihrem Speicherort in das Ziel {#import-data-into-destination}

Lesen Sie die Artikel zu den jeweiligen E-Mail-Marketing-Zielen, um zu erfahren, wie Sie Daten von Ihrem Speicherort in Ziele importieren können:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## Aktivieren von Segmenten für E-Mail-Marketing-Ziele {#activate}

Anweisungen zum Aktivieren von Segmenten für E-Mail-Marketing-Ziele finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md).

## Weitere Ressourcen

* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md)
* [Erstellen von E-Mail-Marketing-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](../../api/connect-activate-batch-destinations.md)
