---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemas;Schemas;Schema-Design;Feldgruppe;Feldgruppe;Endbenutzer;Endbenutzer;Endbenutzer;IDs;
solution: Experience Platform
title: Endbenutzer-ID-Details-Schema-Feldgruppe
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über die Feldgruppe "Endbenutzer-ID-Details"im Schema.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 5%

---


# [!UICONTROL Endbenutzer-ID-] Detailschema-Feldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schema-Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md).

[!UICONTROL Endbenutzer-ID-] Details sind eine Standardfeldgruppe für Schema der  [[!DNL XDM ExperienceEvent] Klasse](../../classes/individual-profile.md), die zur Beschreibung der Identitätsinformationen einer Adobe in mehreren Anwendungen verwendet wird. Die Feldgruppe stellt ein `endUserIDs`-Objekt der Stammebene bereit, das wiederum ein schreibgeschütztes `_experience`-Feld enthält, dessen Werte automatisch aktualisiert werden, wenn Daten erfasst werden.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `aacustomid` | [Identität](../../data-types/identity.md) | Benutzerdefinierte Endbenutzer-IDs für Adobe Analytics Cloud. |
| `aaid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Analytics Cloud. |
| `acid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Campaign. |
| `adcloud` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Advertising Cloud. |
| `emailid` | [Identität](../../data-types/identity.md) | E-Mail-Adresse-IDs. |
| `mcid` | [Identität](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identität](../../data-types/identity.md) | Telefonnummer-IDs. |
| `tntid` | [Identität](../../data-types/identity.md) | Endbenutzer-IDs für Adobe Target. |

Weitere Informationen zur Feldgruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
