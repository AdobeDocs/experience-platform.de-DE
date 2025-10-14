---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;Felder;schemas;Schemas;Schemata;identityMap;IdentityMap;Identitätszuordnung;Schema-Design;map;Map;Zuordnung;event modeling;Ereignismodellierung;Best Practices;Ereignis;Ereignisse;
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
description: Erfahren Sie mehr über die XDM ExperienceEvent-Klasse und die Best Practices für die Modellierung von Ereignisdaten.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 8aa8a1c42e9656716be746ba447a5f77a8155b4c
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 36%

---

# [!DNL XDM ExperienceEvent]-Klasse:

[!DNL XDM ExperienceEvent] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse. Verwenden Sie diese Klasse, um einen mit einem Zeitstempel versehenen Schnappschuss des Systems zu erstellen, wenn ein bestimmtes Ereignis auftritt oder eine Reihe von Bedingungen erfüllt worden sind.

Ein Erlebnisereignis ist eine Aufzeichnung des Geschehens in Form von Fakten, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignisse können entweder explizit (direkt beobachtbare menschliche Aktionen) oder implizit (ohne direkte menschliche Aktion ausgelöst) sein und werden ohne Aggregation oder Interpretation aufgezeichnet. Weitere wichtige Informationen zur Verwendung dieser Klasse im Experience Platform-Ökosystem finden Sie im Abschnitt [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent]-Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Zwei dieser Felder (`_id` und `timestamp`) sind **erforderlich** für alle Schemata, die auf dieser Klasse basieren, während der Rest optional ist. Die Werte einiger Felder werden bei der Datenaufnahme automatisch ausgefüllt.

