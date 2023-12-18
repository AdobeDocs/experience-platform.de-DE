---
title: Schemafeldgruppe Gesundheitsplan Details
description: Erfahren Sie mehr über die Feldergruppe "Details des Gesundheitsplans".
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 9%

---

# [!UICONTROL Details zum Gesundheitsplan] Schemafeldgruppe

[!UICONTROL Details zum Gesundheitsplan] ist eine Standardschemafeldgruppe für die [[!UICONTROL Plan] class](../../classes/plan.md). Es wird ein einzelnes Feld vom Typ Objekt bereitgestellt `healthcarePlanDetails` erfasst Eigenschaften im Zusammenhang mit einem medizinischen Plan.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `networkDetails` | Array von Objekten | Führt die Einzelheiten des bzw. der vom Versicherer definierten Netze der Dienstleistungserbringer auf, bei denen der Begünstigte eine Behandlung beantragen kann, und wird zum &quot;Netzwerk-Tarif&quot; erfasst. Jedes Objekt enthält die folgenden Eigenschaften: <ul><li>`networkID`: (String) Die versicherungsspezifische ID für das Netzwerk.</li><li>`networkName`: (String) Der versicherungsspezifische Name für das Netzwerk.</li></ul> |
| `affiliations` | Zeichenfolgen-Array | Eine Liste der Geschäftsentitäten, die mit dem Plan verbunden sind. |
| `coverageType` | Zeichenfolge | Der Plan-Deckungstyp. Akzeptierte Werte sind:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Boolesch | Gibt an, ob der Plan aktiv ist. |
| `lastVerificationDate` | DateTime | Datum der letzten Überprüfung des Plans. |
| `payerID` | Zeichenfolge | Die eindeutige Kennung für den Auftraggeber (d. h. den Versicherungsanbieter für den Plan). |
| `planLevel` | Zeichenfolge | Gibt die Planebene an. Akzeptierte Werte sind:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Zeichenfolge | Gibt den Plantyp an. Akzeptierte Werte sind:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Zeichenfolge | Der Typ des Eigentümers, für den ein Plan gilt. Beispiele sind Einzelpersonen, Gruppen, Organisationen usw. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
