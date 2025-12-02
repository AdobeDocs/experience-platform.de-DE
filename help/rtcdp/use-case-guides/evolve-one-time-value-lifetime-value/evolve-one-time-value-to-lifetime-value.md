---
title: Weiterentwicklung des einmaligen Kundenwerts zum Lebenszeitwert
description: Erfahren Sie, wie Sie personalisierte Kampagnen erstellen, um die besten komplementären Produkte oder Services basierend auf den Attributen, dem Verhalten und früheren Käufen eines bestimmten Kunden anzubieten.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 2%

---

# Weiterentwicklung des einmaligen Kundenwerts zum Lebenszeitwert

>[!IMPORTANT]
> 
>* Auf dieser Seite wird eine Beispielimplementierung von Real-Time CDP und Adobe Journey Optimizer für den beschriebenen Anwendungsfall vorgestellt. Verwenden Sie die Zahlen, Qualifizierungskriterien und andere Felder auf der Seite als Leitfaden und nicht als verbindliche Zahlen.
>* Um diesen Anwendungsfall abzuschließen, benötigen Sie eine Lizenz für Real-Time CDP und Adobe Journey Optimizer. Weitere Informationen finden Sie [ Abschnitt „Voraussetzungen und Planung](#prerequisites-and-planning) weiter unten.

Implementieren Sie den Anwendungsfall Einmaliger Kundenwert in lebenslanger Wertschöpfung , um die Markeninteraktion und die Markentreue zu fördern. Erstellen Sie ein vernetztes Kundenerlebnis auf mehreren Kanälen oder Journey. Nutzen Sie dazu die Leistungsfähigkeit von Experience Platform, erweitert um [Real-Time CDP](/help/rtcdp/home.md) und [Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home).

Die Personas, an die Sie sich richten, sind die seltenen Besucher Ihrer Eigenschaften, die in den letzten drei Monaten einige Käufe getätigt haben.

Betrachten Sie diese Kunden, die Ihre Immobilien besuchen und sporadisch die Produkte oder Dienstleistungen kaufen, die Sie anbieten. Vielleicht möchten Sie personalisierte Kampagnen erstellen, die diese Kundinnen und Kunden ansprechen, damit Ihre Marke ihnen einen längerfristigen Wert statt eines einmaligen Werts bieten kann. Sie lernen Folgendes:

* Erfassen und Verwalten von Daten
* Erstellen von Zielgruppen
* Erstellen Sie Journeys, um diese Zielgruppen in Adobe Journey Optimizer anzusprechen und in Real-Time CDP zu aktivieren.

![Schritt für Schritt Entwicklung eines einmaligen Werts zu einem Lebenszeitwert Allgemeine visuelle Übersicht.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## Voraussetzungen und Planung {#prerequisites-and-planning}

In Anbetracht der Tatsache, dass Sie intern ein Geschäftsziel und ein Ziel definiert haben, um die Markentreue zu steigern. Dies kann in der Ausführung eines Anwendungsfalls bestehen, um die Kundeninteraktion und -loyalität zu fördern.

Hierfür sind die beiden Experience Platform-Apps [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=de) erforderlich. Im Folgenden sind verschiedene Funktionen und Benutzeroberflächenelemente aus den beiden Apps aufgeführt, die Sie bei der Implementierung des Anwendungsfalls verwenden werden.

>[!TIP]
>
>Vergewissern Sie sich, dass Sie die notwendigen [Attribut-basierten Zugriffsrechte](/help/access-control/abac/end-to-end-guide.md) für alle diese Bereiche haben, oder bitten Sie Ihre Systemadmins, Ihnen die notwendigen Rechte zu erteilen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html): Integrieren Sie Daten in Datenquellen, um die Kampagne zu unterstützen. Diese Daten werden dann verwendet, um die Kampagnen-Audiences zu erstellen und die in der E-Mail und den Web-Promo-Kacheln verwendeten personalisierten Datenelemente (z. B. Name oder kontobezogene Informationen) aufzudecken. Schließlich wird Real-Time CDP auch verwendet, um Zielgruppen für Paid-Media-Ziele zu aktivieren.
   * [Schemata](/help/xdm/home.md)
   * [Profile](/help/profile/home.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
   * [Zielgruppen](/help/segmentation/home.md)
   * [Ziele](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html): Entwerfen Sie Journey, richten Sie Trigger ein und erstellen Sie die richtigen Nachrichten für Ihre Besucher.
   * [Ereignis- oder Zielgruppen-Trigger ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Zielgruppen und Ereignisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=de)
   * [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Architektur von Real-Time CDP und Journey Optimizer

Nachfolgend finden Sie eine allgemeine Architekturansicht der verschiedenen Komponenten von Real-Time CDP und Journey Optimizer. Dieses Diagramm zeigt, wie Daten durch die beiden Experience Platform-Apps von der Datenerfassung bis zu dem Punkt fließen, an dem sie über Journey oder Kampagnen für Ziele aktiviert werden, um den auf dieser Seite beschriebenen Anwendungsfall zu erreichen.

![Überblick über die Architektur.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

Nachstehend finden Sie einen allgemeinen Überblick über den Workflow, eine Kombination aus einem Journey-Workflow und einem Aktivierungs-Workflow.

Im folgenden Beispiel-Workflow suchen Sie nach Kundinnen und Kunden, die bestimmte Kriterien erfüllen, und Sie möchten sie dazu verleiten, zu Ihrer Website oder Ihrem Programm zurückzukehren. Sie möchten sie auf eine Journey legen, auf der sie anstatt einer begrenzten Aktivität auf Ihrer Eigenschaft häufiger zurückkehren. Sie versuchen, sie zu Ihrer Immobilie zurückzubringen, und dann, wenn sie wieder da sind, lassen Sie sie die Journey eingeben, um wiederkehrende Käufe auf Ihrer Website zu tätigen. Die hier eingerichtete Kampagne ist auf eine Interaktion mit Kunden pro Monat begrenzt.

Sie beginnen, indem Sie Ihrer Audience von Kunden mit hohem und niedrigem Frequenzniveau eine Nachricht senden. Sie überprüfen dann, ob sie diese Nachricht innerhalb der letzten dreißig Tage erhalten haben. Wenn nicht, dann können Sie sie auf eine Journey eingeben, zum Beispiel über ein neues Abonnementprogramm. Anschließend können Sie einige Tage warten (in diesem Beispiel sieben Tage). Nach dieser Zeit können Sie bezahlte Medienanzeigen über Ziele senden, wenn der Kunde das Abonnement, über das Sie ihm eine Nachricht gesendet haben, noch nicht erworben hat. Wenn der Kunde das Abonnement erworben hat, kann er eine Journey mit einer Bestellbestätigung eingeben, wodurch der Anwendungsfall abgeschlossen wird.

>[!IMPORTANT]
>
>Wie weiter unten auf dieser Seite beschrieben, werden durch eine [dedizierte Einverständnis-Feldergruppe in Ihrem ](#customer-attributes-schema) und durch [Implementieren von Einverständnisrichtlinien](#privacy-consent) alle Aktionen und Workflows auf eine Datenschutz- und Einverständnis-First-Weise implementiert.

>[!BEGINSHADEBOX]

![Schritt für Schritt Entwicklung eines einmaligen Werts zu einem Lebenszeitwert Allgemeine visuelle Übersicht.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. Sie erstellen Schemata und Datensätze und markieren diese dann zur [!UICONTROL Profile].
2. Daten werden erfasst und über Web SDK, Mobile Edge SDK oder API in Experience Platform integriert. Analytics Data Connector kann ebenfalls verwendet werden, kann jedoch zu Journey-Latenz führen.
3. Sie laden Profile in Real-Time CDP und erstellen Governance-Richtlinien, um eine verantwortungsvolle Nutzung zu gewährleisten.
4. Sie erstellen zielgerichtete Zielgruppen aus der Liste der Profile, um nach Kundinnen und Kunden mit hohem und niedrigem Frequenzwert zu suchen.
5. Sie erstellen in [!DNL Adobe Journey Optimizer] zwei Journey, von denen einer Benutzern eine Nachricht über ein neues Abonnementprogramm und der andere eine Nachricht zur Bestätigung des Kaufs sendet.
6. Falls gewünscht, aktivieren Sie die Zielgruppe von Kunden, die Ihr Abonnement für die gewünschten Paid-Media-Ziele nicht erworben haben.

>[!ENDSHADEBOX]

## So erreichen Sie den Anwendungsfall {#achieve-use-case-instruction}

Um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht abzuschließen, lesen Sie die folgenden Abschnitte, in denen Links zu weiteren Informationen und detaillierteren Anweisungen enthalten sind.

### Funktionen und Elemente der Benutzeroberfläche, die Sie verwenden werden {#ui-functionality-and-elements}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls abgeschlossen haben, verwenden Sie die Elemente von Real-Time CDP, Adobe Journey Optimizer und Benutzeroberfläche, die am Anfang dieses Dokuments aufgeführt sind. Stellen Sie sicher, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu gewähren.

### Erstellen eines Schemaentwurfs und Festlegen von Feldergruppen {#schema-design}

Experience-Datenmodell (XDM)-Ressourcen werden im [!UICONTROL Schemas] Workspace in [!DNL Adobe Experience Platform] verwaltet. Sie können die von [!DNL Adobe] bereitgestellten Kernressourcen (z. B. [!UICONTROL field groups]) anzeigen und untersuchen sowie benutzerdefinierte Ressourcen und Schemata für Ihr Unternehmen erstellen.

Weitere Informationen zum Erstellen von [Schemata](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) finden Sie im Tutorial [Erstellen von Schemata“](/help/xdm/tutorials/create-schema-ui.md)

Es gibt mehrere Schema-Designs, die Sie in dieser Beispielimplementierung für den Anwendungsfall verwenden können, um den Einmalwert zum Lebenszeitwert zu entwickeln. Jedes Schema enthält bestimmte erforderliche Felder, die eingerichtet werden müssen, und einige vorgeschlagene Felder.

Basierend auf Beispielimplementierungen empfiehlt Adobe, die folgenden drei Schemata zu erstellen, um diesen Anwendungsfall zu erreichen:

* [Kundenattribut-](#customer-attributes-schema) (ein Profilschema)
* [Schema für digitale Transaktionen des Kunden](#customer-digital-transactions-schema) (Schema für Erlebnisereignisse)
* [Offline-Transaktions-Schema des Kunden](#customer-offline-transactions-schema) (Schema für Erlebnisereignisse)

#### Kundenattribut-Schema {#customer-attributes-schema}

Verwenden Sie dieses Schema, um die Profildaten, aus denen Ihre Kundeninformationen bestehen, zu strukturieren und zu referenzieren. Diese Daten werden in der Regel über Ihr CRM-System oder ein ähnliches System in [!DNL Adobe Experience Platform] aufgenommen und sind erforderlich, um auf Kundendetails zu verweisen, die für Personalisierung, Marketing-Zustimmung und erweiterte Segmentierungsfunktionen verwendet werden.

![Kundenattribut-Schema mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Das Kundenattribut-Schema wird durch eine [!UICONTROL XDM Individual Profile]-Klasse dargestellt, die die folgenden Feldergruppen enthält:

+++Demografische Details (Feldergruppe)

[Demografische Details](/help/xdm/field-groups/profile/demographic-details.md) ist eine Standardschemafeldgruppe für die Klasse „XDM Individual Profile“. Die Feldergruppe stellt ein Personenobjekt auf der Stammebene bereit, dessen Unterfelder Informationen über eine einzelne Person beschreiben.

+++

+++Persönliche Kontaktdaten (Feldergruppe)

[Persönliche Kontaktdetails](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse „XDM Individual Profile“, die die Kontaktinformationen für eine einzelne Person beschreibt.

+++

+++Audit-Details des externen Source-Systems (Feldergruppe)

[External Source System Audit Attributes](/help/xdm/data-types/external-source-system-audit-attributes.md) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

+++Einverständnis- und Voreinstellungsfeldgruppen (Feldgruppe)

[Die Feldergruppe „Einverständnis und Voreinstellungen](/help/xdm/field-groups/profile/consents.md) bietet ein einzelnes Feld vom Typ „Einverständnis“, um Einverständnis- und Voreinstellungsinformationen zu erfassen.

+++

#### Schema für digitale Transaktionen des Kunden {#customer-digital-transactions-schema}

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht, die auf Ihrer Website oder auf anderen zugehörigen digitalen Plattformen auftritt. Diese Daten werden in der Regel über [!DNL Adobe Experience Platform]Web SDK[ in ](/help/collection/js/js-overview.md) aufgenommen und sind erforderlich, um auf die verschiedenen Durchsuchen- und Konversionsereignisse zu verweisen, die zum Auslösen von Journey-Ereignissen, einer detaillierten Online-Kundenanalyse und erweiterten Segmentierungsfunktionen verwendet werden.

![Schema für digitale Kundentransaktionen mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Das Schema für digitale Transaktionen des Kunden wird durch eine [!UICONTROL XDM ExperienceEvent]-Klasse dargestellt, die die folgenden Feldergruppen enthält:

+++Adobe Experience Platform Web SDK ExperienceEvent (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `device.model` | Vorgeschlagen |
| `environment.browserDetails.userAgent` | Vorgeschlagen |

+++

+++Web-Details (Feldergruppe)

[Web-Details](/help/xdm/field-groups/event/web-details.md) ist eine Standardschemafeldgruppe für die XDM ExperienceEvent-Klasse, mit der Informationen zu Web-Detailereignissen wie Interaktion, Seitendetails und Referrer beschrieben werden.

+++

+++Consumer Experience-Ereignis (Feldergruppe)

Diese Feldergruppe enthält verschiedene Informationen zu Aktionen, z. B. Kauf- oder Browser-Ereignisse, die von Benutzern in Ihrer Web-Eigenschaft durchgeführt werden.

| Feld | Anforderung |
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

+++Details zur Endbenutzer-ID (Feldergruppe)

Die [Details zur Endbenutzer-ID](/help/xdm/field-groups/event/enduserids.md)-Feldergruppe enthält verschiedene Informationen zu Ihren Benutzern, z. B. ob sie beim Besuch auf Ihrer Site authentifiziert sind und Informationen zu ihrer Identität.

+++

+++Audit-Details des externen Source-Systems (Feldergruppe)

External Source System Audit Attributes ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

#### Offline-Transaktionsschema des Kunden {#customer-offline-transactions-schema}

Dieses Schema wird verwendet, um die Ereignisdaten, aus denen Ihre Kundenaktivität besteht und die auf Plattformen außerhalb Ihrer Website auftreten, zu strukturieren und zu referenzieren. Diese Daten werden normalerweise aus einem POS (oder einem ähnlichen System) in [!DNL Adobe Experience Platform] aufgenommen und meistens über eine API-Verbindung an Experience Platform gestreamt. Weitere Informationen [Batch-Aufnahme](/help/ingestion/batch-ingestion/getting-started.md). Sie dient als Referenz für die verschiedenen Offline-Konversionsereignisse, die zum Auslösen von Journey-Ereignissen, einer umfassenden Online- und Offline-Kundenanalyse und erweiterten Segmentierungsfunktionen verwendet werden.

![Offline-Transaktionsschema des Kunden mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Das Offline-Transaktionsschema des Kunden wird durch eine [!UICONTROL XDM ExperienceEvent]-Klasse dargestellt, die die folgenden Feldergruppen enthält:

+++Commerce-Details (Feldergruppe)

[Commerce Details](/help/xdm/field-groups/event/commerce-details.md) ist eine Standardschemafeldgruppe für die [!DNL XDM ExperienceEvent], die zur Beschreibung von Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßigen Warenkorbvorgängen (Bestellung, Kasse, Abbruch) verwendet wird.

+++

+++Persönliche Kontaktdaten (Feldergruppe)

[[!UICONTROL Personal Contact Details]](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse [!DNL XDM Individual Profile] , die die Kontaktinformationen für eine einzelne Person beschreibt.

+++

+++Audit-Details des externen Source-Systems (Feldergruppe) 

External Source System Audit Attributes ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

#### Adobe Web Connector-Schema {#adobe-web-connector-schema}

>[!NOTE]
>
>Dies ist eine optionale Implementierung, wenn Sie die [!DNL Adobe Analytics Data Connector] verwenden.

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht, die auf Ihrer Website oder auf anderen zugehörigen digitalen Plattformen auftritt. Dieses Schema ähnelt dem Schema für digitale Transaktionen bei Kunden, unterscheidet sich jedoch insofern, als es verwendet werden kann, wenn Web SDK keine Option für die Datenerfassung ist. Daher können Sie dieses Schema verwenden, wenn Sie die [!DNL Adobe Analytics Data Connector] verwenden, um Ihre Online-Daten entweder als primären oder sekundären Datenstrom an [!DNL Adobe Experience Platform] zu senden.

![Adobe Web Connector-Schema mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

Das [!DNL Adobe]-Web-Connector-Schema wird durch eine [!UICONTROL XDM ExperienceEvent]-Klasse dargestellt, die die folgenden Feldergruppen enthält:

+++Adobe Analytics ExperienceEvent-Vorlage (Feldergruppe)

[[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](/help/xdm/field-groups/event/analytics-full-extension.md) ist eine Standardschemafeldgruppe, die allgemeine von Adobe Analytics erfasste Metriken erfasst.

+++

### Erstellen eines Datensatzes aus einem Schema {#dataset-from-schema}

Ein Datensatz ist eine Speicher- und Verwaltungsstruktur für eine Gruppe von Daten. Jedes Schema, das für diese Beispielimplementierung verwendet wird, verfügt über einen einzigen Datensatz.

Weitere Informationen zum Erstellen eines [Datensatzes](/help/catalog/datasets/overview.md) aus einem Schema finden Sie im [Handbuch zur Benutzeroberfläche von Datensätzen](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Ähnlich wie beim Schritt zum Erstellen eines Schemas müssen Sie auch aktivieren, dass der Datensatz in das Echtzeit-Kundenprofil aufgenommen wird. Weitere Informationen zur Aktivierung des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie im Tutorial [Erstellen eines Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Datenschutz, Einverständnis und Data Governance {#privacy-consent}

#### Einverständniserklärungen

>[!IMPORTANT]
>
>Es ist gesetzlich vorgeschrieben, den Kunden die Möglichkeit zu geben, den Erhalt von Mitteilungen einer Marke zu stornieren, und sicherzustellen, dass diese Entscheidung respektiert wird. Weitere Informationen zu den geltenden Rechtsvorschriften finden Sie unter [Übersicht über Datenschutzbestimmungen](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Erwägen Sie die Implementierung der [Einverständnisrichtlinien](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) und bitten Sie Ihre Besucher um Zustimmung, bevor Sie sich an sie wenden:

* Wenn `consents.marketing.email.val = "Y"` dann eine E-Mail senden können
* Wenn `consents.marketing.sms.val = "Y"` dann kann SMS
* Wenn `consents.marketing.push.val = "Y"` dann Push ausführen kann
* Wenn `consents.share.val = "Y"` dann werben können

#### Data Governance-Kennzeichnung und -Durchsetzung

Erwägen Sie das Hinzufügen und Erzwingen der folgenden [Data Governance-Kennzeichnungen](/help/data-governance/labels/overview.md):

* Persönliche E-Mail-Adressen werden als direkt identifizierbare Daten verwendet, die zur Identifizierung oder Kontaktaufnahme mit einer bestimmten Person und nicht mit einem Gerät verwendet werden.
   * `personalEmail.address = I1`

#### Marketing-Richtlinien

Für die Journey[ die Sie im Rahmen ](/help/data-governance/policies/overview.md) Anwendungsfalls erstellen, sind keine „Marketing-Richtlinien“ erforderlich. Sie können jedoch die folgenden Richtlinien bei Bedarf berücksichtigen:

* Einschränken sensibler Daten
* Onsite-Advertising einschränken
* E-Mail-Targeting einschränken
* Site-übergreifendes Targeting einschränken
* Einschränkung der Kombination direkt identifizierbarer Daten mit anonymen Daten

### Erstellen von Zielgruppen {#create-audiences}

In diesem Anwendungsfall müssen Sie zwei Zielgruppen erstellen, um bestimmte Attribute oder Verhaltensweisen zu definieren, die von einer Untergruppe von Profilen aus Ihrem Profilspeicher geteilt werden, um eine vermarktbare Personengruppe zu unterscheiden. Zielgruppen können in Adobe Experience Platform auf verschiedene Weise erstellt werden:

* Informationen zum Erstellen einer Zielgruppe finden Sie im [Handbuch zur Benutzeroberfläche des Zielgruppen-Services](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* Informationen zum Erstellen von [Zielgruppen](/help/segmentation/home.md) finden Sie im [Handbuch zur Benutzeroberfläche für die Zielgruppenkomposition](/help/segmentation/ui/audience-composition.md).
* Informationen zum Erstellen von Zielgruppen mithilfe von aus Experience Platform abgeleiteten Segmentdefinitionen finden Sie im [Handbuch zur Audience Builder-Benutzeroberfläche](/help/segmentation/ui/segment-builder.md).

Insbesondere müssen Sie zwei Zielgruppen in verschiedenen Schritten des Anwendungsfalls erstellen und verwenden, wie in der Abbildung unten dargestellt.

![Zielgruppen hervorgehoben.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Adobe Journey Optimizer Qualifying Audience]

Diese hochwertige und niederfrequente Zielgruppe enthält die Profile, mit denen Sie über einen Journey Kontakt aufnehmen möchten, um ihnen Informationen über ein neues Abonnementprogramm zu geben. Die Details der Zielgruppe finden Sie unten:

* Beschreibung: Profile, die in den letzten 3 Monaten insgesamt mehr als 250 USD ausgegeben haben
* Erforderliche Felder und Bedingungen in der Zielgruppe:
   * Ereignis: `commerce.order.payments.paymentamount`
* Aggregierte Summe: >= $250
   * EventType: `commerce.purchases`
* Zeitstempel: weniger als 3 Monate davor


>[!TAB Paid Media-Zielgruppe]

Diese Zielgruppe wird erstellt, um Profile einzuschließen, die in den letzten 3 Monaten insgesamt mehr als 250 USD ausgegeben haben und in den letzten 7 Tagen keinen Kauf getätigt haben. Die Details der Zielgruppe finden Sie unten:

* Beschreibung: Profile, die in den letzten 3 Monaten insgesamt mehr als 250 USD ausgegeben haben und in den letzten 7 Tagen keinen Kauf getätigt haben.
* Erforderliche Felder und Bedingungen:
   * EventType: `journey.feedback`
      * Operand: = true
   * Ereignis: `experience.journeyOrchestration.stepEvents.nodeName`
      * Operand: = JourneyStepEventTracker - Abonnement nicht erworben
      * Zeitstempel: in den letzten 7 Tagen
   * EventType ist nicht: `commerce.purchases`
      * Zeitstempel: &lt;= 7 Tage davor
   * Ereignis: SKU
      * Wert: = `subscription`

>[!ENDTABS]

### Journey-Setup in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] umfasst nicht alles, was in den Diagrammen angezeigt wird. Alle [Paid Media-Anzeigen](/help/destinations/catalog/social/overview.md) werden im [!UICONTROL destinations]Arbeitsbereich[ erstellt](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) können Sie Ihren Kunden vernetzte, kontextbezogene und personalisierte Erlebnisse bieten. Die Kunden-Journey umfasst den gesamten Prozess der Kundeninteraktion mit der Marke. Für jede Anwendungsfall-Journey sind spezifische Informationen erforderlich.

Für diesen Anwendungsfall müssen Sie zwei separate Journey erstellen:

* Die Lebensdauer-Journey, die die Nachricht enthält, die Sie an Ihre hochwertigen Niederfrequenz-Kunden senden
* Die Journey mit der Bestellbestätigung für die Benutzer, die auf Ihren Anruf antworten und ein Abonnement erwerben.

![Journey hervorgehoben.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

Unten finden Sie die genauen Daten, die für jede Journey-Verzweigung benötigt werden.

>[!BEGINTABS]

>[!TAB Lebensdauer-Journey]

Die Lifetime Journey richtet sich an Kunden mit hohem und niedrigem Frequenzwert, die in den letzten 30 Tagen nicht angesprochen wurden. Diesen Kunden wird eine Nachricht angezeigt und wenn sie nach 7 Tagen immer noch nicht einkaufen, können Sie die Nicht-Käufer in eine Zielgruppe einbeziehen, der Sie bezahlte Medienanzeigen anzeigen können. Wenn sie einen Kauf tätigen, können Sie die Käufer auf einer Auftragsbestätigungs-Journey festlegen, die auf der separaten Registerkarte beschrieben wird.

![Allgemeine visuelle Übersicht über das Lifetime Journey.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "Einmaliger Wert für lebenslanges Journey - Allgemeine visuelle Übersicht."){zoomable="yes"}

+++Detailed Journey Logic

Die oben dargestellte Journey folgt der folgenden Logik.

1. Zielgruppe lesen: Verwenden Sie eine [Aktivität „Zielgruppe lesen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) für die erste Zielgruppe, die im Abschnitt „Zielgruppen“ oben erstellt wurde.

2. Bedingung - Bevorzugter Kanal: Verwenden Sie eine [Bedingungsaktivität](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) um zu bestimmen, wie Sie Kunden erreichen können, ob über E-Mail, SMS oder Push-Benachrichtigungen. Verwenden Sie drei Aktionsaktivitäten, um die drei Verzweigungen zu erstellen.

3. Warten: Verwenden Sie eine [Warteaktivität](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) um zu warten, bis Sie auf Käufe warten.

4. Bedingung - Abonnement in den letzten 7 Tagen erworben?: Verwenden Sie eine Aktivität vom Typ Bedingung , um auf Produktkäufe in den letzten sieben Tagen zu warten.

5. JourneyStepEventTracker - Abonnement nicht erworben: Verwenden Sie eine [benutzerdefinierte Aktion](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) für die Besucher, die Ihr Abonnement noch nicht erworben haben, obwohl sie Ihre Nachricht erhalten haben. Erstellen Sie als Teil der benutzerdefinierten Bedingung am Ende des Journey ein `journey.feedback` und fügen Sie es basierend auf dem [!UICONTROL Journey Step Event] Schema zu einem Datensatz hinzu. Mit diesem Ereignis segmentieren Sie die Zielgruppe, die das Abonnement nicht erworben hat und die Sie über Paid-Media-Anzeigen ansprechen können.

+++

>[!TAB Journey zur Bestellbestätigung]

Die Journey zur Bestellbestätigung konzentriert sich darauf, ob ein Kauf über die Website oder die Mobile App getätigt wurde. Nachdem ein Kunde den Kauf z. B. eines Abonnements für Ihr Unternehmen erfolgreich abgeschlossen hat, können Sie diese auf einer Journey mit einer Bestellbestätigung festlegen.

![Kundenauftragsbestätigungs-Journey Allgemeine visuelle Übersicht.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "Kundenauftragsbestätigungs-Journey Allgemeine visuelle Übersicht."){zoomable="yes"}

+++Journey Logic

Verwenden Sie die unten vorgeschlagenen Ereignisse, Felder und Aktionen auf Ihrer Bestätigungs-Journey:

* Die Journey wird durch ein Online-Kaufereignis ausgelöst
   * Schema: Digitale Kundentransaktionen
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

+++Key Journey Logic

* Journey-Eingabelogik
   * Bestellungsereignis

* Bedingungen
   * Wählen Sie den Zielkanal aus (Sie können einen oder mehrere Kanäle für eine größere Reichweite auswählen).
      * Die Bestellbestätigung gilt als Dienstleistung in der Natur, sodass eine Einverständnisprüfung in der Regel nicht erforderlich ist.
      * E-Mail
      * Push-Benachrichtigung
      * SMS

   * Kanalinhalt Personalization
      * Zeigen Sie Informationen zu Bestelldetails an und können Sie eine Liste von Produkten mithilfe eines Tabellenformats anzeigen.

+++

>[!ENDTABS]

Weitere Informationen zum Erstellen von Journey in [!DNL Adobe Journey Optimizer] finden Sie im Handbuch [Erste Schritte mit Journey](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Einrichten eines Ziels für die Anzeige von Paid Media-Anzeigen {#paid-media-ads}

Einige Benutzer haben Ihr Abonnement möglicherweise nicht erworben, selbst nachdem Sie ihnen über das neue Programm eine Nachricht gesendet haben. Nachdem Sie einige Tage gewartet haben (in diesem Anwendungsbeispiel sieben), können Sie entscheiden, diesen Benutzern bezahlte Medienanzeigen anzuzeigen, um sie zum Kauf Ihres Abonnements zu ermutigen.

Verwenden Sie das Ziel-Framework in Real-Time CDP für Paid-Media-Anzeigen. Wählen Sie eines der vielen verfügbaren Werbeziele aus, um Ihren Kunden Paid-Media-Anzeigen anzuzeigen und die Paid-Media-Zielgruppe, die Sie [zuvor erstellt](#create-audiences) für ein Ziel Ihrer Wahl zu aktivieren. Hier finden Sie eine Übersicht über verfügbare [Werbung](/help/destinations/catalog/advertising/overview.md) und [Social](/help/destinations/catalog/social/overview.md)-Ziele.

Informationen zum Aktivieren von Daten für Ziele (z. B. [The Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) oder [Google Customer Match](/help/destinations/catalog/advertising/google-customer-match.md)) finden Sie in der folgenden Dokumentation:

* [Erstellen einer neuen Zielverbindung](/help/destinations/ui/connect-destination.md)
* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Nächste Schritte {#next-steps}

Indem Sie Ihre niederfrequenten und hochwertigen Anwender auf eine Journey setzen und einer Untergruppe von ihnen Paid-Media-Anzeigen anzeigen, haben Sie hoffentlich einige von ihnen von Kunden mit einmaligem Wert zu Kunden mit lebenslangem Wert gemacht und so Ihre Markentreue und Kundeninteraktionsmetriken verbessert.

Als Nächstes können Sie sich mit anderen von Real-Time CDP unterstützten Anwendungsfällen beschäftigen, z. B. [Kunden intelligent wieder mit ](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) zu interagieren oder [nicht authentifizierten Benutzern personalisierte Inhalte ](/help/rtcdp/partner-data/onsite-personalization.md) Ihren Web-Eigenschaften anzuzeigen.
