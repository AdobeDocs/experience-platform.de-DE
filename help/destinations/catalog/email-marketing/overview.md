---
keywords: Email;e-mail;E-Mail;E-Mail-Ziele
title: E-Mail-Marketing-Ziele – Übersicht
type: Tutorial
description: E-Mail-Service-Anbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-E-Mail-Kampagnen. Erfahren Sie, welche ESPs als Experience Platform-Ziele unterstützt werden.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6ea94b275ab0ed7c0638200188fe7ada7bacf5c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# E-Mail-Marketing-Ziele – Übersicht {#email-marketing-destinations}

## Übersicht {#overview}

E-Mail-Service-Anbieter (ESPs) ermöglichen Ihnen die Verwaltung Ihrer E-Mail-Marketing-Aktivitäten, z. B. beim Senden von Werbe-E-Mail-Kampagnen. Adobe Experience Platform lässt sich mit ESPs integrieren und ermöglicht es Ihnen, Segmente für E-Mail-Marketing-Ziele zu aktivieren.

## Unterstützte E-Mail-Marketing-Ziele {#supported-destinations}

Adobe Experience Platform unterstützt die folgenden E-Mail-Marketing-Ziele:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) Salesforce Marketing Cloud](salesforce-marketing-cloud-exact-target.md)
* [(Dateien) Oracle Eloqua](oracle-eloqua.md)
* [(Dateien) Salesforce-Marketing Cloud](salesforce-marketing-cloud.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

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

## Aktivieren von Segmenten für E-Mail-Marketing-Ziele {#activate}

Einige E-Mail-Marketing-Ziele in den Katalogprofilen werden streaming über eine API-Integration mit dem Ziel exportiert.

Andere Ziele exportieren Dateien an einen Cloud-Speicher-Speicherort. Nach Abschluss des Exports müssen Sie Daten vom Cloud-Speicher in Ihr E-Mail-Marketing-Ziel importieren.

Befolgen Sie die Links im [unterstützte E-Mail-Marketing-Ziele](#supported-destinations) Informationen zum Aktivieren von Segmenten für jedes E-Mail-Marketing-Ziel.

## Weitere Ressourcen {#additional-resources}

* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md)
* [Erstellen von E-Mail-Marketing-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](../../api/connect-activate-batch-destinations.md)
