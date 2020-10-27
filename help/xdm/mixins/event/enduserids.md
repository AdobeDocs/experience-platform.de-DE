---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: Vergleich der Endbenutzer-ID-Details
topic: overview
description: Dieses Dokument bietet eine Übersicht über das Mixin "Endbenutzer-ID-Details".
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 6%

---


# [!UICONTROL Mischung der Endbenutzer-ID-Details]

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument zu [Mixin-Namensaktualisierungen](../name-updates.md) .

[!UICONTROL Endbenutzer-ID-Details] sind eine Standardmischung für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/individual-profile.md), mit der die Identitätsinformationen einer Person in mehreren Adoben beschrieben werden. Das mixin stellt ein Stammebene- `endUserIDs` Objekt bereit, das selbst ein schreibgeschütztes `_experience` Feld enthält, dessen Werte automatisch aktualisiert werden, wenn Daten erfasst werden.

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
