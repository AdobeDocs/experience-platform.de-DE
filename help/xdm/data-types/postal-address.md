---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Adresse;xdm:address;datatype;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp für Postanschrift
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp der Postadresse.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 24%

---

# [!UICONTROL Datentyp ] für Postadressen

[!UICONTROL Postadresse ] ist ein Standard-XDM-Datentyp, der die Details einer Postanschrift beschreibt.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `city` | Der Name der Stadt. |
| `country` | Der Name des von der Regierung verwalteten Gebiets. Dies ist ein Freiformfeld, das den Ländernamen in jeder Sprache enthalten kann. |
| `countryCode` | Der zweistellige <a href="https://datahub.io/core/country-list">ISO 3166-1-Alpha-2</a>-Code für das Land. |
| `createdByBatchID` | Die ID der erfassten Stapeldatei, mit der der Adressdatensatz erstellt wurde. |
| `dmaID` | Die Nielsen-Medienforschung bezeichnete als Marktgebiet. |
| `label` | Ein freier Name für die Adresse. |
| `lastVerifiedDate` | Das Datum, an dem die Adresse zuletzt als mit der Person verbunden bestätigt wurde. |
| `modifiedByBatchID` | Die ID der erfassten Batch-Datei, die den Datensatz zuletzt geändert hat. |
| `msaID` | Das metropolitane statistische Gebiet in den Vereinigten Staaten, in dem die Beobachtung stattfand. |
| `postOfficeBox` | Das Postfach der Adresse. |
| `postalCode` | Die Postleitzahl des Ortes. Postleitzahlen sind nicht für alle Länder verfügbar. In einigen Ländern wird dies nur einen Teil der Postleitzahl enthalten. |
| `primary` | Ein boolescher Wert, der angibt, ob es sich hierbei um die primäre Adresse des Benutzers handelt. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary`-Adresse haben. |
| `region` | Die Region, der Kreis oder der Bezirk der Adresse. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `stateProvince` | Das Bundesland oder die Provinz der Beobachtung. Das Format entspricht der [ISO-Norm 3166-2 (Land und Unterteilung)](http://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Gibt an, ob die Adresse derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `street1` - `street4` | Diese vier Felder enthalten Informationen auf der ersten Straßenseite, die Nummer der Wohnung, die Nummer der Straße und den Namen der Straße. `street2` optional  `street4` sind. |

Weitere Informationen zum Datentyp der Postanschrift finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)
