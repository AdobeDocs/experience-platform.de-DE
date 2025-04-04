---
title: B2B-Source-Datentyp
description: Erfahren Sie mehr über den Datentyp B2B-Source-Experience-Datenmodell (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL B2B-Source]-Datentyp

[!UICONTROL B2B-Source] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine zusammengesetzte Kennung für eine B2B-Entität darstellt (z. B. [Account](../classes/b2b/business-account.md), [Opportunity](../classes/b2b/business-opportunity.md) oder [Campaign](../classes/b2b/business-campaign.md)).

Wenn wir uns ausschließlich auf zeichenfolgenbasierte Kennungen verlassen, kann es zu Überschneidungen zwischen IDs in mehreren Systemen kommen (z. B. könnte eine Opportunity in einem CRM-System eine Zeichenfolge-ID erhalten, aber dieselbe ID könnte sich auf eine völlig andere Opportunity beziehen). Dies kann beim Zusammenführen von Daten in [Echtzeit-Kundenprofil) zu Datenkonflikten ](../../profile/home.md).

Mit dem Datentyp [!UICONTROL B2B Source] können Sie die ursprüngliche String-ID einer Entität verwenden und mit quellenspezifischen Kontextinformationen kombinieren, um sicherzustellen, dass sie im Experience Platform-System unabhängig von der Quelle, aus der sie stammt, vollständig eindeutig bleibt.

![B2B-Source-Struktur](../images/data-types/b2b-source.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `sourceID` | Zeichenfolge | Eine eindeutige ID für den Quelldatensatz. |
| `sourceInstanceID` | String | Die Instanz- oder Organisations-ID der Quelldaten. |
| `sourceKey` | String | Eine eindeutige Kennung, die aus den `sourceId`, `sourceInstanceId` und `sourceType` besteht, die im folgenden Format verkettet sind: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Einige Quell-Connectoren wie Marketo verketten diesen Wert automatisch für bestimmte Kennungen. Andere müssen manuell mithilfe der [Datenvorbereitungs-`concat`-Funktion“ verkettet werden](../../data-prep/functions.md#string) z. B.: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | Der Name der Plattform, die die Quelldaten bereitstellt. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
