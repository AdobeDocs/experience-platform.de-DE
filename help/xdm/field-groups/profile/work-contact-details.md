---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; Schemadesign; Mixin; Mixins; Arbeitsdetails; Profilarbeit;
solution: Experience Platform
title: Schema-Feldergruppe "Kontaktdetails bearbeiten"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe "Arbeitskontaktdetails".
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 15%

---


# [!UICONTROL Kontaktangaben für Arbeitskontakte] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Kontaktangaben für Arbeitskontakte] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Die Feldergruppe bietet mehrere Felder, die berufsbezogene Informationen über eine Person erfassen, z. B. Arbeitsadresse, Arbeits-E-Mail, Berufs-Telefonnummer und Organisationen, zu denen die Person gehört.

![](../../images/field-groups/work-contact-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `workAddress` | [Postadresse](../../data-types/postal-address.md) | Beschreibt die Arbeitsadresse der Person. |
| `workEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die geschäftliche E-Mail-Adresse der Person. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person am Arbeitsplatz. |
| `organizations` | Zeichenfolge (Array) | Ein Array von Freiform-Zeichenfolgen, die die Organisationen darstellen, zu denen die Person gehört. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
