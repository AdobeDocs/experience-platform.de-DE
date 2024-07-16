---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Geo; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Geo-Datentyp
description: Erfahren Sie mehr über den Geo-XDM-Datentyp.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 52%

---

# [!UICONTROL Geo]-Datentyp

[!UICONTROL Geo] ist ein standardmäßiger XDM-Datentyp, der den geografischen Bereich beschreibt, in dem ein Ereignis beobachtet wurde.

<img src="../images/data-types/geo.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten eines Orts. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
| `city` | Zeichenfolge | Der Name der Stadt. |
| `countryCode` | Zeichenfolge | Der zweistellige <a href="https://datahub.io/core/country-list">ISO 3166-1-Alpha-2</a>-Code für das Land. |
| `dmaID` | Ganzzahl | Das von Nielsen Media Research ausgewiesene Marktgebiet. |
| `msaID` | Ganzzahl | Das großstädtische statistische Erhebungsgebiet in den USA, in dem die Beobachtung stattfand. |
| `postalCode` | Zeichenfolge | Die Postleitzahl des Ortes. Postleitzahlen sind nicht für alle Länder verfügbar. In einigen Ländern wird dies nur einen Teil der Postleitzahl enthalten. |
| `stateProvince` | Zeichenfolge | Das Bundesland oder die Provinz der Beobachtung. Das Format entspricht der [ISO-Norm 3166-2 (Land und Unterteilung)](https://www.unece.org/cefact/locode/subdivisions.html). |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
