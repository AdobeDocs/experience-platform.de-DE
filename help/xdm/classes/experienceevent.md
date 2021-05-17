---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätskarte;Identitätskarte;Schema-Design;Map;Vereinigung Schema;Vereinigung
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über die XDM ExperienceEvent-Klasse.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 4%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] ist eine standardmäßige XDM-Klasse (Experience Data Model), mit der Sie einen Schnappschuss des Systems mit Zeitstempel erstellen können, wenn ein bestimmtes Ereignis auftritt oder ein bestimmter Bedingungssatz erreicht wurde.

Ein Experience Ereignis ist ein Faktenbericht über das, was geschehen ist, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignis können entweder explizit (direkt erkennbare menschliche Handlungen) oder implizit (ohne unmittelbare Handlung des Menschen aufgeworfen) sein und ohne Aggregation oder Interpretation aufgezeichnet werden. Weitere Informationen zur Verwendung dieser Klasse im Plattform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent]-Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Die Werte einiger dieser Felder werden automatisch ausgefüllt, wenn Daten erfasst werden:

![](../images/classes/experienceevent/structure.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id` | Eine eindeutige Zeichenfolgenkennung für das Ereignis. Dieses Feld dient der Verfolgung der Einzigartigkeit eines einzelnen Ereignisses, der Vermeidung von Datenduplizierung und der Suche nach diesem Ereignis in nachgelagerten Diensten.<br><br>In einigen Fällen  `_id` kann es sich um eine  [Universally Unique Identifier (UUID) ](https://tools.ietf.org/html/rfc4122) oder eine  [Global Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) handeln. In Adobe Experience Platform Data Prep kann dieser Wert mit den Zuordnungsfunktionen [`uuid` oder `guid` generiert werden.](../../data-prep/functions.md#special-operations)<br><br>Wenn Sie Daten aus einer Quellverbindung streamen oder direkt aus einer Parquet-Datei abrufen, sollten Sie diesen Wert generieren, indem Sie bestimmte Kombinationsfelder miteinander verknüpfen, die das Gerade eindeutig machen, z. B. eine primäre ID, einen Zeitstempel, einen Ereignistyp usw.<br><br>Es ist wichtig zu unterscheiden, dass  **dieses Feld nicht eine Identität darstellt, die mit einer Person** in Beziehung steht, sondern vielmehr die Aufzeichnung der Daten selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) zurückgesetzt werden, die von kompatiblen Mixins bereitgestellt werden. |
| `eventMergeId` | Wenn Sie zum Erfassen von Daten das [Adobe Experience Platform Web SDK](../../edge/home.md) verwenden, stellt dies die ID des erfassten Stapels dar, der zur Erstellung des Datensatzes geführt hat. Dieses Feld wird beim Erfassen von Daten automatisch vom System ausgefüllt. Die Verwendung dieses Felds außerhalb des Kontexts einer Web SDK-Implementierung wird nicht unterstützt. |
| `eventType` | Eine Zeichenfolge, die den Typ oder die Kategorie des Ereignisses angibt. Dieses Feld kann verwendet werden, wenn Sie verschiedene Ereignistyp innerhalb desselben Schemas und desselben Datensatzes unterscheiden möchten, z. B. indem Sie ein Ereignis für die Ansicht eines Produkts von einem Ereignis für den Zusatz zum Einkaufswagen für eine Einzelhandels-Firma unterscheiden.<br><br>Die Standardwerte für diese Eigenschaft werden im Abschnitt [ &quot;](#eventType)Anhang&quot;bereitgestellt, einschließlich Beschreibungen der Verwendungsart. Dieses Feld ist eine erweiterbare Enum, d. h. Sie können auch eigene Ereignistyp-Zeichenfolgen verwenden, um die Ereignis zu kategorisieren, die Sie verfolgen. |
| `producedBy` | Ein Zeichenfolgenwert, der den Produzenten oder die Herkunft des Ereignisses beschreibt. Dieses Feld kann verwendet werden, um bestimmte Ereignis-Hersteller auszufiltern, wenn dies für Segmentierungszwecke erforderlich ist.<br><br>Einige empfohlene Werte für diese Eigenschaft finden Sie im  [Anhang](#producedBy). Dieses Feld ist eine erweiterbare Enum, d. h. Sie können auch eigene Zeichenfolgen verwenden, um verschiedene Ereignis-Produzenten zu repräsentieren. |
| `identityMap` | Ein Zuordnungsfeld, das einen Satz namensbezogener Identitäten für die einzelne Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, wenn Identitätsdaten erfasst werden. Um dieses Feld für [Kundendaten in Echtzeit](../../profile/home.md) richtig zu verwenden, sollten Sie nicht versuchen, den Feldinhalt in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Weitere Informationen zum Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den  [Grundlagen der ](../schema/composition.md#identityMap) Schema-Komposition. |
| `timestamp` | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses, formatiert gemäß [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Dieser Zeitstempel muss in der Vergangenheit auftreten. Bewährte Verfahren zur Verwendung dieses Felds finden Sie im Abschnitt [Zeitstempel](#timestamps). |

## Best Practices für die Modellierung von Ereignissen

Die folgenden Abschnitte beschreiben bewährte Verfahren zum Entwerfen Ihrer Ereignis-basierten Experience Data Model (XDM)-Schema in Adobe Experience Platform.

### Zeitstempel {#timestamps}

Das Stammfeld `timestamp` eines Ereignis-Schemas kann **nur** die Beobachtung des Ereignisses selbst darstellen und muss in der Vergangenheit auftreten. Wenn Ihre Anwendungsfälle für die Segmentierung die Verwendung von Zeitstempeln erfordern, die in der Zukunft auftreten können, müssen diese Werte an anderer Stelle im Experience Ereignis-Schema eingeschränkt werden.

Beispiel: Wenn ein Unternehmen der Reise- und Gastgewerbebranche ein Ereignis für die Flugreservierung modelliert, gibt das Feld auf Klassenebene `timestamp` den Zeitpunkt an, zu dem das Ereignis für die Reservierung eingehalten wurde. Andere Zeitstempel, die mit dem Ereignis zusammenhängen, wie z. B. der Beginn der Reisebuchung, sollten in separaten Feldern erfasst werden, die von Standard- oder benutzerdefinierten Mixins bereitgestellt werden.

![](../images/classes/experienceevent/timestamps.png)

Indem Sie den Zeitstempel auf Klassenebene von anderen zugehörigen Datenzeitwerten in Ihren Ereignis-Schemas trennen, können Sie flexible Anwendungsfälle für die Segmentierung implementieren und gleichzeitig ein Kundenkonto mit Zeitstempel in Ihrer Erlebnisanwendung beibehalten.

### Berechnete Felder verwenden

Bestimmte Interaktionen in Ihren Erlebnisanwendungen können zu mehreren zugehörigen Ereignissen führen, die technisch den gleichen Ereignis-Zeitstempel verwenden und daher als ein Ereignis dargestellt werden können. Wenn ein Kunde beispielsweise ein Ereignis auf Ihrer Website Ansicht, kann dies zu einem Produktdatensatz führen, der sowohl Produktattribute als auch einige überlappende generische Seitenattribute der Ansicht enthält. In diesen Fällen können Sie berechnete Felder verwenden, um die wichtigsten Attribute zu erfassen, wenn mehrere Ereignis in einem Datensatz erfasst werden.

[Adobe Experience Platform Data ](../../data-prep/home.md) Prepallow you to map, transform and validate data to and from XDM. Mithilfe der verfügbaren [Zuordnungsfunktionen](../../data-prep/functions.md), die vom Dienst bereitgestellt werden, können Sie logische Operatoren aufrufen, um Daten aus Datensätzen mit mehreren Ereignissen zu priorisieren, umzuformen und/oder zu konsolidieren, wenn sie in die Experience Platform aufgenommen werden.

Wenn Sie Daten manuell über die Benutzeroberfläche in die Plattform einbinden, finden Sie im Handbuch [Zuordnen einer CSV-Datei zu XDM](../../ingestion/tutorials/map-a-csv-file.md) spezifische Schritte zum Erstellen berechneter Felder.

Wenn Sie Daten mithilfe einer Quellverbindung an die Plattform streamen, können Sie die Quelle so konfigurieren, dass sie stattdessen berechnete Felder verwendet. Anweisungen zum Implementieren berechneter Felder beim Konfigurieren der Verbindung finden Sie in der [Dokumentation zu Ihrer jeweiligen Quelle](../../sources/home.md).

## Kompatible Schema-Feldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../field-groups/name-updates.md).

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM ExperienceEvent]-Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldgruppen für die Klasse:

* [[!UICONTROL Details zur Endbenutzer-ID]](../field-groups/event/enduserids.md)
* [[!UICONTROL Umgebung]](../field-groups/event/environment-details.md)

## Anhang

Der folgende Abschnitt enthält weitere Informationen zur Klasse [!UICONTROL XDM ExperienceEvent].

### Akzeptierte Werte für `eventType` {#eventType}

In der folgenden Tabelle sind die für `eventType` zulässigen Werte und ihre Definitionen aufgeführt:

| Wert | Definition |
| --- | --- |
| `advertising.completes` | Ein zeitgesteuertes Medienelement wurde bis zum Abschluss überwacht. Dies bedeutet nicht unbedingt, dass der Viewer das gesamte Video angesehen hat, da der Viewer möglicherweise vorzeitig übersprungen wurde. |
| `advertising.timePlayed` | Beschreibt die Zeitdauer, die ein Benutzer für ein bestimmtes zeitgesteuertes Medienelement verbringt. |
| `advertising.federated` | Gibt an, ob ein Experience Ereignis über den Datenverband (Datenfreigabe zwischen Kunden) erstellt wurde. |
| `advertising.clicks` | Klicken Sie auf Aktion(en) für eine Werbung. |
| `advertising.conversions` | Vordefinierte Aktionen, die von einem Kunden ausgeführt werden, der ein Ereignis zur Leistungsbewertung Trigger. |
| `advertising.firstQuartiles` | Eine digitale Videoanzeige hat 25 % ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.impressions` | Impression(en) einer Werbung für einen Kunden mit dem Potenzial, angezeigt zu werden. |
| `advertising.midpoints` | Eine digitale Videoanzeige hat 50% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `advertising.starts` | Die Wiedergabe einer digitalen Videoanzeige wurde gestartet. |
| `advertising.thirdQuartiles` | Eine digitale Videoanzeige hat 75% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben. |
| `web.webpagedetails.pageViews` | Eine Webseite hat eine oder mehrere Ansichten erhalten. |
| `web.webinteraction.linkClicks` | Ein Link wurde ein- oder mehrmals ausgewählt. |
| `commerce.checkouts` | Für eine Liste des Produkts ist ein Kassengang-Ereignis aufgetreten. Es kann mehrere Checkout-Ereignis geben, wenn ein Kassengangprozess mehrere Schritte umfasst. Wenn mehrere Schritte durchgeführt werden, werden der Zeitstempel und die referenzierte Seite/Erlebnis für jedes Ereignis verwendet, um das jeweilige Ereignis (Schritt) in der angegebenen Reihenfolge zu identifizieren. |
| `commerce.productListAdds` | Ein Produkt wurde der Liste oder dem Warenkorb hinzugefügt. |
| `commerce.productListOpens` | Eine neue Liste (Warenkorb) wurde initialisiert oder erstellt. |
| `commerce.productListRemovals` | Ein oder mehrere Produkteinträge wurden aus einer Liste oder einem Warenkorb entfernt. |
| `commerce.productListReopens` | Eine Liste (Warenkorb), auf die nicht mehr zugegriffen werden konnte (die abgebrochen wurde), wurde von einem Kunden erneut aktiviert, z. B. über eine Remarketing-Aktivität. |
| `commerce.productListViews` | Eine Liste oder ein Warenkorb hat eine oder mehrere Ansichten erhalten. |
| `commerce.productViews` | Ein Produkt hat eine oder mehrere Ansichten erhalten. |
| `commerce.purchases` | Eine Bestellung wurde angenommen. Dies ist die einzige erforderliche Aktion bei einer Commerce-Konvertierung. Auf ein Ereignis zum Einkauf muss eine Liste verwiesen werden. |
| `commerce.saveForLaters` | Eine ProduktWunschliste wurde zur späteren Verwendung einer Liste gespeichert. |
| `delivery.feedback` | Feedback-Ereignis für einen Versand, z. B. ein E-Mail-Versand. |
| `message.feedback` | Feedback-Ereignis wie Senden/Absprung/Fehler für Nachrichten, die an einen Kunden gesendet werden. |
| `message.tracking` | Verfolgen von Ereignissen wie &quot;Öffnen&quot;/&quot;Klicken&quot;/&quot;Benutzerdefinierte Aktionen&quot;in Nachrichten, die an einen Kunden gesendet werden. |

### Vorgeschlagene Werte für `producedBy` {#producedBy}

In der folgenden Tabelle sind einige für `producedBy` zulässige Werte aufgeführt:

| Wert | Definition |
| --- | --- |
| `self` | self |
| `system` | System |
| `salesRef` | Vertriebsmitarbeiter |
| `customerRep` | Kundenbeauftragter |
