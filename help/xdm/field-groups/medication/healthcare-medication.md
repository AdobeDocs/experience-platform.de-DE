---
title: Schema-Gruppe für Gesundheitsmedikation
description: Erfahren Sie mehr über die Feldergruppe Gesundheitsmedikation .
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL Schemafeldgruppe &quot;Gesundheitsmedikation&quot;]

[!UICONTROL Gesundheitsmedikation] ist eine Standardschemafeldgruppe für die [[!UICONTROL Medikation] -Klasse](../../classes/medication.md). Es wird ein einzelnes Objektfeld `medication` bereitgestellt, das Details wie Markenname, Nummer und Menge erfasst.

![](../../images/field-groups/healthcare-medication.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ingredients` | Array von Objekten | Listet die im Arzneimittel vorhandenen Bestandteile auf. Jedes Objekt enthält die folgenden Eigenschaften: <ul><li>`isActive`: (Boolesch) Gibt an, ob dieser Wirkstoff noch aktiv in dieser Medikation verwendet wird.</li><li>`name`: (String) Der Name der Zutat.</li><li>`quantity`: (String) Die Menge des Inhaltsstoffs, der in der Medikation vorhanden ist.</li></ul> |
| `brandName` | Zeichenfolge | Der Markenname des Medikaments. |
| `codes` | Zeichenfolgen-Array | Eine Liste von Codes, die dieses Medikament identifizieren. |
| `dosageUnitNumber` | Double | Die Nummer der Dosiereinheit für das Arzneimittel. |
| `dosageUnitOfMeasurement` | Zeichenfolge | Die Maßeinheit für die Dosiernummer. |
| `expiryDate` | DateTime | Verfalldatum des Arzneimittels. |
| `genericName` | Zeichenfolge | Der generische Name des Arzneimittels. |
| `lotNumber` | Zeichenfolge | Die eindeutige Kennung für die Charge des Medikaments. |
| `manufacturerName` | Zeichenfolge | Der Name des Arzneimittelherstellers. |
| `quantity` | Double | Die Menge des Arzneimittels in der Packung. |
| `status` | Zeichenfolge | Allgemeiner Status, der angibt, ob das Arzneimittel/Medikament aktiv ist oder nicht. |
| `volume` | Double | Das Arzneimittelvolumen. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
