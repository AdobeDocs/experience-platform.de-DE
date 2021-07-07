---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Schemafeldgruppe für Commerce-Details
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Commerce-Details .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 4%

---


# [!UICONTROL Feldergruppe &quot;Commerce-] Details&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Commerce-] Details sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), mit der Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßige Warenkorbvorgänge (Bestellung, Checkout, Abbruch) beschrieben werden.

![](../../images/field-groups/commerce-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `commerce` | [Handel](../../data-types/commerce.md) | Ein Objekt, das die Produktrückgabe, die Registrierung der Garantie und die Warenkorb-/Bestellvorgänge beschreibt. |
| `productListItems` | Array von [Produktlistenelementen](../../data-types/product-list-item.md) | Eine Liste von Artikeln, die die von einem Kunden ausgewählten Produkte mit bestimmten Optionen und Preisen zu einem bestimmten Zeitpunkt darstellen (die vom Produktdatensatz abweichen können). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
