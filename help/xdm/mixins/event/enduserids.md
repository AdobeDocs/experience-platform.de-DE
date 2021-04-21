---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemas;Schemas;Schema-Design;mixin;mixin;enduserids;Endbenutzer;Endbenutzer;IDs;
solution: Experience Platform
title: Endbenutzer-ID-Details-Mixer
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über das Mixin "Endbenutzer-ID-Details".
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# [!UICONTROL Endbenutzer-ID-] DetailMixin

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument [mixin name updates](../name-updates.md).

[!UICONTROL Endbenutzer-ID-] Details sind ein Standardmixin für die  [[!DNL XDM ExperienceEvent] Klasse](../../classes/individual-profile.md), mit dem die Identitätsinformationen einer Person in mehreren Adoben beschrieben werden. Das mixin stellt ein `endUserIDs`-Objekt der Stammebene bereit, das wiederum ein schreibgeschütztes `_experience`-Feld enthält, dessen Werte automatisch aktualisiert werden, wenn Daten erfasst werden.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

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

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
