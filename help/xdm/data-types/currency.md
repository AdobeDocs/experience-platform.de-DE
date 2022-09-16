---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Gerät; Datentyp; Datentyp; Datentyp; Währung;
solution: Experience Platform
title: Währungs-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Währungs-XDM-Datentyp.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 7%

---

# [!UICONTROL Währung] Datentyp

[!UICONTROL Währung] ist ein standardmäßiger XDM-Datentyp, der einen Währungsbetrag beschreibt, einschließlich des Währungstyps und des Konversionsdatums.

![](../images/data-types/currency.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `amount` | Double | Der Währungsbetrag, der durch die Variable `currencyCode`. |
| `conversionDate` | DateTime | Ein Zeitstempel, der angibt, wann die Währungsumrechnung durchgeführt wurde. |
| `currencyCode` | Zeichenfolge | Ein ISO 4217-Code, der den Währungstyp angibt, der `amount` darstellt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
