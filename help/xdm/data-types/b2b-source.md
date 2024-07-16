---
title: B2B Source-Datentyp
description: Erfahren Sie mehr über den Datentyp B2B Source Experience Data Model (XDM) .
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# Datentyp [!UICONTROL B2B Source]

[!UICONTROL B2B Source] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der eine zusammengesetzte Kennung für eine B2B-Entität darstellt (z. B. ein [Konto](../classes/b2b/business-account.md), eine [Opportunity](../classes/b2b/business-opportunity.md) oder eine [campaign](../classes/b2b/business-campaign.md)).

Wenn Sie sich ausschließlich auf zeichenfolgenbasierte IDs verlassen, können sich IDs über mehrere Systeme hinweg überschneiden (z. B. könnte eine Chance auf eine Zeichenfolgen-ID in einem CRM-System gegeben werden, aber dieselbe ID könnte auf eine völlig andere Möglichkeit verweisen). Dies kann beim Zusammenführen von Daten in [Echtzeit-Kundenprofil](../../profile/home.md) zu Datenkonflikten führen.

Mit dem Datentyp [!UICONTROL B2B Source] können Sie die ursprüngliche Zeichenfolgen-ID einer Entität verwenden und sie mit quellspezifischen Kontextdaten kombinieren, um sicherzustellen, dass sie im Platform-System vollkommen eindeutig bleibt, unabhängig von der Quelle, aus der sie stammt.

![B2B Source-Struktur](../images/data-types/b2b-source.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `sourceID` | Zeichenfolge | Eine eindeutige ID für den Quelldatensatz. |
| `sourceInstanceID` | Zeichenfolge | Die Instanz- oder Organisations-ID der Quelldaten. |
| `sourceKey` | Zeichenfolge | Eine eindeutige Kennung, die aus den im folgenden Format verketteten `sourceId`, `sourceInstanceId` und `sourceType` besteht: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Einige Quell-Connectoren wie Marketo verketten diesen Wert für bestimmte IDs automatisch. Andere müssen manuell mit der Funktion [Datenvorbereitung `concat` ](../../data-prep/functions.md#string) verkettet werden, z. B.: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Zeichenfolge | Der Name der Plattform, die die Quelldaten bereitstellt. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
