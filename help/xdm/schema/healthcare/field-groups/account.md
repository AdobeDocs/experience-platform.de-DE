---
title: Feldgruppe des Kontoschemas
description: Erfahren Sie mehr über die Schemafeldgruppe „Konto“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 376716bd-f79f-421d-b163-0f0e50876b48
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 7%

---

# [!UICONTROL Konto] Schemafeldgruppe

[!UICONTROL Konto] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Sie bietet ein einzelnes Objekttyp-Feld, `healthcareAccount` dem Transaktionen, Dienstleistungen und andere Finanzinformationen im Zusammenhang mit Gesundheitsdienstleistungen erfasst werden, die für einen Patienten oder eine Gruppe von Personen erbracht werden (z. B. für Versicherungs- oder Abrechnungszwecke).

![Feldergruppenstruktur](../../../images/healthcare/field-groups/account/account.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Balance] | `balance` | Array von Objekten | Die vom Finanzsystem berechneten und verarbeiteten Kontostände. Weitere Informationen finden [&#x200B; im &#x200B;](#balances) Abschnitt unten. |
| [!UICONTROL Fakturastatus] | `billingStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Dadurch wird der Lebenszyklus des Kontos während des Abrechnungsprozesses verfolgt. Es zeigt an, wie Transaktionen behandelt werden, wenn sie dem Konto zugeordnet werden. |
| [!UICONTROL Abdeckung] | `coverage` | Array von Objekten | Die Partei(en), die für die Deckung der Kosten dieses Kontos verantwortlich ist (sind), und in welcher Reihenfolge sie angewendet werden sollten. Weitere Informationen finden [&#x200B; im &#x200B;](#coverage) Abschnitt unten. |
| [!UICONTROL Währung] | `currency` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Standardwährung für das Konto. |
| [!UICONTROL Diagnose] | `diagnosis` | Array von Objekten | Die für die Abrechnung relevanten Diagnosen werden hier in dem Konto gespeichert, in dem sie vor der Bearbeitung zur Herstellung von Ansprüchen entsprechend sequenziert werden können. Weitere Informationen finden [&#x200B; im &#x200B;](#diagnosis) Abschnitt unten. |
| [!UICONTROL Garant] | `guarantor` | Array von Objekten | Die für den Kontoausgleich verantwortlichen Parteien, falls andere Zahlungsoptionen nicht ausreichen. Weitere Informationen finden [&#x200B; im &#x200B;](#guarantor) Abschnitt unten. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine eindeutige Kennung, die zum Referenzieren des Kontos verwendet wird. Es kann für den menschlichen Gebrauch bestimmt sein (z. B. Kreditkartennummer). |
| [!UICONTROL Inhaber] | `owner` | [[!UICONTROL Referenz]](../data-types/reference.md) | Gibt den Servicebereich, das Krankenhaus, die Abteilung usw. an. Verantwortlich für die Verwaltung des Kontos. |
| [!UICONTROL Verfahren] | `procedure` | Array von Objekten | Die für die Abrechnung relevanten Vorgänge werden hier auf dem Konto gespeichert, wo sie vor der Bearbeitung zur Herstellung von Ansprüchen entsprechend sequenziert werden können. Weitere Informationen finden [&#x200B; im &#x200B;](#procedure) Abschnitt unten. |
| [!UICONTROL Verknüpftes Konto] | `relatedAccount` | Array von Objekten | Andere mit diesem Konto verknüpfte Konten. Weitere Informationen finden [&#x200B; im &#x200B;](#related-account) Abschnitt unten. |
| [!UICONTROL Dienstzeit] | `servicePeriod` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Datumsbereich der mit diesem Konto verknüpften Services. |
| [!UICONTROL Betreff] | `subject` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Identifiziert das Unternehmen, dem die Kosten entstehen. Während es sich bei den unmittelbaren Empfängern von Dienstleistungen oder Waren um mit dem Gegenstand verbundene Einheiten handeln könnte, wurden die Kosten letztendlich dem Gegenstand des Kontos aufgebürdet. |
| [!UICONTROL Typ] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Kategorisiert das Konto für Reporting- und Suchzwecke. |
| [!UICONTROL Berechnet um] | `calculatedAt` | DateTime | Der Zeitpunkt, zu dem der Saldo berechnet wurde. |
| [!UICONTROL Beschreibung] | `description` | String | Enthält zusätzliche Informationen darüber, was das Konto verfolgt und wie es verwendet wird. |
| [!UICONTROL Name] | `name` | String | Der Name des Kontos. |
| [!UICONTROL Status] | `status` | String | Der Status des Kontos. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> <li> `on-hold` </li> <li> `unknown`</li> |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.schema.json)

## `balances` {#balances}

`balances` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Saldenstruktur](../../../images/healthcare/field-groups/account/balance.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Aggregat] | `aggregate` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Von wem wird erwartet, dass er diesen Teil des Restbetrags zahlt. |
| [!UICONTROL Betrag] | `amount` | [[!UICONTROL Geld]](../data-types/money.md) | Der tatsächliche Saldo, der für das im Begriff „Eigenschaft“ definierte Alter berechnet wurde. |
| [!UICONTROL Begriff] | `term` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Laufzeit des Kontos. |
| [!UICONTROL Schätzung] | `estimate` | Boolesch | Wenn der Betrag ein geschätzter Wert ist. |

## `coverage` {#coverage}

`coverage` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Abdeckungsstruktur](../../../images/healthcare/field-groups/account/coverage.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Abdeckung] | `coverage` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Partei(en), die für die Deckung der Kosten dieses Kontos verantwortlich ist (sind), und in welcher Reihenfolge sie angewendet werden sollten. |
| [!UICONTROL Priorität] | `priority` | Ganzzahl | Die Priorität der Abdeckung im Rahmen dieses Kontos mit einem Mindestwert von `0`. |

## `diagnosis` {#diagnosis}

`diagnosis` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Diagnosestruktur](../../../images/healthcare/field-groups/account/diagnosis.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Bedingung] | `condition` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Die für das Konto relevante Diagnose. |
| [!UICONTROL Paketcode] | `packageCode` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Paketcode kann verwendet werden, um Diagnosen zu gruppieren, die als Preis berechnet oder als ein Produkt geliefert werden können (z. B. DRGs). |
| [!UICONTROL Typ] | `type` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Geben Sie an, ob diese Diagnose für das Konto relevant ist (z. B. Eintritt, Abrechnung, Entlassung usw.). |
| [!UICONTROL Datum der Diagnose] | `dateOfDiagnosis` | DateTime | Datum der Diagnose (bei kodierter Diagnose). |
| [!UICONTROL Bei Eintritt] | `onAdmission` | Boolesch | Ob die Diagnose bei der Aufnahme vorhanden war. |
| [!UICONTROL Sequenz] | `sequence` | Ganzzahl | Rangfolge der Diagnose (für jeden Typ) mit einem Mindestwert von `0`. |

## `guarantor` {#guarantor}

`guarantor` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Garantiestruktur](../../../images/healthcare/field-groups/account/guarantor.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Party] | `party` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die verantwortliche Entität. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem der Garant die Verantwortung für das Konto übernimmt. |
| [!UICONTROL Zurückgestellt] | `onHold` | Boolesch | Ein Garant kann eine Kreditsperre erhalten oder auf andere Weise seine Funktion vorübergehend aussetzen lassen. |

## `procedure` {#procedure}

`procedure` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Verfahrensstruktur](../../../images/healthcare/field-groups/account/procedure.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Das für das Konto relevante Verfahren. |
| [!UICONTROL Gerät] | `device` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Alle Geräte, die mit dem für das Konto relevanten Verfahren verbunden waren. |
| [!UICONTROL Typ] | `type` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Wie der Prozedurwert bei der Belastung des Kontos verwendet werden soll. |
| [!UICONTROL Paketcode] | `packageCode` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Package-Code kann verwendet werden, um Verfahren zu gruppieren, die als Einzelprodukt berechnet oder geliefert werden können (z. B. DRGs). |
| [!UICONTROL Datum der Zustellung] | `dateOfService` | DateTime | Das Datum bei Verwendung einer codierten Prozedur. Wird auf ein Verfahren verwiesen, so ist das Datum des Verfahrens zu verwenden. |
| [!UICONTROL Sequenz] | `sequence` | Ganzzahl | Rangfolge der Prozedur (für jeden Typ) mit einem Mindestwert von `0`. |

## `relatedAccount` {#related-account}

`relatedAccount` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![relatedAccount-Struktur](../../../images/healthcare/field-groups/account/related-account.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Konto] | `account` | [[!UICONTROL Referenz]](../data-types/reference.md) | Verweis auf ein verknüpftes Konto. |
| [!UICONTROL Beziehung] | `relationship` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beziehung des zugehörigen Kontos. |
