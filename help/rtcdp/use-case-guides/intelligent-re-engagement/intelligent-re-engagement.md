---
title: Intelligente Rückgewinnung
description: Stellen Sie während der wichtigsten Konversionsmomente überzeugende und vernetzte Erlebnisse bereit, um unregelmäßige Kundinnen und Kunden auf intelligente Weise erneut anzusprechen.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '3871'
ht-degree: 4%

---

# Intelligentes erneutes Ansprechen, um Kundinnen und Kunden zur Rückkehr zu bewegen

>[!NOTE]
>
>Dies ist eine Beispielimplementierung, und die Beispiele auf dieser Seite, wie Segmentsyntax, sind nur Beispiele. Verwenden Sie die Beispiele als Anleitung, da Ihre Implementierung unterschiedlich sein kann.

Binden Sie Kunden, die eine Konversion abgebrochen haben, wieder auf intelligente und verantwortungsvolle Weise ein. Kontaktieren Sie abgelaufene Kundinnen und Kunden mit Erlebnissen, um die Konversionsrate zu erhöhen und den Kundenlebenszeitwert zu erhöhen.

Überlegungen in Echtzeit anstellen, alle Verbraucherqualitäten und -verhaltensweisen berücksichtigen und eine schnelle Neuqualifizierung auf der Grundlage von Online- und Offline-Ereignissen bieten.

Nachfolgend finden Sie eine allgemeine Architekturansicht der verschiedenen Komponenten von Real-Time CDP und Journey Optimizer. Dieses Diagramm zeigt, wie Daten durch die beiden Experience Platform-Apps von der Datenerfassung bis zu dem Punkt fließen, an dem sie über Journey oder Kampagnen für Ziele aktiviert werden, um den auf dieser Seite beschriebenen Anwendungsfall zu erreichen.

![Intelligentes Re-Engagement - Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/step-by-step.png)

## Anwendungsfall - Übersicht {#overview}

Während Sie Beispiele für Rückgewinnungsszenarien durcharbeiten, erstellen Sie Schemata, Datensätze und Zielgruppen. Außerdem erfahren Sie, welche Funktionen zum Einrichten der Beispiel-Journey in [!DNL Adobe Journey Optimizer] und welche zum Erstellen von Paid-Media-Anzeigen in Zielen erforderlich sind. In diesem Handbuch werden Beispiele für die erneute Interaktion mit Kundinnen und Kunden in den unten beschriebenen Anwendungsfall-Journey verwendet:

