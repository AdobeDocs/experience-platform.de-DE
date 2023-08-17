---
title: Intelligente Erneute Interaktion
description: Stellen Sie während der wichtigsten Konversionsmomente überzeugende und vernetzte Erlebnisse bereit, um unregelmäßige Kunden intelligent erneut anzusprechen.
hide: true
hidefromtoc: true
source-git-commit: 43e365e20a2fd91a0e822eb6f66bb7db6fc218f5
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 5%

---

# Intelligentes erneutes Ansprechen Ihrer Kunden zur Rückkehr

Kontaktieren Sie Kunden, die eine Konversion abgebrochen haben, bevor Sie sie auf intelligente und verantwortungsvolle Weise abschließen. Engagieren Sie Kunden durch Erlebnisse anstelle von Erinnerungen, um die Konversion zu verbessern und das Wachstum des Kundenlebenszeitwerts zu fördern.

Berücksichtigen Sie dabei Echtzeit-Überlegungen, berücksichtigen Sie alle Eigenschaften und Verhaltensweisen von Verbrauchern und bieten Sie eine schnelle Umqualifizierung basierend auf Online- und Offline-Ereignissen.

![Schrittweise intelligente Wiederaufnahme der Interaktion - Überblick auf hoher Ebene.](../intelligent-re-engagement/images/step-by-step.png)

## Anwendungsfallübersicht

Sie erstellen Schemas, Datensätze und Zielgruppen, während Sie anhand von Beispielen für die Rückgewinnung von Journey arbeiten. Außerdem erfahren Sie, welche Funktionen zum Einrichten der Beispiel-Journey in [!DNL Adobe Journey Optimizer] und diejenigen, die für die Erstellung von Paid-Media-Anzeigen in Zielen erforderlich sind. In diesem Handbuch werden Beispiele dafür verwendet, wie Kunden in den unten beschriebenen Anwendungsfällen erneut angesprochen werden:

