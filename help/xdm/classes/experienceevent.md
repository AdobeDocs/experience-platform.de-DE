---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;Felder;schemas;Schemas;Schemata;identityMap;IdentityMap;Identitätszuordnung;Schema-Design;map;Map;Zuordnung;event modeling;Ereignismodellierung;Best Practices;Ereignis;Ereignisse;
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
description: Dieses Dokument enthält einen Überblick über die XDM ExperienceEvent-Klasse und Best Practices für die Modellierung von Ereignisdaten.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 95%

---

# [!DNL XDM ExperienceEvent]-Klasse:

[!DNL XDM ExperienceEvent] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, mit der Sie einen mit einem Zeitstempel versehenen Schnappschuss des Systems erstellen können, wenn ein bestimmtes Ereignis auftritt oder eine Reihe von Bedingungen erfüllt worden sind.

Ein Erlebnisereignis ist eine Aufzeichnung des Geschehens in Form von Fakten, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignisse können entweder explizit (direkt beobachtbare menschliche Aktionen) oder implizit (ohne direkte menschliche Aktion ausgelöst) sein und werden ohne Aggregation oder Interpretation aufgezeichnet. Weitere wichtige Informationen zur Verwendung dieser Klasse im Platform-Ökosystem finden Sie im Abschnitt [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent]-Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Zwei dieser Felder (`_id` und `timestamp`) **erforderlich** für alle Schemas, die auf der Klasse basieren, während der Rest optional ist. Die Werte einiger Felder werden bei der Datenerfassung automatisch ausgefüllt.

