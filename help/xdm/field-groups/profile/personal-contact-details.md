---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Persönliche Daten;Schema-Design;Feldgruppe;Feldgruppe;
solution: Experience Platform
title: Schema für persönliche Kontaktdetails
topic-legacy: overview
description: In diesem Dokument erhalten Sie eine Übersicht über die Feldgruppe "Persönliche Kontaktdetails"des Schemas.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---


# [!UICONTROL Feldgruppe &quot;Persönliche ] Kontaktdetails&quot;

>[!NOTE]
>
>Die Namen mehrerer Schema-Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md).

[!UICONTROL Persönliche Kontaktinformationen ] sind eine Standardfeldgruppe für das Schema der  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) Klasse, die die Kontaktinformationen für eine Einzelperson beschreibt.

![](../../images/field-groups/personal-contact-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Faxnummer der Person. |
| `homeAddress` | [Postadresse](../../data-types/postal-address.md) | Beschreibt die Wohnadresse der Person. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Telefonnummer der Person. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Beschreibt die Handynummer der Person. |
| `personalEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Beschreibt die E-Mail-Adresse der Person. |

Weitere Informationen zur Feldgruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
