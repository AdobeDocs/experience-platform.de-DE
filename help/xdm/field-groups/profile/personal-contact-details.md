---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; persönliche Details; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe
solution: Experience Platform
title: Feldergruppe "Persönliche Kontaktdetails"
description: Dieses Dokument bietet einen Überblick über die Schemafeldergruppe Persönliche Kontaktdetails .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 20%

---


# [!UICONTROL Persönliche Kontaktangaben] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Persönliche Kontaktangaben] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) beschreibt die Kontaktinformationen einer Person.

![](../../images/field-groups/personal-contact-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Faxnummer der Person. |
| `homeAddress` | [Postadresse](../../data-types/postal-address.md) | Beschreibt die Wohnadresse der Person. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Mobiltelefonnummer der Person. |
| `personalEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die E-Mail-Adresse der Person. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
