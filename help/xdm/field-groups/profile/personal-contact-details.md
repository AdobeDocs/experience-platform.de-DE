---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; persönliche Details; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe
solution: Experience Platform
title: Feldergruppe "Persönliche Kontaktdetails"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Schemafeldergruppe Persönliche Kontaktdetails .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---


# [!UICONTROL Feldergruppe &quot;Persönliche ] Kontaktdaten&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Persönliche Kontaktinformationen ] sind eine Standardschemafeldgruppe für die  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) Klasse, die die Kontaktinformationen für eine Person beschreibt.

![](../../images/field-groups/personal-contact-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Faxnummer der Person. |
| `homeAddress` | [Postadresse](../../data-types/postal-address.md) | Beschreibt die Wohnadresse der Person. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Mobiltelefonnummer der Person. |
| `personalEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die E-Mail-Adresse der Person. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
