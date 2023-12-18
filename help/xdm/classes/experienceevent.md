---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;Felder;schemas;Schemas;Schemata;identityMap;IdentityMap;Identitätszuordnung;Schema-Design;map;Map;Zuordnung;event modeling;Ereignismodellierung;Best Practices;Ereignis;Ereignisse;
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
description: Erfahren Sie mehr über die XDM ExperienceEvent-Klasse und Best Practices für die Modellierung von Ereignisdaten.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '2659'
ht-degree: 43%

---

# [!DNL XDM ExperienceEvent]-Klasse:

[!DNL XDM ExperienceEvent] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, mit der Sie einen mit einem Zeitstempel versehenen Schnappschuss des Systems erstellen können, wenn ein bestimmtes Ereignis auftritt oder eine Reihe von Bedingungen erfüllt worden sind.

Ein Erlebnisereignis ist eine Aufzeichnung des Geschehens in Form von Fakten, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignisse können entweder explizit (direkt beobachtbare menschliche Aktionen) oder implizit (ohne direkte menschliche Aktion ausgelöst) sein und werden ohne Aggregation oder Interpretation aufgezeichnet. Weitere wichtige Informationen zur Verwendung dieser Klasse im Platform-Ökosystem finden Sie im Abschnitt [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent]-Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Zwei dieser Felder (`_id` und `timestamp`) **erforderlich** für alle Schemas, die auf der Klasse basieren, während der Rest optional ist. Die Werte einiger Felder werden bei der Datenerfassung automatisch ausgefüllt.

