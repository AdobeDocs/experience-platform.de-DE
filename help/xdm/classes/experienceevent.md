---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Identitätskarte;Identitätskarte;Schema-Design;Map;Vereinigung Schema;Vereinigung
solution: Experience Platform
title: XDM ExperienceEvent-Klasse
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über die XDM ExperienceEvent-Klasse.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 6%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] ist eine Standard-XDM-Klasse, mit der Sie einen Schnappschuss des Systems mit Zeitstempel erstellen können, wenn ein bestimmtes Ereignis auftritt oder eine bestimmte Bedingungsgruppe erreicht wurde.

Ein Experience Ereignis ist ein Faktenbericht über das, was geschehen ist, einschließlich des Zeitpunkts und der Identität der beteiligten Person. Ereignis können entweder explizit (direkt erkennbare menschliche Handlungen) oder implizit (ohne unmittelbare Handlung des Menschen aufgeworfen) sein und ohne Aggregation oder Interpretation aufgezeichnet werden. Weitere Informationen zur Verwendung dieser Klasse im Plattform-Ökosystem finden Sie in der [XDM-Übersicht](../home.md#data-behaviors).

Die [!DNL XDM ExperienceEvent]-Klasse selbst stellt mehrere zeitreihenbezogene Felder für ein Schema bereit. Die Werte einiger dieser Felder werden automatisch ausgefüllt, wenn Daten erfasst werden:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `_id` | Ein eindeutiger, systemgenerierter Zeichenfolgenbezeichner für das Ereignis. Dieses Feld dient der Verfolgung der Einzigartigkeit eines einzelnen Ereignisses, der Vermeidung von Datenduplizierung und der Nachforschung dieses Ereignisses bei nachgelagerten Dienstleistungen. Da dieses Feld vom System generiert wird, sollte es bei der Datenerfassung nicht als expliziter Wert angegeben werden.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld  **keine Identität** darstellt, die sich auf eine Person bezieht, sondern vielmehr die Aufzeichnung der Daten selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen in [Identitätsfelder](../schema/composition.md#identity) umbenannt werden. |
| `eventMergeId` | Die ID des erfassten Stapels, die zur Erstellung des Datensatzes geführt hat. Dieses Feld wird beim Erfassen von Daten automatisch vom System ausgefüllt. |
| `eventType` | Eine Zeichenfolge, die den primären Ereignistyp für den Datensatz angibt. Akzeptierte Werte und ihre Definitionen finden Sie im Abschnitt [Anhang](#eventType). |
| `identityMap` | Ein Zuordnungsfeld, das einen Satz namensbezogener Identitäten für die einzelne Person enthält, für die das Ereignis gilt. Dieses Feld wird vom System automatisch aktualisiert, wenn Identitätsdaten erfasst werden. Um dieses Feld für [Kundendaten in Echtzeit](../../profile/home.md) richtig zu verwenden, sollten Sie nicht versuchen, den Feldinhalt in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Weitere Informationen zum Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den  [Grundlagen der ](../schema/composition.md#identityMap) Schema-Komposition. |
| `timestamp` | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses, formatiert gemäß [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).<br><br>Dieser Zeitstempel kann  **** nur die Beobachtung des Ereignisses selbst darstellen und muss in der Vergangenheit erfolgen. Wenn Ihre Anwendungsfälle für die Segmentierung die Verwendung von Zeitstempeln erfordern, die in der Zukunft auftreten können (z. B. ein Abflugdatum), müssen diese Werte an anderer Stelle im Experience Ereignis-Schema eingeschränkt werden. |

## Kompatible Schema-Feldgruppen {#field-groups}

>[!NOTE]
>
>Die Namen mehrerer Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../field-groups/name-updates.md).

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM ExperienceEvent]-Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldgruppen für die Klasse:

* [[!UICONTROL Details zur Endbenutzer-ID]](../field-groups/event/enduserids.md)
* [[!UICONTROL Umgebung]](../field-groups/event/environment-details.md)

## Anhang

Der folgende Abschnitt enthält weitere Informationen zur Klasse [!UICONTROL XDM ExperienceEvent].

### Akzeptierte Werte für xdm:eventType {#eventType}

In der folgenden Tabelle sind die für `xdm:eventType` zulässigen Werte und ihre Definitionen aufgeführt:

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
