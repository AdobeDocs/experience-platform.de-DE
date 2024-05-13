---
title: einmaligen Kundenwert auf Lebenszeitwert erhöhen
description: Erfahren Sie, wie Sie personalisierte Kampagnen erstellen, um basierend auf den Attributen, dem Verhalten und früheren Käufen eines bestimmten Kunden die besten ergänzenden Produkte oder Dienste anzubieten.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: 2f1008791a35f33a0379cba14b90334aebf83187
workflow-type: tm+mt
source-wordcount: '3179'
ht-degree: 2%

---

# einmaligen Kundenwert auf Lebenszeitwert erhöhen

>[!IMPORTANT]
> 
>* Auf dieser Seite finden Sie eine Beispielimplementierung von Real-Time CDP und Adobe Journey Optimizer, um den beschriebenen Anwendungsfall zu erreichen. Verwenden Sie die Zahlen, Qualifikationskriterien und andere Felder auf der Seite als Anleitung, nicht als Zahlenangaben.
>* Um dieses Anwendungsbeispiel abzuschließen, müssen Sie eine Lizenz für Real-Time CDP und Adobe Journey Optimizer besitzen. Weitere Informationen finden Sie unter [Voraussetzungen und Planungsabschnitt](#prerequisites-and-planning) weiter unten.

Implementieren Sie den einmaligen Kundenwert in das Nutzungsszenario für den Lebenszeitwert, um die Markeninteraktion und die Markentreue zu fördern. Erstellen Sie ein vernetztes Kundenerlebnis auf mehreren Kanälen oder Journey, indem Sie die Leistungsfähigkeit von Experience Platform nutzen, ergänzt durch [Real-Time CDP](/help/rtcdp/home.md) und [Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home).

Die Personen, die Sie als Ziel auswählen, sind die seltenen Besucher Ihrer Eigenschaften, die in den letzten drei Monaten einige Käufe getätigt haben.

Betrachten Sie diese Kunden, die Ihre Eigenschaften besuchen und sporadisch die von Ihnen angebotenen Produkte oder Services erwerben. Sie können personalisierte Kampagnen erstellen, um diese Kunden anzusprechen, sodass Ihre Marke ihnen anstelle eines einmaligen Wertes einen längeren Wert anbieten kann. Erfahren Sie mehr über:

* Datenerfassung und -verwaltung
* Erstellen von Zielgruppen
* Erstellen Sie Journey, um diese Zielgruppen in Adobe Journey Optimizer anzusprechen und in Real-Time CDP zu aktivieren.

![Schritt für Schritt Einmalige Wertentwicklung für Lebenszeitwert - Überblick auf hoher Ebene.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){width="500" zoomable="yes"}

## Voraussetzungen und Planung {#prerequisites-and-planning}

Beachten Sie, dass Sie intern ein Geschäftsziel und Ziel definiert haben, um die Markentreue zu steigern. Dies kann in der Ausführung eines Anwendungsfalls zur Förderung der Kundeninteraktion und -loyalität münden.

Dazu besteht die erforderliche Technologie aus den beiden Experience Platform-Apps [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=de). Nachfolgend sind verschiedene Funktionen und Benutzeroberflächenelemente der beiden Apps aufgeführt, die Sie bei der Implementierung des Anwendungsfalls verwenden werden.

>[!TIP]
>
>Vergewissern Sie sich, dass Sie die notwendigen [Attribut-basierten Zugriffsrechte](/help/access-control/abac/end-to-end-guide.md) für alle diese Bereiche haben, oder bitten Sie Ihre Systemadmins, Ihnen die notwendigen Rechte zu erteilen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html): Integrieren Sie Daten aus verschiedenen Datenquellen, um die Kampagne zu unterstützen. Diese Daten werden dann verwendet, um die Kampagnenzielgruppen zu erstellen und personalisierte Datenelemente zu unterteilen, die in der E-Mail und in den Kacheln der Web-Promo verwendet werden (z. B. Name oder kontobezogene Informationen). Schließlich wird Real-Time CDP auch verwendet, um Zielgruppen für Paid-Media-Ziele zu aktivieren.
   * [Schemata](/help/xdm/home.md)
   * [Profile](/help/profile/home.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
   * [Zielgruppen](/help/segmentation/home.md)
   * [Ziele](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html): Entwerfen Sie Journey, richten Sie Trigger ein und erstellen Sie die richtige Nachricht, um Ihre Besucher anzusprechen.
   * [Ereignis- oder Audience Trigger](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=de)
   * [Zielgruppen und Ereignisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=de)
   * [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Architektur von Real-Time CDP und Journey Optimizer

Nachstehend finden Sie eine allgemeine Architekturansicht der verschiedenen Komponenten von Real-Time CDP und Journey Optimizer. Dieses Diagramm zeigt, wie Daten durch die beiden Experience Platform-Apps von der Datenerfassung bis zu dem Punkt fließen, an dem sie durch Journey oder Kampagnen aktiviert werden, zu Zielen, um den auf dieser Seite beschriebenen Anwendungsfall zu erreichen.

![Überblick über die Architektur auf hoher Ebene.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){width="600" zoomable="yes"}

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

Nachfolgend finden Sie eine allgemeine Übersicht über den Workflow, eine Kombination aus einem Journey-Workflow und einem Aktivierungs-Workflow.

Im unten abgebildeten Beispiel-Workflow suchen Sie nach Kunden, die bestimmte Kriterien erfüllen, und möchten sie dazu veranlassen, zu Ihrer Website oder App zurückzukehren. Sie möchten sie auf einer Journey festlegen, auf der sie statt einer eingeschränkten Aktivität in Ihrer Eigenschaft wiederkehrender zurückgegeben werden. Sie versuchen, sie zurück in Ihre Eigenschaft zu bringen und lassen sie dann, sobald sie wieder da sind, die Journey eingeben, um wiederkehrende Käufe auf Ihrer Site durchzuführen. Die hier eingerichtete Kampagne ist auf eine Interaktion mit Kunden pro Monat begrenzt.

Sie beginnen damit, Ihrer Audience von Kunden mit hohem und niedrigem Wert eine Nachricht zu senden. Dann überprüfen Sie, ob sie diese Nachricht innerhalb der letzten dreißig Tage erhalten haben. Ist dies nicht der Fall, können Sie sie in eine Journey eingeben, z. B. über ein neues Abonnement-Programm. Sie können dann einige Tage warten (in diesem Beispiel sieben Tage). Danach können Sie Paid-Media-Anzeigen über Ziele senden, wenn sie das Abonnement, über das Sie ihnen kommuniziert haben, nicht gekauft haben. Wenn der Kunde das Abonnement erworben hat, kann er eine Journey zur Bestellbestätigung eingeben lassen und so den Anwendungsfall abschließen.

>[!IMPORTANT]
>
>Wie weiter unten auf dieser Seite beschrieben, durch eine [dedizierte Einwilligungsfeldgruppe in Ihrem Schema](#customer-attributes-schema) und [Implementieren von Zustimmungsrichtlinien](#privacy-consent)festgelegt ist, werden alle Aktionen und Workflows in einer Weise implementiert, die dem Datenschutz und der Zustimmung dient.

>[!BEGINSHADEBOX]

![Schritt für Schritt Einmalige Wertentwicklung für Lebenszeitwert - Überblick auf hoher Ebene.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){width="600" zoomable="yes"}

1. Sie erstellen Schemata und Datensätze und markieren diese dann für [!UICONTROL Profil].
2. Daten werden über das Web SDK, das Mobile Edge SDK oder die API erfasst und in Experience Platform integriert. Analytics Data Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie laden Profile in Real-Time CDP und erstellen Governance-Richtlinien, um eine verantwortungsvolle Nutzung sicherzustellen.
4. Sie erstellen zielgerichtete Zielgruppen aus der Profilliste, um nach Kunden mit hohen und niedrigen Werten zu suchen.
5. Sie erstellen zwei Journey in [!DNL Adobe Journey Optimizer], um Benutzer über ein neues Abonnement-Programm zu informieren, und um ihnen eine Mitteilung zur Bestätigung des Kaufs zu machen.
6. Bei Bedarf aktivieren Sie die Zielgruppe der Kunden, die Ihr Abonnement für die gewünschten Paid-Media-Ziele nicht erworben haben.

>[!ENDSHADEBOX]

## Anwendungsfall {#achieve-use-case-instruction}

Um die einzelnen Schritte in der obigen allgemeinen Übersicht auszuführen, lesen Sie die folgenden Abschnitte durch, die Links zu weiteren Informationen und detaillierteren Anweisungen enthalten.

### Funktionen und Elemente der Benutzeroberfläche, die Sie verwenden werden {#ui-functionality-and-elements}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, verwenden Sie die am Anfang dieses Dokuments aufgelisteten Elemente für Real-Time CDP, Adobe Journey Optimizer und Benutzeroberfläche. Vergewissern Sie sich, dass Sie über die erforderlichen attributbasierten Zugriffssteuerungsberechtigungen für alle diese Bereiche verfügen, oder bitten Sie Ihren Systemadministrator, Ihnen die erforderlichen Berechtigungen zu erteilen.

### Erstellen eines Schemaentwurfs und Angeben von Feldergruppen {#schema-design}

Ressourcen des Experience-Datenmodells (XDM) werden im [!UICONTROL Schemas] Arbeitsbereich in [!DNL Adobe Experience Platform]. Sie können die wichtigsten Ressourcen, die von bereitgestellt werden, anzeigen und untersuchen. [!DNL Adobe] (zum Beispiel: [!UICONTROL Feldergruppen]) und erstellen Sie benutzerdefinierte Ressourcen und Schemata für Ihre Organisation.

Weitere Informationen zur Erstellung von [Schemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de), lesen Sie die [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md)

Es gibt mehrere Schemaentwürfe, die Sie in dieser Beispielimplementierung für den Anwendungsfall verwenden können, um einen einmaligen Wert zu einem Lebenszeitwert zu entwickeln. Jedes Schema enthält spezifische erforderliche Felder, die eingerichtet werden müssen, sowie einige Felder, die vorgeschlagen werden.

Basierend auf Beispielimplementierungen empfiehlt Adobe, die folgenden drei Schemas zu erstellen, um diesen Anwendungsfall zu erreichen:

* [Schema für Kundenattribute](#customer-attributes-schema) (ein Profilschema)
* [Schema für digitale Transaktionen des Kunden](#customer-digital-transactions-schema) (ein Erlebnisereignisschema)
* [Schema für Offline-Transaktionen des Kunden](#customer-offline-transactions-schema) (ein Erlebnisereignisschema)

#### Schema für Kundenattribute {#customer-attributes-schema}

Verwenden Sie dieses Schema, um die Profildaten zu strukturieren und zu referenzieren, aus denen Ihre Kundeninformationen bestehen. Diese Daten werden normalerweise in [!DNL Adobe Experience Platform] über Ihr CRM-System oder ein ähnliches System und ist erforderlich, um auf Kundendetails zu verweisen, die für Personalisierung, Marketing-Zustimmung und erweiterte Segmentierungsfunktionen verwendet werden.

![Schema für Kundenattribute mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Das Kundenattribut-Schema wird durch eine [!UICONTROL Individuelles XDM-Profil] -Klasse, die die folgenden Feldergruppen enthält:

+++Demografische Details (Feldergruppe)

[Demografische Details](/help/xdm/field-groups/profile/demographic-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;. Die Feldergruppe stellt ein Personenobjekt der Stammebene bereit, dessen Unterfelder Informationen über eine Person beschreiben.

+++

+++Persönliche Kontaktdetails (Feldergruppe)

[Persönliche Kontaktangaben](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;, die die Kontaktinformationen für eine Person beschreibt.

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

[Audit-Attribute des externen Quellsystems](/help/xdm/data-types/external-source-system-audit-attributes.md) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

+++Einverständnis- und Präferenzfeldgruppen (Feldergruppe)

[Einverständnis und Voreinstellungen](/help/xdm/field-groups/profile/consents.md) Feldergruppe bietet ein einzelnes Objekt-Feld, die Zustimmung, um Zustimmungs- und Präferenzinformationen zu erfassen.

+++

#### Schema für digitale Transaktionen des Kunden {#customer-digital-transactions-schema}

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht, die auf Ihrer Website oder auf anderen zugehörigen digitalen Plattformen auftreten. Diese Daten werden normalerweise in [!DNL Adobe Experience Platform] via [Web SDK](/help/web-sdk/home.md) und ist erforderlich, um auf die verschiedenen Durchsuchen- und Konversionsereignisse zu verweisen, die zum Auslösen von Journey, zur detaillierten Online-Kundenanalyse und zu erweiterten Segmentierungsfunktionen verwendet werden.

![Schema für digitale Transaktionen des Kunden mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Das Schema für digitale Transaktionen des Kunden wird durch eine [!UICONTROL XDM ExperienceEvent] -Klasse, die die folgenden Feldergruppen enthält:

+ + + Adobe Experience Platform Web SDK ExperienceEvent (Feldergruppe)

| Felder | Anforderung |
| --- | --- |
| `device.model` | Vorgeschlagen |
| `environment.browserDetails.userAgent` | Vorgeschlagen |

+++

+++Webdetails (Feldergruppe)

[Webdetails](/help/xdm/field-groups/event/web-details.md) ist eine Standardschemafeldgruppe für die XDM ExperienceEvent-Klasse, die zur Beschreibung von Informationen zu Webdetailereignissen wie Interaktion, Seitendetails und Referrer verwendet wird.

+++

+++Consumer Experience-Ereignis (Feldergruppe)

Diese Feldergruppe enthält verschiedene Informationen zu Aktionen, z. B. zu Kauf- oder Browsing-Ereignissen, die von Benutzern in Ihrer Web-Eigenschaft ausgeführt werden.

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

+ + + Endbenutzer-ID-Details (Feldergruppe)

Die [Details zur Endbenutzer-ID](/help/xdm/field-groups/event/enduserids.md) Feldergruppe enthält verschiedene Informationen über Ihre Benutzer, z. B. ob sie beim Besuch auf Ihrer Site authentifiziert sind, und Informationen über ihre Identität.

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

#### Schema für Offline-Transaktionen des Kunden {#customer-offline-transactions-schema}

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht, die auf Plattformen außerhalb Ihrer Website auftreten. Diese Daten werden normalerweise in [!DNL Adobe Experience Platform] von einem POS (oder einem ähnlichen System) und meist über eine API-Verbindung in Platform gestreamt werden. Informationen [Batch-Erfassung](/help/ingestion/batch-ingestion/getting-started.md). Ihr Zweck besteht darin, auf die verschiedenen Offline-Konversionsereignisse zu verweisen, die zum Auslösen von Journey verwendet werden, sowie auf eine tiefe Online- und Offline-Kundenanalyse und erweiterte Segmentierungsfunktionen.

![Schema für Offline-Transaktionen des Kunden mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Das Schema der Offline-Transaktionen des Kunden wird durch eine [!UICONTROL XDM ExperienceEvent] -Klasse, die die folgenden Feldergruppen enthält:

+ + + Commerce Details (Feldergruppe)

[Commerce-Details](/help/xdm/field-groups/event/commerce-details.md) ist eine Standardschemafeldgruppe für die [!DNL XDM ExperienceEvent] -Klasse, die zur Beschreibung von Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßigen Warenkorbvorgängen (Bestellung, Checkout, Abbruch) verwendet wird.

+++

+++Persönliche Kontaktdetails (Feldergruppe)

[[!UICONTROL Persönliche Kontaktangaben]](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die [!DNL XDM Individual Profile] -Klasse, die die Kontaktinformationen für eine Person beschreibt.

+++

+ + + externe Details zur Überprüfung des Quellsystems (Feldergruppe)

Externe Quell-System-Audit-Attribute sind ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

#### Adobe-Web-Connector-Schema {#adobe-web-connector-schema}

>[!NOTE]
>
>Dies ist eine optionale Implementierung, wenn Sie die [!DNL Adobe Analytics Data Connector].

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht, die auf Ihrer Website oder auf anderen zugehörigen digitalen Plattformen auftreten. Dieses Schema ähnelt dem Schema Customer Digital Transactions , unterscheidet sich jedoch dadurch, dass es verwendet werden kann, wenn das Web SDK keine Option für die Datenerfassung ist. Daher können Sie dieses Schema verwenden, wenn Sie die [!DNL Adobe Analytics Data Connector] senden Sie Ihre Online-Daten an [!DNL Adobe Experience Platform] entweder als primären oder sekundären Datastream.

![Adobe des Web-Connector-Schemas mit hervorgehobenen Feldergruppen](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

Die [!DNL Adobe] Web-Connector-Schema durch eine [!UICONTROL XDM ExperienceEvent] -Klasse, die die folgenden Feldergruppen enthält:

+ + + Adobe Analytics ExperienceEvent-Vorlage (Feldergruppe)

[[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](/help/xdm/field-groups/event/analytics-full-extension.md) ist eine Standardschemafeldgruppe, die allgemeine Metriken erfasst, die von Adobe Analytics erfasst werden.

+++

### Datensatz aus einem Schema erstellen {#dataset-from-schema}

Ein Datensatz ist eine Speicher- und Verwaltungsstruktur für eine Datengruppe. Jedes Schema, das zur Durchführung dieser Beispielimplementierung verwendet wird, verfügt über einen einzigen Datensatz.

Weitere Informationen zum Erstellen einer [Datensatz](/help/catalog/datasets/overview.md) aus einem Schema lesen Sie die [Handbuch zur Benutzeroberfläche von Datensätzen](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Ähnlich wie beim Schritt zum Erstellen eines Schemas müssen Sie die Aufnahme des Datensatzes in das Echtzeit-Kundenprofil aktivieren. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie in der [Tutorial zum Erstellen von Schemas.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Datenschutz, Einverständniserklärung und Data Governance {#privacy-consent}

#### Einverständniserklärungen

>[!IMPORTANT]
>
>Es ist gesetzlich vorgeschrieben, Kunden die Möglichkeit zu geben, sich vom Erhalt von Nachrichten einer Marke abzumelden und sicherzustellen, dass diese Entscheidung respektiert wird. Weitere Informationen zu den geltenden Rechtsvorschriften finden Sie im Abschnitt [Übersicht über Datenschutzbestimmungen](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Erwägen Sie die Implementierung der folgenden [Einverständnisrichtlinien](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) und Ihre Besucher um Zustimmung bitten, bevor Sie sie kontaktieren:

* Wenn `consents.marketing.email.val = "Y"` then Can Email
* Wenn `consents.marketing.sms.val = "Y"` then Can SMS
* Wenn `consents.marketing.push.val = "Y"` then Can Push
* Wenn `consents.share.val = "Y"` dann kann Werbung

#### Bezeichnung und Durchsetzung von Data Governance

Erwägen Sie das Hinzufügen und Erzwingen folgender Elemente [Data Governance-Beschriftungen](/help/data-governance/labels/overview.md):

* Persönliche E-Mail-Adressen werden als direkt identifizierbare Daten verwendet, mit denen eine bestimmte Person und nicht ein Gerät identifiziert oder in Kontakt mit ihr gelangen kann.
   * `personalEmail.address = I1`

#### Marketing-Richtlinien

Es gibt keine [Marketing-Richtlinien](/help/data-governance/policies/overview.md) erforderlich für die Journey, die Sie im Rahmen dieses Anwendungsbeispiels erstellen. Sie können jedoch die folgenden Richtlinien nach Bedarf berücksichtigen:

* Einschränken vertraulicher Daten
* Einschränken der Onsite-Werbung
* E-Mail-Targeting einschränken
* Site-übergreifendes Targeting einschränken
* Beschränkung der Kombination direkt identifizierbarer Daten mit anonymen Daten

### Erstellen von Zielgruppen {#create-audiences}

Für diesen Anwendungsfall müssen Sie zwei Zielgruppen erstellen, um bestimmte Attribute oder Verhaltensweisen zu definieren, die von einer Untergruppe von Profilen aus Ihrem Profilspeicher gemeinsam genutzt werden, um eine vermarktbare Personengruppe zu unterscheiden. Zielgruppen können in Adobe Experience Platform auf unterschiedliche Weise erstellt werden:

* Informationen zum Erstellen einer Zielgruppe finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche von Audience Service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* Informationen zum Erstellen von [Zielgruppen](/help/segmentation/home.md), lesen Sie die [Handbuch zur Benutzeroberfläche für Zielgruppenkomposition](/help/segmentation/ui/audience-composition.md).
* Informationen zum Erstellen von Zielgruppen mithilfe von Platform-abgeleiteten Segmentdefinitionen finden Sie in der [Handbuch zur Benutzeroberfläche von Audience Builder](/help/segmentation/ui/segment-builder.md).

Insbesondere müssen Sie zwei Zielgruppen in verschiedenen Schritten des Anwendungsbeispiels erstellen und verwenden, wie in der Abbildung unten dargestellt.

![Zielgruppen hervorgehoben.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){width="600" zoomable="yes"}

>[!BEGINTABS]

>[!TAB Adobe Journey Optimizer Qualification Audience]

Diese hochwertige und niederfrequente Audience enthält die Profile, die Sie über eine Journey erreichen möchten, um sie über ein neues Abonnement-Programm zu informieren. Die Details der Zielgruppe finden Sie unten:

* Beschreibung: Profile, die in den letzten drei Monaten insgesamt mehr als 250 USD ausgegeben haben
* Felder und Bedingungen, die in der Audience benötigt werden:
   * Ereignis: `commerce.order.payments.paymentamount`
* Aggregatsumme: >= 250 USD
   * EventType: `commerce.purchases`
* Zeitstempel: weniger als 3 Monate vor jetzt


>[!TAB Paid Media-Zielgruppe]

Diese Zielgruppe wird erstellt, um Profile einzuschließen, die in den letzten drei Monaten insgesamt mehr als 250 USD ausgegeben haben und in den letzten sieben Tagen keinen Kauf getätigt haben. Die Details der Zielgruppe finden Sie unten:

* Beschreibung: Profile, die in den letzten drei Monaten insgesamt mehr als 250 USD ausgegeben haben und in den letzten sieben Tagen keinen Kauf getätigt haben.
* Erforderliche Felder und Bedingungen:
   * EventType: `journey.feedback`
      * Operand: = true
   * Ereignis: `experience.journeyOrchestration.stepEvents.nodeName`
      * Operand: = JourneyStepEventTracker - Subscription not Purchased
      * Zeitstempel: in den letzten 7 Tagen
   * EventType ist nicht: `commerce.purchases`
      * Zeitstempel: &lt;= 7 Tage vor jetzt
   * Ereignis: SKU
      * Wert: = `subscription`

>[!ENDTABS]

### Journey-Setup in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] umfasst nicht alles, was in den Diagrammen angezeigt wird. Alle [Paid Media-Anzeigen](/help/destinations/catalog/social/overview.md) werden im [!UICONTROL Ziele] [Arbeitsbereich](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) hilft Ihnen, Ihren Kunden verknüpfte, kontextbezogene und personalisierte Erlebnisse bereitzustellen. Die Journey ist der gesamte Vorgang der Interaktion eines Kunden mit der Marke. Für jede Journey von Anwendungsfällen sind spezifische Informationen erforderlich.

Um dieses Anwendungsbeispiel zu erstellen, müssen Sie zwei separate Journey erstellen:

* Die Journey zur Lebensdauer, die die Nachricht enthält, die Sie an Ihre Kunden mit hoher und niedriger Häufigkeit senden
* Die Journey zur Bestellbestätigung für die Benutzer, die auf Ihren Anruf antworten und ein Abonnement erwerben.

![Journey hervorgehoben.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){width="600" zoomable="yes"}

Im Folgenden finden Sie die genauen Daten, die für jede Journey-Verzweigung benötigt werden.

>[!BEGINTABS]

>[!TAB Lifetime Journey]

Die Journey zur Lebensdauer richtet sich an die Zielgruppe von Kunden mit hoher und niedriger Häufigkeit, die in den letzten 30 Tagen nicht angesprochen wurden. Diesen Kunden wird eine Nachricht angezeigt. Wenn sie nach 7 Tagen immer noch nicht kaufen, können Sie die Nicht-Käufer in eine Zielgruppe aufnehmen, der Sie Paid-Media-Anzeigen zeigen können. Wenn der Käufer einen Kauf tätigt, können Sie die Käufer auf eine Journey zur Bestellbestätigung setzen, die im separaten Tab beschrieben wird.

![Journey - Überblick über die Lebensdauer](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "Einmaliger Wert für das Journey auf Lebensdauer - Überblick auf hoher Ebene."){width="600" zoomable="yes"}

+++Detaillierte Journey-Logik

Die oben dargestellte Journey folgt der folgenden Logik.

1. Audience lesen: Verwenden Sie eine [Lesen der Zielgruppenaktivität](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) für die erste Audience, die im obigen Abschnitt &quot;Audiences&quot;erstellt wurde.

2. Bedingung - Bevorzugter Kanal: Verwenden Sie einen [Bedingungsaktivität](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) um zu bestimmen, wie Kunden erreicht werden können, sei es über E-Mail-, SMS- oder Push-Benachrichtigungen. Verwenden Sie drei Aktionsaktivitäten, um die drei Verzweigungen zu erstellen.

3. Warten: Verwenden Sie eine [Warteaktivität](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) , um zu warten, bis Sie auf Käufe warten.

4. Bedingung - Kauf Abonnement in den letzten 7 Tagen?: Verwenden Sie eine Bedingungsaktivität, um auf Produktkäufe in den letzten sieben Tagen zu warten.

5. JourneyStepEventTracker - Subscription not Purchased: Use a [benutzerdefinierte Aktion](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) für die Besucher, die Ihr Abonnement noch nicht erworben haben, obwohl sie Ihre Nachricht erhalten haben. Erstellen Sie als Teil der benutzerdefinierten Bedingung am Ende von Journey eine `journey.feedback` -Ereignis ein und fügen Sie es zu einem Datensatz hinzu, der auf der [!UICONTROL Journey-Schrittereignis] Schema. Mit diesem Ereignis segmentieren Sie die Zielgruppe, die das Abonnement nicht erworben hat und die Sie über Paid-Media-Anzeigen ansprechen können.

+++

>[!TAB Journey zur Bestellbestätigung]

Die Journey zur Bestellbestätigung konzentriert sich darauf, ob ein Kauf über die Website oder mobile App getätigt wurde. Nachdem ein Kunde beispielsweise den Kauf eines Abonnements bei Ihrem Unternehmen erfolgreich abgeschlossen hat, können Sie ihn auf einer Journey zur Bestellbestätigung festlegen.

![Kundenauftragsbestätigung Journey - Allgemeine visuelle Übersicht.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "Kundenauftragsbestätigung Journey - Allgemeine visuelle Übersicht."){width="600" zoomable="yes"}

++ + Journey-Logik

Verwenden Sie die folgenden vorgeschlagenen Ereignisse, Felder und Aktionen in Ihrer Bestätigungs-Journey:

* Die Journey wird durch ein Online-Kaufereignis ausgelöst
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
   * Wählen Sie Zielkanal aus (Sie können einen oder mehrere Kanäle für eine größere Reichweite auswählen).
      * Eine Bestellbestätigung gilt als Serving in der Natur, daher ist eine Zustimmungsprüfung in der Regel nicht erforderlich.
      * E-Mail
      * Push-Benachrichtigung
      * SMS

   * Personalisierung von Kanalinhalten
      * Zeigen Sie Bestelldetails an und können eine Liste von Produkten im Tabellenformat anzeigen.

+++

>[!ENDTABS]

Weitere Informationen zum Erstellen von Journey finden Sie unter [!DNL Adobe Journey Optimizer], lesen Sie die [Erste Schritte mit Journey](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) Handbuch.

### Einrichten eines Ziels zur Anzeige von Paid-Media-Anzeigen {#paid-media-ads}

Einige Benutzer haben Ihr Abonnement möglicherweise nicht erworben, selbst wenn Sie ihnen das neue Programm mitgeteilt haben. Nachdem Sie einige Tage gewartet haben (in diesem Anwendungsbeispiel sieben Tage), können Sie diesen Benutzern Paid-Media-Anzeigen zeigen, um sie zum Kauf Ihres Abonnements zu ermutigen.

Verwenden Sie das Ziel-Framework in Real-Time CDP für Paid-Media-Anzeigen. Wählen Sie eines der vielen verfügbaren Werbeziele aus, um Ihren Kunden Paid-Media-Anzeigen anzuzeigen und die gebührenpflichtige Medienzielgruppe zu aktivieren. [früher erstellt](#create-audiences) an ein Ziel Ihrer Wahl. Eine Übersicht der verfügbaren [Werbung](/help/destinations/catalog/advertising/overview.md) und [social](/help/destinations/catalog/social/overview.md) Ziele.

Informationen zum Aktivieren von Daten für Ziele (z. B. [Handelsabteilung](/help/destinations/catalog/advertising/tradedesk.md) oder [Google-Kundenabgleich](/help/destinations/catalog/advertising/google-customer-match.md)), lesen Sie die folgende Dokumentation:

* [Erstellen einer neuen Zielverbindung](/help/destinations/ui/connect-destination.md)
* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Nächste Schritte {#next-steps}

Indem Sie Ihre Benutzer mit geringer Häufigkeit und hoher Wertschöpfung auf einer Journey festlegen und Paid-Media-Anzeigen einer Untergruppe davon anzeigen, haben Sie hoffentlich einige davon von Kunden mit einmaliger Wertermittlung auf Lebenszeitwert umgestellt und so Ihre Markentreue und Kundeninteraktionsmetriken verbessert.

Als Nächstes können Sie weitere von Real-Time CDP unterstützte Anwendungsfälle untersuchen, z. B. [intelligente Wiederaufnahme der Kundenbindung](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) oder [Anzeigen personalisierter Inhalte für nicht authentifizierte Benutzer](/help/rtcdp/partner-data/onsite-personalization.md) in Ihren Web-Eigenschaften.