![Die Struktur von XDM ExperienceEvent, wie sie in der Platform-Benutzeroberfläche angezeigt wird](../images/classes/experienceevent/structure.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id`<br>**(Erforderlich)** | Die Experience Event-Klasse `_id` identifiziert einzelne Ereignisse, die in Adobe Experience Platform erfasst werden. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Ereignisses zu verfolgen, Datendoppelungen zu verhindern und dieses Ereignis in nachgelagerten Diensten nachzuschlagen.<br><br>Wenn doppelte Ereignisse erkannt werden, können Platform-Anwendungen und -Dienste die Duplizierung unterschiedlich handhaben. Beispielsweise werden doppelte Ereignisse im Profildienst abgelegt, wenn das Ereignis mit demselben `_id` bereits im Profilspeicher vorhanden ist.<br><br>In einigen Fällen `_id` kann ein [Universally Unique Identifier (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) oder [Globally Unique Identifier (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei aufnehmen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern miteinander verknüpfen, die das Ereignis eindeutig machen. Beispiele für Ereignisse, die verkettet werden können, sind die primäre ID, der Zeitstempel, der Ereignistyp usw. Der verkettete Wert muss eine formatierte Zeichenfolge des Typs `uri-reference` sein, was bedeutet, dass alle Doppelpunkt-Zeichen entfernt werden müssen. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu erkennen, dass **dieses Feld keine Identität repräsentiert, die mit einer Person in Verbindung steht**, sondern den Datensatz an sich. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) relegiert werden, die von kompatiblen Feldergruppen bereitgestellt werden. |
| `eventMergeId` | Wenn Sie [Adobe Experience Platform Web SDK](../../edge/home.md) verwenden, um Daten aufzunehmen, stellt dies die ID des erfassten Batches dar, der zur Erstellung des Datensatzes geführt hat. Dieses Feld wird bei der Datenaufnahme automatisch vom System ausgefüllt. Die Verwendung dieses Felds außerhalb des Kontexts einer Web SDK-Implementierung wird nicht unterstützt. |
| `eventType` | Eine Zeichenfolge, die den Typ oder die Kategorie des Ereignisses angibt. Dieses Feld kann verwendet werden, wenn Sie innerhalb desselben Schemas und Datensatzes eine Unterscheidung zwischen verschiedenen Ereignistypen treffen möchten, z. B. eine Unterscheidung zwischen einem Produktansichtsereignis und einem Zum-Einkaufskorb-Hinzufügen-Ereignis bei einem Einzelhandelsunternehmen.<br><br>Standardwerte für diese Eigenschaft sind im [Anhang](#eventType) zusammen mit Beschreibungen des vorgesehenen Anwendungsfalls angegeben. Dieses Feld ist eine erweiterbare Aufzählung, d. h. Sie können auch eigene Ereignistyp-Zeichenfolgen verwenden, um die Ereignisse, die Sie nachverfolgen, zu kategorisieren.<br><br>`eventType` beschränkt Sie auf die Verwendung nur eines einzigen Ereignisses pro Treffer in Ihrem Programm. Daher müssen Sie berechnete Felder verwenden, um dem System mitzuteilen, welches Ereignis am wichtigsten ist. Weitere Informationen finden Sie im Abschnitt zu [Best Practices für berechnete Felder](#calculated). |
| `producedBy` | Ein Zeichenfolge-Wert, der den Verursacher oder Ursprung des Ereignisses beschreibt. Dieses Feld kann verwendet werden, um bestimmte Ereignisverursacher bei Bedarf für Segmentierungszwecke herauszufiltern.<br><br>Einige empfohlene Werte für diese Eigenschaft sind im [Anhang](#producedBy) angegeben. Dieses Feld ist eine erweiterbare Aufzählung, d. h. Sie können auch eigene Zeichenfolgen verwenden, um verschiedene Ereignisverursacher darzustellen. |
| `identityMap` | Ein Verknüpfungsfeld, das einen Satz von Identitäten mit Namespace für die Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Um dieses Feld ordnungsgemäß zu verwenden, verwenden Sie [Echtzeit-Kundenprofil](../../profile/home.md)versuchen Sie nicht, den Inhalt des Felds in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Siehe Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `timestamp`<br>**(Erforderlich)** | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß [RFC 3339 Abschnitt 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Dieser Zeitstempel muss in der Vergangenheit erfolgt sein. Best Practices zur Verwendung dieses Feldes finden Sie im nachstehenden Abschnitt [Zeitstempel](#timestamps). |

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
* [[!UICONTROL Details zur MediaAnalytics-Interaktion]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Anführungsanfragedetails]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservierungsdetails]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web-Details]](../field-groups/event/web-details.md)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zur [!UICONTROL XDM ExperienceEvent]-Klasse.

### Akzeptierte Werte für `eventType` {#eventType}

In der folgenden Tabelle sind die akzeptierten Werte für `eventType` zusammen mit ihren Definitionen aufgeführt:

| Wert | Definition |
| --- | --- |
| `advertising.clicks` | Dieses Ereignis verfolgt, wann eine Aktion zur Auswahl einer Anzeige auftritt. |
| `advertising.completes` | Dieses Ereignis verfolgt, wann ein zeitgesteuertes Medien-Asset bis zum Ende angesehen wurde. Das bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat, da der Betrachter voraus hätte überspringen können. |
| `advertising.conversions` | Dieses Ereignis verfolgt eine vordefinierte Aktion, die von einem Kunden ausgeführt wird, der ein Ereignis zur Leistungsbewertung Trigger. |
| `advertising.federated` | Mit diesem Ereignis wird verfolgt, ob ein Erlebnisereignis über eine Datenverknüpfung (Datenfreigabe zwischen Kunden) erstellt wurde. |
| `advertising.firstQuartiles` | Dieses Ereignis verfolgt, wenn eine digitale Videoanzeige 25 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben hat. |
| `advertising.impressions` | Dieses Ereignis verfolgt die Impressionen einer Anzeige für einen Kunden mit dem Potenzial, angezeigt zu werden. |
| `advertising.midpoints` | Dieses Ereignis verfolgt, wenn eine digitale Videoanzeige 50 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben hat. |
| `advertising.starts` | Dieses Ereignis verfolgt, wann die Wiedergabe einer digitalen Videoanzeige gestartet wurde. |
| `advertising.thirdQuartiles` | Dieses Ereignis verfolgt, wenn eine digitale Videoanzeige 75 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben hat. |
| `advertising.timePlayed` | Dieses Ereignis verfolgt die Zeit, die ein Benutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbringt. |
| `application.close` | Dieses Ereignis verfolgt, wann eine Anwendung geschlossen oder in den Hintergrund gesendet wurde. |
| `application.launch` | Dieses Ereignis verfolgt, wann eine Anwendung gestartet oder in den Vordergrund gestellt wurde. |
| `commerce.backofficeCreditMemoIssued` | Dieses Ereignis verfolgt, wenn einem Kunden eine Kreditmeldung erteilt wurde. |
| `commerce.backofficeOrderCancelled` | Dieses Ereignis verfolgt, wann ein zuvor initiierter Kaufprozess vor Abschluss beendet wurde. |
| `commerce.backofficeOrderItemsShipped` | Mit diesem Ereignis wird verfolgt, wann die gekauften Artikel physisch an den Kunden versandt wurden. |
| `commerce.backofficeOrderPlaced` | Dieses Ereignis verfolgt die Platzierung einer Bestellung. |
| `commerce.backofficeShipmentCompleted` | Diese Veranstaltung verfolgt den erfolgreichen Abschluss des gesamten Versandprozesses. |
| `commerce.checkouts` | Dieses Ereignis verfolgt, wenn ein Checkout-Ereignis für eine Produktliste aufgetreten ist. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden der Zeitstempel und die referenzierte Seite/das referenzierte Erlebnis für jedes Ereignis verwendet, um jedes einzelne Ereignis (Schritt) zu identifizieren, das in der angegebenen Reihenfolge dargestellt wird. |
| `commerce.productListAdds` | Dieses Ereignis verfolgt, wann ein Produkt zur Produktliste oder zum Warenkorb hinzugefügt wurde. |
| `commerce.productListOpens` | Dieses Ereignis verfolgt, wann eine neue Produktliste (Warenkorb) initialisiert oder erstellt wurde. |
| `commerce.productListRemovals` | Dieses Ereignis verfolgt, wenn ein Produkteintrag aus einer Produktliste oder einem Warenkorb entfernt wurde. |
| `commerce.productListReopens` | Dieses Ereignis verfolgt, wenn eine Produktliste (Warenkorb), auf die nicht mehr zugegriffen werden konnte (abgebrochen), von einem Kunden reaktiviert wurde, z. B. über eine Remarketing-Aktivität. |
| `commerce.productListViews` | Dieses Ereignis verfolgt, wenn eine Produktliste oder ein Warenkorb eine Ansicht erhalten hat. |
| `commerce.productViews` | Dieses Ereignis verfolgt, wenn ein Produkt eine oder mehrere Ansichten erhalten hat. |
| `commerce.purchases` | Dieses Ereignis verfolgt, wann eine Bestellung akzeptiert wurde. Die ist die einzige erforderliche Aktion bei einer Handelskonversion. Für ein Kaufereignis muss eine Produktliste angegeben sein. |
| `commerce.saveForLaters` | Dieses Ereignis verfolgt, wann eine Produktliste zur zukünftigen Verwendung gespeichert wurde, wie z. B. eine ProduktWunschliste. |
| `decisioning.propositionDisplay` | Dieses Ereignis verfolgt, wann einer Person ein Entscheidungsvorschlag angezeigt wurde. |
| `decisioning.propositionDismiss` | Dieses Ereignis verfolgt, wenn entschieden wurde, das unterbreitete Angebot nicht zu beeinflussen. |
| `decisioning.propositionInteract` | Dieses Ereignis verfolgt, wann eine Person mit einem Entscheidungsvorschlag interagiert hat. |
| `decisioning.propositionSend` | Dieses Ereignis verfolgt, wann entschieden wurde, eine Empfehlung oder ein Angebot zur Prüfung an einen potenziellen Kunden zu senden. |
| `decisioning.propositionTrigger` | Dieses Ereignis verfolgt die Aktivierung eines Vorschlags-Prozesses. Es ist eine bestimmte Bedingung oder Aktion aufgetreten, um die Vorlage eines Angebots zu ermuntern. |
| `delivery.feedback` | Dieses Ereignis verfolgt Feedback-Ereignisse für einen Versand, z. B. einen E-Mail-Versand. |
| `directMarketing.emailBounced` | Dieses Ereignis verfolgt, wann eine E-Mail an eine Person abgestürzt ist. |
| `directMarketing.emailBouncedSoft` | Dieses Ereignis verfolgt, wenn eine E-Mail an eine Person mit Softbounce gesendet wird. |
| `directMarketing.emailClicked` | Dieses Ereignis verfolgt, wenn eine Person auf einen Link in einer Marketing-E-Mail klickt. |
| `directMarketing.emailDelivered` | Dieses Ereignis verfolgt, wann eine E-Mail erfolgreich an den E-Mail-Dienst einer Person gesendet wurde. |
| `directMarketing.emailOpened` | Dieses Ereignis verfolgt, wann eine Person eine Marketing-E-Mail geöffnet hat. |
| `directMarketing.emailSent` | Dieses Ereignis verfolgt, wann eine Marketing-E-Mail an eine Person gesendet wurde. |
| `directMarketing.emailUnsubscribed` | Dieses Ereignis verfolgt, wenn sich eine Person von einer Marketing-E-Mail abgemeldet hat. |
| `inappmessageTracking.dismiss` | Dieses Ereignis verfolgt, wann eine In-App-Nachricht verworfen wurde. |
| `inappmessageTracking.display` | Dieses Ereignis verfolgt, wann eine In-App-Nachricht angezeigt wurde. |
| `inappmessageTracking.interact` | Dieses Ereignis verfolgt, wann mit einer In-App-Nachricht interagiert wurde. |
| `leadOperation.callWebhook` | Dieses Ereignis verfolgt, wann ein Webhook als Reaktion auf einen Lead aufgerufen wurde. |
| `leadOperation.changeCampaignStream` | Dieses Ereignis bedeutet eine Veränderung in der Marketing- oder Interaktionsstrategie für einen bestimmten geschäftlichen Lead. |
| `leadOperation.changeEngagementCampaignCadence` | Dieses Ereignis verfolgt, wann sich die Interaktion eines Leads im Rahmen einer Kampagne geändert hat. |
| `leadOperation.convertLead` | Dieses Ereignis verfolgt, wann ein Lead konvertiert wurde. |
| `leadOperation.interestingMoment` | Diese Veranstaltung verfolgt, wann ein interessanter Moment für eine Person aufgezeichnet wurde. |
| `leadOperation.mergeLeads` | Dieses Ereignis verfolgt, wann Informationen aus mehreren Leads, die auf dieselbe Entität verweisen, konsolidiert wurden. |
| `leadOperation.newLead` | Dieses Ereignis verfolgt, wann ein Lead erstellt wurde. |
| `leadOperation.scoreChanged` | Dieses Ereignis verfolgt, wann der Wert des Ergebnisattributs des Leads geändert wurde. |
| `leadOperation.statusInCampaignProgressionChanged` | Dieses Ereignis verfolgt, wann sich der Status eines Leads in einer Kampagne geändert hat. |
| `listOperation.addToList` | Dieses Ereignis verfolgt, wann eine Person zu einer Marketing-Liste hinzugefügt wurde. |
| `listOperation.removeFromList` | Dieses Ereignis verfolgt, wann eine Person aus einer Marketing-Liste entfernt wurde. |
| `media.adBreakComplete` | Dieses Ereignis verfolgt, wenn eine `adBreakComplete` -Ereignis aufgetreten ist. Dieses Ereignis wird zu Beginn einer Werbeunterbrechung ausgelöst. |
| `media.adBreakStart` | Dieses Ereignis verfolgt, wenn eine `adBreakStart` -Ereignis aufgetreten ist. Dieses Ereignis wird am Ende einer Werbeunterbrechung ausgelöst. |
| `media.adComplete` | Dieses Ereignis verfolgt, wenn eine `adComplete` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn eine Anzeige abgeschlossen ist. |
| `media.adSkip` | Dieses Ereignis verfolgt, wenn eine `adSkip` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn eine Anzeige übersprungen wurde. |
| `media.adStart` | Dieses Ereignis verfolgt, wenn eine `adStart` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn eine Anzeige begonnen hat. |
| `media.bitrateChange` | Dieses Ereignis verfolgt, wenn ein `bitrateChange` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn sich die Bitrate ändert. |
| `media.bufferStart` | Dieses Ereignis verfolgt, wenn ein `bufferStart` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn die Pufferung von Medien begonnen hat. |
| `media.chapterComplete` | Dieses Ereignis verfolgt, wenn ein `chapterComplete` -Ereignis aufgetreten ist. Dieses Ereignis wird nach Abschluss eines Medienkapitels ausgelöst. |
| `media.chapterSkip` | Dieses Ereignis verfolgt, wenn ein `chapterSkip` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn ein Benutzer einen vorwärts- oder rückwärts zu einem anderen Abschnitt oder Kapitel im Medieninhalt springt. |
| `media.chapterStart` | Dieses Ereignis verfolgt, wenn ein `chapterStart` -Ereignis aufgetreten ist. Dieses Ereignis wird zu Beginn eines bestimmten Abschnitts oder Kapitels im Medieninhalt ausgelöst. |
| `media.downloaded` | Dieses Ereignis verfolgt, wann Medien heruntergeladene Inhalte aufgetreten sind. |
| `media.error` | Dieses Ereignis verfolgt, wenn eine `error` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn während der Medienwiedergabe ein Fehler oder Problem auftritt. |
| `media.pauseStart` | Dieses Ereignis verfolgt, wenn ein `pauseStart` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn ein Benutzer eine Pause in der Medienwiedergabe initiiert. |
| `media.ping` | Dieses Ereignis verfolgt, wenn eine `ping` -Ereignis aufgetreten ist. Dadurch wird die Verfügbarkeit einer Medienressource überprüft. |
| `media.play` | Dieses Ereignis verfolgt, wenn ein `play` -Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn der Medieninhalt wiedergegeben wird, was auf die aktive Nutzung durch den Benutzer hinweist. |
| `media.sessionComplete` | Dieses Ereignis verfolgt, wenn ein `sessionComplete` -Ereignis aufgetreten ist. Dieses Ereignis markiert das Ende einer Medienwiedergabesitzung. |
| `media.sessionEnd` | Dieses Ereignis verfolgt, wenn ein `sessionEnd` -Ereignis aufgetreten ist. Dieses Ereignis gibt den Abschluss einer Mediensitzung an. Zu diesem Schluss kann das Schließen des Medienplayers oder das Beenden der Wiedergabe gehören. |
| `media.sessionStart` | Dieses Ereignis verfolgt, wenn ein `sessionStart` -Ereignis aufgetreten ist. Dieses Ereignis markiert den Anfang einer Medienwiedergabesitzung. Sie wird ausgelöst, wenn ein Benutzer mit der Wiedergabe einer Mediendatei beginnt. |
| `media.statesUpdate` | Dieses Ereignis verfolgt, wenn ein `statesUpdate` -Ereignis aufgetreten ist. Die Funktionen für das Player-Status-Tracking können an einen Audio- oder Videostream angehängt werden. Die Standardstatus sind: Vollbild, Stumm, Untertitel, BildinBild und InFokus. |
| `opportunityEvent.addToOpportunity` | Diese Veranstaltung verfolgt, wann eine Person zu einer Gelegenheit hinzugefügt wurde. |
| `opportunityEvent.opportunityUpdated` | Dieses Ereignis verfolgt, wann eine Gelegenheit aktualisiert wurde. |
| `opportunityEvent.removeFromOpportunity` | Dieses Ereignis verfolgt, wann eine Person aus einer Gelegenheit entfernt wurde. |
| `pushTracking.applicationOpened` | Dieses Ereignis verfolgt, wann eine Person eine Anwendung über eine Push-Benachrichtigung geöffnet hat. |
| `pushTracking.customAction` | Dieses Ereignis verfolgt, wann eine Person eine benutzerdefinierte Aktion in einer Push-Benachrichtigung ausgewählt hat. |
| `web.formFilledOut` | Dieses Ereignis verfolgt, wenn eine Person ein Formular auf einer Webseite ausfüllt. |
| `web.webinteraction.linkClicks` | Dieses Ereignis verfolgt, wenn ein Link mindestens einmal ausgewählt wurde. |
| `web.webpagedetails.pageViews` | Dieses Ereignis verfolgt, wenn eine Webseite eine oder mehrere Ansichten erhalten hat. |
| `location.entry` | Dieses Ereignis verfolgt den Eintritt einer Person oder eines Geräts an einem bestimmten Ort. |
| `location.exit` | Dieses Ereignis verfolgt den Ausstieg einer Person oder eines Geräts von einem bestimmten Ort aus. |

{style="table-layout:auto"}

### Vorgeschlagene Werte für `producedBy` {#producedBy}

In der folgenden Tabelle sind einige akzeptierte Werte für `producedBy` angegeben:

| Wert | Definition |
| --- | --- |
| `self` | Selbst |
| `system` | System |
| `salesRef` | Vertriebsmitarbeiter |
| `customerRep` | Kundenbetreuer |
