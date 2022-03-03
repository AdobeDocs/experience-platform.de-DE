---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;XDM;Felder;Schemas;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Ereignismodellierung;Ereignismodellierung;Best Practices;Ereignis;Ereignisse;
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die XDM ExperienceEvent-Klasse und Best Practices für die Modellierung von Ereignisdaten.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 3%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] ist eine standardmäßige XDM-Klasse (Experience-Datenmodell), mit der Sie einen Schnappschuss des Systems mit Zeitstempel erstellen können, wenn ein bestimmtes Ereignis auftritt oder ein bestimmter Bedingungssatz erreicht wurde.

Ein Erlebnisereignis ist ein Faktendatensatz dessen, was geschehen ist, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignisse können entweder explizit (direkt beobachtbare menschliche Aktionen) oder implizit (ohne direkte menschliche Aktion ausgelöst) sein und ohne Aggregation oder Interpretation aufgezeichnet werden. Weiterführende Informationen zur Verwendung dieser Klasse im Platform-Ökosystem finden Sie im Abschnitt [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent] -Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Die Werte einiger dieser Felder werden bei der Datenerfassung automatisch ausgefüllt:

![](../images/classes/experienceevent/structure.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id` | Eine eindeutige Zeichenfolgenkennung für das Ereignis. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Ereignisses zu verfolgen, Datendoppelungen zu verhindern und dieses Ereignis in nachgelagerten Diensten nachzuschlagen. In einigen Fällen `_id` kann ein [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei erfassen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern miteinander verknüpfen, die das Ereignis eindeutig machen, z. B. eine primäre ID, einen Zeitstempel, einen Ereignistyp usw. Der verkettete Wert muss eine `uri-reference` formatierte Zeichenfolge, was bedeutet, dass alle Doppelpunkt-Zeichen entfernt werden müssen. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu unterscheiden, dass **Dieses Feld stellt keine Identität dar, die mit einer Person in Verbindung steht**, sondern der Datensatz selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten auf [Identitätsfelder](../schema/composition.md#identity) bereitgestellt von kompatiblen Feldergruppen. |
| `eventMergeId` | Wenn Sie [Adobe Experience Platform Web SDK](../../edge/home.md) um Daten zu erfassen, stellt dies die Kennung des erfassten Batches dar, der zur Erstellung des Datensatzes geführt hat. Dieses Feld wird bei der Datenerfassung automatisch vom System ausgefüllt. Die Verwendung dieses Felds außerhalb des Kontexts einer Web SDK-Implementierung wird nicht unterstützt. |
| `eventType` | Eine Zeichenfolge, die den Typ oder die Kategorie für das Ereignis angibt. Dieses Feld kann verwendet werden, wenn Sie verschiedene Ereignistypen innerhalb desselben Schemas und Datensatzes unterscheiden möchten, z. B. die Unterscheidung eines Produktansichtsereignisses von einem Add-zu-Warenkorb-Ereignis für ein Einzelhandelsunternehmen.<br><br>Standardwerte für diese Eigenschaft werden im Abschnitt [Anhang](#eventType), einschließlich Beschreibungen des vorgesehenen Anwendungsfalls. Dieses Feld ist eine erweiterbare Enumeration, d. h. Sie können auch eigene Ereignistypen-Zeichenfolgen verwenden, um die Ereignisse zu kategorisieren, die Sie verfolgen.<br><br>`eventType` beschränkt die Verwendung eines einzelnen Ereignisses pro Treffer in Ihrer Anwendung. Daher müssen Sie berechnete Felder verwenden, um dem System mitzuteilen, welches Ereignis am wichtigsten ist. Weitere Informationen finden Sie im Abschnitt zu [Best Practices für berechnete Felder](#calculated). |
| `producedBy` | Ein string -Wert, der den Hersteller oder Ursprung des Ereignisses beschreibt. Dieses Feld kann verwendet werden, um bestimmte Ereignisproduzenten bei Bedarf für Segmentierungszwecke herauszufiltern.<br><br>Einige empfohlene Werte für diese Eigenschaft werden im Abschnitt [Anhang](#producedBy). Dieses Feld ist eine erweiterbare Enumeration, d. h. Sie können auch eigene Zeichenfolgen verwenden, um verschiedene Ereignisproduzenten zu repräsentieren. |
| `identityMap` | Ein map -Feld, das einen Satz von Namespaced-Identitäten für die Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Um dieses Feld ordnungsgemäß zu verwenden, verwenden Sie [Echtzeit-Kundenprofil](../../profile/home.md)versuchen Sie nicht, den Inhalt des Felds in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Siehe Abschnitt zu Identitätskarten im Abschnitt [Grundlagen der Schemakomposition](../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `timestamp` | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß [RFC 3339 Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Dieser Zeitstempel muss in der Vergangenheit auftreten. Siehe den Abschnitt unten unter [Zeitstempel](#timestamps) für Best Practices zur Verwendung dieses Felds. |

{style=&quot;table-layout:auto&quot;}

## Best Practices für die Ereignismodellierung

In den folgenden Abschnitten finden Sie Best Practices zum Entwerfen Ihrer ereignisbasierten Experience-Datenmodell (XDM)-Schemas in Adobe Experience Platform.

### Zeitstempel {#timestamps}

Der Stamm `timestamp` -Feld eines Ereignisschemas kann **only** die Beobachtung des Ereignisses selbst darstellen und in der Vergangenheit auftreten müssen. Wenn Ihre Segmentierungsanwendungsfälle die Verwendung von Zeitstempeln erfordern, die in Zukunft auftreten können, müssen diese Werte an einer anderen Stelle im Erlebnisereignis-Schema eingeschränkt werden.

Beispiel: Wenn ein Unternehmen der Reise- und Gastgewerbe ein Flugreservierungsereignis modelliert, wird die Klasse `timestamp` -Feld gibt den Zeitpunkt an, zu dem das Reservierungsereignis beobachtet wurde. Andere Zeitstempel, die mit dem Ereignis in Verbindung stehen, wie z. B. das Startdatum der Reisereservierung, sollten in separaten Feldern erfasst werden, die von standardmäßigen oder benutzerdefinierten Feldergruppen bereitgestellt werden.

![](../images/classes/experienceevent/timestamps.png)

Indem Sie den Zeitstempel auf Klassenebene von anderen zugehörigen Datums-/Zeitwerten in Ihren Ereignisschemas trennen, können Sie flexible Anwendungsfälle für die Segmentierung implementieren und gleichzeitig ein Kundenkonto mit Zeitstempel in Ihrer Erlebnisanwendung beibehalten.

### Berechnete Felder verwenden {#calculated}

Bestimmte Interaktionen in Ihren Erlebnisanwendungen können zu mehreren verwandten Ereignissen führen, die technisch denselben Ereigniszeitstempel aufweisen, und daher als einzelner Ereignisdatensatz dargestellt werden. Wenn ein Kunde beispielsweise ein Produkt auf Ihrer Website ansieht, kann dies zu einem Ereignisdatensatz mit zwei potenziellen `eventType` -Werte: ein &quot;product view&quot;-Ereignis (`commerce.productViews`) oder ein generisches &quot;Seitenansichtsereignis&quot;(`web.webpagedetails.pageViews`). In diesen Fällen können Sie berechnete Felder verwenden, um die wichtigsten Attribute zu erfassen, wenn mehrere Ereignisse in einem einzelnen Treffer erfasst werden.

[Adobe Experience Platform-Datenvorbereitung](../../data-prep/home.md) ermöglicht die Zuordnung, Umwandlung und Validierung von Daten zu und von XDM. Verfügbare [Zuordnungsfunktionen](../../data-prep/functions.md) durch den Dienst bereitgestellte Dienste können Sie logische Operatoren aufrufen, um bei der Aufnahme in Experience Platform Daten aus Datensätzen mit mehreren Ereignissen zu priorisieren, umzuwandeln und/oder zu konsolidieren. Im obigen Beispiel können Sie `eventType` als berechnetes Feld, das einer &quot;Produktansicht&quot;Priorität vor einer &quot;Seitenansicht&quot;einräumt, wann immer beide auftreten.

Wenn Sie Daten manuell über die Benutzeroberfläche in Platform erfassen, lesen Sie das Handbuch unter [berechnete Felder](../../data-prep/ui/mapping.md#calculated-fields) für spezifische Schritte zur Erstellung berechneter Felder.

Wenn Sie Daten mithilfe einer Quellverbindung an Platform streamen, können Sie die Quelle so konfigurieren, dass stattdessen berechnete Felder verwendet werden. Siehe Abschnitt [Dokumentation zu Ihrer jeweiligen Quelle](../../sources/home.md) für Anweisungen zur Implementierung berechneter Felder beim Konfigurieren der Verbindung.

## Kompatible Schemafeldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldergruppen wurden geändert. Siehe Dokument unter [Namensaktualisierungen für Feldergruppen](../field-groups/name-updates.md) für weitere Informationen.

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM ExperienceEvent] -Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Bilanzübertragungen]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Kampagnen-Marketingdetails]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Kartenaktionen]](../field-groups/event/card-actions.md)
* [[!UICONTROL Kanaldetails]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce-Details]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Einlagendetails]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Details zum Gerätehandel]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Speisereservierung]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Details zur Endbenutzer-ID]](../field-groups/event/enduserids.md)
* [[!UICONTROL Umgebungsdetails]](../field-groups/event/environment-details.md)
* [[!UICONTROL Flugreservierung]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0-Zustimmung]](../field-groups/event/iab.md)
* [[!UICONTROL Unterkunftsreservierung]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Anführungsanfragedetails]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Buchungsdetails]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Webdetails]](../field-groups/event/web-details.md)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum [!UICONTROL XDM ExperienceEvent] -Klasse.

### Akzeptierte Werte für `eventType` {#eventType}

In der folgenden Tabelle sind die für `eventType`, zusammen mit ihren Definitionen:

| Wert | Definition |
| --- | --- |
| `advertising.clicks` | Klicken Sie auf eine(n) Aktion(en) für eine Anzeige. |
| `advertising.completes` | Ein zeitgesteuertes Medien-Asset wurde bis zum Ende angesehen. Das bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat, da der Betrachter voraus hätte überspringen können. |
| `advertising.conversions` | Vordefinierte Aktion(en), die von einem Kunden durchgeführt wird, der ein Ereignis zur Leistungsbewertung Trigger. |
| `advertising.federated` | Gibt an, ob ein Erlebnisereignis über eine Datenverknüpfung (Datenfreigabe zwischen Kunden) erstellt wurde. |
| `advertising.firstQuartiles` | Eine digitale Videoanzeige hat 25 % ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.impressions` | Impression(en) einer Anzeige für einen Kunden mit dem Potenzial, angezeigt zu werden. |
| `advertising.midpoints` | Eine digitale Videoanzeige hat 50% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.starts` | Die Wiedergabe einer digitalen Videoanzeige hat begonnen. |
| `advertising.thirdQuartiles` | Eine digitale Videoanzeige hat 75% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.timePlayed` | Beschreibt die Zeit, die ein Benutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbringt. |
| `application.close` | Eine Anwendung wurde geschlossen oder in den Hintergrund gestellt. |
| `application.launch` | Eine Anwendung wurde gestartet oder in den Vordergrund gestellt. |
| `commerce.checkouts` | Für eine Produktliste ist ein Checkout-Ereignis aufgetreten. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden der Zeitstempel und die referenzierte Seite/das referenzierte Erlebnis für jedes Ereignis verwendet, um jedes einzelne Ereignis (Schritt) zu identifizieren, das in der angegebenen Reihenfolge dargestellt wird. |
| `commerce.productListAdds` | Ein Produkt wurde zur Produktliste oder zum Warenkorb hinzugefügt. |
| `commerce.productListOpens` | Eine neue Produktliste (Warenkorb) wurde initialisiert oder erstellt. |
| `commerce.productListRemovals` | Ein oder mehrere Produkteinträge wurden aus einer Produktliste oder einem Warenkorb entfernt. |
| `commerce.productListReopens` | Eine Produktliste (Warenkorb), auf die nicht mehr zugegriffen werden konnte (abgebrochen), wurde von einem Kunden erneut aktiviert, z. B. über eine Remarketing-Aktivität. |
| `commerce.productListViews` | Eine Produktliste oder ein Warenkorb hat eine oder mehrere Ansichten erhalten. |
| `commerce.productViews` | Ein Produkt hat eine oder mehrere Ansichten erhalten. |
| `commerce.purchases` | Eine Bestellung wurde angenommen. Dies ist die einzige erforderliche Aktion bei einer Commerce-Konversion. Auf ein Kaufereignis muss eine Produktliste verwiesen werden. |
| `commerce.saveForLaters` | Eine Produktliste wurde für die zukünftige Verwendung gespeichert, z. B. eine ProduktWunschliste. |
| `decisioning.propositionDisplay` | Eine Person wurde ein Entscheidungsvorschlag angezeigt. |
| `decisioning.propositionInteract` | Eine Person hat mit einem Entscheidungsvorschlag interagiert. |
| `delivery.feedback` | Feedback-Ereignisse für einen Versand, z. B. ein E-Mail-Versand. |
| `directMarketing.emailBounced` | Eine E-Mail an eine Person mit Absprung. |
| `directMarketing.emailBouncedSoft` | Eine E-Mail an eine Person mit Softbounce. |
| `directMarketing.emailClicked` | Eine Person hat auf einen Link in einer Marketing-E-Mail geklickt. |
| `directMarketing.emailDelivered` | Eine E-Mail wurde dem E-Mail-Dienst einer Person erfolgreich zugestellt |
| `directMarketing.emailOpened` | Eine Person hat eine Marketing-E-Mail geöffnet. |
| `directMarketing.emailUnsubscribed` | Eine Person hat sich von einer Marketing-E-Mail abgemeldet. |
| `inappmessageTracking.dismiss` | Eine In-App-Nachricht wurde verworfen. |
| `inappmessageTracking.display` | Eine In-App-Nachricht wurde angezeigt. |
| `inappmessageTracking.interact` | Mit einer In-App-Nachricht wurde interagiert. |
| `leadOperation.callWebhook` | Als Reaktion auf einen Lead wurde ein Webhook aufgerufen. |
| `leadOperation.convertLead` | Ein Lead wurde konvertiert. |
| `leadOperation.interestingMoment` | Ein interessanter Moment wurde für eine Person aufgezeichnet. |
| `leadOperation.newLead` | Ein Lead wurde erstellt. |
| `leadOperation.scoreChanged` | Der Wert des Ergebnisattributs des Leads wurde geändert. |
| `leadOperation.statusInCampaignProgressionChanged` | Der Status eines Leads in einer Kampagne hat sich geändert. |
| `listOperation.addToList` | Eine Person wurde zu einer Marketingliste hinzugefügt. |
| `listOperation.removeFromList` | Eine Person wurde aus einer Marketing-Liste entfernt. |
| `message.feedback` | Feedback-Ereignisse wie Senden/Bounce/Fehler für Nachrichten, die an einen Kunden gesendet werden. |
| `message.tracking` | Tracking von Ereignissen wie Öffnen/Klicken/benutzerdefinierten Aktionen für Nachrichten, die an einen Kunden gesendet werden. |
| `opportunityEvent.addToOpportunity` | Eine Person wurde zu einer Gelegenheit hinzugefügt. |
| `opportunityEvent.opportunityUpdated` | Eine Gelegenheit wurde aktualisiert. |
| `opportunityEvent.removeFromOpportunity` | Eine Person wurde aus einer Gelegenheit entfernt. |
| `pushTracking.applicationOpened` | Eine Person hat eine Anwendung über eine Push-Benachrichtigung geöffnet. |
| `pushTracking.customAction` | Eine Person hat in einer Push-Benachrichtigung auf eine benutzerdefinierte Aktion geklickt. |
| `web.formFilledOut` | Eine Person hat ein Formular auf einer Webseite ausgefüllt. |
| `web.webinteraction.linkClicks` | Ein Link wurde mindestens einmal ausgewählt. |
| `web.webpagedetails.pageViews` | Eine Webseite hat eine oder mehrere Ansichten erhalten. |

{style=&quot;table-layout:auto&quot;}

### Vorgeschlagene Werte für `producedBy` {#producedBy}

In der folgenden Tabelle sind einige für `producedBy`:

| Wert | Definition |
| --- | --- |
| `self` | Selbst |
| `system` | System |
| `salesRef` | Vertriebsmitarbeiter |
| `customerRep` | Kundenbetreuer |
