---
title: Profilexportverhalten
description: Erfahren Sie, wie sich das Verhalten beim Profilexport zwischen den verschiedenen Integrationsmustern unterscheidet, die in Experience Platform-Zielen unterstützt werden.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 97%

---

# Profilexportverhalten für verschiedene Zieltypen

Es gibt mehrere Zieltypen in Experience Platform, wie in der Abbildung unten dargestellt. Diese Ziele weisen im Hinblick darauf, was einen Zielexport auslöst und was in einem Export enthalten ist, geringfügig unterschiedliche Exportmuster auf, wie in den folgenden Abschnitten beschrieben.

>[!IMPORTANT]
>
>Auf dieser Dokumentationsseite wird nur das Verhalten beim Profilexport für die Verbindungen beschrieben, die im unteren Bereich der Abbildung hervorgehoben sind.

![Abbildung mit den Zieltypen](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Microbatching und Aggregationsrichtlinie

Bevor Sie sich mit bestimmten Informationen nach Zieltyp befassen, müssen Sie die Konzepte des Microbatching und der Aggregationsrichtlinie für *Streaming-Ziele* verstehen.

Experience Platform-Ziele exportieren Daten an API-basierte Integrationen in Form von HTTPS-Aufrufen. Sobald der Ziel-Service von anderen Upstream-Services darüber informiert wird, dass Profile infolge der Batch-Aufnahme, Streaming-Aufnahme, Batch-Segmentierung, Streaming-Segmentierung oder Identitätsdiagramm-Änderungen aktualisiert wurden, werden die Daten exportiert und an Streaming-Ziele gesendet.

Der Vorgang, durch den Profile in HTTPS-Nachrichten aggregiert werden, bevor sie an Ziel-API-Endpunkte gesendet werden, wird als *Microbatching* bezeichnet.

Nehmen wir das [Facebook-Ziel](/help/destinations/catalog/social/facebook.md) mit *[konfigurierbarer Aggregationsrichtlinie](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* als Beispiel. Daten werden aggregiert gesendet, wobei der Ziel-Service alle eingehenden Daten aus dem Upstream-Profil-Service nach einem der folgenden Kriterien aggregiert, bevor sie an Facebook gesendet werden:

* Anzahl der Datensätze (maximal 10.000) oder
* Zeitfenster-Intervall (30 Minuten)

Der Schwellenwert, der von den oben genannten zuerst erreicht wird, löst einen Export nach Facebook aus. Im Dashboard [!DNL Facebook Custom Audiences] werden möglicherweise Zielgruppen aus Experience Platform in Schritten von 10.000 Datensätzen angezeigt. Es kann sein, dass alle 10 bis 15 Minuten 10.000 Datensätze angezeigt werden, da die Daten schneller verarbeitet und aggregiert werden als durch das 30-minütige Exportintervall vorgesehen. Außerdem werden sie schneller gesendet, etwa alle 10 bis 15 Minuten, bis alle Datensätze verarbeitet wurden. Wenn für einen Batch von 10.000 Datensätzen nicht genügend Datensätze vorhanden sind, wird die aktuelle Datensatzanzahl gesendet, sobald der Schwellenwert des Zeitfensters erreicht wird. Also werden möglicherweise auch kleinere Batches an Facebook gesendet.

Ein weiteres Beispiel ist das [HTTP-API-Ziel](/help/destinations/catalog/streaming/http-destination.md), das mit `maxUsersPerRequest: 10` über eine Richtlinie zur *[Aggregation nach bestem Bemühen](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* verfügt. Das bedeutet, dass maximal zehn Profile aggregiert werden, bevor ein HTTP-Aufruf an dieses Ziel gesendet wird. Experience Platform versucht jedoch, Profile an das Ziel zu senden, sobald der Ziel-Service aktualisierte Neubewertungsinformationen von einem Upstream-Service erhält.

Die Aggregationsrichtlinie ist konfigurierbar, und das Zielentwickler-Team kann entscheiden, wie die Aggregationsrichtlinie so konfiguriert werden soll, dass die Ratenbeschränkungen der Downstream-API-Endpunkte am besten eingehalten werden. Weitere Informationen zur [Aggregationsrichtlnie](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) finden Sie in der Destination SDK-Dokumentation.

## Exportziele (Unternehmensziele) für Streaming-Profile {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Unternehmensziele sind nur mit [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) verfügbar.

Die [Unternehmensziele](/help/destinations/destination-types.md#streaming-profile-export) in Experience Platform sind Amazon Kinesis, Azure Event Hubs und HTTP-API.

Experience Platform optimiert das Verhalten beim Profilexport für Ihr Unternehmensziel, sodass nur Daten an Ihren API-Endpunkt exportiert werden, wenn relevante Profilaktualisierungen nach der Segmentqualifikation oder anderen wichtigen Ereignissen durchgeführt wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der [Segmentzugehörigkeit](/help/xdm/field-groups/profile/segmentation.md) für mindestens eines der dem Ziel zugeordneten Segmente bestimmt. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder es hat eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) bestimmt. Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig von der Art der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten?

Was die Daten betrifft, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte zu verstehen, nämlich *was den Datenexport an Ihr Unternehmensziel bestimmt* und *welche Daten im Export enthalten sind*.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Dies bedeutet, dass, wenn zugeordnete Segmente den Status ändern (aus `null` nach `realized` oder von `realized` nach `exiting`) oder alle zugeordneten Attribute aktualisiert werden, wird ein Zielexport gestartet.</li><li>Da Identitäten derzeit nicht Unternehmenszielen zugeordnet werden können, bestimmen Änderungen an der Identität eines bestimmten Profils auch die Zielexporte.</li><li>Als Änderung für ein Attribut wird jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass das Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Das `segmentMembership`-Objekt enthält das Segment, das im Aktivierungsdatenfluss zugeordnet ist und für das sich der Status des Profils nach einem Qualifikations- oder Segmentaustrittsereignis geändert hat. Beachten Sie, dass andere nicht zugeordnete Segmente, für die sich das Profil qualifiziert hat, Teil des Zielexports sein können, wenn diese Segmente zu derselben [Zusammenführungsrichtlinie](/help/profile/merge-policies/overview.md) wie das im Aktivierungsdatenfluss zugeordnete Segment gehören. </li><li>Alle Identitäten im `identityMap`-Objekt sind ebenfalls enthalten (Experience Platform unterstützt derzeit keine Identitätszuordnung im Unternehmensziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Unternehmensziele streamen Aufstockungsdaten, wenn Profile für ein Ziel aktiviert werden. Das bedeutet, dass der erste Datenexport nach der Konfiguration eines Aktivierungs-Workflows für ein Ziel Profile enthält, die sich für das aktivierte Segment qualifiziert haben, bevor das Segment dem Ziel zugeordnet wird.

>[!BEGINSHADEBOX]

Betrachten Sie beispielsweise den folgenden Datenfluss an ein HTTP-Ziel, bei dem drei Segmente im Datenfluss ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![Unternehmensziel-Datenfluss](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der *drei zugeordneten Segmente* qualifiziert. Im Datenexport jedoch können im Objekt `segmentMembership` andere nicht zugeordnete Segmente angezeigt werden, wenn dieses bestimmte Profil zu diesem Profil gehört und diese Segmente dieselbe Zusammenführungsrichtlinie wie das Segment verwenden, das den Export ausgelöst hat. Wenn ein Profil sich für das Segment **Kundschaft mit DeLorean-Autos** qualifiziert hat, aber auch zum Segment **Hat „Zurück in die Zukunft“ gesehen** und **Science-Fiction-Fans** gehört, sind diese beiden anderen Segmente ebenfalls im Objekt `segmentMembership` des Datenexports vorhanden, obwohl diese nicht im Datenfluss zugeordnet sind, falls diese dieselbe Zusammenführungsrichtlinie wie das Segment **Kundschaft mit DeLorean-Autos** verwenden.

Aus Sicht der Profilattribute bestimmt jede Änderung an den vier oben zugeordneten Attributen einen Zielexport, und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

>[!ENDSHADEBOX]

>[!TIP]
>
> Beispiele exportierter Daten für verschiedene Unternehmensziele finden Sie in den Dokumentationsseiten für die [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data)-, [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)- und [HTTP-API](/help/destinations/catalog/streaming/http-destination.md#exported-data)-Ziele.

## API-basierte Streaming-Ziele {#streaming-api-based-destinations}

Das Verhalten beim Profilexport für Streaming-Ziele wie Facebook, Trade Desk und andere API-basierte Integrationen ist dem oben beschriebenen Verhalten für Unternehmensziele sehr ähnlich.

Beispiele für Streaming-Ziele sind die Ziele, die zu den [Social-Media- und Werbekategorien](/help/destinations/destination-types.md#categories) im Katalog gehören.

Experience Platform optimiert das Verhalten beim Profilexport für Ihr Streaming-Ziel, sodass nur Daten an Ihre API-basierten Streaming-Ziele exportiert werden, wenn relevante Profilaktualisierungen nach der Segmentqualifikation oder anderen wichtigen Ereignissen durchgeführt wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der [Segmentzugehörigkeit](/help/xdm/field-groups/profile/segmentation.md) für mindestens eines der dem Ziel zugeordneten Segmente bestimmt. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder es hat eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) für einen Identity-Namespace bestimmt, der für diese Zielinstanz für den Export markiert ist. Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.
* Das Einverständnis wurde für ein Profil geändert, wenn die automatisierte Einverständnisdurchsetzung konfiguriert ist und ein Profil sich davon abmeldet. Durch die automatisierte Einverständnisdurchsetzung wird ein Zielgruppenaustritt-Ereignis an das Ziel gesendet, sodass das Profil in keinem Targeting am Ziel enthalten ist.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig von der Art der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten?

Was die Daten betrifft, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte zu verstehen, nämlich was den Datenexport an Ihr Streaming-API-Ziel bestimmt und welche Daten im Export enthalten sind.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Dies bedeutet, dass, wenn zugeordnete Segmente den Status ändern (aus `null` nach `realized` oder von `realized` nach `exiting`) oder alle zugeordneten Attribute aktualisiert werden, wird ein Zielexport gestartet.</li><li>Eine Änderung in der Identitätszuordnung wird als eine Identität definiert, die für das [Identitätsdiagramm](/help/identity-service/ui/identity-graph-viewer.md) des Profils hinzugefügt/entfernt wird – für Identity-Namespaces, die für den Export zugeordnet sind.</li><li>Als Änderung für ein Attribut wird jede Aktualisierung des Attributs definiert – für Attribute, die dem Ziel zugeordnet sind.</li></ul> | <ul><li>Die Segmente, die dem Ziel zugeordnet sind und sich geändert haben, werden in das Objekt `segmentMembership` eingeschlossen. In einigen Szenarien können sie mit mehreren Aufrufen exportiert werden. In einigen Szenarien können auch bestimmte Segmente, die sich nicht geändert haben, in den Aufruf eingeschlossen werden. In jedem Fall werden nur zugeordnete Segmente exportiert.</li><li>Alle Identitäten aus den Namespaces, die dem Ziel im Objekt `identityMap` zugeordnet sind, sind ebenfalls eingeschlossen.</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Streaming-API-Ziele streamen Aufstockungsdaten, wenn Profile für ein Ziel aktiviert werden. Das bedeutet, dass der erste Datenexport nach der Konfiguration eines Aktivierungs-Workflows für ein Ziel Profile enthält, die sich für das aktivierte Segment qualifiziert haben, bevor das Segment dem Ziel zugeordnet wird.

>[!BEGINSHADEBOX]

Betrachten Sie beispielsweise diesen Datenfluss zu einem Streaming-Ziel, bei dem im Datenfluss drei Segmente ausgewählt sind.

![Streaming-Ziel-Datenfluss](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der drei zugeordneten Segmente qualifiziert. Wenn sich ein Profil für das Segment **Kundschaft mit DeLorean-Autos** qualifziert hat, wird dadurch ein Export ausgelöst. Die anderen Segmente (**Stadt - Dallas** und **Grundlegende Site-Aktivität**) kann auch exportiert werden, wenn das Profil dieses Segment mit einem der möglichen Status (`realized` oder `exited`). Nicht zugeordnete Segmente (z. B. **Science-Fiction-Fans**) werden nicht exportiert.

Was die Profilattribute angeht, bestimmt jede Änderung an den drei oben zugeordneten Attributen einen Zielexport.

>[!ENDSHADEBOX]

## Batch-Ziele (dateibasiert) {#file-based-destinations}

Beim Export von Profilen an [dateibasierte Ziele](/help/destinations/destination-types.md#file-based) in Experience Platform gibt es drei Arten von Zeitplänen (siehe unten) und zwei Dateiexportoptionen (vollständige oder inkrementelle Dateien), die Sie verwenden können. Alle diese Einstellungen werden auf Segmentebene festgelegt, selbst wenn mehrere Segmente einem einzelnen Zieldatenfluss zugeordnet sind.

* Geplante Exporte: Konfigurieren Sie ein Ziel, fügen Sie ein oder mehrere Segmente hinzu, wählen Sie aus, ob Sie vollständige oder inkrementelle Dateien exportieren möchten, und bestimmen Sie eine bestimmte Zeit pro Tag oder mehrere Zeitpunkte pro Tag für den Dateiexport. Beispielsweise bedeutet eine Exportzeit von 17 Uhr, dass jedes Profil, das für das Segment qualifiziert ist, um 17 Uhr exportiert wird.
* Nach der Segmentauswertung: Der Export wird sofort nach Ausführung des täglichen Segmentauswertungsauftrags ausgelöst. Das bedeutet, dass die Anzahl der exportierten Profile in der Datei so nah wie möglich an der zuletzt bewerteten Population des Segments liegt.
* Exporte auf Anfrage ([Datei jetzt exportieren](/help/destinations/ui/export-file-now.md)): Basierend auf dem neuesten Segmentauswertungsauftrag wird eine vollständige Datei einmal zusätzlich zu den regelmäßig geplanten Exporten exportiert.

In allen oben genannten Exportsituationen enthalten die exportierten Dateien die Profile, die für den Export qualifiziert sind, sowie die Spalten, die Sie als XDM-Attribute für den Export ausgewählt haben.

>[!TIP]
>
>Wenn ein Streaming-Segment einem Batch-Ziel zugeordnet wird, besteht eine höhere Wahrscheinlichkeit, dass die Anzahl der Profile in der exportierten Datei näher an der Anzahl der Benutzenden im Segment liegt. Dies ist darauf zurückzuführen, dass die aktuelle Segmentauswertung mit größerer Nähe zur Exportzeit durchgeführt wurde.

### Inkrementelle Dateiexporte {#incremental-file-exports}

Ein Profil qualifiziert sich nicht bei jeder Aktualisierung für die Aufnahme in inkrementelle Dateiexporte. Wenn beispielsweise ein Attribut einem Profil hinzugefügt oder daraus entfernt wurde, wird das Profil nicht in den Export eingeschlossen. Nur Profile, bei denen sich das Attribut `segmentMembership` geändert hat, werden in die exportierten Dateien aufgenommen. Das heißt, nur wenn das Profil Teil des Segments wird oder aus dem Segment entfernt wird, wird es in inkrementelle Dateiexporte einbezogen.

Wenn eine neue Identität (neue E-Mail-Adresse, Telefonnummer, ECID usw.) einem Profil im [Identitätsdiagramm](/help/identity-service/ui/identity-graph-viewer.md) hinzugefügt wird, stellt dies auch keinen Grund dar, das Profil in einen neuen inkrementellen Dateiexport einzuschließen.

Wenn einer Zielzuordnung ein neues Segment hinzugefügt wird, hat dies keine Auswirkungen auf Qualifikationen und Exporte für ein anderes Segment. Exportpläne werden für jedes Segment einzeln konfiguriert und Dateien werden separat für jedes Segment exportiert, selbst wenn die Segmente demselben Zieldatenfluss hinzugefügt wurden.

>[!BEGINSHADEBOX]

Beachten Sie beispielsweise in der unten dargestellten Exporteinstellung, bei der ein Segment inkrementelle Dateiaktualisierungen exportiert, folgende Umstände, unter denen ein Profil in einen inkrementellen Dateiexport eingeschlossen oder nicht eingeschlossen wird:

![Exporteinstellung mit mehreren ausgewählten Attributen](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Ein Profil wird in einen inkrementellen Dateiexport eingeschlossen, wenn es für das Segment qualifiziert oder nicht qualifiziert ist.
* Ein Profil wird *nicht* in einen inkrementellen Dateiexport eingeschlossen, wenn dem Identitätsdiagramm eine neue Telefonnummer hinzugefügt wird.
* Ein Profil wird *nicht* in einen inkrementellen Dateiexport eingeschlossen, wenn der Wert eines zugeordneten XDM-Felds wie `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` in einem Profil aktualisiert wird.
* Sobald das XDM-Feld `segmentMembership.status` im Zielaktivierungs-Workflow zugeordnet wird, werden Profile, die das Segment verlassen, ebenfalls mit einem `exited`-Status in exportierte inkrementelle Dateien eingeschlossen.

>[!ENDSHADEBOX]

### Was bestimmt einen Datenexport und was ist im Export enthalten?

Basierend auf den Informationen im obigen Abschnitt kann das Verhalten beim Profilexport an dateibasierte Ziele wie unten beschrieben zusammengefasst werden:

**Vollständige Dateiexporte**

Die gesamte aktive Population des Segments wird täglich exportiert.

| Was einen Zielexport bestimmt | In der exportierten Datei enthaltene Informationen |
|---------|----------|
| <ul><li>Der in der Benutzeroberfläche oder API festgelegte Exportzeitplan und die Benutzeraktion (Auswahl von [Datei jetzt exportieren](/help/destinations/ui/export-file-now.md) in der Benutzeroberfläche oder Verwendung der [Ad-hoc-Aktivierungs-API](/help/destinations/api/ad-hoc-activation-api.md)) bestimmen den Start eines Zielexports.</li></ul> | In vollständigen Dateiexporten wird die gesamte aktive Profilpopulation eines Segments, basierend auf der neuesten Segmentauswertung, in jeden Dateiexport eingeschlossen. Die neuesten Werte für jedes für den Export ausgewählte XDM-Attribut werden ebenfalls als Spalten in jeder Datei eingeschlossen. Beachten Sie, dass Profile mit dem Status „Beendet“ nicht in den Dateiexport eingeschlossen werden. |

{style="table-layout:fixed"}

**Inkrementelle Dateiexporte**

Im ersten Dateiexport nach der Einrichtung des Aktivierungs-Workflows wird die gesamte Population des Segments exportiert. In nachfolgenden Exporten werden nur die geänderten Profile exportiert.

| Was einen Zielexport bestimmt | In der exportierten Datei enthaltene Informationen |
|---------|----------|
| <ul><li>Der in der Benutzeroberfläche oder API festgelegte Exportzeitplan bestimmt den Start eines Zielexports.</li><li>Alle Änderungen an der Segmentzugehörigkeit eines Profils, unabhängig davon, ob es für das Segment qualifiziert oder nicht qualifiziert ist, qualifizieren ein Profil für die Aufnahme in inkrementelle Exporte. Änderungen an Attributen oder Identitätszuordnungen für ein Profil qualifizieren ein Profil *nicht* für die Aufnahme in inkrementelle Exporte.</li></ul> | <p>Die Profile, für die die Segmentzugehörigkeit geändert wurde, sowie die neuesten Informationen zu jedem für den Export ausgewählten XDM-Attribut.</p><p>Profile mit dem Status „Beendet“ werden in Zielexporte eingeschlossen, wenn im Zuordnungsschritt das XDM-Feld `segmentMembership.status` ausgewählt wird.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Zur Erinnerung: Änderungen an Attributwerten oder Identitätszuordnungen für ein Profil qualifizieren ein Profil nicht für die Aufnahme in einen inkrementellen Dateiexport.

## Nächste Schritte {#next-steps}

Nachdem Sie dieses Dokuments gelesen haben, wissen Sie jetzt, was Sie bei Profilexporten an Streaming-, Unternehmens- und dateibasierten Ziele erwarten können.

Als Nächstes können Sie mehr darüber erfahren, wie [Identitäten im Aktivierungs-Workflow verarbeitet werden](/help/destinations/how-destinations-work/identity-handling.md).
