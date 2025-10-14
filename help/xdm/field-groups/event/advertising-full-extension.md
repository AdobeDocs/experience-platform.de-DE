---
title: Schemafeldgruppe Adobe Advertising Cloud ExperienceEvent Full Extension
description: Machen Sie sich mit der Schemafeldgruppe Adobe Advertising Cloud ExperienceEvent Full Extension vertraut.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 11%

---

# Schemafeldgruppe [!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]

>[!AVAILABILITY]
>
>Die [!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]-Feldergruppe befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalitäten können sich ändern.

[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), die allgemeine von Adobe Advertising erfasste Metriken (früher als &quot;[!DNL Advertising Cloud]&quot; bezeichnet) erfasst.

In diesem Dokument werden die Struktur und der Anwendungsfall der Feldergruppe der [!DNL Advertising Cloud]-Erweiterung beschrieben.

>[!NOTE]
>
>Sie können auch diese Feldergruppe (in [&#x200B; Benutzeroberfläche von Experience Platform) &#x200B;](../../ui/explore.md) oder das vollständige Schema im [öffentlichen XDM-Repository) &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Feldgruppenstruktur

Die Feldgruppe stellt ein einzelnes `_experience`-Objekt für ein Schema bereit, das selbst ein einzelnes `adcloud`-Objekt enthält.

![Felder der obersten Ebene für die [!DNL Advertising Cloud] Feldergruppe](../../images/field-groups/advertising-full-extension/full-schema.png "Felder der obersten Ebene für die  [!DNL Advertising Cloud] Feldergruppe")

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `adDeliveryDetails` | Objekt | Hinzufügen von Versanddetails. Weitere Informationen [&#x200B; Inhalt dieses Objekts finden Sie im `adDeliveryDetails`Unterabschnitt zum &#x200B;](#adDeliveryDetails)-Objekt“. |
| `advertisement` | Objekt | Details zur digitalen Werbung. Weitere Informationen [&#x200B; Inhalt dieses Objekts finden Sie im &#x200B;](#advertisement)Unterabschnitt zum Werbeobjekt“. |
| `campaign` | Objekt | Details zur Kampagnenhierarchie. Weitere Informationen [&#x200B; Inhalt dieses Objekts finden Sie im &#x200B;](#campaign-campaign)Unterabschnitt zum Kampagnenobjekt“. |
| `conversionDetails` | Objekt | Konversionsdetails für eine Anzeige. Weitere Informationen zum Inhalt dieses Objekts finden Sie im [nachfolgenden Unterabschnitt](#conversionDetails). |
| `eventType` | String | Der Ereignistyp von Adobe Advertising. |
| `fees` | Objekt | Advertising-Gebührendetails. Weitere Informationen [&#x200B; Inhalt dieses Objekts finden Sie im &#x200B;](#fees)Unterabschnitt zum Gebührenobjekt“. |
| `inventory` | Objekt | Inventardetails. Weitere Informationen zum Inhalt dieses Objekts finden Sie im [nachfolgenden Unterabschnitt](#inventory). |
| `productDetails` | Objekt | Details zur Produktanzeige. Weitere Informationen [&#x200B; Inhalt dieses Objekts finden Sie im &#x200B;](#productDetails)Unterabschnitt zum productDetails-Objekt“. |
| `stitchId` | String | ID von den Adobe Advertising-Werbeservern zur Verfolgung von Clickthrough-Konversionen in Browsern, die Drittanbieter-Cookies blockieren. |

## `adDeliveryDetails` {#adDeliveryDetails}

Das Objekt adDeliveryDetails stellt Informationen dazu bereit, wo und wie die Werbung bereitgestellt wurde, einschließlich Platzierungs-Websites und Standortkennungen.

![Schemadiagramm mit dem `adDeliveryDetails` und seinen Feldern.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `placementWebsite` | Zeichenfolge | Die Website, auf der die Werbung angezeigt wurde. |
| `siteLinkText` | String | Der tatsächlich in der Anzeige ausgewählte Website-Link. |
| `interestLocationID` | String | Der Speicherort, der aus der Suchanfrage abgeleitet wurde. Beispielsweise gibt eine Abfrage für „Hotel in Goa“ die ID für Goa zurück, unabhängig vom tatsächlichen Navigationsstandort des Benutzers. |
| `physicalLocationID` | String | Der Browser-Standort des Benutzers, dargestellt durch eine Referenz-ID aus dem Werbenetzwerk. Diese ID ist kein lesbarer Ortsname (z. B. eine Stadt oder ein Land), sondern ein Code, der vom Werbenetzwerk zugewiesen wird, um ein geografisches Ziel zu identifizieren. |

## `advertisement` {#advertisement}

Das Werbeobjekt beschreibt Details zur digitalen Anzeige, wie Kennungen, Typ, Kreativ, Zielgruppenbestimmung und zugehörige Schlüsselwörter.

![Schemadiagramm mit dem `advertisement` und seinen Feldern.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `adId` | Zeichenfolge | Die Kennung für die mit diesem Ereignis verknüpfte Anzeige. Diese ID steht in keiner Beziehung zum Ad-ID-Branchenstandard. |
| `runtime` | String | Die Laufzeit der Werbeeinheit, die sich von der Laufzeit des Browsers oder des Betriebssystems unterscheidet. Mögliche Werte sind: `unknown` und `HTML5`. |
| `adClass` | String | Die Werbeklasse des Fahrereignisses: `display`, `video` oder `social`. |
| `adUnitType` | String | Die Kennung für den Code, der die Anzeige in einem Browser oder Gerät rendert. Mögliche Werte:<ul><li>`linearVideo`: Lineares Video</li><li>`interactiveVideo`: Interaktives Video</li><li>`banner`: Banner,</li><li>`richMediaBanner`: Rich-Media-Banner,</li><li>`newsFeedVideo`: Videos zu Nachrichten-Feeds,</li><li>`newsFeedDisplay`: Anzeige von Newsfeeds,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: Im Seitenvideo</li><li>`inPageDisplay`: In der Seitenanzeige,</li><li>`facebook`: Facebook,</li><li>`twitter`: Twitter,</li><li>`linearTv`: Linear-TV,</li><li>`vod`: Video on Demand</li></ul> |
| `promotedAssetId` | String | Die Kennung für das hochgestufte Asset in der diesem Ereignis zugeordneten Anzeige. |
| `creativeID` | String | Die Kennung für die kreative Anzeige (z. B. Banner, Video oder Social-Media-Anzeige), die mit diesem Ereignis verknüpft ist. |
| `keywordID` | String | Die Kennung für das Keyword, die vom Benutzer in einer Suchabfrage eingegeben wurde, die dieses Ereignis ausgelöst hat. |
| `keyword` | String | Das Auflistungsschlüsselwort, für das der Kunde ein Gebot abgibt. |
| `isDynamicSearchAd` | Boolesch | Gibt an, ob das Ereignis von einer dynamischen Suchanzeige stammt. |
| `audienceID` | String | Die Kennung für das Zielgruppensegment, auf das sich die Anzeige bezieht. |
| `adGroupID` | String | Die Kennung für die Anzeigengruppe, die mit der Anzeige verknüpft ist, die dieses Ereignis ausgelöst hat. |
| `campaignID` | String | Die Kennung der Kampagne, die mit der Anzeige verknüpft ist, die dieses Ereignis ausgelöst hat. |
| `networkType` | String | Der Netzwerktyp, in dem das Ereignis aufgetreten ist. Mögliche Werte: <ul><li>`search`: Die Anzeige wurde im Suchnetzwerk angezeigt.</li><li>`content`: Die Anzeige wurde im Content Network angezeigt.</li></ul> |
| `matchType` | String | Der Übereinstimmungstyp des Keywords. Mögliche Werte: <ul><li>`exact`: Exakte Übereinstimmung des Keywords</li><li>`broad`: Grobe Übereinstimmung des Keywords</li><li>`phrase`: Übereinstimmung der Phrase des Keywords</li></ul> |

## `campaign` {#campaign}

Das Kampagnenobjekt definiert die Hierarchie der Anzeigenkampagnen, einschließlich Konto-, Advertiser-, Platzierungs- und Paketkennungen, sowie Währungsdetails.

![Schemadiagramm mit dem `campaign` und seinen Feldern.](../../images/field-groups/advertising-full-extension/campaign.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountId` | Zeichenfolge | Die Kennung für das Konto. |
| `dspId` | String | Die Kennung für die Demand Side Platform (DSP), in der die Kampagne definiert ist. Normalerweise ist diese Kennung die ID für Adobe Advertising Cloud DSP. |
| `campaignId` | String | Die Kennung der Kampagne. |
| `placementId` | String | Die Kennung der Platzierung. |
| `packageId` | String | Die Kennung für das Advertising DSP-Paket. |
| `advertiserId` | String | Die Kennung für den Advertiser. |
| `experimentId` | String | Die Kennung für das Experiment. |
| `sampleGroupId` | String | Die Kennung für die Beispielgruppe. |
| `currency` | String | Der ISO 4217-Rechnungswährungs-Code für das Konto. Verwendet das Muster für reguläre Ausdrücke ^[A-Z]{3}$ (drei Großbuchstaben). Beispiel: USD, EUR. |

## `conversionDetails` {#conversionDetails}

Das ConversionDetails-Objekt erfasst Tracking-Informationen für Anzeigenkonvertierungen, einschließlich Trackingcodes, Identitäten und Konversionseigenschaften.

![Schemadiagramm mit dem `conversionDetails` Objekt und seinen Feldern.](../../images/field-groups/advertising-full-extension/conversionDetails.png "Feld „conversionDetails“")

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `trackingCode` | Zeichenfolge | Der Konversions-Trackingcode für das Ereignis. Eine Liste der möglichen Formate finden Sie unter [AMO-ID-Formate](https://experienceleague.adobe.com/de/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats). |
| `trackingIdentities` | String | Die EF-ID oder Tracking-Identitätsdetails für ein Ereignis. Eine Liste der möglichen Formate finden Sie unter [EF ID Formats](https://experienceleague.adobe.com/de/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Objekt | Eine Zuordnung von Konvertierungseigenschaften, dargestellt als ein Array von Zeichenfolgen mit Schlüssel-Wert-Paaren (z. B. `subscriptions=253`). |

## `fees` {#fees}

Das Gebührenobjekt erfasst Medien, Daten und andere Werbekosten, aufgeschlüsselt nach Advertising DSP, Account und Advertiser.

![Schemadiagramm mit dem `fees` und seinen Feldern.](../../images/field-groups/advertising-full-extension/fees.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `DSPMediaFees` | Zahl | Die von Advertising DSP in Rechnung gestellten Mediengebühren. |
| `DSPDataFees` | Zahl | Die von Advertising DSP in Rechnung gestellten Datengebühren. |
| `DSPOtherFees` | Zahl | Weitere von Advertising DSP in Rechnung gestellte Gebühren. |
| `accountMediaFees` | Zahl | Die Mediengebühren für das Konto, die von Advertising DSP jedoch nicht in Rechnung gestellt werden. |
| `accountDataFees` | Zahl | Die Datengebühren für das Konto, die von Advertising DSP jedoch nicht in Rechnung gestellt werden. |
| `accountOtherFees` | Zahl | Sonstige Kontogebühren, die von Advertising DSP nicht in Rechnung gestellt werden können. |
| `advertiserMediaFees` | Zahl | Die dem Werbetreibenden vom Konto berechneten Mediawerbegebühren. |
| `advertiserDataFees` | Zahl | Andere dem Inserenten vom Konto in Rechnung gestellte Werbegebühren. |
| `advertiserOtherFees` | Zahl | Andere dem Inserenten vom Konto in Rechnung gestellte Werbegebühren. |
| `billableMediaNetSpend` | Zahl | Die fakturierbaren Nettoausgaben für Medienwerbung. |
| `totalMediaNetSpend` | Zahl | Die gesamten Nettoausgaben für Medienwerbung. |
| `billableDataNetSpend` | Zahl | Die fakturierbaren Nettoausgaben für die Datenwerbung. |
| `billableOtherNetSpend` | Zahl | Die fakturierbaren Nettoausgaben für andere Arten von Werbung. |
| `totalBillableNetSpend` | Zahl | Die gesamten fakturierbaren Nettoausgaben. |
| `totalNonBillableNetSpend` | Zahl | Die gesamten nicht fakturierbaren Nettoausgaben. |
| `totalNetSpend` | Zahl | Die Gesamtnettoausgaben. |

## `inventory` {#inventory}

Das Inventarobjekt zeichnet Details zur Inventar-Opportunity auf, einschließlich Sitzungsdaten, Partner-Codes, Site-IDs, Kostenwährung und Segmentierungsregeln.

![Schemadiagramm mit dem `inventory` und seinen Feldern.](../../images/field-groups/advertising-full-extension/inventory.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `sessionId` | Zeichenfolge | Die Sitzungs-ID, die mit einem Erlebnisereignis verknüpft ist und zum Verknüpfen unabhängiger Ereignisse in derselben Sitzung verwendet wird. |
| `feedID` | String | Eine zusammengesetzte ID des Herausgebers, Anzeigenaustausch und andere Funktionen. |
| `sspPartnerCode` | String | Der Partner (Exchange), über den Adobe Advertising Cloud die Inventar-Opportunity erhält. |
| `siteID` | String | Die Kennung für die Website, auf der die Anzeigenimpression bereitgestellt wurde. |
| `costCurrency` | String | Der ISO 4217-Währungscode, mit dem ein Partner für eine Anzeigengelegenheit bezahlt wird. Der Wert muss dem Muster für reguläre Ausdrücke ^[A-Z]{3}$ entsprechen (drei Großbuchstaben). Beispiel: USD, EUR. |
| `inventorySourceId` | String | Die ID der Adobe Advertising Cloud-Bestandsquelle, für die diese Opportunity bereitgestellt wurde. |
| `segment` | Objekt | Details zu Benutzersegmentierungsregeln. Zu den Eigenschaften gehören:<ul><li>`attributablePartnerId` (Zeichenfolge): Der Bezeichner für den Segmentanbieter, dem die attributeSegmentId gehört.</li><li>`attributableSegmentId` (Zeichenfolge): Das Segment, das für das Benutzer-Targeting in der Zielgruppenbestimmungsregel der Platzierung gutgeschrieben wird. Dies wird für die Verfolgung von Kosten und zahlenden Partnern verwendet.</li><li>`segments` (Zeichenfolge): Die Schnittmenge der Benutzersegmente a\), zu denen der Benutzer gehörte, und b\), auf die sich die Anzeige bezog. Dies ist nicht die vollständige Liste der Segmente, zu denen der Benutzer zum Zeitpunkt der Auktion gehörte.</li></ul> |
| `optimizationTag` | String | Das Tag für die Optimierung. |
| `attributableDeviceGraphId` | String | Die Kennung für das Gerätediagramm, die einem Konversionsereignis zugeordnet wurde. |

## `productDetails` {#productDetails}

Das `productDetails`-Objekt enthält Informationen zu Produkten, die in Shopping-Anzeigen für [!DNL Adobe Advertising Search, Social, & Commerce] enthalten sind, einschließlich Produktkennungen, Land, Sprache, Partition, Titel und Anzeigentyp.

![Schemadiagramm mit dem `productDetails` und seinen Feldern.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `productID` | Zeichenfolge | Die Kennung für das Produkt, das in der diesem Ereignis zugeordneten Anzeige angezeigt wird. |
| `country` | String | Das Land, in dem das Produkt verkauft wurde, das in der mit der Veranstaltung verknüpften Anzeige aufgeführt ist. |
| `language` | String | Die Sprache Ihrer Produktinformationen, wie im Daten-Feed des Client für das Merchant Center angegeben. |
| `partitionID` | String | Die Kennung für die Produktgruppe, die mit der Anzeige in diesem Ereignis verknüpft ist. |
| `title` | String | Der in der Werbung angezeigte Produkttitel. |
| `adType` | String | Der Anzeigentyp für das Produkt, das in [!DNL Google] Shopping-Kampagnen verwendet wird. Mögliche Werte:<ul><li>`pla_with_pog`: Wenn das Ereignis von einem Kauf durch eine Shopping-Anzeige kam</li><li>`pla`: Wenn das Ereignis aus einer Shopping-Anzeige kam.</li><li>`pla_multichannel`: Wenn die Veranstaltung aus einer Shopping-Anzeige Optionen für „Online“- und „lokale“ Shopping-Kanäle.</li><li>`pla_with_promotion`: Wenn das Ereignis aus einer Shopping-Anzeige eine Händler-Promotion angezeigt hat.</li></ul> |

## Nächste Schritte

In diesem Dokument wurden die Struktur und der Anwendungsfall für die Feldergruppe der [!DNL Advertising Cloud]-Erweiterung behandelt. Weitere Informationen zur Feldgruppe selbst finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Wenn Sie diese Feldergruppe verwenden, um [!DNL Advertising] mit der Adobe Experience Platform Web SDK zu erfassen, erfahren Sie in der Anleitung unter [Konfigurieren eines Datenstroms](../../../datastreams/overview.md), wie Sie Daten Server-seitig XDM zuordnen.
