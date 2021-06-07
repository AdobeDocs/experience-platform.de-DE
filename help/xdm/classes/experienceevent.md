---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;XDM;Felder;Schemas;Schemas;Schemas;Identitätszuordnung;Identitätszuordnung;Schema-Design;Map;Map;Ereignismodellierung;Ereignismodellierung;Best Practices;Ereignis;Ereignisse;
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die XDM ExperienceEvent-Klasse und Best Practices für die Modellierung von Ereignisdaten.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: ecb9c9a4158f3d2981ab60ee3bf419464ac7b8f1
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 4%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] ist eine standardmäßige XDM-Klasse (Experience-Datenmodell), mit der Sie einen Schnappschuss des Systems mit Zeitstempel erstellen können, wenn ein bestimmtes Ereignis auftritt oder ein bestimmter Bedingungssatz erreicht wurde.

Ein Erlebnisereignis ist ein Faktendatensatz dessen, was geschehen ist, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignisse können entweder explizit (direkt beobachtbare menschliche Aktionen) oder implizit (ohne direkte menschliche Aktion ausgelöst) sein und ohne Aggregation oder Interpretation aufgezeichnet werden. Weiterführende Informationen zur Verwendung dieser Klasse im Platform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent]-Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Die Werte einiger dieser Felder werden bei der Datenerfassung automatisch ausgefüllt:

