---
title: Schemafeldgruppe „Details zum versicherten Mitglied“
description: Erfahren Sie mehr über die Schemafeldgruppe „Details zum versicherten Mitglied“.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 3%

---

# [!UICONTROL Details zum versicherten Mitglied] Schemafeldgruppe

[!UICONTROL Details zum versicherten Mitglied] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md) in der Details zu einer Person erfasst werden, die einen medizinischen Dienst oder eine medizinische Versorgung erhalten hat oder erhalten wird, z. B. Kontaktinformationen, medizinische Grundversorgung und Informationen zur Vorsorge.

![Feldergruppenstruktur](../../images/field-groups/healthcare-member-details/structure.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Anschrift]](../../data-types/postal-address.md) | Die Rechnungsadresse der Person. |
| `faxPhone` | [[!UICONTROL Telefonnummer]](../../data-types/phone-number.md) | Die Faxnummer der Person. |
| `homeAddress` | [[!UICONTROL Anschrift]](../../data-types/postal-address.md) | Die Privatadresse der Person. |
| `homePhone` | [[!UICONTROL Telefonnummer]](../../data-types/phone-number.md) | Die private Telefonnummer der Person. |
| `mailingAddress` | [[!UICONTROL Anschrift]](../../data-types/postal-address.md) | Die Anschrift der Person. |
| `memberDetails` | Objekt | Ein Objekt, das detaillierte Informationen zu den gesundheitsbezogenen Attributen und Beziehungen der Person enthält. Weitere Informationen [ Struktur des ](#memberDetails) finden Sie im Abschnitt „Unterabschnitt unten“. |
| `mobilePhone` | [[!UICONTROL Telefonnummer]](../../data-types/phone-number.md) | Die Mobiltelefonnummer der Person. |
| `person` | [[!UICONTROL Person]](../../data-types/person.md) | Ein einzelner Akteur, Kontakt oder Eigentümer, der mit der Gesundheitszugehörigkeit der Person in Verbindung steht. |
| `personalEmail` | [[!UICONTROL E-Mail-Adresse]](../../data-types/email-address.md) | Die persönliche E-Mail-Adresse der Person. |
| `shippingAddress` | [[!UICONTROL Anschrift]](../../data-types/postal-address.md) | Die Lieferadresse der Person. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` ist ein Objekt, das detaillierte Informationen zu den gesundheitsbezogenen Attributen und Beziehungen der Person enthält. Die Struktur von `memberDetails` wird nachfolgend beschrieben.

![memberDetails-Struktur](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `emergencyContact` | Objekt | Erfasst die folgenden Notfallkontaktdetails für die Person: <ul><li>`fullName`: (String) Der vollständige Name des Notfallkontakts.</li><li>`phone`: (String) Die Telefonnummer für den Notfallkontakt.</li><li>`relationshipToMember`: (String) Die Beziehung des Notfallkontakts zur Person.</li></ul> |
| `medications` | Array von Objekten | Listet die Details der aktuellen und früheren Medikationen auf, die mit der Person verbunden sind. Jedes Array-Element ist ein -Objekt, das die folgenden Details erfasst: <ul><li>`refillLocation`: ([[!UICONTROL Postanschrift]](../../data-types/postal-address.md)) Der Nachfüllort für das Medikament.</li><li>`ID`: (String) Medikament-ID.</li><li>`isCurrent`: (Boolesch) Gibt an, ob das Medikament aktuell oder veraltet ist.</li><li>`numberOfRefills`: (Integer) Die Anzahl der Nachfüllungen, die vom Anbieter dieses Medikaments verschrieben werden.</li><li>`startDate`: (DateTime) Das Datum, an dem die Person mit der Einnahme der Medikation begonnen hat.</li></ul> |
| `multipleBirth` | Objekt | Erfasst Details zu Mehrfachgeburten: <ul><li>`isMultipleBirth`: (Boolesch) Gibt an, ob die Person mehrere Geburten hatte.</li><li>`multipleBirthNumber`: (Integer) Die Anzahl der geborenen Babys, wenn `isMultipleBirth` wahr ist.</li></ul> |
| `plans` | Array von Objekten | Listet die Details der aktuellen und früheren medizinischen Pläne auf, die mit der Person verbunden sind. Jedes Array-Element ist ein -Objekt, das die folgenden Details erfasst: <ul><li>`coverageEndDate`: (DateTime) Das Datum, an dem die Abdeckung des Plans endet.</li><li>`coverageStartDate`: (DateTime) Das Datum, an dem die Abdeckung des Plans beginnt.</li><li>`isActive`: (Boolesch) Gibt an, ob der Plan aktiv ist.</li><li>`planId`: (String) Die Plan-ID.</li></ul> |
| `primaryCarePhysicians` | Array von Objekten | Listet die Details der mit der Person verbundenen Hausärzte auf. Jedes Array-Element ist ein -Objekt, das die folgenden Details erfasst: <ul><li>`endDate`: (DateTime) Das Datum, an dem der Hausarzt die Versorgung der Person beendet hat.</li><li>`fullname`: (String) Der vollständige Name des Arztes.</li><li>`providerId`: (String) Eine eindeutige Kennung für den Arzt.</li><li>`startDate`: (DateTime) Das Datum, an dem der Hausarzt mit der Pflege der Person begonnen hat.</li></ul> |
| `specialists` | Array von Objekten | Listet die Details der medizinischen Fachkräfte auf, die mit der Person verbunden sind. Jedes Array-Element ist ein -Objekt, das die folgenden Details erfasst: <ul><li>`fullname`: (String) Der vollständige Name des Spezialisten.</li><li>`providerId`: (String) Eine eindeutige Kennung für den Spezialisten.</li><li>`specialty`: (String) Die Spezialität des Anbieters (wie Anästhesiologie, Urologie, Radiologie, Dermatologie usw.).</li></ul> |
| `beneficiaryRelationship` | String | Die Beziehung des Begünstigten zum versicherten Mitglied, wenn die Person eine abhängige Person ist (Beispiele sind: Selbst, Ehegatte, Kind usw.). |
| `billingAccountID` | String | Eine eindeutige Kennung für das Abrechnungskonto der Person. |
| `dateAgeCollected` | DateTime | Das Datum, an dem das Alter der Person erfasst wurde. |
| `deceasedDate` | DateTime | Das Datum, an dem die Person gestorben ist, wenn sie verstorben ist. |
| `isDeceased` | Boolesch | Gibt an, ob die Person verstorben ist. |
| `isDependent` | Boolesch | Gibt an, ob die Person eine abhängige Person ist. |
| `nationality` | String | Die rechtliche Beziehung zwischen der Person und ihrem Staat, dargestellt mit dem ISO 3166-1 Alpha-2-Code. |
| `preferredAvailability` | String | Die von der Person bevorzugte Zeit- und Tagesverfügbarkeit für einen Termin. |
| `primaryMemberID` | String | Eine eindeutige Kennung des primären Abonnenten, wenn die Person eine abhängige Person ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Weitere Informationen dazu, wie diese Feldergruppe zur Unterstützung gängiger Anwendungsfälle (Anwendungsfälle der Gesundheitsbranche) verwendet werden kann, finden Sie in der Dokumentation [ Branchenschemas ](../../schema/industries/healthcare.md).
