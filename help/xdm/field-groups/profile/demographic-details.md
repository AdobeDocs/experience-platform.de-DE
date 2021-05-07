---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemas;Schema-Design;Feldgruppe;Feldgruppe;Personendaten;Profil;Personendaten;Person;
solution: Experience Platform
title: Schema-Feldgruppe "Demografische Details"
topic-legacy: overview
description: In diesem Dokument erhalten Sie eine Übersicht über die Feldgruppe "Schema mit demografischen Details".
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: f5beb57acf4cc1827bf08b549cd2b3a02fd82b18
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 21%

---


# [!UICONTROL Feldgruppe &quot;Demografische ] Details&quot;

>[!NOTE]
>
>Die Namen mehrerer Schema-Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md).

[!UICONTROL Demografische ] Details sind eine Standardfeldgruppe für Schemas für die  [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldgruppe stellt ein `person`-Objekt der Stammebene bereit, dessen Unterfelder Informationen zu einer bestimmten Person beschreiben.

![](../../images/field-groups/demographic-details.png)

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

Weitere Informationen zur Feldgruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)