* **Szenario zum Abbruch der Produktsuche** - Targeting von Kunden, die das Durchsuchen von Produkten sowohl auf der Website als auch in der Mobile App abgebrochen haben.
* **Szenario „Warenkorbabbruch** - Targeting von Kunden, die Produkte in den Warenkorb gelegt haben, aber noch nicht sowohl auf der Website als auch in der Mobile App gekauft wurden.
* **Szenario zur Bestellbestätigung** - Konzentrieren Sie sich auf Produktkäufe, die über die Website und die Mobile App getätigt werden.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, nutzen Sie die folgenden Funktionen von Real-Time CDP und Adobe Journey Optimizer (aufgeführt in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie die notwendigen [Attribut-basierten Zugriffsrechte](/help/access-control/home.md) für alle diese Bereiche haben, oder bitten Sie Ihre Systemadmins, Ihnen die notwendigen Rechte zu erteilen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Integriert Daten in alle Datenquellen, um die Kampagne zu unterstützen. Diese Daten werden dann verwendet, um die Kampagnen-Audiences zu erstellen und die in der E-Mail und den Web-Promo-Kacheln verwendeten personalisierten Datenelemente (z. B. Name oder kontobezogene Informationen) aufzudecken. Die CDP wird auch verwendet, um Zielgruppen in E-Mails und im Internet zu aktivieren (über [!DNL Adobe Target]).
   * [Schemata](/help/xdm/home.md)
   * [Profile](/help/profile/home.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
   * [Zielgruppen](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Ziele](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=de) - Hilft Ihnen, Ihren Kunden vernetzte, kontextbezogene und personalisierte Erlebnisse bereitzustellen.
   * [Ereignis- oder Zielgruppen-Trigger &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Zielgruppen/ Ereignisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=de)
   * [Journey-Aktionen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## So erreichen Sie den Anwendungsfall {#achieve-use-case-instruction}

Im Folgenden finden Sie einen allgemeinen Überblick über die drei Beispielszenarien für die Rückgewinnung von Kontakten.

>[!BEGINTABS]

>[!TAB Szenario mit abgebrochener Produktsuche]

Das Szenario zum Durchsuchen abgebrochener Produkte zielt auf das Durchsuchen abgebrochener Produkte sowohl auf der Website als auch in der mobilen App ab. Dieses Szenario wird ausgelöst, wenn ein Produkt angesehen, aber nicht gekauft oder zum Warenkorb hinzugefügt wurde. In diesem Beispiel wird die Interaktion mit einer Marke nach drei Tagen ausgelöst, wenn innerhalb der letzten 24 Stunden keine zusätzlichen Listen vorhanden sind.<p>![Kunden-Szenario mit intelligentem Produktabbruch - Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/re-engagement-journey.png "Kundenspezifisches Szenario für die Suche nach verworfenen Produkten - Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemata und Datensätze und aktivieren sie dann für [!UICONTROL Profile].
2. Sie nehmen Daten über Web SDK, Mobile SDK oder API in Experience Platform auf. Analytics Source Connector kann ebenfalls verwendet werden, kann jedoch zu Journey-Latenz führen.
3. Sie nehmen zusätzliche profilaktivierte Daten auf, die über Identitätsdiagramme mit dem authentifizierten Web- und Mobile-App-Besucher verknüpft werden können.
4. Sie erstellen zielgerichtete Zielgruppen aus der Liste der Profile, um zu überprüfen **ob ein** in den letzten drei Tagen eine Interaktion abgeschlossen hat.
5. Sie erstellen in [!DNL Adobe Journey Optimizer] eine Journey zur Produktsuche, die nicht mehr verwendet wird.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** zusammen, um Zielgruppen für die gewünschten Paid-Media-Ziele zu aktivieren.
7. [!DNL Adobe Journey Optimizer] sucht nach Einverständnis und sendet die verschiedenen konfigurierten Aktionen.

>[!TAB Szenario mit Transaktionsabbruch]

Das Szenario „Transaktionsabbruch“ gilt, wenn Produkte in den Warenkorb gelegt, aber noch nicht sowohl auf der Website als auch in der Mobile App gekauft wurden. Außerdem werden Kampagnen mit bezahlten Medien mit dieser Methode gestartet und gestoppt.<p>![Szenario mit abgebrochenem Warenkorb - Allgemeine visuelle Übersicht](../intelligent-re-engagement/images/abandoned-cart-journey.png "Szenario mit abgebrochenem Warenkorb - Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

1. Wenn Sie Schemata und Datensätze erstellen, aktivieren Sie für [!UICONTROL Profile].
2. Sie nehmen Daten über Web SDK, Mobile SDK oder API in Experience Platform auf. Analytics Source Connector kann ebenfalls verwendet werden, kann jedoch zu Journey-Latenz führen.
3. Sie nehmen zusätzliche profilaktivierte Daten auf, die über Identitätsdiagramme mit dem authentifizierten Web- und Mobile-App-Besucher verknüpft werden können.
4. Sie erstellen zielgerichtete Zielgruppen aus der Liste der Profile, um zu überprüfen, ob ein **Kunde** einen Artikel in seinen Warenkorb gelegt, den Kauf jedoch nicht abgeschlossen hat. Das **[!UICONTROL Add to cart]**-Ereignis startet einen Timer, der 30 Minuten wartet und dann auf den Kauf prüft. Wenn kein Kauf getätigt wurde, wird der **Kunde** zu den **[!UICONTROL Abandon Cart]** Zielgruppen hinzugefügt.
5. Sie erstellen eine Journey aus einem Transaktionsabbruch in [!DNL Adobe Journey Optimizer].
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** zusammen, um Zielgruppen für die gewünschten Paid-Media-Ziele zu aktivieren.
7. [!DNL Adobe Journey Optimizer] sucht nach Einverständnis und sendet die verschiedenen konfigurierten Aktionen.

>[!TAB Szenario zur Bestellbestätigung]

Das Szenario der Bestellbestätigung konzentriert sich auf Produktkäufe, die über die Website und die Mobile App getätigt werden.<p>![Kundenbestellungsbestätigungsszenario Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Szenario mit Bestätigung von Kundenaufträgen - Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemata und Datensätze und aktivieren sie dann für [!UICONTROL Profile].
2. Sie nehmen Daten über Web SDK, Mobile SDK oder API in Experience Platform auf. Analytics Source Connector kann ebenfalls verwendet werden, kann jedoch zu Journey-Latenz führen.
3. Sie nehmen zusätzliche profilaktivierte Daten auf, die über Identitätsdiagramme mit dem authentifizierten Web- und Mobile-App-Besucher verknüpft werden können.
4. Sie erstellen eine Bestätigungs-Journey in [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] sendet eine Bestätigungsnachricht über den bevorzugten Kanal.

>[!ENDTABS]

Um die einzelnen Schritte in den oben stehenden allgemeinen Übersichten abzuschließen, lesen Sie die folgenden Abschnitte, in denen Links zu weiteren Informationen und detaillierteren Anweisungen enthalten sind.

### Erstellen von Schemata und Festlegen von Feldergruppen {#schema-design}

Experience-Datenmodell (XDM)-Ressourcen werden im [!UICONTROL Schemas] Workspace in [!DNL Adobe Experience Platform] verwaltet. Sie können die von [!DNL Adobe] bereitgestellten Kernressourcen (z. B. Feldgruppen) anzeigen und untersuchen sowie benutzerdefinierte Ressourcen und Schemata für Ihr Unternehmen erstellen.

Weitere Informationen zum Erstellen von [Schemata](/help/xdm/home.md) finden Sie im Tutorial [Erstellen eines Schemas“.](/help/xdm/tutorials/create-schema-ui.md) und [Modellieren von Kundenerlebnisdaten mit XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Es gibt vier Schema-Designs, die für den Anwendungsfall zur erneuten Interaktion verwendet werden. Für jedes Schema müssen bestimmte Felder eingerichtet werden. Sie müssen das Schema aktivieren, damit es in das Echtzeit-Kundenprofil aufgenommen werden kann. Weitere Informationen zur Aktivierung des Schemas für die Verwendung im Echtzeit-Kundenprofil finden Sie unter [Aktivieren eines Schemas für das Echtzeit-Kundenprofil](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Kundenattribut-Schema

Dieses Schema wird verwendet, um die Profildaten, aus denen Ihre Kundeninformationen bestehen, zu strukturieren und zu referenzieren. Diese Daten werden in der Regel über Ihr CRM-System oder ein ähnliches System in [!DNL Adobe Experience Platform] aufgenommen und sind erforderlich, um auf Kundendetails zu verweisen, die für Personalisierung, Marketing-Einverständnis und erweiterte Zielgruppenfunktionen verwendet werden.

Das Kundenattribut-Schema wird durch eine [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md)-Klasse dargestellt, die die folgenden Feldergruppen enthält:

+++Persönliche Kontaktdaten (Feldergruppe)

[Persönliche Kontaktdetails](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse „XDM Individual Profile“, die die Kontaktinformationen für eine einzelne Person beschreibt.

| Felder | Beschreibung |
| --- | --- |
| `mobilePhone.number` | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| `personalEmail.address` | Die E-Mail-Adresse der Person. |

+++

+++Audit-Details des externen Source-Systems (Feldergruppe)

[External Source System Audit Attributes](/help/xdm/data-types/external-source-system-audit-attributes.md) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

+++Einverständnis- und Voreinstellungsfeldgruppen (Feldgruppe)

Die [Einverständnis und Voreinstellungen](/help/xdm/field-groups//profile/consents.md) bietet ein einzelnes Feld vom Typ „Einverständnis“, um Einverständnis- und Voreinstellungsinformationen zu erfassen.

| Felder | Anforderung |
| --- | --- |
| `consents.marketing.email.val` | Erforderlich |
| `consents.marketing.preferred` | Erforderlich |
| `consents.marketing.push.val` | Erforderlich |
| `consents.marketing.sms.val` | Erforderlich |
| `consents.personalize.content.val` | Erforderlich |
| `consents.share.val` | Erforderlich |

+++

+++Details zum Profiltest (Feldergruppe)

Mit dieser Feldergruppe können Sie Ihren Journey vor der Veröffentlichung mithilfe von Testprofilen testen. Weitere Informationen zum Erstellen von Testprofilen finden Sie im Tutorial [Erstellen von Testprofilen](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html) und [Testen des Journey-](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/testing-the-journey.html?lang=de).

+++

#### Schema für digitale Transaktionen des Kunden

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität auf Ihrer Website oder auf zugehörigen digitalen Plattformen besteht. Diese Daten werden in der Regel über [!DNL Adobe Experience Platform]Web SDK[&#x200B; in &#x200B;](/help/web-sdk/home.md) aufgenommen und sind erforderlich, um auf die verschiedenen Durchsuchen- und Konversionsereignisse zu verweisen, die zum Auslösen von Journey, zur detaillierten Online-Kundenanalyse, zu erweiterten Zielgruppenfunktionen und zum personalisierten Messaging verwendet werden.

Das Schema für digitale Transaktionen des Kunden wird durch eine [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md)-Klasse dargestellt.

+++XDM ExperienceEvent (Klasse)

Die [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md)-Klasse umfasst die folgenden Feldergruppen:

| Felder | Beschreibung |
| --- | --- |
| `_id` | identifiziert einzelne Ereignisse, die in [!DNL Adobe Experience Platform] aufgenommen werden, eindeutig. |
| `timestamp` | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß RFC 3339 Abschnitt 5.6. Dieser Zeitstempel muss in der Vergangenheit liegen. |
| `eventType` | Eine Zeichenfolge, die den Kategorietyp für das Ereignis angibt. |

+++

+++Details zur Endbenutzer-ID (Feldergruppe)

Die [Details zur Endbenutzer-](/help/xdm/field-groups/event/enduserids.md)) wird verwendet, um die Identitätsinformationen einer Person in mehreren Adobe-Programmen zu beschreiben.

| Felder | Beschreibung |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.id` | Endbenutzer-E-Mail-Adressen-ID. |
| `endUserIDs._experience.emailid.namespace.code` | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] Authentifizierungsstatus der Marketing Cloud ID (MCID). Die ECID wird jetzt als Experience Cloud ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud ID (MCID). Die ECID wird jetzt als Experience Cloud ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] Namespace-Code der Marketing Cloud-ID (MCID). |

+++

+++Commerce-Details (Feldergruppe)

Die Feldergruppe [Commerce-Details](/help/xdm/field-groups/event/commerce-details.md) wird verwendet, um Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßige Warenkorbvorgänge (Bestellung, Kasse, Abbruch) zu beschreiben.

| Felder | Beschreibung |
| --- | --- |
| `commerce.cart.cartID` | Eine ID für den Warenkorb. |
| `commerce.order.orderType` | Ein Objekt, das den Produktbestelltyp beschreibt. |
| `commerce.order.payments.paymentAmount` | Ein Objekt, das den Zahlungsbetrag der Produktbestellung beschreibt. |
| `commerce.order.payments.paymentType` | Ein Objekt, das den Zahlungstyp für Produktbestellungen beschreibt. |
| `commerce.order.payments.transactionID` | Eine Objektproduktauftragstransaktions-ID. |
| `commerce.order.purchaseID` | Eine Objektproduktbestellungs-Kauf-ID. |
| `productListItems.name` | Eine Liste von Elementnamen, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.priceTotal` | Der Gesamtpreis der Liste der Artikel, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.product` | Die ausgewählten Produkte. |
| `productListItems.quantity` | Die Menge der Liste der Artikel, die die von einem Kunden ausgewählten Produkte darstellen. |

+++

+++Audit-Details des externen Source-Systems (Feldergruppe)

External Source System Audit Attributes ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

#### Offline-Transaktionsschema des Kunden

Dieses Schema wird verwendet, um die Ereignisdaten, aus denen Ihre Kundenaktivität besteht und die auf Plattformen außerhalb Ihrer Website auftreten, zu strukturieren und zu referenzieren. Diese Daten werden normalerweise aus einem POS (oder einem ähnlichen System) in [!DNL Adobe Experience Platform] aufgenommen und meistens über eine API-Verbindung an Experience Platform gestreamt. Sie dient als Referenz für die verschiedenen Offline-Konversionsereignisse, die zum Auslösen von Journey-Analysen, einer umfassenden Online- und Offline-Kundenanalyse, erweiterten Zielgruppenfunktionen und personalisiertem Messaging verwendet werden.

Das Offline-Transaktionsschema des Kunden wird durch eine [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md)-Klasse dargestellt.

+++XDM ExperienceEvent (Klasse)

Die [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md)-Klasse umfasst die folgenden Feldergruppen:

| Felder | Beschreibung |
| --- | --- |
| `_id` | identifiziert einzelne Ereignisse, die in [!DNL Adobe Experience Platform] aufgenommen werden, eindeutig. |
| `timestamp` | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß RFC 3339 Abschnitt 5.6. Dieser Zeitstempel muss in der Vergangenheit liegen. |
| `eventType` | Eine Zeichenfolge, die den Kategorietyp für das Ereignis angibt. |

+++

+++Commerce-Details (Feldergruppe)

Die Feldergruppe [Commerce-Details](/help/xdm/field-groups/event/commerce-details.md) wird verwendet, um Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßige Warenkorbvorgänge (Bestellung, Kasse, Abbruch) zu beschreiben.

| Felder | Beschreibung |
| --- | --- |
| `commerce.cart.cartID` | Eine ID für den Warenkorb. |
| `commerce.order.orderType` | Ein Objekt, das den Produktbestelltyp beschreibt. |
| `commerce.order.payments.paymentAmount` | Ein Objekt, das den Zahlungsbetrag der Produktbestellung beschreibt. |
| `commerce.order.payments.paymentType` | Ein Objekt, das den Zahlungstyp für Produktbestellungen beschreibt. |
| `commerce.order.payments.transactionID` | Eine Objektproduktauftragstransaktions-ID. |
| `commerce.order.purchaseID` | Eine Objektproduktbestellungs-Kauf-ID. |
| `productListItems.name` | Eine Liste von Elementnamen, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.priceTotal` | Der Gesamtpreis der Liste der Artikel, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.product` | Die ausgewählten Produkte. |
| `productListItems.quantity` | Die Menge der Liste der Artikel, die die von einem Kunden ausgewählten Produkte darstellen. |

+++

+++Persönliche Kontaktdaten (Feldergruppe)

[Persönliche Kontaktdetails](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse „XDM Individual Profile“, die die Kontaktinformationen für eine einzelne Person beschreibt.

| Felder | Beschreibung |
| --- | --- |
| `mobilePhone.number` | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| `personalEmail.address` | Die E-Mail-Adresse der Person. |

+++

+++Audit-Details des externen Source-Systems (Feldergruppe) 

External Source System Audit Attributes ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

#### Adobe Web Connector-Schema

>[!NOTE]
>
>Dies ist eine optionale Implementierung, wenn Sie die [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md) verwenden.

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität auf Ihrer Website oder auf zugehörigen digitalen Plattformen besteht. Dieses Schema ähnelt dem Schema für digitale Transaktionen bei Kunden, unterscheidet sich jedoch insofern, als es verwendet werden soll, wenn [Web SDK](/help/web-sdk/home.md) keine Option für die Datenerfassung ist. Daher wird dieses Schema benötigt, wenn Sie die [!DNL Adobe Analytics Source Connector] verwenden, um Ihre Online-Daten entweder als primären oder sekundären Datenstrom an [!DNL Adobe Experience Platform] zu senden.

Das [!DNL Adobe] Web-Connector-Schema wird durch eine [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md)-Klasse dargestellt.

+++XDM ExperienceEvent (Klasse)

Die [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md)-Klasse umfasst die folgenden Feldergruppen:

| Felder | Beschreibung |
| --- | --- |
| `_id` | identifiziert einzelne Ereignisse, die in [!DNL Adobe Experience Platform] aufgenommen werden, eindeutig. |
| `timestamp` | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß RFC 3339 Abschnitt 5.6. Dieser Zeitstempel muss in der Vergangenheit liegen. |
| `eventType` | Eine Zeichenfolge, die den Kategorietyp für das Ereignis angibt. |

+++

+++Adobe Analytics ExperienceEvent-Vorlage (Feldergruppe)

Die Feldergruppe [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) erfasst allgemeine Metriken, die von Adobe Analytics erfasst werden.

| Felder | Beschreibung |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.id` | Endbenutzer-E-Mail-Adressen-ID. |
| `endUserIDs._experience.emailid.namespace.code` | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] Authentifizierungsstatus der Marketing Cloud ID (MCID). Die ECID wird jetzt als Experience Cloud ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud ID (MCID). Die ECID wird jetzt als Experience Cloud ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] Namespace-Code der Marketing Cloud-ID (MCID). |

+++

+++Audit-Details des externen Source-Systems (Feldergruppe)

External Source System Audit Attributes ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Audit-Details über ein externes Quellsystem erfasst.

+++

### Erstellen eines Datensatzes aus einem Schema {#create-datasets}

Ein Datensatz ist eine Speicher- und Verwaltungsstruktur für eine Gruppe von Daten. Jedes Schema für Szenarien zur intelligenten erneuten Interaktion sollte über einen eigenen Datensatz verfügen.

Weitere Informationen zum Erstellen eines [Datensatzes](/help/catalog/datasets/overview.md) aus einem Schema finden Sie im [Handbuch zur Benutzeroberfläche von Datensätzen](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Ähnlich wie beim Schritt zum Erstellen eines Schemas müssen Sie auch aktivieren, dass der Datensatz in das Echtzeit-Kundenprofil aufgenommen wird. Weitere Informationen zur Aktivierung des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie im Tutorial [Einbringen von Daten in das Echtzeit-Kundenprofil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=de).

### Einverständnis und Data Governance {#privacy-consent}

>[!IMPORTANT]
>
>Es ist gesetzlich vorgeschrieben, den Kunden die Möglichkeit zu geben, den Erhalt von Mitteilungen einer Marke zu stornieren, und sicherzustellen, dass diese Entscheidung respektiert wird. Weitere Informationen zu den geltenden Rechtsvorschriften finden Sie unter [Übersicht über Datenschutzbestimmungen](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

#### Einverständniserklärungen

Erwägen Sie beim Erstellen eines Rückgewinnungspfads das Hinzufügen der folgenden [Einverständnisrichtlinien](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html):

* Wenn `consents.marketing.email.val = "Y"` dann eine E-Mail senden können
* Wenn `consents.marketing.sms.val = "Y"` dann kann SMS
* Wenn `consents.marketing.push.val = "Y"` dann Push ausführen kann
* Wenn `consents.share.val = "Y"` dann werben können

#### Data Governance-Kennzeichnung und -Durchsetzung

Erwägen Sie beim Erstellen eines Rückgewinnungspfads das Hinzufügen der folgenden [Data Governance-Kennzeichnungen](/help/data-governance/labels/overview.md):

* Personenbezogene E-Mail-Adressen werden als direkt identifizierbare Daten verwendet, die zur Identifizierung oder Kontaktaufnahme mit einer bestimmten Person und nicht mit einem Gerät verwendet werden.
   * `personalEmail.address = I1`

#### Datennutzungsrichtlinien

Für [&#x200B; Szenario mit abgebrochener Produktsuche sind keine &#x200B;](/help/data-governance/policies/overview.md)Datennutzungsrichtlinien“ erforderlich. Beachten Sie jedoch Folgendes:

* Einschränken sensibler Daten
* Onsite-Advertising einschränken
* E-Mail-Targeting einschränken
* Site-übergreifendes Targeting einschränken
* Einschränkung der Kombination direkt identifizierbarer Daten mit anonymen Daten

### Erstellen von Zielgruppen {#create-audience}

Die Rückgewinnungsszenarien verwenden Zielgruppen, um bestimmte Attribute oder Verhaltensweisen zu definieren, die von einer Untergruppe von Profilen aus Ihrem Profilspeicher geteilt werden, um eine vermarktbare Personengruppe aus Ihrem Kundenstamm zu unterscheiden. Zielgruppen können in [!DNL Adobe Experience Platform] auf verschiedene Weise erstellt werden.

Weitere Informationen zum Erstellen einer Zielgruppe finden Sie im [Handbuch zur Zielgruppen-Service-Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Weitere Informationen zum direkten Erstellen von [Zielgruppen](/help/segmentation/home.md) finden Sie im [Handbuch zur Benutzeroberfläche für die Zielgruppenkomposition](/help/segmentation/ui/audience-composition.md).

Weitere Informationen zum Erstellen von Zielgruppen mithilfe von aus Experience Platform abgeleiteten Zielgruppendefinitionen finden Sie im [Handbuch für die Audience Builder-Benutzeroberfläche](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Szenario mit abgebrochener Produktsuche]

Diese Zielgruppe wird als Erweiterung des klassischen Szenarios „Warenkorbabbruch“ erstellt. Während sich der Warenkorbabbruch in der Regel auf einen Zusatz zum Warenkorb ohne nachfolgenden Kauf in einem bestimmten Zeitraum konzentriert, sucht diese Zielgruppe nach einem früheren Interaktion, insbesondere nach denjenigen, die ein bestimmtes Produkt besucht haben, es jedoch nicht zum Warenkorb hinzugefügt haben und innerhalb eines bestimmten Zeitraums keine Folgeaktivität auf Ihrer Site hatten. Diese Zielgruppe hilft dabei, Ihre Marke für Kunden, die diese Einschlusskriterien erfüllen, „am besten zu verstehen“ und kann auch für Kunden genutzt werden, deren digitale Eigenschaften sich von einem herkömmlichen E-Commerce-Modell unterscheiden können.

+++Abgebrochene Produktansicht ohne Interaktion in den letzten drei Tagen

Das folgende Ereignis wird für das Szenario zum Durchsuchen abgebrochener Produkte verwendet, in dem Benutzer Produkte online angesehen und in den 3 Tagen danach nicht interagiert haben (Site-Besuche, App-Besuche, Online-Kauf, Offline-Kauf und Ereignisse zum Hinzufügen zum Warenkorb).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Zielgruppe erforderlich:

* `eventType: commerce.productViews`
* Und `THEN` (sequenzielles Ereignis) schließen `eventType: commerce.productListAdds` UND `application.launch` UND `web.webpagedetails.pageViews` UND `commerce.purchases` aus (dies umfasst sowohl online als auch offline)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`

+++

+++Produktansicht mit Interaktion in den letzten drei Tagen

Das folgende Ereignis wird für das Szenario zum Durchsuchen abgebrochener Produkte verwendet, in dem Benutzer Produkte online angesehen und in den 3 Tagen danach interagiert haben (Site-Besuche, App-Besuche, Online-Kauf, Offline-Kauf und Ereignisse zum Warenkorb hinzufügen).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Zielgruppe erforderlich:

* `eventType: commerce.productViews`
* Und `THEN` (sequenzielles Ereignis) umfassen `eventType: commerce.productListAdds` ODER `application.launch` ODER `web.webpagedetails.pageViews` ODER `commerce.purchases` (dies umfasst sowohl online als auch offline)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`
+++

+++Interaktions-Streaming in den letzten Tagen

Das folgende Ereignis wird für das Szenario zum Durchsuchen abgebrochener Produkte verwendet, bei dem sich Benutzende in den letzten 1 Tag engagiert haben (Site-Besuche, App-Besuche, Online-Kauf, Offline-Kauf und Ereignisse zum Warenkorb hinzufügen).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Zielgruppe erforderlich:

* `eventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 1 day` (Streaming)

+++

+++Interaktions-Batch in den letzten drei Tagen

Das folgende Ereignis wird für das Szenario zum Durchsuchen abgebrochener Produkte verwendet, bei dem sich Benutzende in den letzten 3 Tagen engagiert haben (Site-Besuche, App-Besuche, Online-Kauf, Offline-Kauf und Ereignisse zum Warenkorb hinzufügen).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Zielgruppe erforderlich:

* `EventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 3 days` (Stapel)

+++

>[!TAB Szenario mit Transaktionsabbruch]

Diese Zielgruppe wird erstellt, um das klassische Szenario „Warenkorbabbruch“ zu unterstützen. Sie dient dazu, Kunden zu finden, die ein Produkt in ihren Warenkorb gelegt haben, es aber letztendlich nicht durch einen Kauf umgesetzt haben. Diese Zielgruppe wird nicht nur dazu beitragen, dass Ihre Marke für Ihre Kunden „auf dem Laufenden bleibt“, sondern auch die Produkte, die sie ohne einen späteren Kauf zurückgelassen haben.

Die folgenden Ereignisse werden für das Szenario „Warenkorbabbruch“ verwendet, in dem Benutzer vor 1 bis 4 Tagen ein Produkt zum Warenkorb hinzugefügt, den Kauf jedoch nicht abgeschlossen oder den Warenkorb nicht geleert haben.

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Zielgruppe erforderlich:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now AND <= 4 days before now`
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

Der Deskriptor für das Szenario „Transaktionsabbruch“ wird wie folgt angezeigt:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Szenario zur Bestellbestätigung]

Auf dieser Journey müssen keine Zielgruppen erstellt werden.

>[!ENDTABS]

### Journey-Setup in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] umfasst nicht alles, was in den Diagrammen angezeigt wird. Alle [Paid Media-Anzeigen](/help/destinations/catalog/social/overview.md) werden in [!UICONTROL Destinations] erstellt.

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) können Sie Ihren Kunden vernetzte, kontextbezogene und personalisierte Erlebnisse bieten. Die Kunden-Journey umfasst den gesamten Prozess der Kundeninteraktion mit der Marke. Für jede Anwendungsfall-Journey sind spezifische Informationen erforderlich. Unten finden Sie die genauen Daten, die für jede Journey benötigt werden.

>[!BEGINTABS]

>[!TAB Szenario mit abgebrochener Produktsuche]

Das Szenario zum Durchsuchen abgebrochener Produkte zielt auf das Durchsuchen abgebrochener Produkte sowohl auf der Website als auch in der mobilen App ab.<p>![Vom Kunden aufgegebenes Szenario zur Produktsuche Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/re-engagement-journey.png "Szenario zur Produktsuche durch Kunden aufgegeben Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

+++Ereignisse

Mit Hilfe von Ereignissen können Sie Ihre Journeys einheitlich auslösen, um Nachrichten in Echtzeit an die Kontakte zu senden, die in die Journey eintreten. Weitere Informationen zu Ereignissen finden Sie im [Handbuch zu allgemeinen Ereignissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Ereignis 1: Produktansichten
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType = commerce.productViews`
      * Felder:
         * `eventType`
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

* Ereignis 2: Zum Warenkorb hinzufügen
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType = commerce.productListAdds`
      * Felder:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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

* Veranstaltung 3: Markeninteraktion
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

+++Journey Canvas-Schlüssellogik

Die Schlüssellogik der Journey-Arbeitsfläche erfordert es, bestimmte Ereignisse zu identifizieren und Aktionen zu konfigurieren, die nach dem Eintreten des Ereignisses stattfinden sollen.

* Journey-Eingabelogik
   * Produktansichtsereignis

* Bedingungen
   * Suchen Sie nach mindestens einem Online- oder Offline-Kaufereignis seit der letzten Anzeige des Produkts.
      * Schema: Digitale Kundentransaktionen
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Suchen Sie nach mindestens einem Offline-Kauf seit der letzten Anzeige des Produkts:
      * Schema: Offline-Transaktionen von Kunden
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Bedingungen - Wählen Sie den Zielkanal aus
      * E-Mail
         * `consents.marketing.email.val = y`
      * Push-Benachrichtigung
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Channel Personalization
      * Personalisierte Kanalinhalte basierend auf der Produktansicht.

+++

>[!TAB Szenario mit Transaktionsabbruch]

Das Szenario „Transaktionsabbruch“ zielt auf Produkte ab, die in den Warenkorb gelegt, aber noch nicht sowohl auf der Website als auch in der Mobile App gekauft wurden.<p>![Szenario mit abgebrochenem Warenkorb - Allgemeine visuelle Übersicht](../intelligent-re-engagement/images/abandoned-cart-journey.png "Szenario mit abgebrochenem Warenkorb - Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

+++Ereignisse

Mit Hilfe von Ereignissen können Sie Ihre Journeys einheitlich auslösen, um Nachrichten in Echtzeit an die Kontakte zu senden, die in die Journey eintreten. Weitere Informationen zu Ereignissen finden Sie im [Handbuch zu allgemeinen Ereignissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Ereignis 2: Zum Warenkorb hinzufügen
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType = commerce.productListAdds`
      * Felder:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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

* Event 4: Online-Käufe
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType = commerce.purchases`
      * Felder:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

* Veranstaltung 3: Markeninteraktion
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

+++Journey Canvas-Schlüssellogik

Die Schlüssellogik der Journey-Arbeitsfläche erfordert es, bestimmte Ereignisse zu identifizieren und Aktionen zu konfigurieren, die nach dem Eintreten des Ereignisses stattfinden sollen.

* Journey-Eingabelogik
   * `AddToCart`

* AuthenticatedState in Authenticated

* Bedingung: Offline-Käufe seit dem letzten Abbruch des Warenkorbs:
   * Schema: Offline-Transaktionen von Kunden
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Bedingung: Der Warenkorb wurde geleert, da der Warenkorb zuletzt verlassen wurde:
   * Schema: Digitale Kundentransaktionen
   * `eventType = commerce.cartCleared`
   * `cartID` (ID des Warenkorbs)
   * `timestamp > timestamp of cart was last abandoned`

* Zielkanal auswählen (einen oder mehrere Kanäle für eine breitere Reichweite auswählen)
   * E-Mail
      * `consents.marketing.email.val = y`
   * Push-Benachrichtigung
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Channel Personalization
      * Zeigen Sie Informationen zu Warenkorbdetails an und können mehrere Produkte in einem Tabellenformat anzeigen.

+++

>[!TAB Szenario zur Bestellbestätigung]

Das Szenario der Bestellbestätigung konzentriert sich auf Produktkäufe, die über die Website und die Mobile App getätigt werden.<p>![Kundenbestellungsbestätigungsszenario Allgemeine visuelle Übersicht.](../intelligent-re-engagement/images/order-confirmation-journey.png "Szenario mit Bestätigung von Kundenaufträgen - Allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

+++Ereignisse

Mit Hilfe von Ereignissen können Sie Ihre Journeys einheitlich auslösen, um Nachrichten in Echtzeit an die Kontakte zu senden, die in die Journey eintreten. Weitere Informationen zu Ereignissen finden Sie im [Handbuch zu allgemeinen Ereignissen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Event 4: Online-Käufe
   * Schema: Digitale Kundentransaktionen
   * Felder:
      * `eventType`
   * Bedingung:
      * `eventType = commerce.purchases`
      * Felder:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

+++Journey Canvas-Schlüssellogik

Die Schlüssellogik der Journey-Arbeitsfläche erfordert es, bestimmte Ereignisse zu identifizieren und Aktionen zu konfigurieren, die nach dem Eintreten des Ereignisses stattfinden sollen.

* Journey-Eingabelogik
   * Bestellungsereignis

* Bedingungen
   * Zielkanal auswählen (einen oder mehrere Kanäle für eine breitere Reichweite auswählen).
      * Die Bestellbestätigung gilt als Dienstleistung in der Natur, sodass eine Einverständnisprüfung in der Regel nicht erforderlich ist.
      * E-Mail
      * Push-Benachrichtigung
      * SMS

   * Kanalinhalt Personalization
      * Zeigen Sie Informationen zu Bestelldetails an und können Sie eine Liste von Produkten mithilfe eines Tabellenformats anzeigen.

+++

>[!ENDTABS]

Weitere Informationen zum Erstellen von Journey in [!DNL Adobe Journey Optimizer] finden Sie im Handbuch [Erste Schritte mit Journey](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Einrichten von Paid Media-Anzeigen in Zielen {#paid-media-ads}

Das Ziel-Framework wird für Paid-Media-Anzeigen verwendet. Nachdem das Einverständnis geprüft wurde, wird es an die verschiedenen konfigurierten Ziele gesendet. Weitere Informationen zu Zielen finden Sie im Dokument [Ziele - Übersicht](/help/destinations/home.md).

#### Für Ziele erforderliche Daten

Exportziele für Streaming-Zielgruppen (z. B. Facebook, Google Customer Match, Google DV360) unterstützen verschiedene Identitäten aus Kundendaten:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Sie können Zielgruppen für abgebrochene Produkte aktivieren und Zielgruppen für bezahlte Medienanzeigen aus dem Warenkorb entfernen.

* Stream/Ausgelöst
   * [Advertising](/help/destinations/catalog/advertising/overview.md)/[Bezahlte Medien und Social Media](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming-Ziel](/help/destinations/catalog/streaming/http-destination.md)
   * [Benutzerdefiniertes Ziel, erstellt mithilfe von Destination SDK.](/help/destinations/destination-sdk/overview.md). Wenn Sie Real-Time CDP Ultimate-Kunde sind, können Sie auch ein privates (benutzerdefiniertes[&#x200B; Ziel mit Destination SDK erstellen](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)

## Nächste Schritte {#next-steps}

Indem Sie Ihre Kunden, die eine Konversion abgebrochen haben, wieder auf intelligente und verantwortungsvolle Weise angesprochen haben, haben Sie hoffentlich die Konversionen erhöht und den Kundenlebenszeitwert erhöht.

Als Nächstes können Sie sich mit anderen von Real-Time CDP unterstützten Anwendungsfällen beschäftigen, z. B. [Anzeigen personalisierter Inhalte für nicht authentifizierte Benutzende](/help/rtcdp/partner-data/onsite-personalization.md) in Ihren Web-Eigenschaften.
