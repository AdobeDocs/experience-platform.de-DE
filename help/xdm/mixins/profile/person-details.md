---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: Profil Person Details mixen
topic: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 26%

---


# [!UICONTROL Profil Person Details] mixen

[!UICONTROL Profil-Personendetails] sind eine Standardmischung für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das Mixin stellt ein Objekt auf der Stammebene bereit, dessen Unterfelder Informationen zu einer bestimmten Person beschreiben. `person`

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `person.name` | [Personenname](../../data-types/person-name.md) | Ein Objekt, dessen Unterfelder verschiedene Elemente des Namens einer Person beschreiben. |
| `person.birthDate` | Datum | Das vollständige Datum, an dem eine Person geboren wurde, in Form eines ISO 8601 Zeitstempels. |
| `person.birthDayAndMonth` | Zeichenfolge | Der Tag und Monat, an dem eine Person geboren wurde, im Format MM-TT. Dieses Feld sollte verwendet werden, wenn der Geburtstag und -monat bekannt sind, nicht aber das Jahr. |
| `person.birthYear` | Ganzzahl | Das Jahr, in dem eine Person geboren wurde, einschließlich des Jahrhunderts (wie 1989). Dieses Feld sollte verwendet werden, wenn nur das Alter der Person bekannt ist, nicht das vollständige Geburtsdatum. |
| `person.gender` | Zeichenfolge | Die Geschlechtsidentität der Person. |
| `person.martialStatus` | Zeichenfolge | Beschreibt die Beziehung einer Person zu einer bedeutenden anderen Person. |
| `person.nationality` | Zeichenfolge | Die Rechtsbeziehung zwischen einer Person und ihrem Status, die durch den ISO-Code 3166-1 Alpha-2 repräsentiert wird. |
| `person.taxId` | Zeichenfolge | Die Steuer-/Steuer-ID der Person, wie die TIN in den USA oder die CIF/NIF in Spanien. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
