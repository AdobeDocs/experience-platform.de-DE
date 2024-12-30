---
title: Feldgruppe des Behandlungsplans
description: Erfahren Sie mehr über die Schemafeldgruppe für den Behandlungsplan.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL Care Plan] Schemafeldgruppe

[!UICONTROL Care Plan] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM Individual Profile] ](../../../classes/individual-profile.md). Es bietet ein einzelnes Objekttyp-Feld, in `healthcareCarePlan` ein Gesundheitsplan für einen Patienten oder eine Gruppe erfasst wird.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Aktivität] | `activity` | Array von Objekten | kennzeichnet eine Aktion, die im Rahmen des Plans stattgefunden hat oder geplant ist. Weitere Informationen finden [ im ](#activity) Abschnitt unten. |
| [!UICONTROL Adressen] | `addresses` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Identifiziert die Bedingungen oder Bedenken, die der Behandlungsplan handhabt. |
| [!UICONTROL basierend auf] | `basedOn` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Eine Anfrageressource auf höherer Ebene, die ganz oder teilweise von diesem Behandlungsplan erfüllt wird. |
| [!UICONTROL Betreuerteam] | `careTeam` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Identifiziert alle Personen und Organisationen, von denen erwartet wird, dass sie an der in diesem Plan vorgesehenen Versorgung beteiligt sind. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Legt fest, welche Art von Plan es ist, um die Unterscheidung zwischen mehreren nebeneinander bestehenden Plänen zu unterstützen. |
| [!UICONTROL Mitwirkender] | `contributor` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Identifiziert die Person(en), die Organisation oder das Gerät, die bzw. das den Inhalt des Behandlungsplans zur Verfügung gestellt hat bzw. haben. |
| [!UICONTROL Verwalter] | `custodian` | [[!UICONTROL Referenz]](../data-types/reference.md) | Nach der Befüllung ist der Betreuer für den Behandlungsplan verantwortlich und dem Betreuungsplan zugeordnet. |
| [!UICONTROL Begegnung] | `encounter` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Begegnung, während der der Behandlungsplan erstellt wurde. |
| [!UICONTROL Ziel] | `goal` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Die beabsichtigten Ziele der Durchführung des Plans. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Die Geschäftskennungen, die diesem Versorgungsplan vom Ausführenden oder anderen Systemen zugewiesen wurden, die konstant bleiben, während die Ressource aktualisiert wird und sich von Server zu Server ausbreitet. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Allgemeine Hinweise zum Behandlungsplan, die nicht von anderen Attributen abgedeckt werden. |
| [!UICONTROL Teil von] | `partOf` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Der größere Behandlungsplan, in dem dieser spezielle Behandlungsplan eine Komponente oder ein Schritt ist. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Gibt an, wann der Plan in Kraft getreten ist (oder treten soll) und wann er beendet wird. |
| [!UICONTROL ersetzt] | `replaces` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Der abgeschlossene oder beendete Behandlungsplan, dessen Funktion von diesem Behandlungsplan übernommen wird. |
| [!UICONTROL Betreff] | `subject` | [[!UICONTROL Referenz]](../data-types/reference.md) | Identifiziert den Patienten oder die Gruppe, dessen bzw. deren vorgesehene Behandlung durch den Plan beschrieben wird. |
| [!UICONTROL Unterstützende Informationen] | `supportingInfo` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | kennzeichnet Teile der Patientenakte, die die Erstellung des Plans beeinflusst haben. Dazu können Komorbiditäten, kürzlich durchgeführte Verfahren, Einschränkungen oder kürzlich durchgeführte Bewertungen gehören. |
| [!UICONTROL Erstellt] | `created` | DateTime | Stellt dar, wann dieser Behandlungsplan im System erstellt wurde, wobei es sich häufig um ein systemgeneriertes Datum handelt. |
| [!UICONTROL Beschreibung] | `description` | String | Eine Beschreibung des Umfangs und der Art des Plans. |
| [!UICONTROL Instanziiert kanonisch] | `instantiatesCanonical` | Zeichenfolgen-Array | Die URL, die auf ein vom FHIR definiertes Protokoll, eine Richtlinie, einen Fragebogen oder eine andere Definition verweist, die ganz oder teilweise von diesem Plan eingehalten wird. |
| [!UICONTROL instanziiert URI] | `instantiatesUri` | Zeichenfolgen-Array | Die URL, die auf ein extern verwaltetes Protokoll, eine Richtlinie, einen Fragebogen oder eine andere Definition verweist, die ganz oder teilweise von diesem Plan eingehalten wird, wird als URI dargestellt. |
| [!UICONTROL Intent] | `intent` | String | Die Absicht des Behandlungsplans. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Status] | `status` | String | Der Status des Behandlungsplans. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Titel] | `title` | String | Der Name des Behandlungsplans. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Aktivitätsstruktur](../../../images/healthcare/field-groups/care-plan/activity.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ausgeführte Aktivität] | `performedActivity` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Die Ergebnisse der Aktivität, z. B. ein Termin oder ein Verfahren. |
| [!UICONTROL Referenz zur geplanten Aktivität] | `plannedActivityReference` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Details der vorgeschlagenen Aktivität. |
| [!UICONTROL Fortschritt] | `progress` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Notizen zur Einhaltung, zum Status oder Fortschritt der Aktivität. |
