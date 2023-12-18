---
keywords: Experience Platform; home; beliebte Themen; schema; XDM; Felder; Schemas; Schemas; Gerät; Datentyp; Datentyp; Datentyp; Währung;
solution: Experience Platform
title: Währungs-Datentyp
description: Erfahren Sie mehr über den Währungs-XDM-Datentyp.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# [!UICONTROL Währung] Datentyp

[!UICONTROL Währung] ist ein standardmäßiger XDM-Datentyp, der einen Währungsbetrag beschreibt, einschließlich des Währungstyps und des Konversionsdatums.

![](../images/data-types/currency.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `amount` | Double | Der Währungsbetrag, der durch die Variable `currencyCode`. |
| `conversionDate` | DateTime | Ein Zeitstempel, der angibt, wann die Währungsumrechnung durchgeführt wurde. |
| `currencyCode` | Zeichenfolge | Ein ISO 4217-Code, der den Währungstyp angibt, der `amount` darstellt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
