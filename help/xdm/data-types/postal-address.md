---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Adresse;xdm:address;datatype;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp der Postanschrift
description: Erfahren Sie mehr über den XDM-Datentyp „Anschrift“.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 35%

---

# [!UICONTROL Postanschrift] Datentyp

[!UICONTROL Postanschrift] ist ein standardmäßiger XDM-Datentyp, der die Details einer Postanschrift beschreibt.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `city` | Der Name der Stadt. |
| `country` | Der Name des von der Regierung verwalteten Gebiets. Dies ist ein Freiformfeld, das den Ländernamen in jeder Sprache enthalten kann. |
| `countryCode` | Der zweistellige <a href="https://datahub.io/core/country-list">ISO 3166-1-Alpha-2</a>-Code für das Land. |
| `createdByBatchID` | Die ID der aufgenommenen Batch-Datei, die den Adressdatensatz erstellt hat. |
| `dmaID` | Das von Nielsen Media Research ausgewiesene Marktgebiet. |
| `label` | Ein Freiformname für die Adresse. |
| `lastVerifiedDate` | Das Datum, an dem die Adresse zuletzt als noch mit der Person verbunden verifiziert wurde. |
| `modifiedByBatchID` | Die ID der aufgenommenen Batch-Datei, die den Datensatz zuletzt geändert hat. |
| `msaID` | Das großstädtische statistische Erhebungsgebiet in den USA, in dem die Beobachtung stattfand. |
| `postOfficeBox` | Das Postfach der Adresse. |
| `postalCode` | Die Postleitzahl des Ortes. Postleitzahlen sind nicht für alle Länder verfügbar. In einigen Ländern wird dies nur einen Teil der Postleitzahl enthalten. |
| `primary` | Ein boolescher Wert, der angibt, ob dies die primäre Adresse des Kontakts ist. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary` haben. |
| `region` | Die Region, der Kreis oder der Bezirk der Adresse. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `stateProvince` | Das Bundesland oder die Provinz der Beobachtung. Das Format entspricht der [ISO-Norm 3166-2 (Land und Unterteilung)](https://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Gibt an, ob die Adresse derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `street1` – `street4` | Diese vier Felder sollen primäre Straßeninformationen, Wohnungsnummer, Straßennummer und Straßennamen enthalten. `street2` zu `street4` sind optional. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp der Postanschrift finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
