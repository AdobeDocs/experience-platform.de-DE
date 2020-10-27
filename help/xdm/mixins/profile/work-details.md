---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Vergleich "Work Contact Details"
topic: overview
description: In diesem Dokument erhalten Sie einen Überblick über das Mixin "Work Contact Details".
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%

---


# [!UICONTROL Mischung aus Arbeitskontaktinformationen]

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument zu [Mixin-Namensaktualisierungen](../name-updates.md) .

[!UICONTROL Work Contact Details] ist ein Standardmix für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das Mixin bietet mehrere Felder, in denen berufsbezogene Informationen zu einer einzelnen Person erfasst werden, z. B. Arbeitsadresse, E-Mail-Adresse, Telefonnummer der Arbeit und Organisationen, zu denen die Person gehört.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `workAddress` | [Postadresse](../../data-types/postal-address.md) | Beschreibt die Arbeitsadresse der Person. |
| `workEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die Arbeits-E-Mail-Adresse der Person. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person am Arbeitsplatz. |
| `organizations` | Zeichenfolge (Array) | Ein Array von Freiform-Zeichenfolgen, die die Organisationen repräsentieren, denen die Person angehört. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)