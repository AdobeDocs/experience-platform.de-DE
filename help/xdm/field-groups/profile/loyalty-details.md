---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemata;Schemata;Treuedetails;Schema-Design;Feldergruppe;Feldergruppe;
solution: Experience Platform
title: Schemafeldgruppe „Treuedetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „Treuedetails“.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 11%

---

# [!UICONTROL Treuedetails] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Treuedetails] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md). Die Feldergruppe bietet ein einzelnes Feld vom Typ „Objekt“, `loyalty`, das Informationen über die Zugehörigkeit einer Person zu einem Treueprogramm für Kunden erfasst.

![](../../images/field-groups/loyalty-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `pointsExpiration` | Array von Objekten | Listet alle Treuepunkte (oder Gruppen von Treuepunkten) auf, die ablaufen werden, sowie die Daten, an denen sie ablaufen. Jedes Array-Element muss ein -Objekt sein, das die beiden folgenden Eigenschaften enthält: <ul><li>`pointsExpirationDate`: Ein ISO 8601-Datum/Uhrzeit, zu dem die Punkte ablaufen.</li><li>`pointsExpiring`: Der Punktsaldo, der zum zugehörigen Ablaufdatum abläuft.</li></ul> |
| `joinDate` | DateTime | Ein ISO 8601-Datum/Uhrzeit, zu dem die Person dem Treueprogramm beigetreten ist. |
| `loyaltyID` | Zeichenfolgen-Array | Stellt die Treueprogramm-ID(s) dar, die mit dem Mitglied des Treueprogramms verknüpft sind. |
| `points` | Double | Das aktuelle Guthaben an Treuepunkten oder -prämien für das Mitglied des Treueprogramms. |
| `pointsRedeemed` | Double | Die Anzahl der Punkte, die das Mitglied des Treueprogramms auf einen Kauf angewendet oder anderweitig eingelöst hat. |
| `program` | String | Der Name des Treueprogramms, für das die Person registriert ist. |
| `status` | String | Der aktuelle Status der Treueprogramm-Mitgliedschaft der Person, z. B. `active`, `disabled` oder `suspended`. |
| `tier` | String | Erfasst die Treueprogrammstufe, in der die Person registriert ist. |
| `upgradeDate` | String | Das Datum, an dem das Mitglied des Treueprogramms auf seine neueste Stufe aktualisiert wurde. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
