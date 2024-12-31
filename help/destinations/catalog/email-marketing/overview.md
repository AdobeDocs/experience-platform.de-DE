---
keywords: Email;e-mail;E-Mail;E-Mail-Ziele
title: E-Mail-Marketing-Ziele – Übersicht
type: Tutorial
description: E-Mail-Dienstanbieter (ESPs) ermöglichen es Ihnen, Ihre E-Mail-Marketing-Aktivitäten zu verwalten, z. B. zum Senden von Werbe-E-Mail-Kampagnen. Erfahren Sie, welche ESPs als Experience Platform-Ziele unterstützt werden.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 4566d5241f287801569e0cfa5b86ea6210fd1638
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 60%

---

# E-Mail-Marketing-Ziele – Übersicht {#email-marketing-destinations}

## Übersicht {#overview}

E-Mail-Service-Anbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-E-Mail-Kampagnen. Adobe Experience Platform lässt sich mit ESPs integrieren, indem Sie Zielgruppen für E-Mail-Marketing-Ziele aktivieren können.

## Unterstützte E-Mail-Marketing-Ziele {#supported-destinations}

Adobe Experience Platform unterstützt die folgenden E-Mail-Marketing-Ziele:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Mailchimp-Interessenkategorien](mailchimp-interest-categories.md)
* [Mailchimp-Tags](mailchimp-tags.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(Dateien) Oracle Eloqua](oracle-eloqua.md)
* [(Dateien) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Verbinden mit einem neuen E-Mail-Marketing-Ziel {#connect-destination}

Um Zielgruppen an E-Mail-Marketing-Ziele für Ihre Kampagnen zu senden, muss Platform zunächst eine Verbindung mit dem Ziel herstellen. Siehe [Tutorial zur Zielerstellung](../../ui/connect-destination.md) für detaillierte Informationen zur Einrichtung eines neuen Ziels.

## Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele {#best-practices}

### Identitätsauswahl {#identity}

Adobe empfiehlt die Auswahl einer eindeutigen Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Dies ist das Feld, in dem Ihre Benutzeridentitäten verschlüsselt werden. In der Regel enthält das Feld die E-Mail-Adresse, es kann aber auch eine Treueprogramm-Kennung oder eine Telefonnummer sein. In der folgenden Tabelle sehen Sie die gängigsten eindeutigen Kennungen und deren XDM-Feld im Schema.

| Eindeutige Kennung | XDM-Feld im einheitlichen Schema |
|----------------- | ---------------------------|
| E-Mail-Adresse | `personalEmail.address` |
| Telefon | `mobilePhone.number` |
| Treueprogramm-Kennung | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Andere Zielattribute {#other-destination-attributes}

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

{style="table-layout:auto"}

## Zielgruppen für E-Mail-Marketing-Ziele aktivieren {#activate}

Einige E-Mail-Marketing-Ziele in den Katalogprofilen werden per Streaming über eine API-Integration mit dem Ziel exportiert.

Andere Ziele exportieren Dateien an einen Cloud-Speicherort. Nach Abschluss des Exports müssen Sie Daten vom Cloud-Speicherort in Ihr E-Mail-Marketing-Ziel importieren.

Folgen Sie den Links im Abschnitt [Unterstützte E-Mail](#supported-destinations)Marketing-Ziele, um zu erfahren, wie Sie Zielgruppen für jedes E-Mail-Marketing-Ziel aktivieren.

## Weitere Ressourcen {#additional-resources}

* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md)
* [Erstellen von E-Mail-Marketing-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](../../api/connect-activate-batch-destinations.md)
