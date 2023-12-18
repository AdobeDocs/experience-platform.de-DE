---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Endbenutzer; Endbenutzer; Endbenutzer; ID;
solution: Experience Platform
title: Schemafeldgruppe "Endbenutzer-ID-Details"
description: Erfahren Sie mehr über die Feldergruppe "Endbenutzer-ID-Details".
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 16%

---


# [!UICONTROL Details zur Endbenutzer-ID] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Details zur Endbenutzer-ID] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), mit dem die Identitätsdaten einer Person in mehreren Adobe-Applikationen beschrieben werden. Die Feldergruppe stellt eine Stammebene bereit `endUserIDs` -Objekt, das selbst ein schreibgeschütztes enthält `_experience` -Feld, dessen Werte automatisch aktualisiert werden, wenn Daten erfasst werden.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `aacustomid` | [Identität](../../data-types/identity.md) | Benutzerdefinierte Endbenutzer-IDs für Adobe Analytics Cloud. |
| `aaid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Analytics Cloud. |
| `acid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Campaign. |
| `adcloud` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Advertising Cloud. |
| `emailid` | [Identität](../../data-types/identity.md) | E-Mail-Adresse-IDs. |
| `mcid` | [Identität](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). Die MCID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `phonenumberid` | [Identität](../../data-types/identity.md) | Telefonnummer-IDs. |
| `tntid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Target. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