![](../images/classes/experienceevent/structure.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id` | Eine eindeutige Zeichenfolgenkennung für das Ereignis. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Ereignisses zu verfolgen, Datendoppelungen zu verhindern und dieses Ereignis in nachgelagerten Diensten nachzuschlagen. In einigen Fällen kann `_id` eine [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) oder [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) sein.<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei erfassen, sollten Sie diesen Wert generieren, indem Sie eine bestimmte Kombination von Feldern miteinander verknüpfen, die das Ereignis eindeutig machen, z. B. eine primäre ID, einen Zeitstempel, einen Ereignistyp usw. Der verkettete Wert muss eine `uri-reference` formatierte Zeichenfolge sein, d. h. alle Doppelpunkt-Zeichen müssen entfernt werden. Danach sollte der verkettete Wert mit SHA-256 oder einem anderen Algorithmus Ihrer Wahl gehasht werden.<br><br>Es ist wichtig zu unterscheiden, dass  **dieses Feld keine Identität darstellt, die mit einer Person** in Verbindung steht, sondern vielmehr den Datensatz selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) beschränkt werden, die von kompatiblen Feldergruppen bereitgestellt werden. |
| `eventMergeId` | Wenn Sie das [Adobe Experience Platform Web SDK](../../edge/home.md) zum Erfassen von Daten verwenden, stellt dies die Kennung des erfassten Batches dar, der zur Erstellung des Datensatzes geführt hat. Dieses Feld wird bei der Datenerfassung automatisch vom System ausgefüllt. Die Verwendung dieses Felds außerhalb des Kontexts einer Web SDK-Implementierung wird nicht unterstützt. |
| `eventType` | Eine Zeichenfolge, die den Typ oder die Kategorie für das Ereignis angibt. Dieses Feld kann verwendet werden, wenn Sie verschiedene Ereignistypen innerhalb desselben Schemas und Datensatzes unterscheiden möchten, z. B. die Unterscheidung eines Produktansichtsereignisses von einem Add-zu-Warenkorb-Ereignis für ein Einzelhandelsunternehmen.<br><br>Standardwerte für diese Eigenschaft finden Sie im  [Anhang](#eventType), einschließlich Beschreibungen des vorgesehenen Anwendungsfalls. Dieses Feld ist eine erweiterbare Enumeration, d. h. Sie können auch eigene Ereignistypen-Zeichenfolgen verwenden, um die Ereignisse zu kategorisieren, die Sie verfolgen.<br><br>`eventType` beschränkt die Verwendung eines einzelnen Ereignisses pro Treffer in Ihrer Anwendung. Daher müssen Sie berechnete Felder verwenden, um dem System mitzuteilen, welches Ereignis am wichtigsten ist. Weitere Informationen finden Sie im Abschnitt [Best Practices für berechnete Felder](#calculated). |
| `producedBy` | Ein string -Wert, der den Hersteller oder Ursprung des Ereignisses beschreibt. Dieses Feld kann verwendet werden, um bestimmte Ereignisproduzenten bei Bedarf für Segmentierungszwecke herauszufiltern.<br><br>Einige empfohlene Werte für diese Eigenschaft finden Sie im  [Anhang](#producedBy). Dieses Feld ist eine erweiterbare Enumeration, d. h. Sie können auch eigene Zeichenfolgen verwenden, um verschiedene Ereignisproduzenten zu repräsentieren. |
| `identityMap` | Ein map -Feld, das einen Satz von Namespaced-Identitäten für die Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Um dieses Feld für [Echtzeit-Kundenprofil](../../profile/home.md) richtig zu nutzen, sollten Sie nicht versuchen, den Inhalt des Felds in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Weitere Informationen zu ihrem Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den  [Grundlagen der Schemakomposition ](../schema/composition.md#identityMap) . |
| `timestamp` | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist, formatiert gemäß [RFC 3339 Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Dieser Zeitstempel muss in der Vergangenheit auftreten. Best Practices zur Verwendung dieses Felds finden Sie im folgenden Abschnitt zu [Zeitstempel](#timestamps) . |

{style=&quot;table-layout:auto&quot;}

## Best Practices für die Ereignismodellierung

In den folgenden Abschnitten finden Sie Best Practices zum Entwerfen Ihrer ereignisbasierten Experience-Datenmodell (XDM)-Schemas in Adobe Experience Platform.

### Zeitstempel {#timestamps}

Das Stammfeld `timestamp` eines Ereignisschemas kann **nur** die Beobachtung des Ereignisses selbst darstellen und muss in der Vergangenheit auftreten. Wenn Ihre Segmentierungsanwendungsfälle die Verwendung von Zeitstempeln erfordern, die in Zukunft auftreten können, müssen diese Werte an einer anderen Stelle im Erlebnisereignis-Schema eingeschränkt werden.

Wenn beispielsweise ein Unternehmen der Reise- und Gastgewerbe ein Flugreservierungsereignis modelliert, stellt das Feld auf Klassenebene `timestamp` den Zeitpunkt dar, zu dem das Reservierungsereignis beobachtet wurde. Andere Zeitstempel, die mit dem Ereignis in Verbindung stehen, wie z. B. das Startdatum der Reisereservierung, sollten in separaten Feldern erfasst werden, die von standardmäßigen oder benutzerdefinierten Feldergruppen bereitgestellt werden.

![](../images/classes/experienceevent/timestamps.png)

Indem Sie den Zeitstempel auf Klassenebene von anderen zugehörigen Datums-/Zeitwerten in Ihren Ereignisschemas trennen, können Sie flexible Anwendungsfälle für die Segmentierung implementieren und gleichzeitig ein Kundenkonto mit Zeitstempel in Ihrer Erlebnisanwendung beibehalten.

### Berechnete Felder verwenden {#calculated}

Bestimmte Interaktionen in Ihren Erlebnisanwendungen können zu mehreren verwandten Ereignissen führen, die technisch denselben Ereigniszeitstempel aufweisen, und daher als einzelner Ereignisdatensatz dargestellt werden. Wenn ein Kunde beispielsweise ein Produkt auf Ihrer Website anzeigt, kann dies zu einem Ereignisdatensatz mit zwei potenziellen `eventType` -Werten führen: ein &quot;product view&quot;-Ereignis (`commerce.productViews`) oder ein generisches &quot;page view&quot;-Ereignis (`web.webpagedetails.pageViews`). In diesen Fällen können Sie berechnete Felder verwenden, um die wichtigsten Attribute zu erfassen, wenn mehrere Ereignisse in einem einzelnen Treffer erfasst werden.

[Adobe Experience Platform-Daten ](../../data-prep/home.md) Vorbereiten ermöglicht die Zuordnung, Umwandlung und Validierung von Daten zu und von XDM. Mithilfe der verfügbaren [Zuordnungsfunktionen](../../data-prep/functions.md), die vom Dienst bereitgestellt werden, können Sie logische Operatoren aufrufen, um bei der Erfassung in Experience Platform Daten aus Datensätzen mit mehreren Ereignissen zu priorisieren, umzuwandeln und/oder zu konsolidieren. Im obigen Beispiel könnten Sie `eventType` als berechnetes Feld festlegen, bei dem eine &quot;Produktansicht&quot;Vorrang vor einer &quot;Seitenansicht&quot;hat, wann immer beide auftreten.

Wenn Sie Daten manuell über die Benutzeroberfläche in Platform erfassen, finden Sie im Handbuch [Zuordnen einer CSV-Datei zu XDM](../../ingestion/tutorials/map-a-csv-file.md) spezifische Schritte zum Erstellen berechneter Felder.

Wenn Sie Daten mithilfe einer Quellverbindung an Platform streamen, können Sie die Quelle so konfigurieren, dass stattdessen berechnete Felder verwendet werden. Eine Anleitung zur Implementierung berechneter Felder beim Konfigurieren der Verbindung finden Sie in der [Dokumentation für Ihre jeweilige Quelle](../../sources/home.md) .

## Kompatible Schemafeldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldergruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../field-groups/name-updates.md) .

Adobe stellt mehrere Standardfeldgruppen für die Verwendung mit der Klasse [!DNL XDM ExperienceEvent] bereit. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Kampagnen-Marketingdetails]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Kanaldetails]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce-Details]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Details zur Endbenutzer-ID]](../field-groups/event/enduserids.md)
* [[!UICONTROL Umgebungsdetails]](../field-groups/event/environment-details.md)
* [[!UICONTROL Webdetails]](../field-groups/event/web-details.md)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Klasse [!UICONTROL XDM ExperienceEvent].

### Zulässige Werte für `eventType` {#eventType}

In der folgenden Tabelle sind die für `eventType` zulässigen Werte sowie deren Definitionen aufgeführt:

| Wert | Definition |
| --- | --- |
| `advertising.completes` | Ein zeitgesteuertes Medien-Asset wurde bis zum Ende angesehen. Das bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat, da der Betrachter voraus hätte überspringen können. |
| `advertising.timePlayed` | Beschreibt die Zeit, die ein Benutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbringt. |
| `advertising.federated` | Gibt an, ob ein Erlebnisereignis über eine Datenverknüpfung (Datenfreigabe zwischen Kunden) erstellt wurde. |
| `advertising.clicks` | Klicken Sie auf eine(n) Aktion(en) für eine Anzeige. |
| `advertising.conversions` | Vordefinierte Aktion(en), die von einem Kunden durchgeführt wird, der ein Ereignis zur Leistungsbewertung Trigger. |
| `advertising.firstQuartiles` | Eine digitale Videoanzeige hat 25 % ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.impressions` | Impression(en) einer Anzeige für einen Kunden mit dem Potenzial, angezeigt zu werden. |
| `advertising.midpoints` | Eine digitale Videoanzeige hat 50% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.starts` | Die Wiedergabe einer digitalen Videoanzeige hat begonnen. |
| `advertising.thirdQuartiles` | Eine digitale Videoanzeige hat 75% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `web.webpagedetails.pageViews` | Eine Webseite hat eine oder mehrere Ansichten erhalten. |
| `web.webinteraction.linkClicks` | Ein Link wurde mindestens einmal ausgewählt. |
| `commerce.checkouts` | Für eine Produktliste ist ein Checkout-Ereignis aufgetreten. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Wenn mehrere Schritte vorhanden sind, werden der Zeitstempel und die referenzierte Seite/das referenzierte Erlebnis für jedes Ereignis verwendet, um jedes einzelne Ereignis (Schritt) zu identifizieren, das in der angegebenen Reihenfolge dargestellt wird. |
| `commerce.productListAdds` | Ein Produkt wurde zur Produktliste oder zum Warenkorb hinzugefügt. |
| `commerce.productListOpens` | Eine neue Produktliste (Warenkorb) wurde initialisiert oder erstellt. |
| `commerce.productListRemovals` | Ein oder mehrere Produkteinträge wurden aus einer Produktliste oder einem Warenkorb entfernt. |
| `commerce.productListReopens` | Eine Produktliste (Warenkorb), auf die nicht mehr zugegriffen werden konnte (abgebrochen), wurde von einem Kunden erneut aktiviert, z. B. über eine Remarketing-Aktivität. |
| `commerce.productListViews` | Eine Produktliste oder ein Warenkorb hat eine oder mehrere Ansichten erhalten. |
| `commerce.productViews` | Ein Produkt hat eine oder mehrere Ansichten erhalten. |
| `commerce.purchases` | Eine Bestellung wurde angenommen. Dies ist die einzige erforderliche Aktion bei einer Commerce-Konversion. Auf ein Kaufereignis muss eine Produktliste verwiesen werden. |
| `commerce.saveForLaters` | Eine Produktliste wurde für die zukünftige Verwendung gespeichert, z. B. eine ProduktWunschliste. |
| `delivery.feedback` | Feedback-Ereignisse für einen Versand, z. B. ein E-Mail-Versand. |
| `message.feedback` | Feedback-Ereignisse wie Senden/Bounce/Fehler für Nachrichten, die an einen Kunden gesendet werden. |
| `message.tracking` | Tracking von Ereignissen wie Öffnen/Klicken/benutzerdefinierten Aktionen für Nachrichten, die an einen Kunden gesendet werden. |

{style=&quot;table-layout:auto&quot;}

### Vorgeschlagene Werte für `producedBy` {#producedBy}

In der folgenden Tabelle sind einige akzeptierte Werte für `producedBy` aufgeführt:

| Wert | Definition |
| --- | --- |
| `self` | Selbst |
| `system` | System |
| `salesRef` | Vertriebsmitarbeiter |
| `customerRep` | Kundenbetreuer |
