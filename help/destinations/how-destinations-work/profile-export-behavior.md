---
title: Profilexportverhalten
description: Erfahren Sie, wie sich das Verhalten beim Profilexport zwischen den verschiedenen Integrationspattern unterscheidet, die in Experience Platform-Zielen unterstützt werden.
source-git-commit: 1c844d86834ef78d1206a8698dbcbfe2fae49661
workflow-type: tm+mt
source-wordcount: '2926'
ht-degree: 24%

---

# Profil-Exportverhalten für verschiedene Zieltypen

Es gibt mehrere Zieltypen in der Experience Platform, wie in der Abbildung unten dargestellt. Diese Bestimmungsländer weisen im Hinblick darauf, welche Trigger eine Zielausfuhr ist und was in einer Ausfuhr enthalten ist, etwas unterschiedliche Ausfuhrmuster auf, wie in den folgenden Abschnitten beschrieben.

>[!IMPORTANT]
>
>Auf dieser Dokumentationsseite wird nur das Verhalten des Profilexports für die Verbindungen beschrieben, die unten im Diagramm hervorgehoben sind.

![Zieltyp-Diagramm](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Microbatching- und Aggregationspolitik

Bevor Sie sich mit bestimmten Informationen nach Zieltyp befassen, müssen Sie die Konzepte der Mikrobatching- und Aggregationsrichtlinie für *Streaming-Ziele*.

Experience Platform-Ziele exportieren Daten als HTTPS-Aufrufe in API-basierte Integrationen. Sobald der Zieldienst von anderen Upstream-Diensten darüber informiert wird, dass Profile infolge der Batch-Erfassung, Streaming-Erfassung, Batch-Segmentierung, Streaming-Segmentierung oder von Änderungen an Identitätsdiagrammen aktualisiert wurden, werden die Daten exportiert und an Streaming-Ziele gesendet.

Der Prozess, durch den Profile in HTTPS-Nachrichten aggregiert werden, bevor sie an Ziel-API-Endpunkte gesendet werden, wird aufgerufen *Microbatching*.

Nehmen Sie die [Facebook-Ziel](/help/destinations/catalog/social/facebook.md) mit *[konfigurierbare Aggregation](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* -Richtlinie als Beispiel dient - Daten werden aggregiert gesendet, wobei der Zieldienst alle eingehenden Daten aus dem Profildienst vorgelagert nimmt und nach einem der folgenden Elemente aggregiert, bevor sie an Facebook gesendet werden:

* Anzahl der Datensätze (maximal 10.000) oder
* Zeitfenster-Intervall (30 Minuten)

Die oben genannten Schwellenwerte werden zum ersten Mal für Trigger und den Export nach Facebook verwendet. In der [!DNL Facebook Custom Audiences] Dashboard können Sie sehen, dass Zielgruppen aus der Experience Platform in 10.000 Schritten eingehen. Es kann vorkommen, dass alle 10 bis 15 Minuten 10.000 Datensätze angezeigt werden, da die Daten schneller verarbeitet und aggregiert werden als das 30-minütige Exportintervall. Außerdem werden sie schneller gesendet. Etwa alle 10 bis 15 Minuten, bis alle Datensätze verarbeitet wurden. Wenn für einen 10.000-Batch nicht genügend Datensätze vorhanden sind, wird die aktuelle Datensatzanzahl so gesendet, wie es der Zeitfensterschwellenwert erreicht. So werden möglicherweise auch kleinere Batches an Facebook gesendet.

Betrachten Sie als weiteres Beispiel die [HTTP-API-Ziel](/help/destinations/catalog/streaming/http-destination.md), die über eine *[Aggregation des besten Aufwands](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* Politik, mit `maxUsersPerRequest: 10`. Das bedeutet, dass maximal zehn Profile aggregiert werden, bevor ein HTTP-Aufruf an dieses Ziel gesendet wird. Experience Platform versucht jedoch, Profile an das Ziel zu senden, sobald der Zieldienst aktualisierte Neubewertungsinformationen von einem vorgelagerten Dienst erhält.

Die Aggregationsrichtlinie ist konfigurierbar, und die Zielentwickler können entscheiden, wie die Aggregationsrichtlinie so konfiguriert werden soll, dass die Ratenbeschränkungen der API-Endpunkte nachgelagert am besten eingehalten werden. Mehr dazu [Aggregationspolitik](/help/destinations/destination-sdk/destination-configuration.md#aggregation) in der Dokumentation zur Destination SDK.

## Export von Streaming-Profilen (Enterprise)-Zielen {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Enterprise-Ziele sind nur für verfügbar. [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) -Kunden.

Die [Enterprise-Ziele](/help/destinations/destination-types.md#streaming-profile-export) in Experience Platform sind Amazon Kinesis, Azure Event Hubs und HTTP API.

Experience Platform optimiert das Profil-Exportverhalten für Ihr Unternehmensziel, sodass nur Daten an Ihren API-Endpunkt exportiert werden, wenn relevante Profilaktualisierungen nach der Segmentqualifizierung oder anderen wichtigen Ereignissen vorgenommen wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung in [Segmentmitgliedschaft](/help/xdm/field-groups/profile/segmentation.md) für mindestens eines der Segmente, die dem Ziel zugeordnet sind. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder es hat eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) bestimmt. Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten?

Für die Daten, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte von *was den Datenexport an Ihr Unternehmensziel bestimmt* und *welche Daten im Export enthalten sind*.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport gestartet wird, wenn zugeordnete Segmente den Status ändern (von null zu realisiert oder von realisiert/existierend zu verlassend) oder alle zugeordneten Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht Enterprise-Zielen zugeordnet werden können, bestimmen Änderungen an der Identität eines bestimmten Profils auch die Zielexporte.</li><li>Als Änderung für ein Attribut wird jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass das Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Die `segmentMembership` -Objekt enthält das Segment, das im Aktivierungsdatenfluss zugeordnet ist und für das sich der Status des Profils nach einem Qualifizierungs- oder Segmentexit-Ereignis geändert hat. Beachten Sie, dass andere nicht zugeordnete Segmente, für die sich das Profil qualifiziert hat, Teil des Zielexports sein können, wenn diese Segmente zum selben Segment gehören [Zusammenführungsrichtlinie](/help/profile/merge-policies/overview.md) als Segment, das im Aktivierungsdataflow zugeordnet ist. </li><li>Alle Identitäten in der `identityMap` -Objekt werden ebenfalls einbezogen (Experience Platform unterstützt derzeit keine Identitätszuordnung im Enterprise-Ziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Enterprise-Ziele streamen Aufstockungsdaten, wenn Profile für ein Ziel aktiviert werden. Das bedeutet, dass der erste Datenexport nach der Konfiguration eines Aktivierungs-Workflows für ein Ziel Profile enthält, die sich für das aktivierte Segment qualifiziert haben, bevor das Segment dem Ziel zugeordnet wird.

>[!BEGINSHADEBOX]

Betrachten Sie beispielsweise den folgenden Datenfluss an ein HTTP-Ziel, bei dem drei Segmente im Datenfluss ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![Enterprise-Ziel-Datenfluss](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der *drei zugeordneten Segmente* qualifiziert. Im Datenexport jedoch wird im `segmentMembership` -Objekt können andere nicht zugeordnete Segmente angezeigt werden, wenn dieses bestimmte Profil ein Mitglied dieses Profils ist und diese dieselbe Zusammenführungsrichtlinie wie das Segment nutzen, das den Export ausgelöst hat. Wenn ein Profil für die **Kunde mit DeLorean Cars** -Segment, ist aber auch Mitglied der **Film &quot;Back to the Future&quot;** und **Fans von Science-Fiction** Segmente, dann sind auch diese beiden anderen Segmente im `segmentMembership` -Objekt des Datenexports, auch wenn diese nicht im Datenfluss zugeordnet sind, wenn diese dieselbe Zusammenführungsrichtlinie mit der **Kunde mit DeLorean Cars** Segment.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport, und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

>[!ENDSHADEBOX]

>[!TIP]
>
> Beispiele für exportierte Daten an verschiedene Unternehmensziele finden Sie in der [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)und [HTTP-API](/help/destinations/catalog/streaming/http-destination.md#exported-data) Zieldokumentationsseiten.

## API-basierte Streaming-Ziele {#streaming-api-based-destinations}

Das Verhalten beim Profilexport für Streaming-Ziele wie Facebook, Trade Desk und andere API-basierte Integrationen ist mit dem oben stehenden identisch.

Zielbeispiele: Werbung, soziale Netzwerke usw.

Experience Platform optimiert das Verhalten beim Profilexport an Ihr Streaming-Ziel, sodass nur Daten an Streaming-API-basierte Ziele exportiert werden, wenn nach der Segmentqualifizierung oder anderen wichtigen Ereignissen relevante Profilaktualisierungen vorgenommen wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung in [Segmentmitgliedschaft](/help/xdm/field-groups/profile/segmentation.md) für mindestens eines der Segmente, die dem Ziel zugeordnet sind. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder es hat eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) für einen Identitäts-Namespace, der für diese Zielinstanz für den Export markiert ist. Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.
* Einverständnisänderungen für ein Profil, wenn die automatisierte Einverständniserzwingung konfiguriert ist und ein Profil sich abmeldet. Durch die automatisierte Einwilligungserzwingung wird ein aus der Zielgruppe bestehendes Ereignis an das Ziel gesendet, sodass das Profil in keinem Targeting am Ziel enthalten ist.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten?

In Bezug auf die Daten, die für ein bestimmtes Profil exportiert werden, müssen Sie die beiden Konzepte kennen, die den Datenexport an Ihr Streaming-API-Ziel bestimmen und festlegen, welche Daten in den Export einbezogen werden.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport gestartet wird, wenn zugeordnete Segmente den Status ändern (von null zu realisiert oder von realisiert/existierend zu verlassend) oder alle zugeordneten Attribute aktualisiert werden.</li><li>Eine Änderung in der Identitätszuordnung wird als eine Identität definiert, die für die [Identitätsdiagramm](/help/identity-service/ui/identity-graph-viewer.md) des Profils für Identitäts-Namespaces, die für den Export zugeordnet sind.</li><li>Eine Änderung für ein Attribut ist definiert als jede Aktualisierung des Attributs für Attribute, die dem Ziel zugeordnet sind.</li></ul> | <ul><li>Die Segmente, die dem Ziel zugeordnet sind und sich geändert haben, werden in die `segmentMembership` -Objekt. In einigen Szenarien können sie mit mehreren -Aufrufen exportiert werden. In einigen Szenarien können auch einige Segmente, die sich nicht geändert haben, in den -Aufruf einbezogen werden. In jedem Fall werden nur zugeordnete Segmente exportiert.</li><li>Alle Identitäten aus den Namespaces, die dem Ziel im `identityMap` -Objekt enthalten sind.</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Streaming-API-Ziele streamen Aufstockungsdaten, wenn Profile für ein Ziel aktiviert werden. Das bedeutet, dass der erste Datenexport nach der Konfiguration eines Aktivierungs-Workflows für ein Ziel Profile enthält, die sich für das aktivierte Segment qualifiziert haben, bevor das Segment dem Ziel zugeordnet wird.

>[!BEGINSHADEBOX]

Betrachten Sie beispielsweise diesen Datenfluss zu einem Streaming-Ziel, bei dem im Datenfluss drei Segmente ausgewählt sind.

![Streaming-Ziel-Datenfluss](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der drei zugeordneten Segmente qualifiziert. Wenn sich ein Profil für die **Kunde mit DeLorean Cars** -Segment ein, wird dies einen Export Trigger. Die anderen Segmente (**Stadt - Dallas** und **Grundlegende Site-Aktivität**) kann auch exportiert werden, wenn das Profil dieses Segment mit einem der möglichen Status (`realized`, `existing`, `exited`). Nicht zugeordnete Segmente (z. B. **Fans von Science-Fiction**) wird nicht exportiert.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den drei oben zugeordneten Attributen einen Zielexport.

>[!BEGINSHADEBOX]

## Batch-Ziele (dateibasiert) {#file-based-destinations}

Beim Export von Profilen in [dateibasierte Ziele](/help/destinations/destination-types.md#file-based) in Experience Platform gibt es drei Arten von Zeitplänen (siehe unten) und zwei Dateiexportoptionen (vollständige oder inkrementelle Dateien), die Sie verwenden können. Alle diese Einstellungen werden auf Segmentebene festgelegt, selbst wenn mehrere Segmente einem einzelnen Ziel-Datenfluss zugeordnet sind.

* Geplante Exporte: Konfigurieren Sie ein Ziel, fügen Sie ein oder mehrere Segmente hinzu, wählen Sie aus, ob Sie vollständige oder inkrementelle Dateien exportieren möchten, und wählen Sie eine bestimmte Zeit pro Tag oder mehrmals pro Tag aus, zu der die Dateien exportiert werden sollen. Beispielsweise bedeutet eine Exportzeit von 17 Uhr, dass jedes Profil, das für das Segment qualifiziert ist, um 17 Uhr exportiert wird.
* Nach der Segmentbewertung: Der Export wird sofort nach Ausführung des täglichen Segmentbewertungsauftrags ausgelöst. Das bedeutet, dass die exportierten Profilnummern in der Datei so nah wie möglich an der zuletzt bewerteten Population des Segments sind.
* On-Demand-Ausfuhren ([Export-Datei jetzt](/help/destinations/ui/export-file-now.md)): Basierend auf dem neuesten Segmentbewertungsauftrag wird eine vollständige Datei einmal zusätzlich zu den regelmäßig geplanten Exporten exportiert.

In allen oben genannten Exportsituationen enthalten die exportierten Dateien die Profile, die für den Export qualifiziert sind, zusammen mit den Spalten, die Sie als XDM-Attribute für den Export ausgewählt haben.

>[!TIP]
>
>Wenn ein Streaming-Segment einem Batch-Ziel zugeordnet wird, besteht eine höhere Wahrscheinlichkeit, dass die Anzahl der Profile in der exportierten Datei näher an der Anzahl der Benutzer im Segment liegt. Dies liegt daran, dass die aktuelle Segmentauswertung näher an der Exportzeit liegt.

### Inkrementelle Dateiexporte {#incremental-file-exports}

Nicht alle Aktualisierungen eines Profils qualifizieren ein Profil für die Aufnahme in inkrementelle Dateiexporte. Wenn beispielsweise ein Attribut einem Profil hinzugefügt oder daraus entfernt wurde, wird das Profil nicht in den Export einbezogen. Nur Profile, für die `segmentMembership` -Attribut geändert wurde, wird in die exportierten Dateien aufgenommen. Das heißt, nur wenn das Profil Teil des Segments wird oder aus dem Segment entfernt wird, wird es in inkrementelle Dateiexporte einbezogen.

Wenn einem Profil in der Variablen [Identitätsdiagramm](/help/identity-service/ui/identity-graph-viewer.md), der keinen Grund darstellt, das Profil in einen neuen inkrementellen Dateiexport aufzunehmen.

Wenn einem Zielzuordnung ein neues Segment hinzugefügt wird, hat dies keine Auswirkungen auf Qualifikationen und Exporte für ein anderes Segment. Exportpläne werden für jedes Segment einzeln konfiguriert und Dateien werden separat für jedes Segment exportiert, selbst wenn die Segmente demselben Zieldatenfluss hinzugefügt wurden.

>[!BEGINSHADEBOX]

Beachten Sie beispielsweise in der unten dargestellten Exporteinstellung, in der ein Segment inkrementelle Dateiaktualisierungen exportiert, die folgenden Umstände, unter denen ein Profil in einen inkrementellen Dateiexport aufgenommen wird oder nicht:

![Exporteinstellung mit mehreren ausgewählten Attributen.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Ein Profil wird in einen inkrementellen Dateiexport aufgenommen, wenn es für das Segment qualifiziert oder disqualifiziert ist.
* Ein Profil ist *not* wird in einen inkrementellen Dateiexport aufgenommen, wenn dem Identitätsdiagramm eine neue Telefonnummer hinzugefügt wird.
* Ein Profil ist *not* in einen inkrementellen Dateiexport eingeschlossen, wenn der Wert eines der zugeordneten XDM-Felder wie `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` auf ein Profil aktualisiert wird.
* Immer `segmentMembership.status` Das XDM-Feld wird im Zielaktivierungs-Workflow zugeordnet. Profile, die das Segment verlassen, werden auch in exportierte inkrementelle Dateien mit einem `exited` Status.

>[!ENDSHADEBOX]

### Was bestimmt einen Datenexport und was ist im Export enthalten?

Basierend auf den Informationen im obigen Abschnitt kann das Verhalten beim Profilexport an dateibasierte Ziele wie unten beschrieben zusammengefasst werden:

**Vollständige Dateiexporte**

Die gesamte Population des Segments wird täglich exportiert.

| Was einen Zielexport bestimmt | Was ist in der exportierten Datei enthalten? |
|---------|----------|
| <ul><li>Der in der Benutzeroberfläche oder API festgelegte Exportzeitplan und die Benutzeraktion (Auswahl von [Datei jetzt exportieren](/help/destinations/ui/export-file-now.md) in der Benutzeroberfläche oder mithilfe der [Ad-hoc-Aktivierungs-API](/help/destinations/api/ad-hoc-activation-api.md)) den Start eines Zielexports bestimmen.</li><li>Alle Änderungen an der Segmentzugehörigkeit eines Profils, unabhängig davon, ob es sich für das Segment qualifiziert oder von ihm abweicht, qualifizieren ein Profil für die Aufnahme in inkrementelle Exporte.</li></ul> | In vollständigen Dateiexporten wird die gesamte Profilpopulation eines Segments, basierend auf der neuesten Segmentbewertung, in jeden Dateiexport einbezogen. Die neuesten Werte für jedes für den Export ausgewählte XDM-Attribut werden ebenfalls als Spalten in jeder Datei enthalten sein. |

{style=&quot;table-layout:fixed&quot;}

**Inkrementelle Dateiexporte**

Im ersten Dateiexport nach der Einrichtung des Aktivierungs-Workflows wird die gesamte Population des Segments exportiert. In nachfolgenden Exporten werden nur die geänderten Profile exportiert.

| Was einen Zielexport bestimmt | Was ist in der exportierten Datei enthalten? |
|---------|----------|
| <ul><li>Der in der Benutzeroberfläche oder API festgelegte Exportzeitplan bestimmt den Beginn eines Zielexports.</li><li>Alle Änderungen an der Segmentzugehörigkeit eines Profils, unabhängig davon, ob es sich für das Segment qualifiziert oder von ihm abweicht, qualifizieren ein Profil für die Aufnahme in inkrementelle Exporte. Änderungen an Attributen oder in Identitätszuordnungen für ein Profil *nicht* ein Profil für inkrementelle Exporte qualifizieren.</li></ul> | Die Profile, für die die Segmentzugehörigkeit geändert wurde, sowie die neuesten Informationen zu jedem für den Export ausgewählten XDM-Attribut. |

{style=&quot;table-layout:fixed&quot;}

>[!TIP]
>
>Zur Erinnerung: Änderungen an Attributwerten oder in Identitätszuordnungen für ein Profil qualifizieren ein Profil nicht für die Aufnahme in einen inkrementellen Dateiexport.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, was Sie bei Profilexporten an Streaming-, Enterprise- und dateibasierte Ziele erwarten können.

Als Nächstes können Sie darüber lesen, wie [-Identitäten verarbeitet werden](/help/destinations/how-destinations-work/identity-handling.md) im Aktivierungs-Workflow.