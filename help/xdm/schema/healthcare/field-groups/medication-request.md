---
title: Feldgruppe für das Medikationsanforderungsschema
description: Erfahren Sie mehr über die Schemafeldgruppe „Medikamentenanfrage“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8502380f-9557-4ca6-84bc-65010dfc6066
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL Medikationsanfrage] Schemafeldgruppe

[!UICONTROL Medikationsanfrage] ist eine Standardschemafeldgruppe für die [[!DNL Medication] Klasse](../../../classes/medication.md), die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es bietet ein einzelnes Objektartfeld, `healthcareMedicationDispense` einen Auftrag oder eine Anfrage sowohl für die Lieferung des Medikaments als auch für die Anweisungen für die Verabreichung des Medikaments an einen Patienten erfasst.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/medication-request/medication-request.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL basierend auf] | `basedOn` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Der Plan oder die Anfrage, die von dieser Medikamentenanfrage erfüllt wird. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Kategorisierung oder Gruppierung der Medikamentenanfrage. |
| [!UICONTROL Verlauf der Therapie Typ] | `courseOfTherapyType` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Beschreibung des Gesamtmusters für die Verabreichung des Medikaments an den Patienten. |
| [!UICONTROL Gerät] | `device` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Die Art des Geräts, das für die Verabreichung des Arzneimittels verwendet werden soll. |
| [!UICONTROL Anfrage ausgeben] | `dispenseRequest` | Objekt | Gibt die spezifischen Details der Ausgabeanfrage an, häufig als Medikamentenanweisung bezeichnet. Weitere Informationen finden [&#x200B; im &#x200B;](#dispense-request) Abschnitt unten. |
| [!UICONTROL Dosierungsanleitung] | `dosageInstructions` | Array von [[!UICONTROL Dosierung]](../data-types/dosage.md) | Spezifische Anweisungen, wie das Arzneimittel vom Patienten anzuwenden ist. |
| [!UICONTROL Wirksamer Dosiszeitraum] | `effectiveDosePeriod` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, über den das Medikament eingenommen werden soll. Bei mehreren `dosageInstruction` (z. B. beim Ausschleichen der Dosis) ist dies das früheste Datum und das letzte Datum der Dosierungsanleitung. |
| [!UICONTROL Begegnung] | `encounter` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Begegnung, während der die Anfrage erstellt wurde. |
| [!UICONTROL Ereignisverlauf] | `eventHistory` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Verknüpfung zu Aufzeichnungen von Ereignissen im Zusammenhang mit der Medikamentenanfrage, wie z. B. die Erfüllung der Anfrage, Momente wichtiger Statusübergänge oder relevante Aktualisierungen. |
| [!UICONTROL Gruppenkennung] | `groupIdentifier` | [[!UICONTROL ID]](../data-types/identifier.md) | Eine freigegebene Kennung über mehrere unabhängige Anfrageinstanzen hinweg, die von einem einzelnen Autor aktiviert wurden. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Mit der Medikamentenanfrage verknüpfte Kennungen, die von Geschäftsprozessen definiert und/oder verwendet werden, um darauf zu verweisen, wenn ein direkter URL-Verweis auf die Ressource selbst nicht geeignet ist. |
| [!UICONTROL Informationen Source] | `informationSource` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Die Person oder Organisation, die die Informationen für die Anfrage bereitgestellt hat, wenn die Quelle eine andere Person als die `requester` ist. |
| [!UICONTROL Versicherung] | `insurance` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Versicherungspläne, Deckungserweiterungen, Vorabgenehmigungen und/oder Vorabbestimmungen, die für die Erbringung der angeforderten Dienstleistung erforderlich sein können. |
| [!UICONTROL Medizin] | `medication` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Identifiziert das angeforderte Medikament. Dies sollte ein Link zu einer Ressource sein, die Details des Medikaments darstellt, oder ein Code, der das Medikament identifiziert. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Zusätzliche Informationen über die Verschreibung, die von den anderen Attributen nicht vermittelt werden konnten. |
| [!UICONTROL Ausführende] | `performer` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Der spezifizierte Ausführende der medikamentösen Behandlung/Verabreichung. Bei Produkten ist dies das Gerät, das die Verabreichung des Medikaments durchführen soll. |
| [!UICONTROL Ausführenden-Typ] | `performerType` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Gibt die Art des Ausführenden für die Verabreichung des Medikaments an. |
| [!UICONTROL Voranmeldung] | `priorPrescription` | [[!UICONTROL Referenz]](../data-types/reference.md) | Der Verweis auf eine Bestellung oder ein Rezept, die durch diesen Antrag ersetzt wird. |
| [!UICONTROL Grund] | `reason` | Array von [[!UICONTROL Codeable Reference]](../data-types/reference.md) | Der Grund oder Hinweis für die Bestellung oder Nichtbestellung des Medikaments. |
| [!UICONTROL Rekorder] | `recorder` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Person, die den Auftrag im Namen einer anderen Person eingegeben hat. |
| [!UICONTROL Auftraggeber] | `requester` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Person, Organisation oder das Gerät, die bzw. das die Anfrage initiiert hat und für deren Aktivierung verantwortlich ist. |
| [!UICONTROL Statusgrund] | `statusReason` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Grund für den aktuellen Status der Anfrage. |
| [!UICONTROL Betreff] | `subject` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Person oder Gruppe, für die das Medikament beantragt wurde. |
| [!UICONTROL Substitution] | `substitution` | Objekt | Gibt an, ob eine Substitution Teil der Abgabe sein kann oder nicht. Enthält drei Eigenschaften: <li>`allowedBoolean`: Ein boolescher Wert, der „true“ ist, wenn der verschreibende Arzt eine Substitution zulässt.</li> <li>`allowedCodeableConcept`: Ein [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md)-Wert, der einen Code bereitstellt, wenn der verschreibende Arzt eine Ersetzung zulässt.</li> <li>`reason`: Ein [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md)-Wert, der einen Grund für die Ersetzung angibt.</li> |
| [!UICONTROL unterstützende Informationen] | `supportingInformation` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Informationen zur Unterstützung bei der Erfüllung des Medikaments, z. B. Größe und Gewicht des Patienten. |
| [!UICONTROL Erstellt am] | `authoredOn` | DateTime | Das Datum (und optional die Uhrzeit), an dem das Rezept ausgestellt wurde. |
| [!UICONTROL Nicht ausführen] | `doNotPerform` | Boolesch | Ein boolescher Indikator, der wahr ist, ist, dass der Patient die Einnahme des Medikaments beenden (oder nicht beginnen) sollte. |
| [!UICONTROL Intent] | `intent` | String | Die Absicht der Anfrage. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Priorität] | `priority` | String | Die Priorität der Anfrage. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL gerenderte Dosierungsanweisung] | `renderedDosageInstruction` | String | Die vollständige Darstellung der Dosis, die in allen Dosierungsanweisungen enthalten ist. Wird verwendet, wenn mehrere Dosierungsanweisungen enthalten sind, um komplexe Dosierungen wie die Erhöhung oder das Ausschleichen darzustellen. |
| [!UICONTROL Gemeldet] | `reported` | Boolesch | Gibt an, ob dieser Datensatz als sekundärer gemeldeter Datensatz und nicht als ursprünglicher primärer Quell-der-Wahrheit-Datensatz erfasst wurde. |
| [!UICONTROL Status] | `status` | String | Der Status der Ausgabe. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status geändert] | `statusChanged` | DateTime | Das Datum (und optional die Uhrzeit), an dem der Status von geändert wurde. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Struktur der Ausgabenanfrage](../../../images/healthcare/field-groups/medication-request/dispense-request.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ausgabeintervall] | `dispenseInterval` | [[!UICONTROL Dauer]](../data-types/duration.md) | Der Mindestzeitraum, der zwischen der Abgabe des Arzneimittels eintreten muss. |
| [!UICONTROL Dispenser] | `dispenser` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die beabsichtigte Organisation, die das Arzneimittel gemäß den Angaben des verschreibenden Arztes abgibt. |
| [!UICONTROL Ausgabebefehl] | `dispenserInstruction` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Zusätzliche Informationen für den Spender, z. B. Beratung für den Patienten |
| [!UICONTROL Dosisverabreichungshilfe] | `doseAdministrationAid` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Informationen über die Art der für die Medikamentenabgabe zu liefernden Adhärenzverpackung. |
| [!UICONTROL Erwartete Lieferdauer] | `expectedSupplyDuration` | [[!UICONTROL Dauer]](../data-types/duration.md) | Der Zeitraum, über den das gelieferte Produkt voraussichtlich verwendet wird, oder die Dauer der Ausgabe. |
| [!UICONTROL Erstausfüllung] | `initialFill` | Objekt | Informationen zum ersten Ausfüllen. Enthält zwei Eigenschaften: <li>`quantity`: Ein [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md)-Wert, der den Betrag angibt, der bei der ersten Ausgabe bereitgestellt werden soll.</li> <li>`duration`: Ein [[!UICONTROL Dauer]](../data-types/duration.md)-Wert, der die Zeitdauer angibt, für die die erste Ausgabe voraussichtlich gültig ist.</li> |
| [!UICONTROL Menge] | `quantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Menge, die für eine Füllung ausgegeben werden soll. |
| [!UICONTROL Gültigkeitszeitraum] | `validityPeriod` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Die Gültigkeitsdauer der Verschreibung. |
| [!UICONTROL Anzahl der zulässigen Wiederholungen] | `numberOfRepeatsAllowed` | Ganzzahl | Die Anzahl der zulässigen Nachfüllungen mit einem Mindestwert von 0. |
