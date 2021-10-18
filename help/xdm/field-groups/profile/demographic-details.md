---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; Schemadesign; Feldergruppe; Feldergruppe; Personen; Personendetails; Profilpersonendetails; Person
solution: Experience Platform
title: Schemafeldgruppe "Demografische Details"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Schemafeldergruppe "Demografische Details".
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 22%

---


# [!UICONTROL Feldgruppe &quot;Demografisches ] Detailschema&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Demografische ] Details sind eine Standardschemafeldgruppe für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldergruppe stellt ein `person`-Objekt auf der Stammebene bereit, dessen Unterfelder Informationen über eine Person beschreiben.

![](../../images/field-groups/demographic-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `person.name` | [Personenname](../../data-types/person-name.md) | Ein Objekt, dessen Unterfelder verschiedene Elemente des Namens einer Person beschreiben. |
| `person.birthDate` | Datum | Das vollständige Datum, an dem eine Person geboren wurde, in Form eines Zeitstempels nach ISO 8601. |
| `person.birthDayAndMonth` | Zeichenfolge | Der Tag und Monat, an dem eine Person geboren wurde, im Format MM-TT. Dieses Feld sollte verwendet werden, wenn der Geburtstag und -monat bekannt sind, nicht aber das Jahr. |
| `person.birthYear` | Ganzzahl | Das Jahr, in dem eine Person geboren wurde, einschließlich des Jahrhunderts (wie 1989). Dieses Feld sollte verwendet werden, wenn nur das Alter der Person bekannt ist, nicht das vollständige Geburtsdatum. |
| `person.gender` | Zeichenfolge | Die Geschlechtsidentität der Person. |
| `person.martialStatus` | Zeichenfolge | Beschreibt die Beziehung einer Person zu einer wichtigen anderen. |
| `person.nationality` | Zeichenfolge | Die Rechtsbeziehung zwischen einer Person und ihrem Staat, der anhand des ISO 3166-1 Alpha-2-Codes dargestellt wird. |
| `person.taxId` | Zeichenfolge | Die Steuer-/Steuerkennung der Person, wie die TIN in den USA oder die CIF/NIF in Spanien. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)