* **Journey zur erneuten Interaktion** - Zielgruppe von Kunden, die das Durchsuchen von Produkten auf der Website und in der App abgebrochen haben.
* **Journey zum Warenkorb abgebrochen** - Kunden, die Produkte in den Warenkorb gelegt, aber noch nicht sowohl auf der Website als auch in der App gekauft haben.
* **Journey zur Bestellbestätigung** - Konzentriert sich auf Produktkäufe, die über die Website und die mobile App getätigt werden.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, nutzen Sie die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente (aufgelistet in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Aggregiert Daten aus verschiedenen Datenquellen, um die Kampagne anzukurbeln. Diese Daten werden dann verwendet, um die Kampagnenzielgruppen zu erstellen und personalisierte Datenelemente zu unterteilen, die in der E-Mail und in den Kacheln der Web-Promo verwendet werden (z. B. Name oder kontobezogene Informationen). Die CDP wird auch verwendet, um Zielgruppen über E-Mail und Web (über Adobe Target) zu aktivieren.
   * [Schemata](/help/xdm/home.md)
   * [Profile](/help/profile/home.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
   * [Zielgruppen](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=de)
   * [Ziele](/help/destinations/home.md)
   * [Ereignis- oder Audience Trigger](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Zielgruppen/Ereignisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Journey-Aktionen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=de)

### Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

Nachstehend finden Sie einen Überblick über die drei beispielhaften Journey zur erneuten Interaktion.

>[!BEGINTABS]

>[!TAB Journey zur erneuten Interaktion]

Die Rückgewinnungs-Journey ermöglicht sowohl das Website- als auch das App-Browsen auf abgegebene Produkte. Diese Journey wird ausgelöst, wenn ein Produkt angesehen, aber nicht gekauft oder zum Warenkorb hinzugefügt wurde. Die Markeninteraktion wird nach drei Tagen ausgelöst, wenn innerhalb der letzten 24 Stunden keine Listen hinzugefügt wurden.<p>![Kundenintelligente Journey-Rückgewinnung - Überblick über die allgemeine visuelle Darstellung.](../intelligent-re-engagement/images/re-engagement-journey.png "Kundenintelligente Journey-Rückgewinnung - Überblick über die allgemeine visuelle Darstellung."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemata und Datensätze, die für [!UICONTROL Profil].
2. Die Daten werden über das Web SDK, das Mobile Edge SDK oder die API in Experience Platform aggregiert. Analytics Data Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie laden Profile in Real-Time CDP und erstellen Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Sie erstellen zielgerichtete Zielgruppen aus der Profilliste, um zu überprüfen, ob eine **customer** hat in den letzten drei Tagen eine Interaktion durchgeführt.
5. Sie erstellen eine Journey zur erneuten Interaktion in [!DNL Adobe Journey Optimizer].
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** für die Aktivierung von Zielgruppen zu gewünschten Paid-Media-Zielen.
7. [!DNL Adobe Journey Optimizer] prüft die Zustimmung und sendet die verschiedenen konfigurierten Aktionen.

>[!TAB Journey zum abgesetzten Warenkorb]

Die Journey mit dem abgebrochenen Warenkorb ist auf Produkte ausgerichtet, die im Warenkorb platziert, aber noch nicht auf der Website und in der App erworben wurden. Darüber hinaus werden Paid Media-Kampagnen mit dieser Methode gestartet und beendet.<p>![Der Kunde hat die Journey des Warenkorbs abgebrochen und eine allgemeine visuelle Übersicht erstellt.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Der Kunde hat die Journey des Warenkorbs abgebrochen und eine allgemeine visuelle Übersicht erstellt."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemata und Datensätze, die für [!UICONTROL Profil].
2. Die Daten werden über das Web SDK, das Mobile Edge SDK oder die API in Experience Platform aggregiert. Analytics Data Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie laden Profile in Real-Time CDP und erstellen Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Sie erstellen zielgerichtete Zielgruppen aus der Profilliste, um zu überprüfen, ob eine **customer** hat einen Artikel in den Warenkorb gelegt, aber den Kauf nicht abgeschlossen. Die **[!UICONTROL Zum Warenkorb hinzufügen]** -Ereignis startet einen Timer, der 30 Minuten lang wartet, und sucht dann nach dem Kauf. Wenn kein Kauf getätigt wurde, wird die **customer** wird zum **[!UICONTROL Warenkorb verlassen]** Zielgruppen.
5. Sie erstellen eine Journey zum abgebrochenen Warenkorb in Adobe Journey Optimizer
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** für die Aktivierung von Zielgruppen zu gewünschten Paid-Media-Zielen.
7. [!DNL Adobe Journey Optimizer] prüft die Zustimmung und sendet die verschiedenen konfigurierten Aktionen.

>[!TAB Journey zur Bestellbestätigung]

Die Journey zur Bestellbestätigung konzentriert sich auf Produktkäufe, die über die Website und die mobile App getätigt werden.<p>![Kundenauftragsbestätigung Journey - Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Kundenauftragsbestätigung Journey - Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemata und Datensätze, die für [!UICONTROL Profil].
2. Die Daten werden über das Web SDK, das Mobile Edge SDK oder die API in Experience Platform aggregiert. Analytics Data Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie laden Profile in Real-Time CDP und erstellen Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Sie erstellen zielgerichtete Zielgruppen aus der Profilliste, um zu überprüfen, ob eine **customer** hat einen Kauf getätigt.
5. Sie erstellen eine Bestätigungs-Journey in Adobe Journey Optimizer.
6. [!DNL Adobe Journey Optimizer] sendet eine Auftragsbestätigungsnachricht über den bevorzugten Kanal.

>[!ENDTABS]

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Um die einzelnen Schritte in den obigen Übersichten auf hoher Ebene abzuschließen, lesen Sie die folgenden Abschnitte durch, die Links zu weiteren Informationen und detaillierteren Anweisungen enthalten.

### Benutzeroberflächenfunktionen und -elemente, die Sie verwenden {#ui-functionality-and-elements}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, verwenden Sie die am Anfang dieses Dokuments aufgelisteten Real-Time CDP-Funktionen und Benutzeroberflächenelemente. Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

### Erstellen eines Schemaentwurfs und Angeben von Feldergruppen

Ressourcen des Experience-Datenmodells (XDM) werden im [!UICONTROL Schemas] Arbeitsbereich in Adobe Experience Platform. Sie können die von Adobe bereitgestellten Kernressourcen anzeigen und untersuchen und benutzerdefinierte Ressourcen und Schemata für Ihr Unternehmen erstellen.

Weitere Informationen zum Erstellen von Schemas finden Sie im Abschnitt [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md)

Es gibt vier Schemaentwürfe, die für die Journey zur erneuten Interaktion verwendet werden. Für jedes Schema müssen spezifische Felder und einige dringend empfohlene Felder eingerichtet werden.

#### Schema für Kundenattribute

Das Kundenattribut-Schema wird durch eine [!UICONTROL Individuelles XDM-Profil] -Klasse, die die folgenden Feldergruppen enthält:

+++Persönliche Kontaktdetails (Feldergruppe)

[Persönliche Kontaktangaben](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;, die die Kontaktinformationen für eine Person beschreibt.

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| `mobilePhone.number` | Erforderlich | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| `personalEmail.address` | Erforderlich | Die E-Mail-Adresse der Person. |

+++

+++Demografische Details (Feldergruppe)

[Demografische Details](/help/xdm/field-groups/profile/demographic-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;. Die Feldergruppe stellt ein Personenobjekt der Stammebene bereit, dessen Unterfelder Informationen über eine Person beschreiben.

| Felder | Anforderung |
| --- | --- |
| `person.name.firstName` | Vorgeschlagen |
| `person.name.lastName` | Vorgeschlagen |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

[Audit-Attribute des externen Quellsystems](/help/xdm/data-types/external-source-system-audit-attributes.md) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

+++Einverständnis- und Präferenzfeldgruppen (Feldergruppe)

[Einverständnis und Voreinstellungen](/help/xdm/field-groups//profile/consents.md) Feldergruppe bietet ein einzelnes Objekt-Feld, die Zustimmung, um Zustimmungs- und Präferenzinformationen zu erfassen.

| Felder | Anforderung |
| --- | --- |
| `consents.marketing.email.val` | Erforderlich |
| `consents.marketing.preferred` | Erforderlich |
| `consents.marketing.push.val` | Erforderlich |
| `consents.marketing.sms.val` | Erforderlich |
| `consents.personalize.content.val` | Erforderlich |
| `consents.share.val` | Erforderlich |

+++

+++ Profiltestdetails (Feldergruppe)

Diese Feldergruppe wird für Best Practices verwendet.

+++

#### Schema für digitale Transaktionen des Kunden

Das Schema für digitale Transaktionen des Kunden wird durch eine [!UICONTROL XDM ExperienceEvent] -Klasse, die die folgenden Feldergruppen enthält:

+ + + Adobe Experience Platform Web SDK ExperienceEvent (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `device.model` | Vorgeschlagen |
| `environment.browserDetails.userAgent` | Vorgeschlagen |

+++

+++Webdetails (Feldergruppe)

Web Details ist eine Standardschemafeldgruppe für die XDM ExperienceEvent-Klasse, die zur Beschreibung von Informationen zu Webdetailereignissen wie Interaktion, Seitendetails und Referrer verwendet wird.

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Vorgeschlagen | Die ID für den Web-Link oder die URL, die der Interaktion entspricht. |
| `web.webInteraction.linkClicks.value` | Vorgeschlagen | Die Anzahl der Klicks für den Weblink oder die URL, die der Interaktion entspricht. |
| `web.webInteraction.name` | Vorgeschlagen | Der Name der Webseite. |
| `web.webInteraction.URL` | Vorgeschlagen | Die URL für die Webseite. |
| `web.webPageDetails.name` | Vorgeschlagen | Der Name der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| `web.webPageDetails.URL` | Vorgeschlagen | Die URL der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| `web.webReferrer.URL` | Vorgeschlagen | Beschreibt den Referrer einer Web-Interaktion, d. h. die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. |

+++

+++Consumer Experience-Ereignis (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `commerce.cart.cartID` | Vorgeschlagen |
| `commerce.cart.cartSource` | Vorgeschlagen |
| `commerce.cartAbandons.id` | Vorgeschlagen |
| `commerce.cartAbandons.value` | Vorgeschlagen |
| `commerce.order.orderType` | Vorgeschlagen |
| `commerce.order.payments.paymentAmount` | Vorgeschlagen |
| `commerce.order.payments.paymentType` | Vorgeschlagen |
| `commerce.order.payments.transactionID` | Vorgeschlagen |
| `commerce.order.priceTotal` | Vorgeschlagen |
| `commerce.order.purchaseID` | Vorgeschlagen |
| `commerce.productListAdds.id` | Vorgeschlagen |
| `commerce.productListAdds.value` | Vorgeschlagen |
| `commerce.productListOpens.id` | Vorgeschlagen |
| `commerce.productListOpens.value` | Vorgeschlagen |
| `commerce.productListRemoval.id` | Vorgeschlagen |
| `commerce.productListRemoval.value` | Vorgeschlagen |
| `commerce.productListViews.id` | Vorgeschlagen |
| `commerce.productListViews.value` | Vorgeschlagen |
| `commerce.productViews.id` | Vorgeschlagen |
| `commerce.productViews.value` | Vorgeschlagen |
| `commerce.purchases.id` | Vorgeschlagen |
| `commerce.purchases.value` | Vorgeschlagen |
| `marketing.campaignGroup` | Vorgeschlagen |
| `marketing.campaignName` | Vorgeschlagen |
| `marketing.trackingCode` | Vorgeschlagen |
| `productListItems.name` | Vorgeschlagen |
| `productListItems.priceTotal` | Vorgeschlagen |
| `productListItems.product` | Vorgeschlagen |
| `productListItems.quantity` | Vorgeschlagen |

+++

+ + + Endbenutzer-ID-Details (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Erforderlich | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.id` | Erforderlich | E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.namespace.code` | Erforderlich | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.mcid.authenticatedState` | Erforderlich | Authentifizierter Status der Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.id` | Erforderlich | Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.namespace.code` | Erforderlich | Namespace-Code für die Adobe Marketing Cloud ID (MCID). |

+++

+++Klassenwert (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `eventType` | Erforderlich |
| `timestamp` | Erforderlich |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

#### Schema für Offline-Transaktionen des Kunden

Das Schema der Offline-Transaktionen des Kunden wird durch eine [!UICONTROL XDM ExperienceEvent] -Klasse, die die folgenden Feldergruppen enthält:

+++Commerce-Details (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| `commerce.cart.cartID` | Erforderlich | Eine ID für den Warenkorb. |
| `commerce.order.orderType` | Erforderlich | Ein Objekt, das den Produktanordnungstyp beschreibt. |
| `commerce.order.payments.paymentAmount` | Erforderlich | Ein Objekt, das den Zahlungsbetrag der Produktbestellung beschreibt. |
| `commerce.order.payments.paymentType` | Erforderlich | Ein Objekt, das den Produktzahlungstyp beschreibt. |
| `commerce.order.payments.transactionID` | Erforderlich | Eine Transaktions-ID der Objektproduktbestellung. |
| `commerce.order.purchaseID` | Erforderlich | Eine Kauf-ID für Objektprodukte. |
| `productListItems.name` | Erforderlich | Eine Liste von Artikelnamen, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.priceTotal` | Erforderlich | Der Gesamtpreis der Artikelliste, die die von einem Kunden ausgewählten Produkte darstellt. |
| `productListItems.product` | Erforderlich | Die ausgewählten Produkte. |
| `productListItems.quantity` | Erforderlich | Die Anzahl der Elemente, die für die von einem Kunden ausgewählten Produkte stehen. |

+++

+++Persönliche Kontaktdetails (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| `mobilePhone.number` | Erforderlich | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| `personalEmail.address` | Erforderlich | Die E-Mail-Adresse der Person. |

+++

+++Klassenwert (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `eventType` | Erforderlich |
| `timestamp` | Erforderlich |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

#### Adobe-Web-Connector-Schema

Das Adobe-Web-Connector-Schema wird durch eine [!UICONTROL XDM ExperienceEvent] -Klasse, die die folgenden Feldergruppen enthält:

+ + + Adobe Analytics ExperienceEvent-Vorlage (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Vorgeschlagen | Die ID für den Web-Link oder die URL, die der Interaktion entspricht. |
| `web.webInteraction.linkClicks.value` | Vorgeschlagen | Die Anzahl der Klicks für den Weblink oder die URL, die der Interaktion entspricht. |
| `web.webInteraction.name` | Vorgeschlagen | Der Name der Webseite. |
| `web.webInteraction.URL` | Vorgeschlagen | Die URL für die Webseite. |
| `web.webPageDetails.name` | Vorgeschlagen | Der Name der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| `web.webPageDetails.URL` | Vorgeschlagen | Die URL der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| `web.webReferrer.URL` | Vorgeschlagen | Beschreibt den Referrer einer Web-Interaktion, d. h. die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. |
| `commerce.cart.cartID` | Vorgeschlagen | |
| `commerce.cart.cartSource` | Vorgeschlagen | |
| `commerce.cartAbandons.id` | Vorgeschlagen | |
| `commerce.cartAbandons.value` | Vorgeschlagen | |
| `commerce.order.orderType` | Vorgeschlagen | |
| `commerce.order.payments.paymentAmount` | Vorgeschlagen | |
| `commerce.order.payments.paymentType` | Vorgeschlagen | |
| `commerce.order.payments.transactionID` | Vorgeschlagen | |
| `commerce.order.priceTotal` | Vorgeschlagen | |
| `commerce.order.purchaseID` | Vorgeschlagen | |
| `commerce.productListAdds.id` | Vorgeschlagen | |
| `commerce.productListAdds.value` | Vorgeschlagen | |
| `commerce.productListOpens.id` | Vorgeschlagen | |
| `commerce.productListOpens.value` | Vorgeschlagen | |
| `commerce.productListRemoval.id` | Vorgeschlagen | |
| `commerce.productListRemoval.value` | Vorgeschlagen | |
| `commerce.productListViews.id` | Vorgeschlagen | |
| `commerce.productListViews.value` | Vorgeschlagen | |
| `commerce.productViews.id` | Vorgeschlagen | |
| `commerce.productViews.value` | Vorgeschlagen | |
| `commerce.purchases.id` | Vorgeschlagen | |
| `commerce.purchases.value` | Vorgeschlagen | |
| `marketing.campaignGroup` | Vorgeschlagen | |
| `marketing.campaignName` | Vorgeschlagen | |
| `marketing.trackingCode` | Vorgeschlagen | |
| `productListItems.name` | Vorgeschlagen | |
| `productListItems.priceTotal` | Vorgeschlagen | |
| `productListItems.product` | Vorgeschlagen | |
| `productListItems.quantity` | Vorgeschlagen | |
| `endUserIDs._experience.emailid.authenticatedState` | Erforderlich | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.id` | Erforderlich | E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.namespace.code` | Erforderlich | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.mcid.authenticatedState` | Erforderlich | Authentifizierter Status der Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.id` | Erforderlich | Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.namespace.code` | Erforderlich | Namespace-Code für die Adobe Marketing Cloud ID (MCID). |

+++

+++Klassenwert (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `eventType` | Erforderlich |
| `timestamp` | Erforderlich |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

### Datensatz aus einem Schema erstellen

Ein Datensatz ist eine Speicher- und Verwaltungsstruktur für eine Datengruppe, häufig eine Tabelle mit Feldern (Zeilen) und einem Schema (Spalten). Jedes Schema für intelligente Journey zur erneuten Interaktion verfügt über einen einzigen Datensatz.

Weitere Informationen zum Erstellen eines Datensatzes aus einem Schema finden Sie unter [Handbuch zur Benutzeroberfläche von Datensätzen](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Ähnlich wie beim Schritt zum Erstellen eines Schemas müssen Sie die Aufnahme des Datensatzes in das Echtzeit-Kundenprofil aktivieren. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie in der [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Datenschutz, Einverständnis und Data Governance

#### Einverständnisrichtlinien

>[!IMPORTANT]
>
>Es ist gesetzlich vorgeschrieben, Kunden die Möglichkeit zu geben, sich vom Erhalt von Nachrichten einer Marke abzumelden, und sicherzustellen, dass diese Entscheidung respektiert wird. Weitere Informationen zu den geltenden Rechtsvorschriften finden Sie in der Dokumentation zu [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Beim Erstellen eines Rückgewinnungspfads müssen die folgenden Zustimmungsrichtlinien berücksichtigt und verwendet werden:

* Wenn `consents.marketing.email.val = "Y"` then Can Email
* Wenn `consents.marketing.sms.val = "Y"` then Can SMS
* Wenn `consents.marketing.push.val = "Y"` then Can Push
* Wenn `consents.share.val = "Y"` dann kann Werbung
* Von der Kundenimplementierung definiert

#### DULE-Bezeichnung und -Durchsetzung

Persönliche E-Mail-Adressen werden als direkt identifizierbare Daten verwendet, die zur Identifizierung oder zum Kontakt mit einer bestimmten Person und nicht mit einem Gerät verwendet werden.

* `personalEmail.address = I1`

#### Marketing-Richtlinien

Es sind keine zusätzlichen Marketing-Richtlinien erforderlich, um die Journey zur erneuten Interaktion zu unterstützen. Bei Bedarf sollten jedoch die folgenden Punkte berücksichtigt werden:

* Einschränken vertraulicher Daten
* Einschränken der Onsite-Werbung
* E-Mail-Targeting einschränken
* Site-übergreifendes Targeting einschränken
* Beschränkung der Kombination direkt identifizierbarer Daten mit anonymen Daten

### Erstellen einer Zielgruppe

#### Zielgruppenerstellung für Journey zur Wiederaufnahme der Markeninteraktion

Die Journey der Rückgewinnung verwenden Zielgruppen, um bestimmte Attribute oder Verhaltensweisen zu definieren, die von einer Untergruppe von Profilen aus Ihrem Profilspeicher gemeinsam genutzt werden, um eine vermarktbare Personengruppe aus Ihrem Kundenstamm zu unterscheiden. Zielgruppen können auf zwei verschiedene Arten in Adobe Experience Platform erstellt werden - entweder direkt als Zielgruppen oder über Platform-abgeleitete Segmentdefinitionen.

Weitere Informationen zum direkten Erstellen von Zielgruppen finden Sie in der [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](/help/segmentation/ui/audience-composition.md).

Weitere Informationen zum Erstellen von Zielgruppen mithilfe von Platform-abgeleiteten Segmentdefinitionen finden Sie in der [Handbuch zur Benutzeroberfläche von Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Journey zur erneuten Interaktion]

Die folgenden Ereignisse werden für die Journey zur erneuten Interaktion verwendet, bei der Benutzer Produkte online angesehen und in den nächsten 24 Stunden nicht zum Warenkorb hinzugefügt haben, gefolgt von keiner Markeninteraktion in den folgenden 3 Tagen.

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.productListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

Der Deskriptor für die Journey zur erneuten Interaktion wird wie folgt angezeigt:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Journey zum abgesetzten Warenkorb]

Die folgenden Ereignisse werden für die Journey im Warenkorb verworfen, bei der Benutzer ein Produkt zum Warenkorb hinzugefügt, den Kauf jedoch nicht abgeschlossen oder den Warenkorb in den letzten 24 Stunden gelöscht haben.

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 30 minutes before now and <= 1440 minutes before now`
* `EventType: commerce.purchases`
   * `Timestamp: <= 30 minutes before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 30 minutes before now`

Der Deskriptor für die Journey zum abgebrochenen Warenkorb wird wie folgt angezeigt:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Journey-Setup in Adobe Journey Optimizer

>[!NOTE]
>
>Adobe Journey Optimizer umfasst nicht alle Elemente, die in den Diagrammen oben auf dieser Seite angezeigt werden. Alle Anzeigen für gebührenpflichtige Medien werden in erstellt [!UICONTROL Ziele].

Mit Adobe Journey Optimizer können Sie Ihren Kunden verknüpfte, kontextbezogene und personalisierte Erlebnisse bereitstellen. Die Journey ist der gesamte Vorgang der Interaktion eines Kunden mit der Marke. Für jede Journey von Anwendungsfällen sind spezifische Informationen erforderlich. Im Folgenden finden Sie die genauen Daten, die für jede Journey-Verzweigung benötigt werden.

>[!BEGINTABS]

>[!TAB Journey zur erneuten Interaktion]

+++Events

* Produktansichten
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType = commerce.productViews`
      * Felder:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Zum Warenkorb hinzufügen
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType = commerce.productListAdds`
      * Felder:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Markeninteraktion
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Felder:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Schlüssel-Journey-Logik

* Journey-Einstiegslogik
   * Ereignis für Produktansicht

* Bedingungen
   * Suchen Sie nach mindestens einem Online- oder Offline-Kaufereignis seit der letzten Ansicht des Produkts.
      * Schema: Customer Digital Transactions
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Suchen Sie nach mindestens einem Offline-Kauf seit der letzten Ansicht des Produkts:
      * Schema: Offline-Kundentransaktionen v.1
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Bedingungen - Auswählen des Target-Kanals
      * E-Mail
         * `consents.marketing.email.val = y`
      * Push-Benachrichtigung
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Kanalpersonalisierung
      * Personalisierte Kanalinhalte basierend auf der Produktansicht.

+++

>[!TAB Journey zum abgesetzten Warenkorb]

+++Events

* Zum Warenkorb hinzufügen
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType = commerce.productListAdds`
      * Felder:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Online-Käufe
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType = commerce.purchases`
      * Felder:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Markeninteraktion
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Felder:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Key Journey Logic

* Journey-Einstiegslogik
   * `AddToCart` Ereignis

* AuthenticatedState in authenticated

* Bedingung: Offline-Käufe seit dem letzten Abbruch des Warenkorbs:
   * Schema: Offline-Kundentransaktionen v.1
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Bedingung: Der Warenkorb wurde gelöscht, da der Warenkorb zuletzt abgebrochen wurde:
   * Schema: Customer Digital Transactions v.1
   * `eventType = commerce.cartCleared`
   * `cartID` (Kennung des Warenkorbs)
   * `timestamp > timestamp of cart was last abandoned`

* Target-Kanal auswählen (einen oder mehrere Kanäle für eine größere Reichweite auswählen)
   * E-Mail
      * `consents.marketing.email.val = y`
   * Push-Benachrichtigung
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Kanalpersonalisierung
      * Zeigen Sie Informationen zu Warenkorbdetails an und können mehrere Produkte in einem Tabellenformat anzeigen.

+++

>[!TAB Journey zur Bestellbestätigung]

+++Events

* Online-Käufe
   * Schema: Customer Digital Transactions
   * Felder:
      * `EventType`
   * Bedingung:
      * `EventType = commerce.purchases`
      * Felder:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Schlüssel-Journey-Logik

* Journey-Einstiegslogik
   * Bestellereignis

* Bedingungen
   * Wählen Sie Zielkanal (wählen Sie einen oder mehrere Kanäle für eine größere Reichweite aus).
      * Eine Bestellbestätigung gilt als Serving in der Natur, daher ist eine Zustimmungsprüfung in der Regel nicht erforderlich.
      * E-Mail
      * Push-Benachrichtigung
      * SMS

   * Personalisierung von Kanalinhalten
      * Zeigen Sie Bestelldetails an und können eine Liste von Produkten im Tabellenformat anzeigen.

+++

>[!ENDTABS]

Weitere Informationen zum Erstellen von Journey finden Sie unter [Adobe Journey Optimizer], lesen Sie die [Erste Schritte mit Journey-Handbuch](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=de).

### Einrichten von Paid-Media-Anzeigen in Zielen

Das Ziel-Framework wird für Paid-Media-Anzeigen verwendet. Nachdem die Einwilligung überprüft wurde, wird sie an die verschiedenen konfigurierten Ziele gesendet. Zum Beispiel Briefpost, E-Mail, Push und SMS.

#### Für Ziele erforderliche Daten

Streaming-Segmentexportziele (wie Facebook, Google Customer Match, Google DV360) unterstützen verschiedene Identitäten aus Kundendaten:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Das Segment &quot;Warenkorb abbrechen&quot;ist Streaming und kann daher vom Ziel-Framework für diesen Anwendungsfall verwendet werden.

* Stream/Ausgelöst
   * [Werbung](/help/destinations/catalog/advertising/overview.md)/[Paid Media und Social](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming-Ziel](/help/destinations/catalog/streaming/http-destination.md)
   * [Benutzerdefinierte Destination SDK](/help/destinations/destination-sdk/overview.md)

* Datei/Geplant alle drei Stunden
   * [E-Mail-Marketing](/help/destinations/catalog/email-marketing/overview.md)
