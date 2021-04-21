---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Schema-Design;Mixin;Mixins;Arbeitsdetails;Profil arbeiten;
solution: Experience Platform
title: Details des Arbeitskontakts-Mixer
topic-legacy: overview
description: In diesem Dokument erhalten Sie einen Überblick über das Mixin "Work Contact Details".
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 5%

---

# [!UICONTROL Work Contact ] DetailsMixin

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument [mixin name updates](../name-updates.md).

[!UICONTROL Work Contact ] Details ist ein Standard-Mixin für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das Mixin bietet mehrere Felder, in denen berufsbezogene Informationen zu einer einzelnen Person erfasst werden, z. B. Arbeitsadresse, E-Mail-Adresse, Telefonnummer der Arbeit und Organisationen, zu denen die Person gehört.

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
