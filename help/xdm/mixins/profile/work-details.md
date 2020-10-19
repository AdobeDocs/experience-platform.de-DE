---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Profil-Arbeitsdetails-Mixin
topic: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---


# [!UICONTROL Profil-Arbeitsdetails] -mixen

[!UICONTROL Profil-Arbeitsdetails] sind eine Standardmischung für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das Mixin bietet mehrere Felder, in denen berufsbezogene Informationen zu einer einzelnen Person erfasst werden, z. B. Arbeitsadresse, E-Mail-Adresse, Telefonnummer der Arbeit und Organisationen, zu denen die Person gehört.

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