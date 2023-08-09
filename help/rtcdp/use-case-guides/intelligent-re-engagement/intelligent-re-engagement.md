---
title: Intelligente Erneute Interaktion
description: Stellen Sie während der wichtigsten Konversionsmomente überzeugende und vernetzte Erlebnisse bereit, um unregelmäßige Kunden intelligent erneut anzusprechen.
hide: true
hidefromtoc: true
source-git-commit: 23f9f73158b08a765cb47078b1525284e4c2e6e5
workflow-type: tm+mt
source-wordcount: '3263'
ht-degree: 9%

---

# Intelligentes erneutes Ansprechen Ihrer Kunden zur Rückkehr

Mit einer intelligenten Rückgewinnungsaktivität können Sie eine maßgeschneiderte, kanalübergreifende Drip-Kampagne einrichten, um Kunden zur Durchführung einer bestimmten Aktion zu bewegen. Die Abspielkampagne soll für eine begrenzte Zeit durchgeführt werden. Dazu gehört der Versand von E-Mails, SMS und bezahlten Anzeigen an Abonnenten. Sobald der Kunde die entsprechenden Maßnahmen getroffen hat, endet die Kampagne mit der Anschubkampagne sofort.

![Schrittweise intelligente Wiederaufnahme der Interaktion - Überblick auf hoher Ebene.](../intelligent-re-engagement/images/step-by-step.png)

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, nutzen Sie die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente (aufgelistet in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Aggregiert Daten aus verschiedenen Datenquellen, um die Kampagne anzukurbeln. Diese Daten werden dann verwendet, um die Kampagnenzielgruppen zu erstellen und personalisierte Datenelemente zu unterteilen, die in der E-Mail und in den Kacheln der Web-Promo verwendet werden (z. B. Name oder kontobezogene Informationen). Die CDP wird auch verwendet, um die Zielgruppen per E-Mail und Web (über Adobe Target) zu aktivieren.
   * [Schemata](/help/xdm/home.md)
   * [Profile](/help/profile/home.md)
   * [Zielgruppen](/help/segmentation/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=de)
   * [Ereignis- oder Audience Trigger](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Zielgruppen/Ereignisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Journey-Aktionen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=de)

### Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

Es wurden drei Journey zur Rückgewinnung erstellt.

>[!BEGINTABS]

>[!TAB Journey zur erneuten Interaktion]

Die Rückgewinnungs-Journey ermöglicht sowohl auf der Website als auch in der App das Abbrechen des Produktdurchsuchs. Diese Journey wird ausgelöst, wenn ein Produkt angezeigt wurde, ohne dass es gekauft oder zum Warenkorb hinzugefügt wurde. Die Markeninteraktion wird nach drei Tagen ausgelöst, wenn innerhalb der letzten 24 Stunden keine Liste hinzugefügt wird.

![Kundenintelligente Journey-Rückgewinnung - Überblick über die allgemeine visuelle Darstellung.](../intelligent-re-engagement/images/re-engagement-journey.png)

1. Die Daten werden in die Erfassung der Web SDK/Mobile SDK/Edge Network API über Edge Network (bevorzugte Methode) aggregiert.
2. Als **customer**, erstellen Sie Datensätze, die für [!UICONTROL Profil].
3. Als **customer**, laden Sie Profile in Real-Time CDP und erstellen Sie Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Als **customer**, erstellen Sie zielgerichtete Zielgruppen aus der Profilliste, um zu überprüfen, ob eine **Benutzer** hat in den letzten drei Tagen eine Markeninteraktion durchgeführt.
5. Als **customer**, erstellen Sie eine Journey zur erneuten Interaktion in Adobe Journey Optimizer.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** zur Aktivierung von Zielgruppen für gewünschte Paid-Media-Ziele.
7. Adobe Journey Optimizer prüft die Zustimmung und sendet die verschiedenen konfigurierten Aktionen aus.

>[!TAB Journey zum abgesetzten Warenkorb]

Diese Journey dient der Bestimmung von Produkten, die zwar in den Warenkorb gelegt, aber nicht auf der Website und in der App erworben wurden. Wird zum Starten und Beenden von Paid Media-Kampagnen verwendet

![Der Kunde hat die Journey des Warenkorbs abgebrochen und eine allgemeine visuelle Übersicht erstellt.](../intelligent-re-engagement/images/abandoned-cart-journey.png)

1. Die Daten werden in die Erfassung der Web SDK/Mobile SDK/Edge Network API über Edge Network (bevorzugte Methode) aggregiert.
2. Als **customer**, erstellen Sie Datensätze, die für [!UICONTROL Profil].
3. Als **customer**, laden Sie Profile in Real-Time CDP und erstellen Sie Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Als **customer**, erstellen Sie zielgerichtete Zielgruppen aus der Profilliste, um zu überprüfen, ob eine **Benutzer** hat einen Artikel in den Warenkorb gelegt, aber den Kauf nicht abgeschlossen. Die **[!UICONTROL Zum Warenkorb hinzufügen]** -Ereignis startet einen Timer, der 30 Minuten wartet, und sucht dann nach dem Kauf. Wenn kein Kauf getätigt wurde, wird die Variable **Benutzer** wird zum **[!UICONTROL Warenkorb verlassen]** Zielgruppen.
5. Als **customer**, erstellen Sie in Adobe Journey Optimizer eine Journey zum abgebrochenen Warenkorb.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** zur Aktivierung von Zielgruppen für gewünschte Paid-Media-Ziele.
7. Adobe Journey Optimizer prüft die Zustimmung und sendet die verschiedenen konfigurierten Aktionen aus.

>[!TAB Journey zur Bestellbestätigung]

Diese Journey ermöglicht Produktkäufe sowohl auf der Website als auch in der App.

![Kundenauftragsbestätigung Journey - Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/order-confirmation-journey.png)

1. Die Daten werden in die Erfassung der Web SDK/Mobile SDK/Edge Network API über Edge Network (bevorzugte Methode) aggregiert.
2. Als **customer**, erstellen Sie Datensätze, die für [!UICONTROL Profil].
3. Als **customer**, laden Sie Profile in Real-Time CDP und erstellen Sie Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Als **customer**, erstellen Sie zielgerichtete Zielgruppen aus der Profilliste, um zu überprüfen, ob eine **Benutzer** hat einen Kauf getätigt.
5. Als **customer**, erstellen Sie eine Bestätigungs-Journey in Adobe Journey Optimizer.
6. Adobe Journey Optimizer sendet eine Auftragsbestätigungsnachricht über den bevorzugten Kanal.

>[!ENDTABS]

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte durch, die Links zur weiteren Dokumentation enthalten, um die einzelnen Schritte in den obigen Übersichten auf hoher Ebene durchzuführen.

### Benutzeroberflächenfunktionen und -elemente, die Sie verwenden {#ui-functionality-and-elements}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, nutzen Sie die folgenden Real-Time CDP-Funktionen und Benutzeroberflächenelemente (aufgelistet in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

* [Schemata](/help/xdm/home.md)
* [Profile](/help/profile/home.md)
* [Datensätze](/help/catalog/datasets/overview.md)
* [Zielgruppen](/help/segmentation/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=de)
* [Ziele](/help/destinations/home.md)

### Einrichten eines Schemaentwurfs und von Feldgruppen

Es werden vier Schemaentwürfe für die intelligenten Journey zur erneuten Interaktion verwendet. Für jedes Schema müssen bestimmte Felder sowie einige dringend empfohlene Felder eingerichtet werden.

>[!BEGINTABS]

>[!TAB Kundenattribute (Profilschema)]

Die für das Profilschema erforderlichen Feldgruppen sind:

+++Persönliche Kontaktdetails (Feldergruppe)

[Persönliche Kontaktangaben](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;, die die Kontaktinformationen für eine Person beschreibt.

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| mobilePhone.number | Erforderlich | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| personalEmail.address | Erforderlich | Die E-Mail-Adresse der Person. |

+++

+++Demografische Details (Feldergruppe)

[Demografische Details](/help/xdm/field-groups/profile/demographic-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;. Die Feldergruppe stellt ein Personenobjekt der Stammebene bereit, dessen Unterfelder Informationen über eine Person beschreiben.

| Felder | Anforderung |
| --- | --- |
| person.name.firstName | Vorgeschlagen |
| person.name.lastName | Vorgeschlagen |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

[Audit-Attribute des externen Quellsystems](/help/xdm/data-types/external-source-system-audit-attributes.md) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

+++Einverständnis- und Präferenzfeldgruppen (Feldergruppe)

[Einverständnis und Voreinstellungen](/help/xdm/field-groups//profile/consents.md) Feldergruppe bietet ein einzelnes Objekt-Feld, die Zustimmung, um Zustimmungs- und Präferenzinformationen zu erfassen.

| Felder | Anforderung |
| --- | --- |
| consents.marketing.email.val | Erforderlich |
| consents.marketing.preferred | Erforderlich |
| consents.marketing.push.val | Erforderlich |
| consents.marketing.sms.val | Erforderlich |
| consents.personalize.content.val | Erforderlich |
| consents.share.val | Erforderlich |

+++

+++ Profiltestdetails (Feldergruppe)

Diese Feldergruppe wird für Best Practices verwendet.

+++

![Eine Aufzeichnung des Kundenattribut-Schemas mit einer Liste von Feldergruppen.](../intelligent-re-engagement/images/customer-attributes.gif)

>[!TAB Digitale Kundentransaktionen]

Die für das Experience Event-Schema für Online-Aktivitäten (nicht Adobe Analytics Connector) erforderlichen Feldergruppen sind:

+ + + Adobe Experience Platform Web SDK ExperienceEvent (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| device.model | Vorgeschlagen |
| environment.browserDetails.userAgent | Vorgeschlagen |

+++

+++Webdetails (Feldergruppe)

Web Details ist eine Standardschemafeldgruppe für die XDM ExperienceEvent-Klasse, die zur Beschreibung von Informationen zu Webdetailereignissen wie Interaktion, Seitendetails und Referrer verwendet wird.

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | Vorgeschlagen | Die ID für den Web-Link oder die URL, die der Interaktion entspricht. |
| web.webInteraction.linkClicks.value | Vorgeschlagen | Die Anzahl der Klicks für den Weblink oder die URL, die der Interaktion entspricht. |
| web.webInteraction.name | Vorgeschlagen | Der Name der Webseite. |
| web.webInteraction.URL | Vorgeschlagen | Die URL für die Webseite. |
| web.webPageDetails.name | Vorgeschlagen | Der Name der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| web.webPageDetails.URL | Vorgeschlagen | Die URL der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| web.webReferrer.URL | Vorgeschlagen | Beschreibt den Referrer einer Web-Interaktion, d. h. die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. |

+++

+++Consumer Experience-Ereignis (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| commerce.cart.cartID | Vorgeschlagen |
| commerce.cart.cartSource | Vorgeschlagen |
| commerce.cartAbandons.id | Vorgeschlagen |
| commerce.cartAbandons.value | Vorgeschlagen |
| commerce.order.orderType | Vorgeschlagen |
| commerce.order.payments.paymentAmount | Vorgeschlagen |
| commerce.order.payments.paymentType | Vorgeschlagen |
| commerce.order.payments.transactionID | Vorgeschlagen |
| commerce.order.priceTotal | Vorgeschlagen |
| commerce.order.purchaseID | Vorgeschlagen |
| commerce.productListAdds.id | Vorgeschlagen |
| commerce.productListAdds.value | Vorgeschlagen |
| commerce.productListOpens.id | Vorgeschlagen |
| commerce.productListOpens.value | Vorgeschlagen |
| commerce.productListRemoval.id | Vorgeschlagen |
| commerce.productListRemoval.value | Vorgeschlagen |
| commerce.productListViews.id | Vorgeschlagen |
| commerce.productListViews.value | Vorgeschlagen |
| commerce.productViews.id | Vorgeschlagen |
| commerce.productViews.value | Vorgeschlagen |
| commerce.purchases.id | Vorgeschlagen |
| commerce.purchases.value | Vorgeschlagen |
| marketing.campaignGroup | Vorgeschlagen |
| marketing.campaignName | Vorgeschlagen |
| marketing.trackingCode | Vorgeschlagen |
| productListItems.name | Vorgeschlagen |
| productListItems.priceTotal | Vorgeschlagen |
| productListItems.product | Vorgeschlagen |
| productListItems.quantity | Vorgeschlagen |

+++

+ + + Endbenutzer-ID-Details (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| endUserIDs._experience.emailid.authenticatedState | Erforderlich | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| endUserIDs._experience.emailid.id | Erforderlich | E-Mail-Adresse des Endbenutzers. |
| endUserIDs._experience.emailid.namespace.code | Erforderlich | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| endUserIDs._experience.mcid.authenticatedState | Erforderlich | Authentifizierter Status der Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| endUserIDs._experience.mcid.id | Erforderlich | Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| endUserIDs._experience.mcid.namespace.code | Erforderlich | Namespace-Code für die Adobe Marketing Cloud ID (MCID). |

+++

+++Klassenwert (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| eventType | Erforderlich |
| Zeitstempel | Erforderlich |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

![Eine Aufzeichnung des Schemas für digitale Transaktionen von Kunden mit einer Liste von Feldergruppen.](../intelligent-re-engagement/images/customer-digital-transactions.gif)

>[!TAB Offline-Transaktionen von Kunden]

Die für das Erlebnisereignis-Schema für die Offline-Aktivität erforderlichen Feldergruppen sind:

+++Commerce-Details (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| commerce.cart.cartID | Erforderlich | Eine ID für den Warenkorb. |
| commerce.order.orderType | Erforderlich | Ein Objekt, das den Produktanordnungstyp beschreibt. |
| commerce.order.payments.paymentAmount | Erforderlich | Ein Objekt, das den Zahlungsbetrag der Produktbestellung beschreibt. |
| commerce.order.payments.paymentType | Erforderlich | Ein Objekt, das den Produktzahlungstyp beschreibt. |
| commerce.order.payments.transactionID | Erforderlich | Eine Transaktions-ID der Objektproduktbestellung. |
| commerce.order.purchaseID | Erforderlich | Eine Kauf-ID für Objektprodukte. |
| productListItems.name | Erforderlich | Eine Liste von Artikelnamen, die die von einem Kunden ausgewählten Produkte darstellen. |
| productListItems.priceTotal | Erforderlich | Der Gesamtpreis der Artikelliste, die die von einem Kunden ausgewählten Produkte darstellt. |
| productListItems.product | Erforderlich | Die ausgewählten Produkte. |
| productListItems.quantity | Erforderlich | Die Anzahl der Elemente, die für die von einem Kunden ausgewählten Produkte stehen. |

+++

+++Persönliche Kontaktdetails (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| mobilePhone.number | Erforderlich | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| personalEmail.address | Erforderlich | Die E-Mail-Adresse der Person. |

+++

+++Klassenwert (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| eventType | Erforderlich |
| Zeitstempel | Erforderlich |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

![Eine Aufzeichnung des Kunden-Offline-Transaktionsschemas mit einer Liste von Feldergruppen.](../intelligent-re-engagement/images/customer-offline-transactions.gif)

>[!TAB Adobe-Web-Connector-Schema]

Die für das Experience Event-Schema für den Adobe Analytics Data Feed erforderlichen Feldergruppen sind:

+ + + Adobe Analytics ExperienceEvent-Vorlage (Feldergruppe)

| Felder | Anforderung | Beschreibung |
| --- | --- | --- |
| web.webInteraction.linkClicks.id | Vorgeschlagen | Die ID für den Web-Link oder die URL, die der Interaktion entspricht. |
| web.webInteraction.linkClicks.value | Vorgeschlagen | Die Anzahl der Klicks für den Weblink oder die URL, die der Interaktion entspricht. |
| web.webInteraction.name | Vorgeschlagen | Der Name der Webseite. |
| web.webInteraction.URL | Vorgeschlagen | Die URL für die Webseite. |
| web.webPageDetails.name | Vorgeschlagen | Der Name der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| web.webPageDetails.URL | Vorgeschlagen | Die URL der Webseite, auf der die Web-Interaktion stattgefunden hat. |
| web.webReferrer.URL | Vorgeschlagen | Beschreibt den Referrer einer Web-Interaktion, d. h. die URL, von der ein Besucher unmittelbar vor der Aufzeichnung der aktuellen Web-Interaktion kam. |
| commerce.cart.cartID | Vorgeschlagen | |
| commerce.cart.cartSource | Vorgeschlagen | |
| commerce.cartAbandons.id | Vorgeschlagen | |
| commerce.cartAbandons.value | Vorgeschlagen | |
| commerce.order.orderType | Vorgeschlagen | |
| commerce.order.payments.paymentAmount | Vorgeschlagen | |
| commerce.order.payments.paymentType | Vorgeschlagen | |
| commerce.order.payments.transactionID | Vorgeschlagen | |
| commerce.order.priceTotal | Vorgeschlagen | |
| commerce.order.purchaseID | Vorgeschlagen | |
| commerce.productListAdds.id | Vorgeschlagen | |
| commerce.productListAdds.value | Vorgeschlagen | |
| commerce.productListOpens.id | Vorgeschlagen | |
| commerce.productListOpens.value | Vorgeschlagen | |
| commerce.productListRemoval.id | Vorgeschlagen | |
| commerce.productListRemoval.value | Vorgeschlagen | |
| commerce.productListViews.id | Vorgeschlagen | |
| commerce.productListViews.value | Vorgeschlagen | |
| commerce.productViews.id | Vorgeschlagen | |
| commerce.productViews.value | Vorgeschlagen | |
| commerce.purchases.id | Vorgeschlagen | |
| commerce.purchases.value | Vorgeschlagen | |
| marketing.campaignGroup | Vorgeschlagen | |
| marketing.campaignName | Vorgeschlagen | |
| marketing.trackingCode | Vorgeschlagen | |
| productListItems.name | Vorgeschlagen | |
| productListItems.priceTotal | Vorgeschlagen | |
| productListItems.product | Vorgeschlagen | |
| productListItems.quantity | Vorgeschlagen | |
| endUserIDs._experience.emailid.authenticatedState | Erforderlich | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| endUserIDs._experience.emailid.id | Erforderlich | E-Mail-Adresse des Endbenutzers. |
| endUserIDs._experience.emailid.namespace.code | Erforderlich | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| endUserIDs._experience.mcid.authenticatedState | Erforderlich | Authentifizierter Status der Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| endUserIDs._experience.mcid.id | Erforderlich | Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| endUserIDs._experience.mcid.namespace.code | Erforderlich | Namespace-Code für die Adobe Marketing Cloud ID (MCID). |

+++

+++Klassenwert (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| eventType | Erforderlich |
| Zeitstempel | Erforderlich |

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

![Eine Aufzeichnung des Adobe Web Connector-Schemas mit einer Liste von Feldgruppen.](../intelligent-re-engagement/images/adobe-web-connector.png)

>[!ENDTABS]

### Datensatz aus einem Schema erstellen

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Für intelligente Journey zur erneuten Interaktion verfügt jedes Schema über einen Datensatz.

Um einen Datensatz aus einem Schema zu erstellen, führen Sie die folgenden Schritte aus:

1. Navigieren Sie zu **[!UICONTROL Data Management]** > **[!UICONTROL Datensätze]** und wählen **[!UICONTROL Datensatz erstellen]**.
2. Wählen Sie **[!UICONTROL Datensatz aus Schema erstellen]** aus.
3. Wählen Sie das von Ihnen erstellte relevante Rückgewinnungsschema aus.
4. Geben Sie Ihrem Datensatz einen Namen und optional eine Beschreibung.
5. Wählen Sie **[!UICONTROL Beenden]** aus.

![Eine Aufzeichnung der Schritte zum Erstellen eines Datensatzes aus einem Schema.](../intelligent-re-engagement/images/dataset-from-schema.gif)

Beachten Sie, dass Sie ähnlich wie beim Schritt zum Erstellen eines Schemas die Aufnahme des Datensatzes in das Echtzeit-Kundenprofil aktivieren müssen. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie in der [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Datensatz für Profil aktivieren.](../intelligent-re-engagement/images/enable-dataset-for-profile.png)

### Datenschutz, Einverständnis und Data Governance

#### Einverständnisrichtlinien

>[!IMPORTANT]
>
>Es ist gesetzlich vorgeschrieben, Kunden die Möglichkeit zu geben, sich vom Erhalt von Nachrichten einer Marke abzumelden, und sicherzustellen, dass diese Entscheidung respektiert wird. Weitere Informationen zu den geltenden Rechtsvorschriften finden Sie in der Dokumentation zu [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Die folgenden Zustimmungsrichtlinien müssen bei der Einrichtung einer Rückgewinnungs-Journey berücksichtigt und verwendet werden:

* Wenn williges.marketing.email.val = &quot;Y&quot;, dann kann E-Mail gesendet werden
* Wenn williges.marketing.sms.val = &quot;Y&quot;, dann Can SMS
* Wenn die Datei &quot;Consents.marketing.push.val = &quot;Y&quot;ist, kann Push
* Wenn williges.share.val = &quot;Y&quot;ist, kann Werbung
* Von der Kundenimplementierung definiert

#### DULE-Bezeichnung und -Durchsetzung

Die persönliche E-Mail-Adresse wird als direkt identifizierbare Daten verwendet, die anstelle eines Geräts zur Identifizierung oder zum Kontakt einer bestimmten Person verwendet werden können.

* personalEmail.address = I1

#### Marketing-Richtlinien

Es gibt keine zusätzlichen Marketing-Richtlinien für die Rückgewinnungs-Journey, jedoch sollte Folgendes als gewünscht betrachtet werden:

* Berücksichtigen Sie bei Bedarf
* Einschränken vertraulicher Daten
* Einschränken der Onsite-Werbung
* E-Mail-Targeting einschränken
* Site-übergreifendes Targeting einschränken
* Beschränkung der Kombination direkt identifizierbarer Daten mit anonymen Daten

### Zielgruppenerstellung für Journey zur Wiederaufnahme der Markeninteraktion

Zielgruppen für jede Journey zur erneuten Interaktion müssen mit bestimmten Ereignissen für die Segmentqualifizierung eingerichtet werden.  Diese Details finden Sie unten auf den entsprechenden Registerkarten für jede Journey.

>[!BEGINTABS]

>[!TAB Journey zur erneuten Interaktion]

Die folgenden Ereignisse werden für die Journey zur erneuten Interaktion verwendet, bei der Profile Online-Produkte anzeigten, in den nächsten 24 Stunden nicht zum Warenkorb hinzugefügt wurden und in den folgenden 3 Tagen keine Markeninteraktion folgte.

Schließen Sie Zielgruppe ein, die mindestens 1 EventType = ProductViews -Ereignis THEN mindestens 1 Beliebiges Ereignis hat, bei dem (EventType ist nicht gleich commerce.productListAdds) und in den letzten 24 Stunden stattfindet und nach 3 Tagen kein Beliebiges Ereignis aufweist, bei dem (EventType = application.launch oder web.webpagedetails.pageViews oder commerce.purchase) und in den letzten 2 Tagen auftritt.

![Screenshot der Rückgewinnungs-Audience mit dem Regelsatz.](../intelligent-re-engagement/images/re-engagement-audience.png)

>[!TAB Journey zum abgesetzten Warenkorb]

Die folgenden Ereignisse werden für Profile verwendet, die ein Produkt zum Warenkorb hinzugefügt, den Kauf jedoch nicht abgeschlossen oder den Warenkorb in den letzten 24 Stunden gelöscht haben.

include EventType = commerce.productListFügt zwischen 30 und 1440 Minuten vor jetzt hinzu.
exclude EventType = commerce.purchases 30 Minuten vor jetzt ODER EventType = commerce.productListRemovals UND Warenkorb-ID gleich Produktlisten-IDs1 Warenkorb-ID (das Aufnahmeereignis).

![Screenshot der Rückgewinnungs-Audience mit dem Regelsatz.](../intelligent-re-engagement/images/abandoned-cart-audience.png)

>[!ENDTABS]

Weitere Informationen zum Erstellen von Zielgruppen finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche von Audience Builder](/help/segmentation/ui/segment-builder.md).

### Journey-Setup in Adobe Journey Optimizer

>[!NOTE]
>
>Adobe Journey Optimizer umfasst nicht alle Elemente, die in den Diagrammen oben auf dieser Seite angezeigt werden. Alle Anzeigen für gebührenpflichtige Medien werden in erstellt [!UICONTROL Ziele].

Spezifische Informationen sind für die verschiedenen Journey erforderlich, die jeder Anwendungsfall haben kann. Die für jede Journey-Verzweigung erforderlichen Daten finden Sie unten auf den entsprechenden Registerkarten.

>[!BEGINTABS]

>[!TAB Journey zur erneuten Interaktion]

![Customer Re-Interaction-Journey in Adobe Journey Optimizer - Übersicht](../intelligent-re-engagement/images/re-engagement-ajo.png)

+++Events

* Produktansichten
   * Schema: Customer Digital Transactions
   * Felder:
      * EventType
   * Bedingung:
      * EventType = commerce.productViews
      * Felder:
         * Commerce.productViews.id
         * Commerce.productViews.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Zum Warenkorb hinzufügen
   * Schema: Customer Digital Transactions
   * Felder:
      * Ereignistyp
   * Bedingung:
      * Ereignistyp = commerce.productListAdds
      * Felder:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * commerce.cart.cartID
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Markeninteraktion
   * Schema: Customer Digital Transactions
   * Felder:
      * EventType
   * Bedingung:
      * EventType in application.launch, commerce.purchases, web.webpageDetails.pageViews
      * Felder:
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++Schlüssel-Journey-Logik

* Journey-Einstiegslogik
   * Ereignis für Produktansicht

* Bedingungen
   * Suchen Sie nach mindestens einem Online- oder Offline-Kaufereignis seit der letzten Ansicht des Produkts.
      * Schema: Customer Digital Transactions
      * eventType = commerce.purchases
      * Zeitstempel > Zeitstempel des zuletzt angezeigten Produkts

   * Suchen Sie nach mindestens einem Offline-Kauf seit der letzten Ansicht des Produkts:
      * Schema: Offline-Kundentransaktionen v.1
      * eventType = commerce.purchases
      * Zeitstempel > Zeitstempel des zuletzt angezeigten Produkts

   * Bedingungen - Auswählen des Target-Kanals
      * E-Mail
         * consent.marketing.email.val = y
      * Push-Benachrichtigung
         * consents.marketing.push.val=y
      * SMS
         * consent.marketing.sms.val = y

   * Kanalpersonalisierung
      * Personalisierte Kanalinhalte basierend auf der Produktansicht.

+++

>[!TAB Journey zum abgesetzten Warenkorb]

![Journey zum abgebrochenen Warenkorb in Adobe Journey Optimizer - Übersicht](../intelligent-re-engagement/images/abandoned-cart-ajo.png)

+++Events

* Zum Warenkorb hinzufügen
   * Schema: Customer Digital Transactions
   * Felder:
      * Ereignistyp
   * Bedingung:
      * Ereignistyp = commerce.productListAdds
      * Felder:
         * Commerce.productListAdds.id
         * Commerce.productListAdds.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * commerce.cart.cartID
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Online-Käufe
   * Schema: Customer Digital Transactions
   * Felder:
      * Ereignistyp
   * Bedingung:
      * Ereignistyp = commerce.purchases
      * Felder:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

* Markeninteraktion
   * Schema: Customer Digital Transactions
   * Felder:
      * EventType
   * Bedingung:
      * EventType in application.launch, commerce.purchases, web.webpageDetails.pageViews
      * Felder:
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * web.webpagedetails.URL
         * web.webpagedetails.isHomePage
         * web.webpagedetails.name
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id
         * Commerce.purchases.id
         * Commerce.purchases.value
         * shipping.address.city
         * shipping.address.countryCode
         * shipping.address.postalCode
         * shipping.address.state
         * shipping.address.street1
         * shipping.address.street2
         * shipping.shipDate
         * shipping.trackingNumber
         * shipping.trackingURL

+++

+++Key Journey Logic

* Journey-Einstiegslogik
   * AddToCart-Ereignis

* AuthenticatedState in authenticated

* Bedingung: Offline-Käufe seit dem letzten Abbruch des Warenkorbs:
   * Schema: Offline-Kundentransaktionen v.1
   * eventType = commerce.purchases
   * timestamp > timestamp of cart was last abandoned

* Bedingung: Der Warenkorb wurde gelöscht, da der Warenkorb zuletzt abgebrochen wurde:
   * Schema: Customer Digital Transactions v.1
   * eventType = commerce.cartCleared
   * cartID (ID des Warenkorbs)
   * timestamp > timestamp of cart was last abandoned

* Target-Kanal auswählen (einen oder mehrere Kanäle für eine größere Reichweite auswählen)
   * E-Mail
      * consent.marketing.email.val = y
   * Push-Benachrichtigung
      * consents.marketing.push.val = y
   * SMS
      * consent.marketing.sms.val = y
   * Kanalpersonalisierung
      * Zeigen Sie Informationen zu Warenkorbdetails an und können mehrere Produkte in einem Tabellenformat anzeigen.

+++

>[!TAB Journey zur Bestellbestätigung]

![Journey zur Bestellbestätigung in Adobe Journey Optimizer - Übersicht](../intelligent-re-engagement/images/order-confirmation-ajo.png)

+++Events

* Online-Käufe
   * Schema: Customer Digital Transactions
   * Felder:
      * EventType
   * Bedingung:
      * Ereignistyp = commerce.purchases
      * Felder:
         * Commerce.purchases.id
         * Commerce.purchases.value
         * eventType
         * identityMap.authenticatedState
         * identityMap.id
         * identityMap.primary
         * productListItems.SKU
         * productListItems.currencyCode
         * productListItems.name
         * productListItems.priceTotal
         * productListItems.product
         * productListItems.productImageUrl
         * productListItems.quantity
         * Zeitstempel
         * endUserIDs._experience.emailid.authenticatedState
         * endUserIDs._experience.emailid.id
         * endUserIDs._experience.emailid.namespace.code
         * _id

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

Das Ziel-Framework wird für Paid-Media-Anzeigen verwendet. Sobald die Einwilligung überprüft wurde, wird sie an die verschiedenen konfigurierten Ziele gesendet. Zum Beispiel Briefpost, E-Mail usw.

#### Für Ziele erforderliche Daten

Streaming-Segmentexportziele (wie Facebook, Google Customer Match, Google DV360) unterstützen verschiedene Identitäten aus Kundendaten:

* personalEmail.address
* ECID
* mobilePhone.number

Das Segment &quot;Warenkorb abbrechen&quot;ist Streaming und kann daher vom Ziel-Framework für diesen Anwendungsfall verwendet werden.

* Stream/Ausgelöst
   * [Werbung](/help/destinations/catalog/advertising/overview.md)/[Paid Media und Social](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming-Ziel](/help/destinations/catalog/streaming/http-destination.md)
   * [Benutzerdefinierte Destination SDK](/help/destinations/destination-sdk/overview.md)

* Datei/Geplant alle drei Stunden
   * [E-Mail-Marketing](/help/destinations/catalog/email-marketing/overview.md)
