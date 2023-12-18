---
title: Schema-Gruppe des Gesundheitsdienstleisters
description: Erfahren Sie mehr über die Schemafeldergruppe "Health Care Provider".
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 4%

---

# [!UICONTROL Gesundheitsdienstleister] Schemafeldgruppe

[!UICONTROL Gesundheitsdienstleister] ist eine Standardschemafeldgruppe für die [[!UICONTROL Anbieter] class](../../classes/provider.md). Es wird ein einzelnes Feld vom Typ Objekt bereitgestellt `healthcareProvider` die Eigenschaften erfasst, die sich auf einen einzelnen Angehörigen der Gesundheitsberufe oder eine Gesundheitseinrichtungen beziehen, die zur Erbringung von Diagnose- und Behandlungsdiensten für die Gesundheitsversorgung zugelassen sind.

![](../../images/field-groups/healthcare-provider.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `addressDetails` | Array von Objekten | Listet die Adressdetails für den Provider auf. Jedes Objekt enthält die folgenden Eigenschaften: <ul><li>`address`: ([[!UICONTROL Postanschrift]](../../data-types/postal-address.md)): Die Postanschrift für den Provider.</li><li>`addressType`: (String) Der Typ der Adresse, die angibt, wo der Provider Dienste anbietet.</li></ul> |
| `emailAddress` | [[!UICONTROL E-Mail-Adresse]](../../data-types/email-address.md) | Die E-Mail-Adresse des Providers. |
| `fax` | [[!UICONTROL Telefonnummer]](../../data-types/phone-number.md) | Faxnummer des Providers. |
| `phoneNumber` | [[!UICONTROL Telefonnummer]](../../data-types/phone-number.md) | Die Telefonnummer des Providers. |
| `qualifications` | Array von Objekten | Führt die für die Betreuung erforderlichen Zertifizierungen, Lizenzen oder Schulungen auf. Jedes Objekt enthält die folgenden Eigenschaften: <ul><li>`issuer`: ([[!UICONTROL Kontodetails]](../../data-types/account-details.md)): Die Organisation, die die Qualifikation reguliert und ausstellt.</li><li>`activePeriod`: (Integer) Das Jahr, bis zu dem die Qualifikation gültig ist.</li><li>`code`: (String) Eine kodierte Darstellung der Qualifizierung.</li></ul> |
| `classification` | Zeichenfolge | Die Service Provider-Klassifizierung basierend auf der Klasse oder Kategorie (wie Patientenversorgung, ambulante Pflege usw.). |
| `isActive` | Boolesch | Gibt an, ob der Provider aktiv ist. |
| `languages` | Zeichenfolgen-Array | Eine Liste der Sprachen, in denen der Provider Vorgänge durchführt. |
| `practiceGroupName` | Zeichenfolge | Der Name der Übungsgruppe für den Dienstanbieter. |
| `practiceGroupType` | Zeichenfolge | Der Praxisgruppentyp für den Dienstleister. |
| `practiceType` | Zeichenfolge | Der Praxistyp für den Dienstleister. |
| `specialties` | Zeichenfolgen-Array | Eine Liste der von diesem Anbieter angebotenen Spezialitäten. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
