---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Commerce;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Commerce-Datentyp
description: Erfahren Sie mehr über den Datentyp Commerce Experience-Datenmodell (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 11%

---

# Datentyp {0]Commerce}[!UICONTROL 

[!UICONTROL Commerce] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Datensätze im Zusammenhang mit Kauf und Verkauf beschreibt.

![Diagramm des Datentyps [!UICONTROL Commerce].](../images/data-types/commerce.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Auftrag] | `order` | [[!UICONTROL Auftrag]](./order.md) | Beschreibt die aufgegebene Bestellung für ein oder mehrere Produkte. |
| [!UICONTROL Promotion-ID] | `promotionID` | [!UICONTROL Zeichenfolge] | Eine Promotion-Kennung für die aufgegebene Bestellung, falls vorhanden. |
| [!UICONTROL Warenkorbabbrüche] | `cartAbandons` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Produktliste vom Benutzer als nicht mehr zugänglich oder käuflich identifiziert wurde. |
| [!UICONTROL Checkouts] | `checkouts` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Aktion während des Checkout-Prozesses einer Produktliste. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Bei mehreren Schritten werden die Zeitinformationen des Ereignisses und die referenzierte Seite oder das referenzierte Erlebnis verwendet, um den Schritt und die einzelnen Ereignisse in der richtigen Reihenfolge zu identifizieren. |
| [!UICONTROL Hinzufügungen zur Produktliste (Warenkorb)] | `productListAdds` | [[!UICONTROL Maßnahme]](./measure.md) | Das Hinzufügen eines Produkts zur Produktliste, z. B. ein Produkt, das zum Warenkorb hinzugefügt wird. |
| [!UICONTROL Produktliste (Warenkorb) wird geöffnet] | `productListOpens` | [[!UICONTROL Maßnahme]](./measure.md) | Die Initialisierungen einer neuen Produktliste, z. B. die Erstellung eines Warenkorbs. |
| [!UICONTROL Entnahmen aus der Produktliste (Warenkorb)] | `productListRemovals` | [[!UICONTROL Maßnahme]](./measure.md) | Das Entfernen oder Entfernen eines Produkteintrags aus einer Produktliste, z. B. ein Produkt, das aus einem Warenkorb entfernt wird. |
| [!UICONTROL Erneute Öffnungen der Produktliste (Warenkorb)] | `productListReopens` | [[!UICONTROL Maßnahme]](./measure.md) | Eine zuvor abgebrochene Produktliste, die vom Benutzer wieder aktiviert wurde. |
| [!UICONTROL Produktlistenansichten (Warenkorbansichten)] | `productListViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten einer Produktliste stattgefunden hat. Ansicht oder Ansichten einer Produktliste sind aufgetreten. |
| [!UICONTROL Produktansichten] | `productViews` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Ansicht oder Ansichten eines einzelnen Produkts aufgetreten ist. |
| [!UICONTROL Käufe] | `purchases` | [[!UICONTROL Maßnahme]](./measure.md) | Wird verwendet, um zu verfolgen, wann eine Bestellung angenommen wurde. Das Kaufereignis ist die einzige erforderliche Aktion bei einer Commerce-Konversion. Für das Kaufereignis muss eine Produktliste referenziert werden. |
| [!UICONTROL Für später speichern] | `saveForLaters` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann eine Produktliste für die zukünftige Verwendung gespeichert wird, z. B. als Wunschliste. |
| [!UICONTROL Einkauf im Geschäft] | `inStorePurchase` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt einen &#39;inStore&#39;-Kauf an. Diese Informationen werden für die Verwendung in der Analyse gespeichert. |
| [!UICONTROL Warenkorb] | `cart` | [[!UICONTROL Warenkorb]](./cart.md) | Die Eigenschaften des Warenkorbs, der ein oder mehrere Produkte enthält. |
| [!UICONTROL Versand] | `shipping` | [[!UICONTROL Versand]](./shipping.md) | Die Versanddetails für ein oder mehrere Produkte. |
| [!UICONTROL Abrechnung] | `billing` | [[!UICONTROL billing]](#billing) | Die Rechnungsdetails für eine oder mehrere Zahlungen. |
| [!UICONTROL Sofortiger Kauf] | `instantPurchase` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt, wann ein Produkt sofort gekauft wurde, wodurch der Warenkorb oder der Checkout möglicherweise übersprungen wird. |
| [!UICONTROL Anforderungsliste wird geöffnet] | `requisitionListOpens` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt die Initialisierung einer neuen Anforderungsliste an. |
| [!UICONTROL Löschvorgänge für Anforderungslisten] | `requisitionListDeletes` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt an, ob die Anforderungsliste entfernt wurde. |
| [!UICONTROL Hinzufügungen zur Anforderungsliste] | `requisitionListAdds` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt an, ob ein Produkt zu einer Anforderungsliste hinzugefügt werden soll. |
| [!UICONTROL Entnahmen aus der Anforderungsliste] | `requisitionListRemovals` | [[!UICONTROL Maßnahme]](./measure.md) | Gibt an, ob ein Produkt aus einer Anforderungsproduktliste entfernt werden soll. |
| [!UICONTROL Anforderungsliste] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | Die Eigenschaften der vom Kunden erstellten Anforderungsliste. |
| [!UICONTROL Perimeter] | `commerceScope` | [[!UICONTROL CommerceScope]](./commerce-scope.md) | Die Commerce-Bereichskennungen, mit denen ein Ereignis aufgetreten ist (Store-Ansicht, Store, Website usw.). |

{style="table-layout:auto"}

## [!UICONTROL billing] Datentyp {#billing}

[!UICONTROL billing] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zu Abrechnungsdetails enthält. Im Einzelnen konzentriert sie sich auf die Rechnungsadresse.

![Ein Diagramm zum Datentyp „Abrechnung“.](../images/data-types/billing.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Rechnungsadresse] | `address` | [[!UICONTROL Postanschrift]](./postal-address.md) | Die Rechnungsadresse. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp [!UICONTROL Commerce] finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
