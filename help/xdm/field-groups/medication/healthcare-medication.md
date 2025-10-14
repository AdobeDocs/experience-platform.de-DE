---
title: Feldgruppe für das Medikationsschema im Gesundheitswesen
description: Erfahren Sie mehr über die Feldergruppe „Medikationsschema im Gesundheitswesen“.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL Gesundheitsmedizin] Schemafeldgruppe

[!UICONTROL Medizin] ist eine Standardschemafeldgruppe für die Klasse [[!UICONTROL Medizin] &#x200B;](../../classes/medication.md). Es bietet ein einzelnes Objekttyp-`medication`, in dem Details wie Markenname, Lotnummer und Menge erfasst werden.

![](../../images/field-groups/healthcare-medication.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ingredients` | Array von Objekten | Listet die Inhaltsstoffe der Medikation auf. Jedes Objekt enthält die folgenden Eigenschaften: <ul><li>`isActive`: (Boolesch) Gibt an, ob dieser Inhaltsstoff in diesem Medikament noch aktiv verwendet wird.</li><li>`name`: (String) Der Name der Zutat.</li><li>`quantity`: (String) Die Menge des Inhaltsstoffs, der im Medikament vorhanden ist.</li></ul> |
| `brandName` | String | Der Markenname des Arzneimittels. |
| `codes` | Zeichenfolgen-Array | Eine Liste von Codes, die dieses Medikament identifizieren. |
| `dosageUnitNumber` | Double | Die Nummer der Dosierungseinheit für das Medikament. |
| `dosageUnitOfMeasurement` | String | Die Maßeinheit für die Dosierungsnummer. |
| `expiryDate` | DateTime | Verfallsdatum des Arzneimittels. |
| `genericName` | String | Der generische Name des Arzneimittels. |
| `lotNumber` | String | Die eindeutige Kennung für die Arzneimittelcharge. |
| `manufacturerName` | String | Der Name des Arzneimittelherstellers. |
| `quantity` | Double | Die Menge des Medikaments in der Packung. |
| `status` | String | Ein allgemeiner Status, der angibt, ob das Medikament/Medikament aktiv ist oder nicht. |
| `volume` | Double | Das Volumen des Medikaments. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
