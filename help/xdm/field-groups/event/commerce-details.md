---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Schemafeldgruppe für Commerce-Details
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Commerce-Details .
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 13%

---

# [!UICONTROL Commerce-Details] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Commerce-Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md)verwendet, um Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßige Warenkorbvorgänge (Bestellung, Checkout, Abbruch) zu beschreiben.

![](../../images/field-groups/commerce-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Ein Objekt, das die Produktrückgabe, die Registrierung der Garantie und die Warenkorb-/Bestellvorgänge beschreibt. |
| `productListItems` | Array von [Produktlistenelemente](../../data-types/product-list-item.md) | Eine Liste von Artikeln, die die von einem Kunden ausgewählten Produkte mit bestimmten Optionen und Preisen zu einem bestimmten Zeitpunkt darstellen (die vom Produktdatensatz abweichen können). |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
