---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Commerce; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Commerce-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Datentyp "Commerce Experience-Datenmodell (XDM)".
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 17%

---

# [!UICONTROL Handel] Datentyp

[!UICONTROL Handel] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Datensätze im Zusammenhang mit Kauf- und Verkaufsaktivitäten beschreibt.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `order` | [[!UICONTROL Auftrag]](./order.md) | Beschreibt die platzierte Bestellung für ein oder mehrere Produkte. |
| `cartAbandons` | [[!UICONTROL Maßnahme]](./measure.md) | Wird verwendet, um zu beschreiben, wann eine Produktliste vom Benutzer als nicht mehr zugänglich oder käuflich identifiziert wurde. |
| `checkouts` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Aktion während des Checkout-Prozesses einer Produktliste. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden die Ereigniszeitinformationen sowie die referenzierte Seite oder das referenzierte Erlebnis verwendet, um den Schritt und die einzelnen Ereignisse in der angegebenen Reihenfolge zu identifizieren. |
| `inStorePurchase` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt einen Wert, der mit einem Kauf im Geschäft zur Verwendung in Analytics verknüpft ist. |
| `productListAdds` | [[!UICONTROL Maßnahme]](./measure.md) | Das Hinzufügen eines Produkts zur Produktliste, z. B. ein Produkt, das einem Warenkorb hinzugefügt wird. |
| `productListOpens` | [[!UICONTROL Maßnahme]](./measure.md) | Die Initialisierungen einer neuen Produktliste, z. B. eines gerade erstellten Warenkorbs. |
| `productListRemovals` | [[!UICONTROL Maßnahme]](./measure.md) | Entfernung oder Entfernung eines Produkteintrags aus einer Produktliste, z. B. Entfernung eines Produkts aus einem Warenkorb. |
| `productListReopens` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Produktliste, die zuvor abgebrochen wurde und vom Benutzer erneut aktiviert wurde. |
| `productListViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten einer Produktliste aufgetreten sind. |
| `productViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten eines einzelnen Produkts aufgetreten sind. |
| `purchases` | [[!UICONTROL Maßnahme]](./measure.md) | Wird verwendet, um zu verfolgen, wann eine Bestellung akzeptiert wurde. Das Kaufereignis ist die einzige erforderliche Aktion bei einer Commerce-Konversion. Auf das Kaufereignis muss eine Produktliste verwiesen werden. |
| `saveForLaters` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Produktliste wird für die zukünftige Verwendung gespeichert, z. B. eine Wunschliste. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
