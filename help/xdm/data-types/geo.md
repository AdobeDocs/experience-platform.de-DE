---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Geo;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Geo-Datentyp
description: Erfahren Sie mehr über den Geo-XDM-Datentyp.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 52%

---

# [!UICONTROL Geo]-Datentyp

[!UICONTROL Geo] ist ein standardmäßiger XDM-Datentyp, der das geografische Gebiet beschreibt, in dem ein Ereignis beobachtet wurde.

![](../images/data-types/geo.png){width=400}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten eines Ortes. |
| `_id` | String | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
| `city` | String | Der Name der Stadt. |
| `countryCode` | String | Der zweistellige <a href="https://datahub.io/core/country-list">ISO 3166-1-Alpha-2</a>-Code für das Land. |
| `dmaID` | Ganzzahl | Das von Nielsen Media Research ausgewiesene Marktgebiet. |
| `msaID` | Ganzzahl | Das großstädtische statistische Erhebungsgebiet in den USA, in dem die Beobachtung stattfand. |
| `postalCode` | String | Die Postleitzahl des Ortes. Postleitzahlen sind nicht für alle Länder verfügbar. In einigen Ländern wird dies nur einen Teil der Postleitzahl enthalten. |
| `stateProvince` | String | Das Bundesland oder die Provinz der Beobachtung. Das Format entspricht der [ISO-Norm 3166-2 (Land und Unterteilung)](https://www.unece.org/cefact/locode/subdivisions.html). |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
