---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Commerce; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Commerce-Datentyp
description: Erfahren Sie mehr über den Datentyp des Commerce Experience-Datenmodells (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 11%

---

# [!UICONTROL Commerce]-Datentyp

[!UICONTROL Commerce] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der die Datensätze im Zusammenhang mit dem Kauf und Verkauf beschreibt.

![Ein Diagramm des Datentyps [!UICONTROL Commerce].](../images/data-types/commerce.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Auftrag] | `order` | [[!UICONTROL Auftrag]](./order.md) | Beschreibt die platzierte Bestellung für ein oder mehrere Produkte. |
| [!UICONTROL Promotion-ID] | `promotionID` | [!UICONTROL string] | Eine Promotion-ID für die platzierte Bestellung, falls vorhanden. |
| [!UICONTROL Warenkorbabbrüche] | `cartAbandons` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Produktliste vom Benutzer als nicht mehr zugänglich oder käuflich identifiziert wurde. |
| [!UICONTROL Checkouts] | `checkouts` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Aktion während des Checkout-Prozesses einer Produktliste. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden die Ereigniszeitinformationen sowie die referenzierte Seite oder das referenzierte Erlebnis verwendet, um den Schritt und die einzelnen Ereignisse in der angegebenen Reihenfolge zu identifizieren. |
| [!UICONTROL Hinzufügen zur Produktliste (Warenkorb)] | `productListAdds` | [[!UICONTROL Maßnahme]](./measure.md) | Das Hinzufügen eines Produkts zur Produktliste, z. B. ein Produkt, das einem Warenkorb hinzugefügt wird. |
| [!UICONTROL Öffnung der Produktliste (Warenkorb)] | `productListOpens` | [[!UICONTROL Maßnahme]](./measure.md) | Die Initialisierungen einer neuen Produktliste, z. B. eines gerade erstellten Warenkorbs. |
| [!UICONTROL Entfernen von Produktlisten (Warenkorb)] | `productListRemovals` | [[!UICONTROL Maßnahme]](./measure.md) | Entfernung oder Entfernung eines Produkteintrags aus einer Produktliste, z. B. Entfernung eines Produkts aus einem Warenkorb. |
| [!UICONTROL Produktliste (Warenkorb) wird erneut geöffnet] | `productListReopens` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Produktliste, die zuvor abgebrochen wurde und vom Benutzer erneut aktiviert wurde. |
| [!UICONTROL Ansichten der Produktliste (Warenkorb)] | `productListViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten einer Produktliste aufgetreten sind. Anzeigen oder Ansichten einer Produktliste sind aufgetreten. |
| [!UICONTROL Produktansichten] | `productViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten eines einzelnen Produkts aufgetreten sind. |
| [!UICONTROL Käufe] | `purchases` | [[!UICONTROL Maßnahme]](./measure.md) | Wird verwendet, um zu verfolgen, wann eine Bestellung akzeptiert wurde. Das Kaufereignis ist die einzige erforderliche Aktion bei einer Commerce-Konversion. Auf das Kaufereignis muss eine Produktliste verwiesen werden. |
| [!UICONTROL Für Später speichern] | `saveForLaters` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Produktliste zur zukünftigen Verwendung gespeichert wird, z. B. eine Wunschliste. |
| [!UICONTROL Im Store-Kauf] | `inStorePurchase` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt einen &quot;InStore&quot;-Kauf an. Diese Informationen werden zur Verwendung in Analytics gespeichert. |
| [!UICONTROL Warenkorb] | `cart` | [[!UICONTROL Warenkorb]](./cart.md) | Die Eigenschaften des Warenkorbs, der ein oder mehrere Produkte enthält. |
| [!UICONTROL Versand] | `shipping` | [[!UICONTROL shipping]](./shipping.md) | Die Versanddetails für ein oder mehrere Produkte. |
| [!UICONTROL Abrechnung] | `billing` | [[!UICONTROL billing]](#billing) | Die Rechnungsdetails für eine oder mehrere Zahlungen. |
| [!UICONTROL Sofortiger Kauf] | `instantPurchase` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann ein Produkt sofort gekauft wurde, und zwar möglicherweise, indem der Warenkorb oder der Checkout übersprungen werden. |
| [!UICONTROL Liste der Anforderungen geöffnet] | `requisitionListOpens` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt die Initialisierung einer neuen Anforderungsliste an. |
| [!UICONTROL Löschung der Anforderungsliste] | `requisitionListDeletes` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt das Entfernen der Anforderungsliste an. |
| [!UICONTROL Hinzufügen zur Anforderungsliste] | `requisitionListAdds` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt das Hinzufügen von Produkten zu einer Anforderungsliste an. |
| [!UICONTROL Entfernung der Anforderungsliste] | `requisitionListRemovals` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt an, wie ein Produkt(e) aus der Produkteliste einer Anforderung entfernt wird. |
| [!UICONTROL Anforderungsliste] | `requisitionList` | [[!UICONTROL requiredList]](./requisition-list.md) | Die Eigenschaften der vom Kunden erstellten Anforderungsliste. |
| [!UICONTROL Perimeter] | `commerceScope` | [[!UICONTROL commerceescope]](./commerce-scope.md) | Die Commerce-Scope-IDs, die angeben, wo ein Ereignis aufgetreten ist (Store-Ansicht, Store, Website usw.). |

{style="table-layout:auto"}

## Datentyp [!UICONTROL billing] {#billing}

[!UICONTROL billing] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zu Rechnungsdetails enthält. Insbesondere konzentriert er sich auf die Rechnungsadresse.

![Ein Diagramm des Rechnungsdatentyps.](../images/data-types/billing.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Abrechnungsadresse] | `address` | [[!UICONTROL Postanschrift]](./postal-address.md) | Die Rechnungsadresse. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp [!UICONTROL Commerce] finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