![Die Struktur von XDM ExperienceEvent, wie sie in der Experience Platform-Benutzeroberfläche angezeigt wird.](../images/classes/experienceevent/structure.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id`<br>**(erforderlich)** | Das Feld Erlebnisereignisklasse `_id` identifiziert einzelne Ereignisse, die in Adobe Experience Platform aufgenommen werden, eindeutig. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Ereignisses nachzuverfolgen, Doppelungen von Daten zu verhindern und dieses Ereignis bei nachgelagerten Services nachzuschlagen.<br><br>Wenn doppelte Ereignisse erkannt werden, können Experience Platform-Programme und -Services die Duplizierung anders handhaben. Beispielsweise werden doppelte Ereignisse im Profil-Service gelöscht, wenn das Ereignis mit demselben `_id` bereits im Profilspeicher vorhanden ist. Diese Ereignisse werden jedoch weiterhin im Data Lake aufgezeichnet.<br><br>In einigen Fällen kann `_id` ein [Universally Unique Identifier (UUID) &#x200B;](https://datatracker.ietf.org/doc/html/rfc4122) ein [Globally Unique Identifier (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei erfassen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern verketten, die das Ereignis eindeutig machen. Beispiele für verkettete Ereignisse sind primäre ID, Zeitstempel, Ereignistyp usw. Der verkettete Wert muss eine formatierte Zeichenfolge des Typs `uri-reference` sein, was bedeutet, dass alle Doppelpunkt-Zeichen entfernt werden müssen. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu erkennen, dass **dieses Feld keine Identität repräsentiert, die mit einer Person in Verbindung steht**, sondern den Dateneintrag an sich. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) relegiert werden, die von kompatiblen Feldergruppen bereitgestellt werden. |
| `eventMergeId` | Wenn Sie [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) verwenden, um Daten aufzunehmen, stellt dies die ID des erfassten Batches dar, der zur Erstellung des Eintrags geführt hat. Dieses Feld wird bei der Datenaufnahme automatisch vom System ausgefüllt. Die Verwendung dieses Felds außerhalb des Kontexts einer Web SDK-Implementierung wird nicht unterstützt. |
| `eventType` | Eine Zeichenfolge, die den Typ oder die Kategorie des Ereignisses angibt. Dieses Feld kann verwendet werden, wenn Sie innerhalb desselben Schemas und Datensatzes eine Unterscheidung zwischen verschiedenen Ereignistypen treffen möchten, z. B. eine Unterscheidung zwischen einem Produktansichtsereignis und einem Zum-Einkaufskorb-Hinzufügen-Ereignis bei einem Einzelhandelsunternehmen.<br><br>Standardwerte für diese Eigenschaft sind im [Anhang](#eventType) zusammen mit Beschreibungen des vorgesehenen Anwendungsfalls angegeben. Dieses Feld ist eine erweiterbare Aufzählung, d. h. Sie können auch eigene Ereignistyp-Zeichenfolgen verwenden, um die Ereignisse, die Sie nachverfolgen, zu kategorisieren.<br><br>`eventType` beschränkt Sie auf die Verwendung nur eines einzigen Ereignisses pro Treffer in Ihrem Programm. Daher müssen Sie berechnete Felder verwenden, um dem System mitzuteilen, welches Ereignis am wichtigsten ist. Weitere Informationen finden Sie im Abschnitt zu [Best Practices für berechnete Felder](#calculated). |
| `producedBy` | Ein Zeichenfolge-Wert, der den Verursacher oder Ursprung des Ereignisses beschreibt. Dieses Feld kann verwendet werden, um bestimmte Ereignisverursacher bei Bedarf für Segmentierungszwecke herauszufiltern.<br><br>Einige empfohlene Werte für diese Eigenschaft sind im [Anhang](#producedBy) angegeben. Dieses Feld ist eine erweiterbare Aufzählung, d. h. Sie können auch eigene Zeichenfolgen verwenden, um verschiedene Ereignisverursacher darzustellen. |
| `identityMap` | Ein Verknüpfungsfeld, das einen Satz von Identitäten mit Namespace für die Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Um dieses Feld ordnungsgemäß für das [Echtzeit-Kundenprofil](../../profile/home.md) zu verwenden, dürfen Sie nicht versuchen, bei Ihren Datenvorgängen den Inhalt des Felds manuell zu aktualisieren.<br /><br />Siehe Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `timestamp`<br>**(erforderlich)** | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß [RFC 3339 Abschnitt 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Dieser Zeitstempel **muss** in der Vergangenheit erfolgen, **muss** ab 1970. Best Practices zur Verwendung dieses Feldes finden Sie im nachstehenden Abschnitt [Zeitstempel](#timestamps). |

{style="table-layout:auto"}

## Best Practices für die Ereignismodellierung

In den folgenden Abschnitten finden Sie Best Practices zum Entwerfen Ihrer ereignisbasierten Experience-Datenmodell (XDM)-Schemata in Adobe Experience Platform.

### Zeitstempel {#timestamps}

Das `timestamp`-Feld im Stamm eines Ereignisschemas kann **nur** die Beobachtung des Ereignisses an sich repräsentieren und muss in der Vergangenheit liegen. Die Veranstaltung **muss** jedoch ab 1970 stattfinden. Wenn Ihre Segmentierungsanwendungsfälle die Verwendung von Zeitstempeln erfordern, die in Zukunft auftreten können, müssen diese Werte an einer anderen Stelle im Erlebnisereignis-Schema eingeschränkt werden.

Beispiel: Wenn ein Unternehmen des Reise- und Beherbergungsgewerbes ein Flugreservierungsereignis modelliert, gibt das `timestamp`-Feld auf Klassenebene den Zeitpunkt an, zu dem das Reservierungsereignis beobachtet wurde. Andere Zeitstempel, die mit dem Ereignis in Verbindung stehen, wie z. B. das Startdatum der Reisereservierung, sollten in separaten Feldern erfasst werden, die von standardmäßigen oder benutzerdefinierten Feldergruppen bereitgestellt werden.

![Beispiel für ein Erlebnisereignis-Schema mit hervorgehobener Option „Flugreservierung und Startdatum“.](../images/classes/experienceevent/timestamps.png)

Indem Sie den Zeitstempel auf Klassenebene von anderen zugehörigen Datums-/Zeitwerten in Ihren Ereignisschemata trennen, können Sie flexible Anwendungsfälle für die Segmentierung implementieren und gleichzeitig ein Kundenkonto mit Zeitstempel in Ihrem Erlebnisprogramm beibehalten.

### Verwenden berechneter Felder {#calculated}

Bestimmte Interaktionen in Ihren Erlebnisprogrammen können zu mehreren verwandten Ereignissen führen, die technisch denselben Ereigniszeitstempel aufweisen und daher als ein Ereigniseintrag dargestellt werden. Wenn ein Kunde beispielsweise ein Produkt auf Ihrer Website ansieht, kann dies zu einem Ereigniseintrag führen, der zwei potenzielle `eventType`-Werte hat: ein „Produktansicht“-Ereignis (`commerce.productViews`) oder ein generisches „Seitenansicht“-Ereignis (`web.webpagedetails.pageViews`). In diesen Fällen können Sie berechnete Felder verwenden, um die wichtigsten Attribute zu erfassen, wenn mehrere Ereignisse in einem Treffer erfasst werden.

Verwenden Sie die [Adobe Experience Platform](../../data-prep/home.md)Datenvorbereitung, um Daten von und zu XDM zuzuordnen, umzuwandeln und zu validieren. Mithilfe der verfügbaren [Zuordnungsfunktionen](../../data-prep/functions.md), die vom Service bereitgestellt werden, können Sie logische Operatoren aufrufen, um Daten aus Einträgen mit mehreren Ereignissen zu priorisieren, umzuwandeln und/oder zu konsolidieren, wenn sie in Experience Platform aufgenommen werden. Im obigen Beispiel könnten Sie `eventType` als berechnetes Feld festlegen, das eine „Produktansicht“ gegenüber einer „Seitenansicht“ priorisiert, wenn beide auftreten.

Wenn Sie Daten manuell über die Benutzeroberfläche in Experience Platform erfassen, finden Sie das Handbuch unter [Berechnete Felder](../../data-prep/ui/mapping.md#calculated-fields) spezifische Anweisungen zum Erstellen berechneter Felder.

Wenn Sie Daten mithilfe einer Quellverbindung an Experience Platform streamen, können Sie die Quelle so konfigurieren, dass stattdessen berechnete Felder verwendet werden. In der [Dokumentation zu Ihrer jeweiligen Quelle](../../sources/home.md) finden Sie Anweisungen zur Implementierung berechneter Felder beim Konfigurieren der Verbindung.

## Kompatible Schemafeldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../field-groups/name-updates.md).

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM ExperienceEvent]-Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Vollständige Erweiterung für Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]](../field-groups/event/advertising-full-extension.md)
* [[!UICONTROL Saldoübertragungen]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Kampagnen-Marketing-Details]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Kartenaktionen]](../field-groups/event/card-actions.md)
* [[!UICONTROL Kanaldetails]](../field-groups/event/channel-details.md)
* [[!UICONTROL Handelsdetails]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Einzahlungsdetails]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Details zum Gerätehandel]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Restaurantreservierung]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Details zur Endbenutzer-ID]](../field-groups/event/enduserids.md)
* [[!UICONTROL Umgebungsdetails]](../field-groups/event/environment-details.md)
* [[!UICONTROL Flugreservierung]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0-Einverständnis]](../field-groups/event/iab.md)
* [[!UICONTROL Unterkunftsreservierung]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics Interaction-Details]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Details zur Angebotsanfrage]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservierungsdetails]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web-Details]](../field-groups/event/web-details.md)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zur [!UICONTROL XDM ExperienceEvent]-Klasse.

### Akzeptierte Werte für `eventType` {#eventType}

In der folgenden Tabelle sind die akzeptierten Werte für `eventType` zusammen mit ihren Definitionen aufgeführt:

| Wert | Definition |
| --- | --- |
| `advertising.clicks` | Dieses Ereignis verfolgt, wann eine Aktion zur Auswahl einer Anzeige stattfindet. |
| `advertising.completes` | Dieses Ereignis verfolgt, wann ein zeitgesteuertes Medien-Asset bis zum Ende angesehen wurde. Dies bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat, denn er könnte auch vorgesprungen sein. |
| `advertising.conversions` | Dieses Ereignis verfolgt eine vordefinierte Aktion, die von einem Kunden ausgeführt wird, der ein Ereignis zur Leistungsbewertung Trigger. |
| `advertising.federated` | Dieses Ereignis verfolgt, ob ein Erlebnisereignis durch Datenverbund (Datenfreigabe zwischen Kunden) erstellt wurde. |
| `advertising.firstQuartiles` | Dieses Ereignis verfolgt, wann eine digitale Videoanzeige zu 25 % ihrer Dauer mit normaler Geschwindigkeit abgespielt wurde. |
| `advertising.impressions` | Dieses Ereignis verfolgt die Impressionen einer Anzeige bei einem Kunden mit dem Potenzial, angezeigt zu werden. |
| `advertising.midpoints` | Dieses Ereignis verfolgt, wann eine digitale Videoanzeige zu 50 % ihrer Dauer mit normaler Geschwindigkeit abgespielt wurde. |
| `advertising.starts` | Dieses Ereignis verfolgt, wann die Wiedergabe einer digitalen Videoanzeige begonnen hat. |
| `advertising.thirdQuartiles` | Dieses Ereignis verfolgt, wann eine digitale Videoanzeige zu 75 % ihrer Dauer mit normaler Geschwindigkeit abgespielt wurde. |
| `advertising.timePlayed` | Dieses Ereignis verfolgt die Zeit, die ein Benutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbracht hat. |
| `application.close` | Dieses Ereignis verfolgt, wann eine Anwendung geschlossen oder in den Hintergrund gesendet wurde. |
| `application.launch` | Dieses Ereignis verfolgt, wann eine Anwendung gestartet oder in den Vordergrund gebracht wurde. |
| `click` | **Veraltet** Verwenden Sie stattdessen `decisioning.propositionInteract`. |
| `commerce.backofficeCreditMemoIssued` | Dieses Ereignis verfolgt, wann einem Kunden eine Gutschrift ausgestellt wurde. |
| `commerce.backofficeOrderCancelled` | Dieses Ereignis verfolgt, wann ein zuvor initiierter Kaufvorgang vor Abschluss beendet wurde. |
| `commerce.backofficeOrderItemsShipped` | Dieses Ereignis verfolgt, wann die gekauften Artikel physisch an den Kunden gesendet wurden. |
| `commerce.backofficeOrderPlaced` | Dieses Ereignis verfolgt die Platzierung einer Bestellung. |
| `commerce.backofficeShipmentCompleted` | Dieses Ereignis verfolgt den erfolgreichen Abschluss des gesamten Versandprozesses. |
| `commerce.checkouts` | Dieses Ereignis verfolgt, wann ein Checkout-Ereignis für eine Produktliste aufgetreten ist. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden der Zeitstempel und die referenzierte Seite/das referenzierte Erlebnis für jedes Ereignis verwendet, um jedes einzelne Ereignis (Schritt) zu identifizieren, das in der angegebenen Reihenfolge dargestellt wird. |
| `commerce.productListAdds` | Dieses Ereignis verfolgt, wann ein Produkt zur Produktliste oder zum Warenkorb hinzugefügt wurde. |
| `commerce.productListOpens` | Dieses Ereignis verfolgt, wann eine neue Produktliste (Warenkorb) initialisiert oder erstellt wurde. |
| `commerce.productListRemovals` | Dieses Ereignis verfolgt, wann ein Produkteintrag aus einer Produktliste oder einem Warenkorb entfernt wurde. |
| `commerce.productListReopens` | Dieses Ereignis verfolgt, wenn eine Produktliste (Warenkorb), die nicht mehr zugänglich (aufgegeben) war, von einem Kunden reaktiviert wurde, z. B. über eine Remarketing-Aktivität. |
| `commerce.productListViews` | Dieses Ereignis verfolgt, wann eine Produktliste oder ein Warenkorb eine Ansicht erhalten hat. |
| `commerce.productViews` | Dieses Ereignis verfolgt, wann ein Produkt eine oder mehrere Ansichten erhalten hat. |
| `commerce.purchases` | Dieses Ereignis verfolgt, wann eine Bestellung angenommen wurde. Die ist die einzige erforderliche Aktion bei einer Handelskonversion. Für ein Kaufereignis muss eine Produktliste angegeben sein. |
| `commerce.saveForLaters` | Dieses Ereignis verfolgt, wann eine Produktliste für die zukünftige Verwendung gespeichert wurde, z. B. eine Produkt-Wunschliste. |
| `decisioning.propositionDisplay` | Dieses Ereignis wird verwendet, wenn die Web-SDK automatisch Informationen darüber sendet, was auf einer Seite angezeigt wird. Sie benötigen diesen Ereignistyp jedoch nicht, wenn Sie bereits Anzeigeinformationen auf andere Weise einbeziehen, z. B. mit Seitenaufrufen am oberen und unteren Rand. Für Seitenaufrufe am unteren Rand können Sie einen beliebigen Ereignistyp auswählen. |
| `decisioning.propositionDismiss` | Dieser Ereignistyp wird verwendet, wenn eine Adobe Journey Optimizer-interne Nachricht oder Inhaltskarte verworfen wird. |
| `decisioning.propositionFetch` | Wird verwendet, um anzugeben, dass ein Ereignis in erster Linie zum Abrufen der Entscheidung verwendet wird. Adobe Analytics löscht dieses Ereignis automatisch. |
| `decisioning.propositionInteract` | Dieser Ereignistyp wird verwendet, um Interaktionen wie Klicks auf personalisierte Inhalte zu verfolgen. |
| `decisioning.propositionSend` | Diese Veranstaltung verfolgt, wann beschlossen wurde, einem potenziellen Kunden eine Empfehlung oder ein Angebot zur Prüfung zu senden. |
| `decisioning.propositionTrigger` | Ereignisse dieses Typs werden von der [Web-SDK&quot; im lokalen Speicher gespeichert](../../web-sdk/home.md) jedoch nicht an Experience Edge gesendet. Jedes Mal, wenn ein Regelsatz erfüllt wird, wird ein Ereignis generiert und im lokalen Speicher gespeichert (sofern diese Einstellung aktiviert ist). |
| `delivery.feedback` | Dieses Ereignis verfolgt Feedback-Ereignisse für einen Versand, z. B. einen E-Mail-Versand. |
| `directMarketing.emailBounced` | Dieses Ereignis verfolgt, wann eine E-Mail an eine Person gebounct hat. |
| `directMarketing.emailBouncedSoft` | Dieses Ereignis verfolgt, wann eine E-Mail an eine Person Softbounce erzeugt. |
| `directMarketing.emailClicked` | Dieses Ereignis verfolgt, wann eine Person auf einen Link in einer Marketing-E-Mail geklickt hat. |
| `directMarketing.emailDelivered` | Dieses Ereignis verfolgt, wann eine E-Mail erfolgreich an den E-Mail-Service einer Person zugestellt wurde. |
| `directMarketing.emailOpened` | Dieses Ereignis verfolgt, wann eine Person eine Marketing-E-Mail geöffnet hat. |
| `directMarketing.emailSent` | Dieses Ereignis verfolgt, wann eine Marketing-E-Mail an eine Person gesendet wurde. |
| `directMarketing.emailUnsubscribed` | Dieses Ereignis verfolgt, wann eine Person sich von einer Marketing-E-Mail abgemeldet hat. |
| `display` | **Veraltet** Verwenden Sie stattdessen `decisioning.propositionDisplay`. |
| `inappmessageTracking.dismiss` | Dieses Ereignis verfolgt, wann eine In-App-Nachricht abgelehnt wurde. |
| `inappmessageTracking.display` | Dieses Ereignis verfolgt, wann eine In-App-Nachricht angezeigt wurde. |
| `inappmessageTracking.interact` | Dieses Ereignis verfolgt, wann mit einer In-App-Nachricht interagiert wurde. |
| `leadOperation.callWebhook` | Dieses Ereignis verfolgt, wann als Reaktion auf einen Lead ein Webhook aufgerufen wurde. |
| `leadOperation.changeCampaignStream` | Dieses Ereignis bedeutet eine Änderung der Marketing- oder Interaktionsstrategie für einen bestimmten Geschäftsleiter. |
| `leadOperation.changeEngagementCampaignCadence` | Dieses Ereignis verfolgt, wann sich die Häufigkeit der Interaktion eines Leads im Rahmen einer Kampagne geändert hat. |
| `leadOperation.convertLead` | Dieses Ereignis verfolgt, wann ein Lead konvertiert wurde. |
| `leadOperation.interestingMoment` | Dieses Ereignis verfolgt, wann ein interessanter Moment für eine Person aufgezeichnet wurde. |
| `leadOperation.mergeLeads` | Dieses Ereignis verfolgt, wann Informationen von mehreren Leads, die sich auf dieselbe Entität beziehen, konsolidiert wurden. |
| `leadOperation.newLead` | Dieses Ereignis verfolgt, wann ein Lead erstellt wurde. |
| `leadOperation.scoreChanged` | Dieses Ereignis verfolgt, wann der Wert des Score-Attributs des Leads geändert wurde. |
| `leadOperation.statusInCampaignProgressionChanged` | Dieses Ereignis verfolgt, wann sich der Status eines Leads in einer Kampagne geändert hat. |
| `listOperation.addToList` | Dieses Ereignis verfolgt, wann eine Person zu einer Marketing-Liste hinzugefügt wurde. |
| `listOperation.removeFromList` | Dieses Ereignis verfolgt, wann eine Person aus einer Marketing-Liste entfernt wurde. |
| `media.adBreakComplete` | Dieses Ereignis signalisiert den Abschluss einer Werbeunterbrechung. |
| `media.adBreakStart` | Dieses Ereignis signalisiert den Beginn einer Werbeunterbrechung. |
| `media.adComplete` | Dieses Ereignis signalisiert den Abschluss einer Anzeige. |
| `media.adSkip` | Dieses Ereignis signalisiert, wenn eine Anzeige übersprungen wurde. |
| `media.adStart` | Dieses Ereignis signalisiert den Start einer Anzeige. |
| `media.bitrateChange` | Dieses Ereignis signalisiert bei einer Änderung der Bitrate. |
| `media.bufferStart` | Der `media.bufferStart` Ereignistyp wird bei Beginn der Pufferung gesendet. Es gibt keinen bestimmten `bufferResume` Ereignistyp. Die Pufferung wird als fortgesetzt betrachtet, wenn nach einem `play` Ereignis ein `bufferStart` Ereignis gesendet wird. |
| `media.chapterComplete` | Dieses Ereignis signalisiert den Abschluss eines Kapitels. |
| `media.chapterSkip` | Dieses Ereignis wird ausgelöst, wenn ein Benutzer einen anderen Abschnitt oder ein anderes Kapitel aufruft oder verlässt. |
| `media.chapterStart` | Dieses Ereignis signalisiert den Beginn eines Kapitels. |
| `media.downloaded` | Dieses Ereignis verfolgt, wann heruntergeladene Medieninhalte aufgetreten sind. |
| `media.error` | Dieses Ereignis signalisiert, wenn bei der Medienwiedergabe ein Fehler aufgetreten ist. |
| `media.pauseStart` | Dieses Ereignis verfolgt, wann ein `pauseStart` Ereignis aufgetreten ist. Dieses Ereignis wird ausgelöst, wenn ein Benutzer eine Pause bei der Medienwiedergabe einleitet. Es gibt keinen Resume-Ereignistyp. Ein Lebenslauf wird abgeleitet, wenn Sie ein Wiedergabeereignis nach einem `pauseStart` senden. |
| `media.ping` | Der `media.ping` Ereignistyp wird verwendet, um den aktuellen Wiedergabestatus anzuzeigen. Für Hauptinhalte muss dieses Ereignis während der Wiedergabe alle 10 Sekunden gesendet werden, beginnend 10 Sekunden nach dem Beginn der Wiedergabe. Bei Anzeigen-Inhalten muss sie jede Sekunde beim Anzeigen-Tracking gesendet werden. Ping-Ereignisse sollten die Parameterzuordnung nicht im Anfrageinhalt enthalten. |
| `media.play` | Der `media.play`-Ereignistyp wird gesendet, wenn der Player von einem anderen Status in den `playing` wechselt, z. B. `buffering,` `paused` (wenn der Benutzer ihn wieder aufnimmt) oder `error` (wenn er wiederhergestellt wird), einschließlich Szenarien wie der automatischen Wiedergabe. Dieses Ereignis wird durch den `on('Playing')` Callback des Players ausgelöst. |
| `media.sessionComplete` | Dieses Ereignis wird gesendet, wenn das Ende des Hauptinhalts erreicht ist. |
| `media.sessionEnd` | Der Ereignistyp `media.sessionEnd` benachrichtigt das Media Analytics-Backend, dass eine Sitzung sofort geschlossen werden soll, wenn ein Benutzer seine Anzeige verlässt, und es unwahrscheinlich ist, dass er zurückkehrt. Wenn dieses Ereignis nicht gesendet wird, wird die Sitzung nach 10 Minuten Inaktivität oder 30 Minuten ohne Abspielkopfbewegung beendet. Alle nachfolgenden Medienaufrufe mit dieser Sitzungs-ID werden ignoriert. |
| `media.sessionStart` | Der `media.sessionStart`-Ereignistyp wird mit dem Sitzungsinitiierungsaufruf gesendet. Nach Erhalt einer Antwort wird die Sitzungs-ID aus dem Location-Header extrahiert und für alle nachfolgenden Ereignisaufrufe an den Sammlungsserver verwendet. |
| `media.statesUpdate` | Dieses Ereignis verfolgt, wann ein `statesUpdate` Ereignis aufgetreten ist. Die Player-Status-Tracking-Funktionen können an einen Audio- oder Video-Stream angehängt werden. Die Standardstatus sind: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` und `inFocus`. |
| `opportunityEvent.addToOpportunity` | Dieses Ereignis verfolgt, wann eine Person zu einer Opportunity hinzugefügt wurde. |
| `opportunityEvent.opportunityUpdated` | Dieses Ereignis verfolgt, wann eine Opportunity aktualisiert wurde. |
| `opportunityEvent.removeFromOpportunity` | Dieses Ereignis verfolgt, wann eine Person aus einer Opportunity entfernt wurde. |
| `personalization.request` | **Veraltet** Verwenden Sie stattdessen `decisioning.propositionFetch`. |
| `pushTracking.applicationOpened` | Dieses Ereignis verfolgt, wann eine Person eine Anwendung über eine Push-Benachrichtigung geöffnet hat. |
| `pushTracking.customAction` | Dieses Ereignis verfolgt, wann eine Person eine benutzerdefinierte Aktion in einer Push-Benachrichtigung ausgewählt hat. |
| `web.formFilledOut` | Dieses Ereignis verfolgt, wann eine Person ein Formular auf einer Web-Seite ausgefüllt hat. |
| `web.webinteraction.linkClicks` | Das Ereignis signalisiert, dass ein Link-Klick automatisch von der Web-SDK aufgezeichnet wurde. |
| `web.webpagedetails.pageViews` | Dieser Ereignistyp ist die Standardmethode zum Markieren des Treffers als Seitenansicht. |
| `location.entry` | Dieses Ereignis verfolgt den Eintritt einer Person oder eines Geräts an einem bestimmten Ort. |
| `location.exit` | Dieses Ereignis verfolgt den Austritt einer Person oder eines Geräts aus einem bestimmten Ort. |

{style="table-layout:auto"}

### Vorgeschlagene Werte für `producedBy` {#producedBy}

In der folgenden Tabelle sind einige akzeptierte Werte für `producedBy` angegeben:

| Wert | Definition |
| --- | --- |
| `self` | Selbst |
| `system` | System |
| `salesRef` | Vertriebsmitarbeiter |
| `customerRep` | Kundenbetreuer |