![Die Struktur von XDM ExperienceEvent, wie sie in der Platform-Benutzeroberfläche angezeigt wird](../images/classes/experienceevent/structure.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id`<br>**(Erforderlich)** | Eine eindeutige Zeichenfolgenkennung für das Ereignis. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Ereignisses nachzuverfolgen, Doppelungen von Daten zu verhindern und dieses Ereignis bei nachgelagerten Services nachzuschlagen. In einigen Fällen kann `_id` ein [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder ein [Globally Unique Identifier (GUID)](https://docs.microsoft.com/de-de/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei erfassen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern miteinander verknüpfen, die das Ereignis eindeutig machen, z. B. eine primäre ID, einen Zeitstempel, einen Ereignistyp usw. Der verkettete Wert muss eine formatierte Zeichenfolge des Typs `uri-reference` sein, was bedeutet, dass alle Doppelpunkt-Zeichen entfernt werden müssen. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu erkennen, dass **dieses Feld keine Identität repräsentiert, die mit einer Person in Verbindung steht**, sondern den Datensatz an sich. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) relegiert werden, die von kompatiblen Feldergruppen bereitgestellt werden. |
| `eventMergeId` | Wenn Sie [Adobe Experience Platform Web SDK](../../edge/home.md) verwenden, um Daten aufzunehmen, stellt dies die ID des erfassten Batches dar, der zur Erstellung des Datensatzes geführt hat. Dieses Feld wird bei der Datenaufnahme automatisch vom System ausgefüllt. Die Verwendung dieses Felds außerhalb des Kontexts einer Web SDK-Implementierung wird nicht unterstützt. |
| `eventType` | Eine Zeichenfolge, die den Typ oder die Kategorie des Ereignisses angibt. Dieses Feld kann verwendet werden, wenn Sie innerhalb desselben Schemas und Datensatzes eine Unterscheidung zwischen verschiedenen Ereignistypen treffen möchten, z. B. eine Unterscheidung zwischen einem Produktansichtsereignis und einem Zum-Einkaufskorb-Hinzufügen-Ereignis bei einem Einzelhandelsunternehmen.<br><br>Standardwerte für diese Eigenschaft sind im [Anhang](#eventType) zusammen mit Beschreibungen des vorgesehenen Anwendungsfalls angegeben. Dieses Feld ist eine erweiterbare Aufzählung, d. h. Sie können auch eigene Ereignistyp-Zeichenfolgen verwenden, um die Ereignisse, die Sie nachverfolgen, zu kategorisieren.<br><br>`eventType` beschränkt Sie auf die Verwendung nur eines einzigen Ereignisses pro Treffer in Ihrem Programm. Daher müssen Sie berechnete Felder verwenden, um dem System mitzuteilen, welches Ereignis am wichtigsten ist. Weitere Informationen finden Sie im Abschnitt zu [Best Practices für berechnete Felder](#calculated). |
| `producedBy` | Ein Zeichenfolge-Wert, der den Verursacher oder Ursprung des Ereignisses beschreibt. Dieses Feld kann verwendet werden, um bestimmte Ereignisverursacher bei Bedarf für Segmentierungszwecke herauszufiltern.<br><br>Einige empfohlene Werte für diese Eigenschaft sind im [Anhang](#producedBy) angegeben. Dieses Feld ist eine erweiterbare Aufzählung, d. h. Sie können auch eigene Zeichenfolgen verwenden, um verschiedene Ereignisverursacher darzustellen. |
| `identityMap` | Ein Verknüpfungsfeld, das einen Satz von Identitäten mit Namespace für die Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Um dieses Feld ordnungsgemäß zu verwenden, verwenden Sie [Echtzeit-Kundenprofil](../../profile/home.md)versuchen Sie nicht, den Inhalt des Felds in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Siehe Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `timestamp`<br>**(Erforderlich)** | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß [RFC 3339 Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Dieser Zeitstempel muss in der Vergangenheit erfolgt sein. Best Practices zur Verwendung dieses Feldes finden Sie im nachstehenden Abschnitt [Zeitstempel](#timestamps). |

{style="table-layout:auto"}

## Best Practices für die Ereignismodellierung

In den folgenden Abschnitten finden Sie Best Practices zum Entwerfen Ihrer ereignisbasierten Experience-Datenmodell (XDM)-Schemata in Adobe Experience Platform.

### Zeitstempel {#timestamps}

Das `timestamp`-Feld im Stamm eines Ereignisschemas kann **nur** die Beobachtung des Ereignisses an sich repräsentieren und muss in der Vergangenheit liegen. Wenn Ihre Segmentierungsanwendungsfälle die Verwendung von Zeitstempeln erfordern, die in Zukunft auftreten können, müssen diese Werte an einer anderen Stelle im Erlebnisereignis-Schema eingeschränkt werden.

Beispiel: Wenn ein Unternehmen des Reise- und Beherbergungsgewerbes ein Flugreservierungsereignis modelliert, gibt das `timestamp`-Feld auf Klassenebene den Zeitpunkt an, zu dem das Reservierungsereignis beobachtet wurde. Andere Zeitstempel, die mit dem Ereignis in Verbindung stehen, wie z. B. das Startdatum der Reisereservierung, sollten in separaten Feldern erfasst werden, die von standardmäßigen oder benutzerdefinierten Feldergruppen bereitgestellt werden.

![Ein Beispiel für ein Erlebnisereignis-Schema mit hervorgehobenem Flugreservierungs- und Startdatum.](../images/classes/experienceevent/timestamps.png)

Indem Sie den Zeitstempel auf Klassenebene von anderen zugehörigen Datums-/Zeitwerten in Ihren Ereignisschemata trennen, können Sie flexible Anwendungsfälle für die Segmentierung implementieren und gleichzeitig ein Kundenkonto mit Zeitstempel in Ihrem Erlebnisprogramm beibehalten.

### Verwenden berechneter Felder {#calculated}

Bestimmte Interaktionen in Ihren Erlebnisprogrammen können zu mehreren verwandten Ereignissen führen, die technisch denselben Ereigniszeitstempel aufweisen und daher als ein Ereignisdatensatz dargestellt werden. Wenn ein Kunde beispielsweise ein Produkt auf Ihrer Website ansieht, kann dies zu einem Ereignisdatensatz führen, der zwei potenzielle `eventType`-Werte hat: ein „Produktansicht“-Ereignis (`commerce.productViews`) oder ein generisches „Seitenansicht“-Ereignis (`web.webpagedetails.pageViews`). In diesen Fällen können Sie berechnete Felder verwenden, um die wichtigsten Attribute zu erfassen, wenn mehrere Ereignisse in einem Treffer erfasst werden.

[Adobe Experience Platform-Datenvorbereitung](../../data-prep/home.md) ermöglicht die Zuordnung, Umwandlung und Validierung von Daten zu und von XDM. Mithilfe der verfügbaren [Zuordnungsfunktionen](../../data-prep/functions.md), die vom Service bereitgestellt werden, können Sie logische Operatoren aufrufen, um Daten aus Datensätzen mit mehreren Ereignissen zu priorisieren, umzuwandeln und/oder zu konsolidieren, wenn sie in Experience Platform aufgenommen werden. Im obigen Beispiel könnten Sie `eventType` als berechnetes Feld festlegen, das eine „Produktansicht“ gegenüber einer „Seitenansicht“ priorisiert, wenn beide auftreten.

Wenn Sie Daten manuell über die UI in Platform erfassen, finden Sie das Handbuch unter [berechnete Felder](../../data-prep/ui/mapping.md#calculated-fields) spezifische Schritte zur Erstellung berechneter Felder.

Wenn Sie Daten mithilfe einer Quellverbindung an Platform streamen, können Sie die Quelle so konfigurieren, dass stattdessen berechnete Felder verwendet werden. In der [Dokumentation zu Ihrer jeweiligen Quelle](../../sources/home.md) finden Sie Anweisungen zur Implementierung berechneter Felder beim Konfigurieren der Verbindung.

## Kompatible Schemafeldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../field-groups/name-updates.md).

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM ExperienceEvent]-Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Bilanzübertragungen]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Kampagnen-Marketing-Details]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Kartenaktionen]](../field-groups/event/card-actions.md)
* [[!UICONTROL Kanaldetails]](../field-groups/event/channel-details.md)
* [[!UICONTROL Handelsdetails]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Einlagendetails]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Details zum Gerätehandel]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Restaurantreservierung]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Details zur Endbenutzer-ID]](../field-groups/event/enduserids.md)
* [[!UICONTROL Umgebungsdetails]](../field-groups/event/environment-details.md)
* [[!UICONTROL Flugreservierung]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0-Einverständnis]](../field-groups/event/iab.md)
* [[!UICONTROL Unterkunftsreservierung]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Preisanfragedetails]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservierungsdetails]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web-Details]](../field-groups/event/web-details.md)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zur [!UICONTROL XDM ExperienceEvent]-Klasse.

### Akzeptierte Werte für `eventType` {#eventType}

In der folgenden Tabelle sind die akzeptierten Werte für `eventType` zusammen mit ihren Definitionen aufgeführt:

| Wert | Definition |
| --- | --- |
| `advertising.clicks` | Klicken Sie auf Aktion(en) in einer Anzeige. |
| `advertising.completes` | Ein zeitgesteuertes Medienelement wurde bis zum Ende angesehen. Dies bedeutet nicht zwangsläufig, dass der Betrachter das gesamte Video angesehen hat, denn er könnte auch Teile übersprungen haben. |
| `advertising.conversions` | Vordefinierte Aktion(en), die von einem Kunden ausgeführt werden und ein Ereignis zur Leistungsbewertung auslösen. |
| `advertising.federated` | Gibt an, ob ein Erlebnisereignis über eine Datenverknüpfung (Datenfreigabe zwischen Kunden) erstellt wurde. |
| `advertising.firstQuartiles` | Eine digitale Videoanzeige hat 25 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.impressions` | Impression(s) einer Anzeige für einen Kunden mit dem Potenzial, angezeigt zu werden. |
| `advertising.midpoints` | Eine digitale Videoanzeige wurde für 50 % ihrer Dauer mit normaler Geschwindigkeit abgespielt. |
| `advertising.starts` | Die Wiedergabe einer digitalen Videoanzeige hat begonnen. |
| `advertising.thirdQuartiles` | Eine digitale Videoanzeige wurde für 75 % ihrer Dauer mit normaler Geschwindigkeit abgespielt. |
| `advertising.timePlayed` | Die Zeit in Sekunden, die ein Benutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbracht hat. |
| `application.close` | Ein Programm wurde geschlossen oder in den Hintergrund gestellt. |
| `application.launch` | Ein Programm wurde gestartet oder in den Vordergrund geholt. |
| `commerce.checkouts` | Für eine Produktliste ist ein Checkout-Ereignis aufgetreten. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden der Zeitstempel und die referenzierte Seite/das referenzierte Erlebnis für jedes Ereignis verwendet, um jedes einzelne Ereignis (Schritt) zu identifizieren, das in der angegebenen Reihenfolge dargestellt wird. |
| `commerce.productListAdds` | Ein Produkt wurde zur Produktliste oder zum Warenkorb hinzugefügt. |
| `commerce.productListOpens` | Eine neue Produktliste (Warenkorb) wurde initialisiert oder erstellt. |
| `commerce.productListRemovals` | Ein oder mehrere Produkteinträge wurden aus einer Produktliste oder einem Warenkorb entfernt. |
| `commerce.productListReopens` | Eine Produktliste (Warenkorb), auf die nicht mehr zugegriffen werden konnte (verworfen), wurde von einem Kunden erneut aktiviert, z. B. über eine Remarketing-Aktivität. |
| `commerce.productListViews` | Eine Produktliste oder ein Warenkorb hat eine oder mehrere Ansichten erhalten. |
| `commerce.productViews` | Ein Produkt hat eine oder mehrere Ansichten erhalten. |
| `commerce.purchases` | Eine Bestellung wurde angenommen. Die ist die einzige erforderliche Aktion bei einer Handelskonversion. Für ein Kaufereignis muss eine Produktliste angegeben sein. |
| `commerce.saveForLaters` | Eine Produktliste wurde für die zukünftige Verwendung gespeichert, z. B. eine Produkt-Wunschliste. |
| `decisioning.propositionDisplay` | Ein Entscheidungsvorschlag wurde einer Person angezeigt. |
| `decisioning.propositionInteract` | Eine Person hat mit einem Entscheidungsvorschlag interagiert. |
| `delivery.feedback` | Feedback-Ereignisse für eine Lieferung, z. B. ein E-Mail-Versand. |
| `directMarketing.emailBounced` | Eine E-Mail an eine Person ist fehlgeschlagen. |
| `directMarketing.emailBouncedSoft` | Eine E-Mail an eine Person mit Softbounce. |
| `directMarketing.emailClicked` | Eine Person hat auf einen Link in einer Marketing-E-Mail geklickt. |
| `directMarketing.emailDelivered` | Eine E-Mail wurde dem E-Mail-Service einer Person erfolgreich zugestellt |
| `directMarketing.emailOpened` | Eine Person hat eine Marketing-E-Mail geöffnet. |
| `directMarketing.emailUnsubscribed` | Eine Person hat sich von einer Marketing-E-Mail abgemeldet. |
| `inappmessageTracking.dismiss` | Eine In-App-Nachricht wurde abgelehnt. |
| `inappmessageTracking.display` | Eine In-App-Nachricht wurde angezeigt. |
| `inappmessageTracking.interact` | Mit einer In-App-Nachricht wurde interagiert. |
| `leadOperation.callWebhook` | Als Reaktion auf einen Lead wurde ein Webhook aufgerufen. |
| `leadOperation.convertLead` | Ein Lead wurde konvertiert. |
| `leadOperation.interestingMoment` | Für eine Person wurde ein interessanter Moment aufgezeichnet. |
| `leadOperation.newLead` | Ein Lead wurde erstellt. |
| `leadOperation.scoreChanged` | Der Wert des Score-Attributs des Leads wurde geändert. |
| `leadOperation.statusInCampaignProgressionChanged` | Der Status eines Leads in einer Kampagne hat sich geändert. |
| `listOperation.addToList` | Eine Person wurde einer Marketing-Liste hinzugefügt. |
| `listOperation.removeFromList` | Eine Person wurde von einer Marketing-Liste gestrichen. |
| `message.feedback` | Feedback-Ereignisse wie gesendet/Bounce/Fehler für Nachrichten, die an einen Kunden gesendet wurden. |
| `message.tracking` | Tracking von Ereignissen wie Öffnen/Klicken/benutzerdefinierte Aktionen bei Nachrichten, die an einen Kunden gesendet wurden. |
| `opportunityEvent.addToOpportunity` | Eine Person wurde zu einer Opportunity hinzugefügt. |
| `opportunityEvent.opportunityUpdated` | Eine Opportunity wurde aktualisiert. |
| `opportunityEvent.removeFromOpportunity` | Eine Person wurde aus einer Opportunity entfernt. |
| `pushTracking.applicationOpened` | Eine Person hat aus einer Push-Benachrichtigung heraus ein Programm geöffnet. |
| `pushTracking.customAction` | Eine Person hat in einer Push-Benachrichtigung auf eine benutzerdefinierte Aktion geklickt. |
| `web.formFilledOut` | Eine Person hat ein Formular auf einer Web-Seite ausgefüllt. |
| `web.webinteraction.linkClicks` | Ein Link wurde mindestens einmal ausgewählt. |
| `web.webpagedetails.pageViews` | Eine Web-Seite wurde mindestens einmal besucht. |

{style="table-layout:auto"}

### Vorgeschlagene Werte für `producedBy` {#producedBy}

In der folgenden Tabelle sind einige akzeptierte Werte für `producedBy` angegeben:

| Wert | Definition |
| --- | --- |
| `self` | Selbst |
| `system` | System |
| `salesRef` | Vertriebsmitarbeiter |
| `customerRep` | Kundenbetreuer |
