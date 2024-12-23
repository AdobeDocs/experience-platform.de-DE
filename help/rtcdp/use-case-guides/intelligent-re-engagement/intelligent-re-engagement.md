---
title: Intelligente Erneute Interaktion
description: Stellen Sie während der wichtigsten Konversionsmomente überzeugende und vernetzte Erlebnisse bereit, um unregelmäßige Kundinnen und Kunden auf intelligente Weise erneut anzusprechen.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3894'
ht-degree: 4%

---

# Intelligentes erneutes Ansprechen, um Kundinnen und Kunden zur Rückkehr zu bewegen

>[!NOTE]
>
>Dies ist eine Beispielimplementierung, und die Beispiele auf dieser Seite, wie z. B. die Segmentsyntax, sind lediglich Beispiele. Sie sollten die Beispiele als Anleitung verwenden, da Ihre Implementierung unterschiedlich sein kann.

Kontaktieren Sie Kunden, die eine Konversion auf intelligente und verantwortungsvolle Weise abgebrochen haben. Engagieren Sie Kunden mit veralteten Erlebnissen, um die Konversion zu steigern und den Kundenlebenszeitwert zu erhöhen.

Berücksichtigen Sie dabei Echtzeit-Überlegungen, berücksichtigen Sie alle Eigenschaften und Verhaltensweisen von Verbrauchern und bieten Sie eine schnelle Umqualifizierung basierend auf Online- und Offline-Ereignissen.

Nachstehend finden Sie eine allgemeine Architekturansicht der verschiedenen Komponenten von Real-Time CDP und Journey Optimizer. Dieses Diagramm zeigt, wie Daten durch die beiden Experience Platform-Apps von der Datenerfassung bis zu dem Punkt fließen, an dem sie durch Journey oder Kampagnen aktiviert werden, zu Zielen, um den auf dieser Seite beschriebenen Anwendungsfall zu erreichen.

![Intelligente visuelle Übersicht zur erneuten Interaktion auf hoher Ebene.](../intelligent-re-engagement/images/step-by-step.png)

## Anwendungsfallübersicht {#overview}

Sie erstellen Schemas, Datensätze und Zielgruppen, während Sie Beispiele für Rückgewinnungsszenarien durcharbeiten. Außerdem lernen Sie die Funktionen kennen, die zum Einrichten der Beispiel-Journey in [!DNL Adobe Journey Optimizer] erforderlich sind, sowie die Funktionen, die zum Erstellen von Paid-Media-Anzeigen in Zielen erforderlich sind. In diesem Handbuch werden Beispiele dafür verwendet, wie Kunden in den unten beschriebenen Anwendungsfällen erneut angesprochen werden:

