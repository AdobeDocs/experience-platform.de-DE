---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;individuelles Profil;Felder;Schemata;Schemata;Schemadesign;mixin;Mixins;Arbeitsdetails;Profilarbeit;
solution: Experience Platform
title: Schemafeldgruppe „Arbeitskontaktdetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „Arbeitskontaktdetails“.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 14%

---


# Schemafeldgruppe [!UICONTROL Geschäftskontaktdetails]

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Arbeitskontaktdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldergruppe bietet mehrere Felder, die berufliche Informationen zu einer einzelnen Person erfassen, z. B. geschäftliche Adresse, geschäftliche E-Mail-Adresse, geschäftliche Telefonnummer und Organisationen, zu denen die Person gehört.

![](../../images/field-groups/work-contact-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `workAddress` | [Anschrift](../../data-types/postal-address.md) | Beschreibt die Arbeitsadresse der Person. |
| `workEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die geschäftliche E-Mail-Adresse der Person. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die geschäftliche Telefonnummer der Person. |
| `organizations` | Zeichenfolge (Array) | Ein Array von Freiform-Zeichenfolgen, die die Organisationen darstellen, denen die Person angehört. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
