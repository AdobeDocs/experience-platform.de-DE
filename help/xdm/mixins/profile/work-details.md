---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Schema-Design;Mixin;Mixins;Arbeitsdetails;Profil arbeiten;
solution: Experience Platform
title: Details des Arbeitskontakts-Mixer
topic: overview
description: In diesem Dokument erhalten Sie einen Überblick über das Mixin "Work Contact Details".
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
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