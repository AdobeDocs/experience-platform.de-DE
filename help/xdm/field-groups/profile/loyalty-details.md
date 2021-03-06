---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; Loyalitätsdetails; Schema-Design; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Schemafeldgruppe "Loyalitätsdetails"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Feldergruppe "Loyalitätsdetails".
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---

# [!UICONTROL Feldergruppe ] &quot;Loyalitätsdetails&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Loyalitätsdetails ] sind eine Standardschemafeldgruppe für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldergruppe bietet ein einzelnes Objekt-Feld, `loyalty`, das Informationen über die Mitgliedschaft einer Person in einem Kundentreueprogramm erfasst.

![](../../images/field-groups/loyalty-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `pointsExpiration` | Array von Objekten | Listet alle Loyalitätspunkte (oder Gruppen von Treuepunkten) auf, die ablaufen, und die Daten, ab denen sie ablaufen. Jedes Array-Element muss ein Objekt sein, das die beiden folgenden Eigenschaften enthält: <ul><li>`pointsExpirationDate`: Ein ISO 8601-Datum, zu dem die Punkte ablaufen.</li><li>`pointsExpiring`: Der Punktstand, der ab dem zugehörigen Ablaufdatum abläuft.</li></ul> |
| `joinDate` | DateTime | Ein ISO 8601-Datum, zu dem die Person dem Treueprogramm beigetreten ist. |
| `loyaltyID` | Zeichenfolgen-Array | Stellt die Kennung des Treueprogramms dar, die dem Mitglied des Treueprogramms zugeordnet ist. |
| `points` | Double | Die aktuelle Bilanz der Treuepunkte oder Auszeichnungen für das Mitglied des Treueprogramms. |
| `pointsRedeemed` | Double | Die Anzahl der Punkte, die das Mitglied des Treueprogramms auf einen Kauf angewendet oder anderweitig eingelöst hat. |
| `program` | Zeichenfolge | Der Name des Treueprogramms, für das die Person angemeldet ist. |
| `status` | Zeichenfolge | Der aktuelle Status der Treuemitgliedschaft der Person, z. B. `active`, `disabled` oder `suspended`. |
| `tier` | Zeichenfolge | Erfasst die Treueprogramm-Ebene, in der die Person angemeldet ist. |
| `upgradeDate` | Zeichenfolge | Das Datum, an dem das Mitglied des Treueprogramms auf die neueste Ebene aktualisiert wurde. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
