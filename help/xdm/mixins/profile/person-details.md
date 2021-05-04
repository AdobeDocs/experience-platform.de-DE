---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Schema-Design;mixin;mixin;Person;Personenangaben;Profil-Personenangaben;Person;
solution: Experience Platform
title: Demografisches Details-Mixin
topic-legacy: overview
description: In diesem Dokument erhalten Sie einen Überblick über das Mixin "Demografische Details".
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: 87b638df8a3b27fb6df5dee60b57d817d5e34a80
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 22%

---

# [!UICONTROL Demografisches ] Detailsmixin

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument [mixin name updates](../name-updates.md).

[!UICONTROL Demographische ] Details sind ein Standard-Mixin für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das mixin stellt ein `person`-Objekt der Stammebene bereit, dessen Unterfelder Informationen über eine Person beschreiben.

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
