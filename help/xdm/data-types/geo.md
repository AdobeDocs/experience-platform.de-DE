---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Geo;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Geo-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Geo XDM-Datentyp.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 36%

---

#  Geodatentyp

 Geois ist ein standardmäßiger XDM-Datentyp, der das geografische Gebiet beschreibt, in dem ein Ereignis beobachtet wurde.

<img src="../images/data-types/geo.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten eines Orts. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
| `city` | Zeichenfolge | Der Name der Stadt. |
| `countryCode` | Zeichenfolge | Der zweistellige <a href="https://datahub.io/core/country-list">ISO 3166-1-Alpha-2</a>-Code für das Land. |
| `dmaID` | Ganzzahl | Die Nielsen-Medienforschung bezeichnete als Marktgebiet. |
| `msaID` | Ganzzahl | Das metropolitane statistische Gebiet in den Vereinigten Staaten, in dem die Beobachtung stattfand. |
| `postalCode` | Zeichenfolge | Die Postleitzahl des Ortes. Postleitzahlen sind nicht für alle Länder verfügbar. In einigen Ländern wird dies nur einen Teil der Postleitzahl enthalten. |
| `stateProvince` | Zeichenfolge | Das Bundesland oder die Provinz der Beobachtung. Das Format entspricht der [ISO-Norm 3166-2 (Land und Unterteilung)](http://www.unece.org/cefact/locode/subdivisions.html). |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)
