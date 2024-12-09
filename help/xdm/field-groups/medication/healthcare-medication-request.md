---
title: Feldergruppe für Mediationsanfrage
description: Erfahren Sie mehr über die Feldergruppe Medikationsanforderung .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL Schemafeldgruppe für Vermittlungsanfrage]

[!UICONTROL Mediation Request] ist eine Standardschemafeldgruppe für die [[!DNL Medication] Klasse](../../classes/location.md), die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md) und die [[!DNL Provider class]](../../classes/provider.md). Es bietet ein einzelnes Objektfeld `healthcareMedicationDispense`, das eine Bestellung oder einen Antrag für die Lieferung des Arzneimittels und die Anweisungen für die Verabreichung des Arzneimittels an einen Patienten erfasst.

![Feldgruppenstruktur](../../images/field-groups/healthcare-medication-request/medication-request.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL basierend auf ] | `basedOn` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Der Plan oder Antrag, der durch diesen Antrag auf Medikamente erfüllt wird. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Die Kategorisierung oder Gruppierung des Arzneimittelantrags. |
| [!UICONTROL Therapieverlauf] | `courseOfTherapyType` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Beschreibung des Gesamtmusters für die Verabreichung des Arzneimittels an den Patienten. |
| [!UICONTROL Gerät] | `device` | Array von [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Die Art der Vorrichtung, die für die Verabreichung des Arzneimittels verwendet werden soll. |
| [!UICONTROL Anfrage verwerfen] | `dispenseRequest` | Objekt | Gibt die spezifischen Details des Ersuchens um eine Abgabe an, die häufig als Arzneimittelbestellung bezeichnet wird. Weitere Informationen finden Sie im Abschnitt [unter ](#dispense-request) . |
| [!UICONTROL Dosierungsanleitung] | `dosageInstructions` | Array von [[!UICONTROL Dosierung]](../../data-types/healthcare/dosage.md) | Spezifische Anweisungen für die Verwendung der Medikation durch den Patienten. |
| [!UICONTROL Wirksamer Dosierzeitraum] | `effectiveDosePeriod` | [[!UICONTROL Zeitraum]](../../data-types/healthcare/period.md) | Der Zeitraum, über den die Medikation eingenommen werden soll. Bei mehreren `dosageInstruction`-Zeilen (z. B. bei der Dosisreduktion) ist dies das früheste Datum und das letzte Datum der Dosiseinstellungen. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Begegnung, bei der die Anfrage erstellt wurde. |
| [!UICONTROL Ereignisverlauf] | `eventHistory` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Link zu Aufzeichnungen von Ereignissen im Zusammenhang mit der Arzneimittelanforderung, z. B. die Erfüllung der Anfrage, Momente der wichtigsten Statusübergänge oder relevante Aktualisierungen. |
| [!UICONTROL Gruppenkennung] | `groupIdentifier` | [[!UICONTROL ID]](../../data-types/healthcare/identifier.md) | Eine gemeinsam genutzte ID für mehrere unabhängige Anfrageinstanzen, die von einem einzelnen Autor aktiviert wurden. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../../data-types/healthcare/identifier.md) | Kennungen, die mit der Arzneimittelanforderung verknüpft sind und durch Geschäftsprozesse definiert werden und/oder verwendet werden, um darauf zu verweisen, wenn eine direkte URL-Referenz auf die Ressource selbst nicht geeignet ist. |
| [!UICONTROL Information Source] | `informationSource` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Die Person oder Organisation, die die Informationen für die Anfrage bereitgestellt hat, wenn es sich bei der Quelle um eine andere Person als die `requester` handelt. |
| [!UICONTROL Versicherung] | `insurance` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Versicherungspläne, Verlängerungen der Versicherungsdeckung, Vorabgenehmigungen und/oder Vorfeststellungen, die für die Erbringung der angeforderten Dienstleistung erforderlich sein können. |
| [!UICONTROL Meditation] | `medication` | [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Identifiziert das angeforderte Arzneimittel. Dies sollte ein Link zu einer Ressource sein, die Details des Arzneimittels darstellt, oder ein Code, der das Arzneimittel identifiziert. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../../data-types/healthcare/annotation.md) | Zusätzliche Informationen über die Verschreibung, die von den anderen Attributen nicht vermittelt werden konnten. |
| [!UICONTROL Performer] | `performer` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Der spezifizierte Darsteller der Medikationsbehandlung/-verabreichung. Bei Produkten ist dies das Gerät, das die Verabreichung der Medikation durchführen soll. |
| [!UICONTROL Performer-Typ] | `performerType` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Gibt die Art des Leisters für die Verabreichung des Arzneimittels an. |
| [!UICONTROL Vorherige Verschreibung] | `priorPrescription` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Der Verweis auf eine Bestellung oder ein Rezept, die durch diese Anfrage ersetzt wird. |
| [!UICONTROL Grund] | `reason` | Array von [[!UICONTROL Codeable Reference]](../../data-types/healthcare/reference.md) | Grund oder Indikation für die Bestellung oder Nichtbestellung des Arzneimittels. |
| [!UICONTROL Recorder] | `recorder` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Person, die den Auftrag für eine andere Person erteilt hat. |
| [!UICONTROL Anforderer] | `requester` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Person, Organisation oder das Gerät, die/das die Anfrage initiiert hat und für die Aktivierung verantwortlich ist. |
| [!UICONTROL Statusgrund] | `statusReason` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Der Grund für den aktuellen Status der Anfrage. |
| [!UICONTROL Betreff] | `subject` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Person oder Gruppe, für die das Arzneimittel beantragt wurde. |
| [!UICONTROL Substitution] | `substitution` | Objekt | Gibt an, ob eine Substitution Teil der Ausgabedarstellung sein kann oder sollte. Enthält drei Eigenschaften: <li>`allowedBoolean`: Ein boolescher Wert, der &quot;true&quot;ist, wenn der verschreibende Arzt eine Ersetzung erlaubt.</li> <li>`allowedCodeableConcept`: Ein [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) -Wert, der einen Code bereitstellt, wenn der verschreibende Benutzer eine Ersetzung zulässt.</li> <li>`reason`: Ein Wert vom Typ [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) , der einen Grund für die Ersetzung angibt.</li> |
| [!UICONTROL Unterstützende Informationen] | `supportingInformation` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Informationen, die die Erfüllung der Medikamente unterstützen, wie z.B. Größe und Gewicht des Patienten. |
| [!UICONTROL Verfasst am] | `authoredOn` | DateTime | Datum (und optional Uhrzeit), an dem die Verschreibung geschrieben wurde. |
| [!UICONTROL Nicht ausführen] | `doNotPerform` | Boolesch | Ein boolescher Indikator, der wahr ist, ist, dass der Patient die Einnahme der Medikation stoppen (oder nicht starten) sollte. |
| [!UICONTROL Intent] | `intent` | String | Der Zweck der Anfrage. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Priorität] | `priority` | String | Die Priorität der Anfrage. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL Rendered Dose Instruction] | `renderedDosageInstruction` | String | Die vollständige Darstellung der Dosis ist in allen Dosierungsanweisungen enthalten. Bei Mehrfachdosierungsanweisungen zur Darstellung einer komplexen Dosierung wie Erhöhung oder Verschlankung der Dosen zu verwenden. |
| [!UICONTROL Gemeldet] | `reported` | Boolesch | Gibt an, ob dieser Datensatz als sekundärer gemeldeter Datensatz und nicht als ursprüngliche primäre &quot;Source of Truth&quot;-Datensatz erfasst wurde. |
| [!UICONTROL Status] | `status` | String | Der Status der Ausgabe. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status geändert] | `statusChanged` | DateTime | Das Datum (und optional die Uhrzeit), an dem sich der Status von geändert hat. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Anforderungsstruktur verwerfen](../../images/field-groups/healthcare-medication-request/dispense-request.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ausgabenintervall] | `dispenseInterval` | [[!UICONTROL Dauer]](../../data-types/healthcare/duration.md) | Die Mindestdauer, die zwischen den Arzneimittelabgaben liegen muss. |
| [!UICONTROL Dispenser] | `dispenser` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die beabsichtigte Organisation, die das Arzneimittel gemäß den Angaben des verschreibenden Arztes abgeben wird. |
| [!UICONTROL Dispenser Instruction] | `dispenserInstruction` | Array von [[!UICONTROL Anmerkung]](../../data-types/healthcare/annotation.md) | Zusätzliche Informationen für den Spender, wie z. B. die Beratung des Patienten |
| [!UICONTROL Dosierung Administration Aid] | `doseAdministrationAid` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Informationen über die Art der Beipackzettel, die für das Arzneimittel zu liefern sind. |
| [!UICONTROL Erwartete Lieferdauer] | `expectedSupplyDuration` | [[!UICONTROL Dauer]](../../data-types/healthcare/duration.md) | Der Zeitraum, über den das gelieferte Produkt voraussichtlich verwendet wird, oder die Dauer der Abgabe. |
| [!UICONTROL Ursprüngliche Füllung] | `initialFill` | Objekt | Informationen für die erste Füllung. Enthält zwei Eigenschaften: <li>`quantity`: Ein Wert vom Typ [[!UICONTROL Einfache Menge]](../../data-types/healthcare/simple-quantity.md) , der den Betrag bereitstellt, der während der ersten Ausgabe bereitgestellt werden soll.</li> <li>`duration`: Ein [[!UICONTROL Dauer]](../../data-types/healthcare/duration.md) -Wert, der angibt, wie lange das erste Ausgabeformat dauern soll.</li> |
| [!UICONTROL Quantity] | `quantity` | [[!UICONTROL Einfache Menge]](../../data-types/healthcare/simple-quantity.md) | Der Betrag, der für eine Füllung ausgegeben werden soll. |
| [!UICONTROL Gültigkeitszeitraum] | `validityPeriod` | [[!UICONTROL Zeitraum]](../../data-types/healthcare/period.md) | Die Gültigkeitsdauer der Verschreibung. |
| [!UICONTROL Anzahl zulässiger Wiederholungen] | `numberOfRepeatsAllowed` | Ganzzahl | Die Anzahl der zugelassenen Nachfüllungen mit einem Mindestwert von 0. |
