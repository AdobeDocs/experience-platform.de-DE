---
title: Schema-Feldgruppe für Betreuung
description: Erfahren Sie mehr über die Schemafeldgruppe Care Plan .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL Care Plan] Schemafeldgruppe

[!UICONTROL Care Plan] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Es stellt ein einzelnes Objektfeld `healthcareCarePlan` bereit, das einen Gesundheitsplan für einen Patienten oder eine Gruppe erfasst.

![Feldgruppenstruktur](../../images/field-groups/healthcare-care-plan/care-plan.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Aktivität] | `activity` | Array von Objekten | Identifiziert eine Aktion, die im Rahmen des Plans stattgefunden hat oder geplant ist. Weitere Informationen finden Sie im Abschnitt [unter ](#activity) . |
| [!UICONTROL Adressen] | `addresses` | Array von [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Identifiziert die Bedingungen oder Bedenken, die der Pflegeplan behandelt. |
| [!UICONTROL basierend auf ] | `basedOn` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Eine Anforderungsressource auf höherer Ebene, die ganz oder teilweise durch diesen Pflegeplan erfüllt wird. |
| [!UICONTROL Care Team] | `careTeam` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Identifiziert alle Personen und Organisationen, von denen erwartet wird, dass sie an der in diesem Plan vorgesehenen Betreuung beteiligt sind. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Gibt an, welche Art von Plan dies zur Unterstützung der Differenzierung zwischen mehreren bereits existierenden Plänen darstellt. |
| [!UICONTROL Contributor] | `contributor` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Identifiziert die Person(en), Organisation oder das Gerät, die/das den Inhalt des Pflegeplans bereitgestellt hat/haben. |
| [!UICONTROL Verwahrer] | `custodian` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Wenn der Kunde ausgefüllt ist, ist er für den Pflegeplan verantwortlich und ihm zugeordnet. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Begegnung, bei der der Pflegeplan erstellt wurde. |
| [!UICONTROL Ziel] | `goal` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Das Ziel/die Ziele der Durchführung des Plans. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../../data-types/healthcare/identifier.md) | Die diesem Pflegeplan vom Leister oder anderen Systemen zugewiesenen Geschäftskennungen, die konstant bleiben, wenn die Ressource aktualisiert wird und von Server zu Server übertragen wird. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../../data-types/healthcare/annotation.md) | Allgemeine Hinweise zum Pflegeplan, der nicht in anderen Attributen behandelt wird. |
| [!UICONTROL Teil von ] | `partOf` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Der größere Pflegeplan, in dem dieser besondere Pflegeplan eine Komponente oder ein Schritt ist. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../../data-types/healthcare/period.md) | Gibt an, wann und wann der Plan in Kraft getreten ist (oder sein soll). |
| [!UICONTROL ersetzt] | `replaces` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Der abgeschlossene oder beendete Pflegeplan, dessen Funktion von diesem Pflegeplan übernommen wird. |
| [!UICONTROL Betreff] | `subject` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Identifiziert den Patienten oder die Gruppe, dessen beabsichtigte Versorgung im Plan beschrieben wird. |
| [!UICONTROL Unterstützende Informationen] | `supportingInfo` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Identifiziert Teile der Patientenakte, die die Bildung des Plans beeinflussten. Dazu zählen Komorbiditäten, aktuelle Verfahren, Einschränkungen oder aktuelle Bewertungen. |
| [!UICONTROL Erstellt] | `created` | DateTime | Gibt an, wann dieser Pflegeplan im System erstellt wurde, was häufig ein vom System erstelltes Datum ist. |
| [!UICONTROL Beschreibung] | `description` | String | Beschreibung des Umfangs und der Art des Plans. |
| [!UICONTROL Instanziiert Canonical] | `instantiatesCanonical` | Zeichenfolgen-Array | Die URL, die auf ein vom FHIR definiertes Protokoll, eine Richtlinie, einen Fragebogen oder eine andere Definition verweist, die ganz oder teilweise von diesem Plan eingehalten wird. |
| [!UICONTROL instanziiert Uri] | `instantiatesUri` | Zeichenfolgen-Array | Die URL, die auf ein extern gepflegtes Protokoll, eine Richtlinie, einen Fragebogen oder eine andere Definition verweist, die ganz oder teilweise von diesem Plan eingehalten wird und als URI dargestellt wird. |
| [!UICONTROL Intent] | `intent` | String | Die Absicht des Pflegeplans. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Status] | `status` | String | Der Status des Pflegeplans. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Titel] | `title` | String | Der Name des Pflegeplans. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Aktivitätsstruktur](../../images/field-groups/healthcare-care-plan/activity.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ausgeführte Aktivität] | `performedActivity` | Array von [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Ergebnisse der Tätigkeit, wie z. B. Bestellung oder Verfahren. |
| [!UICONTROL Referenz zu geplanten Aktivitäten] | `plannedActivityReference` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Einzelheiten der vorgeschlagenen Aktivität. |
| [!UICONTROL Progress] | `progress` | Array von [[!UICONTROL Anmerkung]](../../data-types/healthcare/annotation.md) | Hinweise zur Treue, zum Status oder zum Fortschritt der Aktivität. |
