---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Adresse; xdm:address; Datentyp; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp der Postanschrift
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Postadresse.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 25%

---

# [!UICONTROL Datentyp ] der Postanschrift

[!UICONTROL Postanschrift ] ist ein standardmäßiger XDM-Datentyp, der die Details einer Postanschrift beschreibt.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `city` | Der Name der Stadt. |
| `country` | Der Name des von der Regierung verwalteten Gebiets. Dies ist ein Freiformfeld, das den Ländernamen in jeder Sprache enthalten kann. |
| `countryCode` | Der zweistellige <a href="https://datahub.io/core/country-list">ISO 3166-1-Alpha-2</a>-Code für das Land. |
| `createdByBatchID` | Die ID der erfassten Batch-Datei, mit der der Adressdatensatz erstellt wurde. |
| `dmaID` | Die Nielsen-Medienforschung bezeichnete ein Marktgebiet. |
| `label` | Ein freier Name für die Adresse. |
| `lastVerifiedDate` | Das Datum, an dem zuletzt überprüft wurde, ob die Adresse noch mit der Person verbunden ist. |
| `modifiedByBatchID` | Die Kennung der aufgenommenen Batch-Datei, die den Datensatz zuletzt geändert hat. |
| `msaID` | Das metropolitane statistische Gebiet in den Vereinigten Staaten, in dem die Beobachtung stattfand. |
| `postOfficeBox` | Das Postfach der Adresse. |
| `postalCode` | Die Postleitzahl des Ortes. Postleitzahlen sind nicht für alle Länder verfügbar. In einigen Ländern wird dies nur einen Teil der Postleitzahl enthalten. |
| `primary` | Ein boolescher Wert, der anzeigt, ob dies die primäre Adresse des Kontakts ist. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary`-Adresse haben. |
| `region` | Die Region, der Kreis oder der Bezirk der Adresse. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `stateProvince` | Das Bundesland oder die Provinz der Beobachtung. Das Format entspricht der [ISO-Norm 3166-2 (Land und Unterteilung)](http://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Gibt an, ob die Adresse derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `street1` - `street4` | Diese vier Felder sollen Informationen auf der primären Straßenniveau, Wohnungsnummer, Straßennummer und Straßenname enthalten. `street2` optional  `street4` sind. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp der Postanschrift finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)
