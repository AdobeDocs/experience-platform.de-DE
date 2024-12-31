---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;Endbenutzer-IDs;Endbenutzer;IDs;
solution: Experience Platform
title: Schemafeldgruppe „Endbenutzer-ID-Details“
description: Erfahren Sie mehr über die Schemafeldgruppe „Endbenutzer-ID-Details“.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 16%

---


# Schemafeldgruppe [!UICONTROL Details ] Endbenutzer-ID“

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Details zur Endbenutzer-ID] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), mit der die Identitätsinformationen einer Person in mehreren Adobe-Anwendungen beschrieben werden. Die Feldergruppe stellt ein `endUserIDs`-Objekt auf der Stammebene bereit, das selbst ein schreibgeschütztes `_experience` enthält, dessen Werte bei der Datenaufnahme automatisch aktualisiert werden.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `aacustomid` | [Identität](../../data-types/identity.md) | Benutzerdefinierte Endbenutzer-IDs für Adobe Analytics Cloud. |
| `aaid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Analytics Cloud. |
| `acid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Campaign. |
| `adcloud` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Advertising Cloud. |
| `emailid` | [Identität](../../data-types/identity.md) | E-Mail-Adressen-IDs. |
| `mcid` | [Identität](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). Die ECID wird jetzt als Experience Cloud-ID (ECID) bezeichnet. |
| `phonenumberid` | [Identität](../../data-types/identity.md) | Telefonnummern-IDs. |
| `tntid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Target. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