* **Szenario mit abgebrochener Produktsuche** - Geben Sie Kunden als Ziel an, die das Durchsuchen von Produkten sowohl auf der Website als auch in der App abgebrochen haben.
* **Szenario mit Warenkorb abgebrochen** - Geben Sie Kunden als Ziel an, die Produkte in den Warenkorb gelegt, aber noch nicht auf der Website und in der App gekauft haben.
* **Bestellbestätigungsszenario** - Fokussieren Sie sich auf Produktkäufe, die über die Website und die mobile App getätigt werden.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie die Schritte zur Implementierung des Anwendungsfalls ausführen, nutzen Sie die folgenden Real-Time CDP- und Adobe Journey Optimizer-Funktionen (aufgelistet in der Reihenfolge, in der Sie sie verwenden werden). Vergewissern Sie sich, dass Sie die notwendigen [Attribut-basierten Zugriffsrechte](/help/access-control/home.md) für alle diese Bereiche haben, oder bitten Sie Ihre Systemadmins, Ihnen die notwendigen Rechte zu erteilen.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Integriert Daten aus verschiedenen Datenquellen, um die Kampagne zu unterstützen. Diese Daten werden dann verwendet, um die Kampagnenzielgruppen zu erstellen und personalisierte Datenelemente zu unterteilen, die in der E-Mail und in den Kacheln der Web-Promo verwendet werden (z. B. Name oder kontobezogene Informationen). Die CDP wird auch verwendet, um Zielgruppen über E-Mail und Web zu aktivieren (über [!DNL Adobe Target]).
   * [Schemata](/help/xdm/home.md)
   * [Profile](/help/profile/home.md)
   * [Datensätze](/help/catalog/datasets/overview.md)
   * [Zielgruppen](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Ziele](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=de) - Hilft Ihnen, Ihren Kunden verbundene, kontextbezogene und personalisierte Erlebnisse bereitzustellen.
   * [Ereignis oder Audience Trigger](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Zielgruppen/ Ereignisse](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=de)
   * [Journey Actions](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Anwendungsfall {#achieve-use-case-instruction}

Im Folgenden finden Sie einen allgemeinen Überblick über die drei Beispielszenarien zur erneuten Interaktion.

>[!BEGINTABS]

>[!TAB Szenario für abgebrochene Produktdurchsuchungen]

Das Szenario zum Durchsuchen von nicht mehr unterstützten Produkten zielt sowohl auf das Website- als auch auf die mobile App auf das abgebrochene Durchsuchen von Produkten ab. Dieses Szenario wird ausgelöst, wenn ein Produkt angesehen, aber nicht gekauft oder zum Warenkorb hinzugefügt wurde. In diesem Beispiel wird die Markeninteraktion nach drei Tagen ausgelöst, wenn innerhalb der letzten 24 Stunden keine Listen hinzugefügt wurden.<p>![Kunden - intelligente, abgebrochene Produktsuche - Überblick auf hoher Ebene](../intelligent-re-engagement/images/re-engagement-journey.png "Intelligenter Kunde, abgebrochener Produktbrowser - Überblick auf hoher Ebene."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemas und Datensätze und aktivieren sie dann für [!UICONTROL Profil].
2. Sie erfassen Daten über Web SDK, Mobile SDK oder API in Experience Platform. Analytics Source Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie erfassen zusätzliche profilaktivierte Daten, die über Identitätsdiagramme mit dem authentifizierten Web- und App-Besucher verknüpft werden können.
4. Sie erstellen fokussierte Zielgruppen aus der Profilliste, um zu überprüfen, ob ein **Kunde** in den letzten drei Tagen eine Interaktion durchgeführt hat.
5. Sie erstellen in [!DNL Adobe Journey Optimizer] eine Journey zum Durchsuchen von Produkten, die abgebrochen wurden.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** zusammen, um Zielgruppen für die gewünschten Paid-Media-Ziele zu aktivieren.
7. [!DNL Adobe Journey Optimizer] sucht nach Zustimmung und sendet die verschiedenen konfigurierten Aktionen aus.

>[!TAB Szenario mit abgelaufenem Warenkorb]

Das Szenario &quot;Stehen gelassener Warenkorb&quot;gilt, wenn Produkte in den Warenkorb gelegt, aber noch nicht auf der Website und in der App gekauft wurden. Darüber hinaus werden Paid Media-Kampagnen mit dieser Methode gestartet und beendet.<p>![Kunden haben das Szenario &quot;Warenkorb abgebrochen&quot;mit einer allgemeinen visuellen Übersicht übersehen.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Kunden, die den Warenkorb verlassen haben, haben eine allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemas und Datensätze, die für [!UICONTROL Profil] aktiviert sind.
2. Sie erfassen Daten über Web SDK, Mobile SDK oder API in Experience Platform. Analytics Source Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie erfassen zusätzliche profilaktivierte Daten, die über Identitätsdiagramme mit dem authentifizierten Web- und App-Besucher verknüpft werden können.
4. Sie können fokussierte Zielgruppen aus der Profilliste erstellen, um zu überprüfen, ob ein **Kunde** einen Artikel in den Warenkorb gelegt, aber den Kauf nicht abgeschlossen hat. Das Ereignis **[!UICONTROL Zum Warenkorb hinzufügen]** löst einen Timer aus, der 30 Minuten wartet, und sucht dann nach dem Kauf. Wenn kein Kauf getätigt wurde, wird der **Kunde** den Zielgruppen **[!UICONTROL Warenkorb abbrechen]** hinzugefügt.
5. In [!DNL Adobe Journey Optimizer] erstellen Sie eine Journey für den abgebrochenen Warenkorb.
6. Arbeiten Sie bei Bedarf mit dem **Datenpartner** zusammen, um Zielgruppen für die gewünschten Paid-Media-Ziele zu aktivieren.
7. [!DNL Adobe Journey Optimizer] sucht nach Zustimmung und sendet die verschiedenen konfigurierten Aktionen aus.

>[!TAB Bestellbestätigungsszenario]

Das Szenario zur Bestellbestätigung konzentriert sich auf Produktkäufe, die über die Website und die mobile App getätigt werden.<p>![Szenario zur Bestätigung der Kundenbestellung - Überblick auf hoher Ebene.](../intelligent-re-engagement/images/order-confirmation-journey.png "Szenario zur Bestätigung der Kundenbestellung - Überblick auf hoher Ebene."){width="1920" zoomable="yes"}</p>

1. Sie erstellen Schemas und Datensätze und aktivieren sie dann für [!UICONTROL Profil].
2. Sie erfassen Daten über Web SDK, Mobile SDK oder API in Experience Platform. Analytics Source Connector kann ebenfalls verwendet werden, kann jedoch zu einer Journey-Latenz führen.
3. Sie erfassen zusätzliche profilaktivierte Daten, die über Identitätsdiagramme mit dem authentifizierten Web- und App-Besucher verknüpft werden können.
4. Sie erstellen eine Bestätigungs-Journey in [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] sendet eine Auftragsbestätigungsnachricht mithilfe des bevorzugten Kanals.

>[!ENDTABS]

Um die einzelnen Schritte in den obigen Übersichten auf hoher Ebene abzuschließen, lesen Sie die folgenden Abschnitte durch, die Links zu weiteren Informationen und detaillierteren Anweisungen enthalten.

### Erstellen von Schemata und Angeben von Feldergruppen {#schema-design}

Ressourcen des Experience-Datenmodells (XDM) werden im Arbeitsbereich [!UICONTROL Schemas] in [!DNL Adobe Experience Platform] verwaltet. Sie können die von [!DNL Adobe] bereitgestellten Kernressourcen anzeigen und untersuchen (z. B. Feldgruppen) und benutzerdefinierte Ressourcen und Schemata für Ihre Organisation erstellen.

Weitere Informationen zum Erstellen von [Schemas](/help/xdm/home.md) finden Sie im Tutorial zum Erstellen von Schemas [.](/help/xdm/tutorials/create-schema-ui.md) und [Modellieren Ihrer Kundenerlebnisdaten mit XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Es gibt vier Schemaentwürfe, die für den Anwendungsfall der erneuten Interaktion verwendet werden. Für jedes Schema müssen spezifische Felder eingerichtet werden. Sie müssen die Aufnahme des Schemas in das Echtzeit-Kundenprofil aktivieren. Weitere Informationen zum Aktivieren des Schemas für die Verwendung im Echtzeit-Kundenprofil finden Sie unter [Aktivieren eines Schemas für das Echtzeit-Kundenprofil](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Schema für Kundenattribute

Dieses Schema wird verwendet, um die Profildaten zu strukturieren und zu referenzieren, aus denen Ihre Kundeninformationen bestehen. Diese Daten werden in der Regel über Ihr CRM-System oder ein ähnliches System in [!DNL Adobe Experience Platform] erfasst und sind erforderlich, um auf Kundendetails zu verweisen, die für die Personalisierung, Marketingzustimmung und erweiterte Zielgruppenfunktionen verwendet werden.

Das Kundenattributschema wird durch eine Klasse vom Typ [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md) dargestellt, die die folgenden Feldgruppen enthält:

+++Persönliche Kontaktdetails (Feldergruppe)

[Persönliche Kontaktdetails](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;, die die Kontaktinformationen für eine Person beschreibt.

| Felder | Beschreibung |
| --- | --- |
| `mobilePhone.number` | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| `personalEmail.address` | Die E-Mail-Adresse der Person. |

+++

+ + + externe Source-Systemprüfungsdetails (Feldergruppe)

[Externe Source-Systemprüfungsattribute](/help/xdm/data-types/external-source-system-audit-attributes.md) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Prüfdetails zu einem externen Quellsystem erfasst.

+++

+++Einverständnis- und Präferenzfeldgruppen (Feldergruppe)

Die Feldergruppe [Einverständnisse und Voreinstellungen](/help/xdm/field-groups//profile/consents.md) enthält ein einzelnes Objektfeld, Einverständniserklärungen, um Einverständnisinformationen und Präferenzinformationen zu erfassen.

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

Mit dieser Feldergruppe können Sie Ihre Journey vor der Veröffentlichung mithilfe von Testprofilen testen. Weitere Informationen zum Erstellen von Testprofilen finden Sie in den Tutorials [Testprofile erstellen](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html) und [Testen des Journey-Tutorials](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/testing-the-journey.html?lang=de).

+++

#### Schema für digitale Transaktionen des Kunden

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht und die auf Ihrer Website oder den zugehörigen digitalen Plattformen auftreten. Diese Daten werden in der Regel über das [Web SDK](/help/web-sdk/home.md) in [!DNL Adobe Experience Platform] erfasst und sind erforderlich, um auf die verschiedenen Durchsuchen- und Konversionsereignisse zu verweisen, die zum Auslösen von Journey verwendet werden, sowie auf detaillierte Online-Kundenanalysen, erweiterte Zielgruppenfunktionen und personalisiertes Messaging.

Das Schema für digitale Transaktionen des Kunden wird durch eine [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) -Klasse dargestellt.

+++XDM ExperienceEvent (Klasse)

Die Klasse [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) enthält die folgenden Feldergruppen:

| Felder | Beschreibung |
| --- | --- |
| `_id` | Identifiziert individuelle Ereignisse, die in [!DNL Adobe Experience Platform] erfasst werden. |
| `timestamp` | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses, formatiert gemäß RFC 3339 Abschnitt 5.6. Dieser Zeitstempel muss in der Vergangenheit auftreten. |
| `eventType` | Eine Zeichenfolge, die den Typ der Kategorie für das Ereignis angibt. |

+++

+ + + Endbenutzer-ID-Details (Feldergruppe)

Die Feldergruppe [Endbenutzer-ID-Details](/help/xdm/field-groups/event/enduserids.md) wird verwendet, um die Identitätsdaten einer Person in mehreren Adobe-Applikationen zu beschreiben.

| Felder | Beschreibung |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.id` | E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.namespace.code` | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] Authentifizierter Status der Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud-ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] Marketing Cloud-ID-Namespace-Code (MCID). |

+++

+ + + Commerce Details (Feldergruppe)

Die Feldergruppe [Commerce-Details](/help/xdm/field-groups/event/commerce-details.md) wird verwendet, um Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßige Warenkorbvorgänge (Bestellung, Checkout, Abbruch) zu beschreiben.

| Felder | Beschreibung |
| --- | --- |
| `commerce.cart.cartID` | Eine ID für den Warenkorb. |
| `commerce.order.orderType` | Ein Objekt, das den Produktanordnungstyp beschreibt. |
| `commerce.order.payments.paymentAmount` | Ein Objekt, das den Zahlungsbetrag der Produktbestellung beschreibt. |
| `commerce.order.payments.paymentType` | Ein Objekt, das den Produktzahlungstyp beschreibt. |
| `commerce.order.payments.transactionID` | Eine Transaktions-ID der Objektproduktbestellung. |
| `commerce.order.purchaseID` | Eine Kauf-ID für Objektprodukte. |
| `productListItems.name` | Eine Liste von Artikelnamen, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.priceTotal` | Der Gesamtpreis der Artikelliste, die die von einem Kunden ausgewählten Produkte darstellt. |
| `productListItems.product` | Die ausgewählten Produkte. |
| `productListItems.quantity` | Die Anzahl der Elemente, die für die von einem Kunden ausgewählten Produkte stehen. |

+++

+ + + externe Source-Systemprüfungsdetails (Feldergruppe)

Externe Source-Systemprüfungsattribute sind ein standardmäßiger XDM-Datentyp (Experience Data Model), der Prüfdetails zu einem externen Quellsystem erfasst.

+++

#### Schema für Offline-Transaktionen des Kunden

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht, die auf Plattformen außerhalb Ihrer Website auftreten. Diese Daten werden in der Regel von einem POS (oder ähnlichen System) in [!DNL Adobe Experience Platform] erfasst und meist über eine API-Verbindung an Platform gestreamt. Ihr Zweck besteht darin, auf die verschiedenen Offline-Konversionsereignisse zu verweisen, die zur Auslösung von Journey verwendet werden, eine tiefe Online- und Offline-Kundenanalyse, erweiterte Zielgruppenfunktionen und personalisiertes Messaging.

Das Offline-Transaktionsschema des Kunden wird durch eine [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) -Klasse dargestellt.

+++XDM ExperienceEvent (Klasse)

Die Klasse [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) enthält die folgenden Feldergruppen:

| Felder | Beschreibung |
| --- | --- |
| `_id` | Identifiziert individuelle Ereignisse, die in [!DNL Adobe Experience Platform] erfasst werden. |
| `timestamp` | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses, formatiert gemäß RFC 3339 Abschnitt 5.6. Dieser Zeitstempel muss in der Vergangenheit auftreten. |
| `eventType` | Eine Zeichenfolge, die den Typ der Kategorie für das Ereignis angibt. |

+++

+ + + Commerce Details (Feldergruppe)

Die Feldergruppe [Commerce-Details](/help/xdm/field-groups/event/commerce-details.md) wird verwendet, um Commerce-Daten wie Produktinformationen (SKU, Name, Menge) und standardmäßige Warenkorbvorgänge (Bestellung, Checkout, Abbruch) zu beschreiben.

| Felder | Beschreibung |
| --- | --- |
| `commerce.cart.cartID` | Eine ID für den Warenkorb. |
| `commerce.order.orderType` | Ein Objekt, das den Produktanordnungstyp beschreibt. |
| `commerce.order.payments.paymentAmount` | Ein Objekt, das den Zahlungsbetrag der Produktbestellung beschreibt. |
| `commerce.order.payments.paymentType` | Ein Objekt, das den Produktzahlungstyp beschreibt. |
| `commerce.order.payments.transactionID` | Eine Transaktions-ID der Objektproduktbestellung. |
| `commerce.order.purchaseID` | Eine Kauf-ID für Objektprodukte. |
| `productListItems.name` | Eine Liste von Artikelnamen, die die von einem Kunden ausgewählten Produkte darstellen. |
| `productListItems.priceTotal` | Der Gesamtpreis der Artikelliste, die die von einem Kunden ausgewählten Produkte darstellt. |
| `productListItems.product` | Die ausgewählten Produkte. |
| `productListItems.quantity` | Die Anzahl der Elemente, die für die von einem Kunden ausgewählten Produkte stehen. |

+++

+++Persönliche Kontaktdetails (Feldergruppe)

[Persönliche Kontaktdetails](/help/xdm/field-groups/profile/personal-contact-details.md) ist eine Standardschemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;, die die Kontaktinformationen für eine Person beschreibt.

| Felder | Beschreibung |
| --- | --- |
| `mobilePhone.number` | Die Mobiltelefonnummer der Person, die für SMS verwendet wird. |
| `personalEmail.address` | Die E-Mail-Adresse der Person. |

+++

+ + + externe Source-Systemprüfungsdetails (Feldergruppe)

Externe Source-Systemprüfungsattribute sind ein standardmäßiger XDM-Datentyp (Experience Data Model), der Prüfdetails zu einem externen Quellsystem erfasst.

+++

#### Adobe-Web-Connector-Schema

>[!NOTE]
>
>Dies ist eine optionale Implementierung, wenn Sie den [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md) verwenden.

Dieses Schema wird verwendet, um die Ereignisdaten zu strukturieren und zu referenzieren, aus denen Ihre Kundenaktivität besteht und die auf Ihrer Website oder den zugehörigen digitalen Plattformen auftreten. Dieses Schema ähnelt dem Schema Customer Digital Transactions , ist jedoch insofern anders, als es verwendet werden soll, wenn [Web SDK](/help/web-sdk/home.md) keine Option für die Datenerfassung ist. Daher ist dieses Schema erforderlich, wenn Sie die [!DNL Adobe Analytics Source Connector] verwenden, um Ihre Online-Daten als primären oder sekundären Datastream an [!DNL Adobe Experience Platform] zu senden.

Das Web-Connector-Schema [!DNL Adobe] wird durch eine [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) -Klasse dargestellt.

+++XDM ExperienceEvent (Klasse)

Die Klasse [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) enthält die folgenden Feldergruppen:

| Felder | Beschreibung |
| --- | --- |
| `_id` | Identifiziert individuelle Ereignisse, die in [!DNL Adobe Experience Platform] erfasst werden. |
| `timestamp` | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses, formatiert gemäß RFC 3339 Abschnitt 5.6. Dieser Zeitstempel muss in der Vergangenheit auftreten. |
| `eventType` | Eine Zeichenfolge, die den Typ der Kategorie für das Ereignis angibt. |

+++

+ + + Adobe Analytics ExperienceEvent-Vorlage (Feldergruppe)

Die Feldergruppe [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) erfasst allgemeine Metriken, die von Adobe Analytics erfasst werden.

| Felder | Beschreibung |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Authentifizierter Status der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.id` | E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.emailid.namespace.code` | Namespace-Code der E-Mail-Adresse des Endbenutzers. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] Authentifizierter Status der Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud-ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] Marketing Cloud-ID-Namespace-Code (MCID). |

+++

+ + + externe Source-Systemprüfungsdetails (Feldergruppe)

Externe Source-Systemprüfungsattribute sind ein standardmäßiger XDM-Datentyp (Experience Data Model), der Prüfdetails zu einem externen Quellsystem erfasst.

+++

### Datensatz aus einem Schema erstellen {#create-datasets}

Ein Datensatz ist eine Speicher- und Verwaltungsstruktur für eine Datengruppe. Jedes Schema für intelligente Rückgewinnungsszenarien sollte über einen eigenen Datensatz verfügen.

Weitere Informationen zum Erstellen eines [Datensatzes](/help/catalog/datasets/overview.md) aus einem Schema finden Sie im Handbuch zur [Benutzeroberfläche für Datensätze](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Ähnlich wie beim Schritt zum Erstellen eines Schemas müssen Sie die Aufnahme des Datensatzes in das Echtzeit-Kundenprofil aktivieren. Weitere Informationen zum Aktivieren des Datensatzes für die Verwendung im Echtzeit-Kundenprofil finden Sie in der Anleitung zum [Einbringen von Daten in das Echtzeit-Kundenprofil](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=de).

### Einverständnis und Data Governance {#privacy-consent}

>[!IMPORTANT]
>
>Es ist gesetzlich vorgeschrieben, Kunden die Möglichkeit zu geben, sich vom Erhalt von Nachrichten einer Marke abzumelden und sicherzustellen, dass diese Entscheidung respektiert wird. Weitere Informationen zu den geltenden Rechtsvorschriften finden Sie in der Übersicht über die [Datenschutzbestimmungen](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html) .

#### Einverständniserklärungen

Wenn Sie einen Rückgewinnungspfad erstellen, sollten Sie die folgenden [Zustimmungsrichtlinien](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) hinzufügen:

* Wenn `consents.marketing.email.val = "Y"`, dann Kann E-Mail
* Wenn `consents.marketing.sms.val = "Y"`, dann Kann SMS
* Wenn `consents.marketing.push.val = "Y"`, kann Push
* Wenn `consents.share.val = "Y"`, kann Werbung

#### Beschriftung und Durchsetzung von Data Governance

Ziehen Sie beim Erstellen eines Rückgewinnungspfads die folgenden [Data Governance-Beschriftungen](/help/data-governance/labels/overview.md) hinzu:

* Persönliche E-Mail-Adressen werden als direkt identifizierbare Daten verwendet, die zur Identifizierung oder zum Kontakt mit einer bestimmten Person und nicht mit einem Gerät verwendet werden.
   * `personalEmail.address = I1`

#### Datennutzungsrichtlinien

Für das Szenario mit abgebrochenen Produktdurchsuchvorgängen sind keine [Datennutzungsrichtlinien](/help/data-governance/policies/overview.md) erforderlich. Beachten Sie jedoch Folgendes:

* Einschränken vertraulicher Daten
* Einschränken von Onsite Advertising
* E-Mail-Targeting einschränken
* Site-übergreifendes Targeting einschränken
* Beschränkung der Kombination direkt identifizierbarer Daten mit anonymen Daten

### Erstellen von Zielgruppen {#create-audience}

In den Rückgewinnungsszenarios werden Zielgruppen verwendet, um bestimmte Attribute oder Verhaltensweisen zu definieren, die von einer Untergruppe von Profilen aus Ihrem Profilspeicher gemeinsam genutzt werden, um eine vermarktbare Personengruppe aus Ihrem Kundenstamm zu unterscheiden. Zielgruppen können auf unterschiedliche Weise in [!DNL Adobe Experience Platform] erstellt werden.

Weitere Informationen zum Erstellen einer Zielgruppe finden Sie im Handbuch [Benutzeroberfläche des Zielgruppendienstes](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience) .

Weitere Informationen zum direkten Erstellen von [Zielgruppen](/help/segmentation/home.md) finden Sie im Handbuch [Benutzeroberfläche für Zielgruppenkomposition](/help/segmentation/ui/audience-composition.md) .

Weitere Informationen zum Erstellen von Zielgruppen mithilfe von Platform-abgeleiteten Zielgruppendefinitionen finden Sie im [Handbuch zur Audience Builder-Benutzeroberfläche](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Szenario für abgebrochene Produktdurchsuchungen]

Diese Zielgruppe wird als Erweiterung des klassischen Szenarios &quot;Warenkorbabbruch&quot;erstellt. Während sich der Warenkorbabbruch in der Regel auf einen Zusatz zum Warenkorb ohne anschließenden Kauf in einem bestimmten Zeitraum konzentriert, sucht diese Zielgruppe nach einer früheren Interaktion, insbesondere nach denjenigen, die möglicherweise ein bestimmtes Produkt durchsucht, es jedoch nicht zum Warenkorb hinzugefügt haben und innerhalb eines bestimmten Zeitraums keine Nachbearbeitungsaktivität auf Ihrer Site hatten. Diese Zielgruppe hilft dabei, Ihre Marke für Kunden, die diese Aufnahmekriterien erfüllen, &quot;ganz oben im Kopf&quot;zu halten und kann auch für Kunden genutzt werden, deren digitale Eigenschaften von einem herkömmlichen E-Commerce-Modell abweichen können.

+ + + Abgebrochene Produktansicht ohne Interaktion in den letzten drei Tagen

Das folgende Ereignis wird für das Szenario des abgebrochenen Produktdurchsuchs verwendet, bei dem Benutzer in den folgenden 3 Tagen Produkte online angesehen und nicht interagiert haben (Site-Besuche, App-Besuche, Online-Einkäufe, Offline-Käufe und zum Warenkorbereignis hinzugefügte Ereignisse).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `eventType: commerce.productViews`
* Und `THEN` (sequenzielles Ereignis) schließen `eventType: commerce.productListAdds` UND `application.launch` UND `web.webpagedetails.pageViews` UND `commerce.purchases` aus (dies schließt sowohl online als auch offline ein)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`

+++

+++ Produktansicht mit Interaktion in den letzten drei Tagen

Das folgende Ereignis wird für das Szenario des abgebrochenen Produktdurchsuchs verwendet, bei dem Benutzer Produkte online angesehen und in den folgenden 3 Tagen Interaktionen durchgeführt haben (Site-Besuche, App-Besuche, Online-Einkäufe, Offline-Käufe und Hinzufügen zu Warenkorbereignissen).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `eventType: commerce.productViews`
* Und `THEN` (sequenzielles Ereignis) enthält `eventType: commerce.productListAdds` ODER `application.launch` ODER `web.webpagedetails.pageViews` ODER `commerce.purchases` (dies schließt sowohl online als auch offline ein)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`
+++

+++Interaktions-Streaming am letzten Tag

Das folgende Ereignis wird für das Szenario des abgebrochenen Produktdurchsuchs verwendet, bei dem die Benutzer in den letzten 1 Tagen interagiert haben (Site-Besuche, App-Besuche, Online-Einkäufe, Offline-Käufe und Hinzufügen zu Warenkorbereignissen).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `eventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 1 day` (Streaming)

+++

+++Interaktionsstapel in den letzten drei Tagen

Das folgende Ereignis wird für das Szenario des abgebrochenen Produktdurchsuchs verwendet, bei dem sich die Benutzer in den letzten drei Tagen engagiert haben (Site-Besuche, App-Besuche, Online-Einkäufe, Offline-Käufe und Hinzufügen zu Warenkorbereignissen).

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `EventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 3 days` (Batch)

+++

>[!TAB Szenario mit abgelaufenem Warenkorb]

Diese Zielgruppe wird erstellt, um das klassische Szenario &quot;Warenkorbabbruch&quot;zu unterstützen. Ihr Zweck besteht darin, Kunden zu finden, die ein Produkt zum Warenkorb hinzugefügt, aber letztlich nicht mit einem Kauf ausgeführt haben. Diese Zielgruppe hilft Ihnen dabei, nicht nur Ihre Marke &quot;ganz oben im Kopf&quot;für Ihre Kunden zu halten, sondern auch die Produkte, die sie ohne nachfolgenden Kauf zurückgelassen haben.

Die folgenden Ereignisse werden für das Szenario mit einem abgebrochenen Warenkorb verwendet, in dem Benutzer zwischen 1 und 4 Tagen ein Produkt zum Warenkorb hinzugefügt, den Kauf jedoch nicht abgeschlossen oder den Warenkorb gelöscht haben.

Die folgenden Felder und Bedingungen sind beim Einrichten dieser Audience erforderlich:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now AND <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

Der Deskriptor für das Szenario &quot;Abbruch des Warenkorbs&quot;wird wie folgt angezeigt:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Bestellbestätigungsszenario]

Für diese Journey müssen keine Zielgruppen erstellt werden.

>[!ENDTABS]

### Journey-Setup in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] umfasst nicht alle in den Diagrammen angezeigten Elemente. Alle [gebührenpflichtigen Medienanzeigen](/help/destinations/catalog/social/overview.md) werden in [!UICONTROL Zielen] erstellt.

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) hilft Ihnen, Ihren Kunden verbundene, kontextbezogene und personalisierte Erlebnisse bereitzustellen. Die Journey ist der gesamte Vorgang der Interaktion eines Kunden mit der Marke. Für jede Journey von Anwendungsfällen sind spezifische Informationen erforderlich. Im Folgenden finden Sie die genauen Daten, die für jede Journey benötigt werden.

>[!BEGINTABS]

>[!TAB Szenario für abgebrochene Produktdurchsuchungen]

Das Szenario zum Durchsuchen von nicht mehr unterstützten Produkten zielt sowohl auf das Website- als auch auf die mobile App auf das abgebrochene Durchsuchen von Produkten ab.<p>![Kunden, die das Durchsuchen von Produkten abgebrochen haben, sehen eine allgemeine Übersicht.](../intelligent-re-engagement/images/re-engagement-journey.png "Kunden, die das Durchsuchen von Produkten abgebrochen haben, erhalten eine allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

+++Ereignisse

Mit Hilfe von Ereignissen können Sie Ihre Journeys einheitlich auslösen, um Nachrichten in Echtzeit an die Kontakte zu senden, die in die Journey eintreten. Weitere Informationen zu Ereignissen finden Sie im [allgemeinen Ereignisleitfaden](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Ereignis 1: Produktansichten
   * Schema: Customer Digital Transactions
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
   * Schema: Customer Digital Transactions
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

* Ereignis 3: Markeninteraktion
   * Schema: Customer Digital Transactions
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

+++Journey-Arbeitsfläche für Schlüssellogik

Für die Schlüssellogik der Journey-Arbeitsfläche müssen Sie bestimmte Ereignisse identifizieren und Aktionen konfigurieren, die nach dem Eintreten des Ereignisses ausgeführt werden.

* Journey-Einstiegslogik
   * Ereignis für Produktansicht

* Bedingungen
   * Suchen Sie nach mindestens einem Online- oder Offline-Kaufereignis seit der letzten Ansicht des Produkts.
      * Schema: Customer Digital Transactions
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Suchen Sie nach mindestens einem Offline-Kauf seit der letzten Ansicht des Produkts:
      * Schema: Offline-Kundentransaktionen
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Bedingungen - Auswählen des Target-Kanals
      * E-Mail
         * `consents.marketing.email.val = y`
      * Push-Benachrichtigung
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Channel Personalization
      * Personalisierte Kanalinhalte basierend auf der Produktansicht.

+++

>[!TAB Szenario mit abgelaufenem Warenkorb]

Das Szenario mit einem abgebrochenen Warenkorb zielt auf Produkte ab, die im Warenkorb platziert, aber noch nicht auf der Website und in der App gekauft wurden.<p>![Kunden haben das Szenario &quot;Warenkorb abgebrochen&quot;mit einer allgemeinen visuellen Übersicht übersehen.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Kunden, die den Warenkorb verlassen haben, haben eine allgemeine visuelle Übersicht."){width="1920" zoomable="yes"}</p>

+++Ereignisse

Mit Hilfe von Ereignissen können Sie Ihre Journeys einheitlich auslösen, um Nachrichten in Echtzeit an die Kontakte zu senden, die in die Journey eintreten. Weitere Informationen zu Ereignissen finden Sie im [allgemeinen Ereignisleitfaden](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Ereignis 2: Zum Warenkorb hinzufügen
   * Schema: Customer Digital Transactions
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

* Ereignis 4: Online-Käufe
   * Schema: Customer Digital Transactions
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

* Ereignis 3: Markeninteraktion
   * Schema: Customer Digital Transactions
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

+++Journey-Arbeitsfläche für Schlüssellogik

Für die Schlüssellogik der Journey-Arbeitsfläche müssen Sie bestimmte Ereignisse identifizieren und Aktionen konfigurieren, die nach dem Eintreten des Ereignisses ausgeführt werden.

* Journey-Einstiegslogik
   * `AddToCart` Ereignis

* AuthenticatedState in authenticated

* Bedingung: Offline-Käufe seit dem letzten Abbruch des Warenkorbs:
   * Schema: Offline-Kundentransaktionen
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Bedingung: Der Warenkorb wurde gelöscht, da der Warenkorb zuletzt abgebrochen wurde:
   * Schema: Customer Digital Transactions
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
   * Channel Personalization
      * Zeigen Sie Informationen zu Warenkorbdetails an und können mehrere Produkte in einem Tabellenformat anzeigen.

+++

>[!TAB Bestellbestätigungsszenario]

Das Szenario zur Bestellbestätigung konzentriert sich auf Produktkäufe, die über die Website und die mobile App getätigt werden.<p>![Szenario zur Bestätigung der Kundenbestellung - Überblick auf hoher Ebene.](../intelligent-re-engagement/images/order-confirmation-journey.png "Szenario zur Bestätigung der Kundenbestellung - Überblick auf hoher Ebene."){width="1920" zoomable="yes"}</p>

+++Ereignisse

Mit Hilfe von Ereignissen können Sie Ihre Journeys einheitlich auslösen, um Nachrichten in Echtzeit an die Kontakte zu senden, die in die Journey eintreten. Weitere Informationen zu Ereignissen finden Sie im [allgemeinen Ereignisleitfaden](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Ereignis 4: Online-Käufe
   * Schema: Customer Digital Transactions
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

+++Journey-Arbeitsfläche für Schlüssellogik

Für die Schlüssellogik der Journey-Arbeitsfläche müssen Sie bestimmte Ereignisse identifizieren und Aktionen konfigurieren, die nach dem Eintreten des Ereignisses ausgeführt werden.

* Journey-Einstiegslogik
   * Bestellereignis

* Bedingungen
   * Wählen Sie Zielkanal (wählen Sie einen oder mehrere Kanäle für eine größere Reichweite aus).
      * Eine Bestellbestätigung gilt als Serving in der Natur, daher ist eine Zustimmungsprüfung in der Regel nicht erforderlich.
      * E-Mail
      * Push-Benachrichtigung
      * SMS

   * Kanalinhalt-Personalization
      * Zeigen Sie Bestelldetails an und können eine Liste von Produkten im Tabellenformat anzeigen.

+++

>[!ENDTABS]

Weitere Informationen zum Erstellen von Journey in [!DNL Adobe Journey Optimizer] finden Sie im Leitfaden [Erste Schritte mit Journey](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Einrichten von Paid-Media-Anzeigen in Zielen {#paid-media-ads}

Das Ziel-Framework wird für Paid-Media-Anzeigen verwendet. Nachdem die Einwilligung überprüft wurde, wird sie an die verschiedenen konfigurierten Ziele gesendet. Weitere Informationen zu Zielen finden Sie im Dokument [Ziele - Übersicht](/help/destinations/home.md) .

#### Für Ziele erforderliche Daten

Streaming-Zielgruppenexport-Ziele (z. B. Facebook, Google Customer Match, Google DV360) unterstützen verschiedene Identitäten aus Kundendaten:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Sie können die abgebrochene Produktsuche aktivieren und die Zielgruppen des Warenkorbs für Paid Media-Anzeigen verlassen.

* Stream/Ausgelöst
   * [Advertising](/help/destinations/catalog/advertising/overview.md)/[Paid Media &amp; Social](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Streaming-Ziel](/help/destinations/catalog/streaming/http-destination.md)
   * [Benutzerdefiniertes Ziel, das mithilfe von Destination SDK erstellt wurde.](/help/destinations/destination-sdk/overview.md). Wenn Sie Real-Time CDP Ultimate-Kunde sind, können Sie auch ein privates [benutzerdefiniertes Ziel mit Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations) erstellen

## Nächste Schritte {#next-steps}

Indem Sie Ihre Kunden, die eine Konversion auf intelligente und verantwortungsvolle Weise abgebrochen haben, erneut ansprechen, haben Sie hoffentlich Konversionen erhöht und den Wert für die Kundenlebensdauer erhöht.

Als Nächstes können Sie weitere von Real-Time CDP unterstützte Anwendungsfälle untersuchen, z. B. [Anzeigen personalisierter Inhalte für nicht authentifizierte Benutzer](/help/rtcdp/partner-data/onsite-personalization.md) in Ihren Webeigenschaften.
