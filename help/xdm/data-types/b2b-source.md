---
title: B2B-Quelldatentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp des B2B-Quell-Experience-Datenmodells (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 6%

---

# [!UICONTROL B2B-] Quelldatentyp (Beta)

>[!IMPORTANT]
>
>Dieser Datentyp ist als Teil der Real-time Customer Data Platform B2B Edition verfügbar, die sich derzeit in der Beta-Phase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL B2B ] Sources ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine zusammengesetzte Kennung für eine B2B-Entität darstellt (z. B. ein  [Konto](../classes/b2b/business-account.md), eine  [Gelegenheit](../classes/b2b/business-opportunity.md) oder eine  [Kampagne](../classes/b2b/business-campaign.md)).

Wenn Sie sich ausschließlich auf zeichenfolgenbasierte IDs verlassen, können sich IDs über mehrere Systeme hinweg überschneiden (z. B. könnte eine Chance auf eine Zeichenfolgen-ID in einem CRM-System gegeben werden, aber dieselbe ID könnte auf eine völlig andere Möglichkeit verweisen). Dies kann beim Zusammenführen von Daten in [Echtzeit-Kundenprofil](../../profile/home.md) zu Datenkonflikten führen.

Der Datentyp [!UICONTROL B2B Source] ermöglicht es Ihnen, die ursprüngliche String-ID einer Entität zu verwenden und sie mit quellenspezifischen kontextbezogenen Informationen zu kombinieren, um sicherzustellen, dass sie im Platform-System vollkommen eindeutig bleibt, unabhängig von der Quelle, aus der sie stammt.

![B2B-Quellstruktur](../images/data-types/b2b-source.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `sourceID` | Zeichenfolge | Eine eindeutige ID für den Quelldatensatz. |
| `sourceInstanceID` | Zeichenfolge | Die Instanz- oder Organisations-ID der Quelldaten. |
| `sourceKey` | Zeichenfolge | Eine eindeutige Kennung, die aus den verketteten `sourceId`, `sourceInstanceId` und `sourceType` im folgenden Format besteht: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Einige Quell-Connectoren wie Marketo verketten diesen Wert für bestimmte Kennungen automatisch. Andere müssen manuell mit der Funktion [Data Prep `concat` verkettet werden, z. B.: `concat(id,"@${ORG_ID}.Marketo")`](../../data-prep/functions.md#string) |
| `sourceType` | Zeichenfolge | Der Name der Plattform, die die Quelldaten bereitstellt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
