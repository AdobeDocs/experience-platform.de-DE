---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Commerce;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Commerce-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Commerce Experience Data Model (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---

# [!UICONTROL Typ ] Commercedata

 Commerceis ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der die Datensätze im Zusammenhang mit dem Kauf und Verkauf von Aktivitäten beschreibt.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `order` | [[!UICONTROL Auftrag]](./order.md) | Beschreibt die platzierte Bestellung für ein oder mehrere Produkte. |
| `cartAbandons` | [[!UICONTROL Maßnahme]](./measure.md) | Wird verwendet, um zu beschreiben, wann eine Liste vom Benutzer als nicht mehr verfügbar oder nicht mehr erhältlich identifiziert wurde. |
| `checkouts` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Aktion während des Kassengangs einer Produkt-Liste. Es kann mehrere Checkout-Ereignis geben, wenn ein Kassengangprozess mehrere Schritte umfasst. Bei mehreren Schritten werden die Ereignis-Zeitinformationen und die referenzierte Seite bzw. das Erlebnis verwendet, um den Schritt und die einzelnen Ereignis in der Reihenfolge zu identifizieren. |
| `inStorePurchase` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt einen Wert, der mit einem Kauf im Geschäft für die Verwendung in Analytics verknüpft ist. |
| `productListAdds` | [[!UICONTROL Maßnahme]](./measure.md) | Die Hinzufügung eines Produkts zur Liste des Produkts, z. B. ein Produkt, das einem Warenkorb hinzugefügt wird. |
| `productListOpens` | [[!UICONTROL Maßnahme]](./measure.md) | Die Initialisierungen einer neuen Produkt-Liste, z. B. ein Einkaufswagen, der erstellt wird. |
| `productListRemovals` | [[!UICONTROL Maßnahme]](./measure.md) | Entfernen oder Entfernen eines Produkteintrags aus einer Liste, z. B. Entfernen eines Produkts aus dem Warenkorb. |
| `productListReopens` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Liste, die zuvor abgebrochen wurde und vom Benutzer erneut aktiviert wurde. |
| `productListViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine oder mehrere Ansichten einer Produkt-Liste aufgetreten sind. |
| `productViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten eines bestimmten Produkts aufgetreten ist. |
| `purchases` | [[!UICONTROL Maßnahme]](./measure.md) | Wird verwendet, um nachzuverfolgen, wann eine Bestellung akzeptiert wurde. Das Ereignis purchase ist die einzige erforderliche Aktion bei einer Commerce-Konversion. Auf das Ereignis purchase muss auf eine Liste verwiesen werden. |
| `saveForLaters` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Produkt-Liste wird für die zukünftige Verwendung wie eine Wunschversion gespeichert. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
