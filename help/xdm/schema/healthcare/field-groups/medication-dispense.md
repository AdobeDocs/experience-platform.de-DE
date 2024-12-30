---
title: Feldergruppe „Medikamentenabgabe-Schema“
description: Erfahren Sie mehr über die Schemafeldgruppe „Medikamentenabgabe“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e897c4e0-23ad-4d79-834f-cfbe2dbec771
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 4%

---

# [!UICONTROL Medikamentenabgabe] Schemafeldgruppe

[!UICONTROL Medikamentenabgabe] ist eine Standardschemafeldgruppe für die [[!DNL Medication] Klasse](../../../classes/medication.md), die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es wird ein einzelnes Objekttyp-Feld bereitgestellt, `healthcareMedicationDispense` Informationen über ein Medikament erfasst, das für eine bestimmte Person/Patient abgegeben werden soll oder wurde.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/medication-dispense/medication-dispense.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zulassung von Verschreibungen] | `authorizingPrescription` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Die Reihenfolge, die die Abgabe der Verschreibung erlaubt. |
| [!UICONTROL basierend auf] | `basedOn` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Der Plan für die Abgabe des Medikaments basiert auf. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Kategorie, unter die das Medikament abgegeben wird, fällt, wie die rechtliche Kategorie des Medikaments oder die Arzneimittelklassifizierung. |
| [!UICONTROL Tage Vorrat] | `daysSupply` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Anzahl der Tage, die das Medikament dem Patienten zur Verfügung stellt. |
| [!UICONTROL Ziel] | `destination` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Einrichtung oder der Ort, an die bzw. den das Medikament im Rahmen des Ausgabevorgangs versendet wurde oder werden wird. |
| [!UICONTROL Dosierungsanleitung] | `dosageInstruction` | Array von [[!UICONTROL Dosierung]](../data-types/dosage.md) | Beschreibt, wie das Medikament vom Patienten angewendet werden soll. |
| [!UICONTROL Begegnung] | `encounter` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Begegnung, die den Kontext für dieses Ereignis festlegt. |
| [!UICONTROL Ereignisverlauf] | `eventHistory` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Eine Zusammenfassung der Ereignisse, die bei der Abgabe aufgetreten sind. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Kennungen, die mit der Abgabe verbunden sind. Die Kennungen sollten durch Geschäftsprozesse definiert und/oder verwendet werden, um darauf zu verweisen, wenn ein direkter URL-Verweis nicht geeignet ist. |
| [!UICONTROL Ort] | `location` | [[!UICONTROL Referenz]](../data-types/reference.md) | Der physische Hauptort, an dem das Medikament abgegeben wurde. |
| [!UICONTROL Medizin] | `medication` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Identifiziert das angeforderte Medikament. Dies sollte ein Link zu einer Ressource sein, die Details des Medikaments darstellt, oder ein Code, der das Medikament identifiziert. |
| [!UICONTROL Grund nicht ausgeführt] | `notPerformedReason` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Der Grund, warum das Medikament nicht abgegeben wurde. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Zusätzliche Informationen zur Abgabe. |
| [!UICONTROL Teil von] | `partOf` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Das Verfahren oder die Medikamentenanfrage, die die Abgabe ausgelöst hat. |
| [!UICONTROL Ausführende] | `performer` | Array von Objekten | Gibt an, wer oder was den Abgabefall durchgeführt hat. Weitere Informationen finden [ im ](#performer) Abschnitt unten. |
| [!UICONTROL Menge] | `quantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die Menge des abgegebenen Arzneimittels, einschließlich der Maßeinheit. |
| [!UICONTROL Receiver] | `receiver` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Identifiziert die Person, die das Medikament aufgenommen hat, oder den Ort, an dem das Medikament abgegeben wurde. |
| [!UICONTROL Betreff] | `subject` | [[!UICONTROL Referenz]](../data-types/reference.md) | Ein Link zu einer Ressource, die die Person oder Gruppe repräsentiert, der das Medikament gegeben wird. |
| [!UICONTROL Substitution] | `substitution` | Objekt | Gibt an, ob im Rahmen der Abgabe eine Substitution vorgenommen wurde. Enthält vier Eigenschaften: <li>`wasSubstituted`: Ein boolescher Wert, der „true“ ist, wenn der Dispenser eine Ersetzung angefordert hat.</li> <li>`type`: Ein [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md)-Wert, der einen Code bereitstellt, der angibt, ob eine Ersetzung vorgenommen wurde.</li> <li>`reason`: Ein Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md)-Werten, das den Grund (die Gründe) für die Ersetzung enthält.</li> <li>`responsibleParty`: Ein [[!UICONTROL Referenz]](../data-types/reference.md)-Wert, der die für die Ersetzung verantwortliche Person oder Partei angibt. </li> |
| [!UICONTROL unterstützende Informationen] | `supportingInformation` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Zusätzliche Informationen, die die Abgabe des Medikaments unterstützen. |
| [!UICONTROL Typ] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beschreibt die Art des durchgeführten Spendeereignisses, z. B. eine Notfüllung oder eine Teilfüllung. |
| [!UICONTROL aufgezeichnet] | `recorded` | DateTime | Das Datum und die Uhrzeit, zu der die Ausgabetätigkeit gestartet wurde, wenn `whenPrepared` oder `whenHandedOver` nicht ausgefüllt ist. |
| [!UICONTROL gerenderte Dosierungsanweisung] | `renderedDosageInstruction` | String | Die vollständige Darstellung der Dosis, die in allen Dosierungsanweisungen enthalten ist. Wird verwendet, wenn mehrere Dosierungsanweisungen enthalten sind, um komplexe Dosierungen wie die Erhöhung oder das Ausschleichen darzustellen. |
| [!UICONTROL Status] | `status` | String | Der Status der Ausgabe. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status geändert] | `statusChanged` | DateTime | Datum und Uhrzeit der Änderung des Status des Ausgabedatensatzes. |
| [!UICONTROL Bei Übergabe] | `whenHandedOver` | DateTime | Datum und Uhrzeit der Abgabe des Medikaments an den Patienten. |
| [!UICONTROL Wenn vorbereitet] | `whenPrepared` | DateTime | Datum und Uhrzeit der Verpackung und Überprüfung des abgegebenen Arzneimittels. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Leistungsstruktur](../../../images/healthcare/field-groups/medication-dispense/performer.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Schauspieler] | `actor` | [[!UICONTROL Referenz]](../data-types/reference.md) | Der Praktizierende (oder eine ähnliche Person), der die Aktion ausgeführt hat. Es sollte angenommen werden, dass der Akteur der Spender des Medikaments ist. |
| [!UICONTROL Funktion] | `function` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Typ des Ausführenden bei der Ausgabe, z. B. die Datumsangabe, der Verpacker oder die Endkontrolle. |
