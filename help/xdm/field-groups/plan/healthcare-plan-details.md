---
title: Schemafeldgruppe „Details zum Gesundheitsplan“
description: Erfahren Sie mehr über die Schemafeldgruppe „Details zum Gesundheitsplan“.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 9%

---

# [!UICONTROL Details zum Gesundheitsplan] Schemafeldgruppe

[!UICONTROL Details zum Gesundheitsplan] ist eine Standardschemafeldgruppe für die Klasse [[!UICONTROL Plan]](../../classes/plan.md). Es bietet ein einzelnes Objekttyp-Feld, `healthcarePlanDetails` Eigenschaften erfasst, die sich auf einen medizinischen Plan beziehen.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `networkDetails` | Array von Objekten | Führt die Einzelheiten des/der vom Versicherer definierten Netzwerks/Netzwerke von Anbietern auf, bei denen der Begünstigte eine Behandlung beantragen kann, und wird mit dem netzwerkinternen Tarif abgedeckt. Jedes Objekt enthält die folgenden Eigenschaften: <ul><li>`networkID`: (String) Die versichererspezifische ID für das Netzwerk.</li><li>`networkName`: (String) Der versichererspezifische Name für das Netzwerk.</li></ul> |
| `affiliations` | Zeichenfolgen-Array | Eine Liste der Geschäftseinheiten, die mit dem Plan verbunden sind. |
| `coverageType` | String | Der Typ der Abdeckung des Plans. Akzeptierte Werte sind:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Boolesch | Gibt an, ob der Plan aktiv ist. |
| `lastVerificationDate` | DateTime | Das Datum, an dem der Plan zuletzt überprüft wurde. |
| `payerID` | String | Die eindeutige Kennung des Zahlers (d. h. des Versicherers für den Plan). |
| `planLevel` | String | Gibt die Ebene des Plans an. Akzeptierte Werte sind:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | String | Gibt den Plantyp an. Akzeptierte Werte sind:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | String | Der Typ des Eigentümers, für den ein Plan gilt. Beispiele sind Einzelpersonen, Gruppen, Organisationen usw. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
