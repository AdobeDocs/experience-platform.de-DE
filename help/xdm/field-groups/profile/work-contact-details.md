---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Schema-Design;Mixin;Mixins;Arbeitsdetails;Profil arbeiten;
solution: Experience Platform
title: Schema mit Kontaktdetails arbeiten
topic-legacy: overview
description: In diesem Dokument erhalten Sie eine Übersicht über die Feldgruppe "Arbeitskontaktsdetails"des Schemas.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 5%

---


# [!UICONTROL Feldgruppe ] &quot;Work Contact Details&quot;

>[!NOTE]
>
>Die Namen mehrerer Schema-Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md).

[!UICONTROL Work Contact ] Details ist eine Standardfeldgruppe für Schemas für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldgruppe stellt mehrere Felder bereit, in denen Informationen zu einer bestimmten Person erfasst werden, z. B. Arbeitsadresse, E-Mail-Adresse, Telefonnummer der Arbeit und Organisationen, zu denen die Person gehört.

![](../../images/field-groups/work-contact-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `workAddress` | [Postadresse](../../data-types/postal-address.md) | Beschreibt die Arbeitsadresse der Person. |
| `workEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die Arbeits-E-Mail-Adresse der Person. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person am Arbeitsplatz. |
| `organizations` | Zeichenfolge (Array) | Ein Array von Freiform-Zeichenfolgen, die die Organisationen repräsentieren, denen die Person angehört. |

Weitere Informationen zur Feldgruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
