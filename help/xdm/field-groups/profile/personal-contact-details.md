---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; persönliche Details; Schema-Design; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldergruppe "Persönliche Kontaktdetails"
description: Erfahren Sie mehr über die Feldergruppe Persönliche Kontaktdetails .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 18%

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
| `homeAddress` | [Postanschrift](../../data-types/postal-address.md) | Beschreibt die Wohnadresse der Person. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Mobiltelefonnummer der Person. |
| `personalEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die E-Mail-Adresse der Person. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
