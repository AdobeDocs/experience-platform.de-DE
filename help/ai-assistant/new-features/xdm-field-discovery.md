---
title: XDM-Felderkennung mit KI-Assistent
description: In diesem Dokument erfahren Sie, wie Sie den KI-Assistenten zur Erkennung von Feldern im Experience-Datenmodell (XDM) verwenden können.
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 041034c6-da45-437f-ad46-f9c2ded9f82c
source-git-commit: e2cb6dee0c255c8eaa3729cc7a09ae07a1f33dbc
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# XDM-Felderkennung für mit KI-Assistent

>[!AVAILABILITY]
>
>Diese Funktion befindet sich im Alpha und steht Ihrer Organisation möglicherweise nicht zur Verfügung. Um am Alpha-Programm teilzunehmen und auf diese Funktion zuzugreifen, wenden Sie sich an Ihr Adobe-Account-Team.

Sie können den KI-Assistenten verwenden, um nach Experience-Datenmodell (XDM)-Feldern zu suchen und diese Felder zu entdecken, die Sie dann verwenden können, um Zielgruppen in Experience Platform zu erstellen.

In der folgenden Tabelle finden Sie unterstützte Abfrage- und Eingabeaufforderungsmuster für die XDM-Felderkennung im KI-Assistenten.

>[!TIP]
>
>Während die Abfrage- und Eingabeaufforderungsmuster in verschiedenen Anwendungsfällen identisch sein können, variiert die genaue Formulierung einer Frage je nach den XDM-Feldern und Schemata, die für eine bestimmte Sandbox verwendet werden.

| Abfragetyp | Abfrage-/Eingabeaufforderungsmuster | Beispiele |
| --- | --- | --- |
| XDM-Felderkennung nach Data Domain oder Bereich | XDM-Felder anzeigen, die {DATA_DOMAIN/AREA} repräsentieren. | <ul><li>XDM-Felder anzeigen, die Einverständnisdaten darstellen.</li><li>XDM-Felder anzeigen, die Informationen zu E-Mail-Abonnements darstellen.</li></ul> |
| XDM-Felderkennung nach allgemeinem Feldnamen | <ul><li>XDM-Felder zu {DATA_DOMAIN/AREA} anzeigen.</li><li>Welche XDM-Felder {GENERAL_FIELD_NAME} enthalten.</li></ul> | <ul><li>XDM-Felder für Bestellungen anzeigen.</li><li>XDM-Felder zu Interaktionsdetails anzeigen.</li><li>Welches XDM-Feld enthält Besucher-IDs?</li><li>Welches XDM-Feld enthält Produktkategorien?</li></ul> |
| XDM-Felderkennung nach Datenmodellherkunft | <ul><li>Alle Felder von {FIELD_GROUP/CLASS_NAME} anzeigen, die {GENERAL_FIELD_NAME} enthalten.</li><li>Was ist die {FIELD_GROUP/CLASS_NAME} der XDM-{GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Alle Felder der Feldergruppe anzeigen, die Produktdaten enthalten.</li><li>Anzeigen aller Felder der Feldergruppe, die Analysedaten enthält.</li><li>Was ist die Klasse des Vornamens des XDM-Felds?</li><li>Welche Klasse haben E-Mail-Abonnements im XDM-Feld?</li></ul> |
| Aufforderung zum Abrufen erweiterter Beschreibungen zusammen mit Feldnamen | {FIELD_DISCOVERY_QUERY}. Beinhaltet auch erweiterte Beschreibungen. | <ul><li>XDM-Felder anzeigen, die Einverständnisdaten darstellen. Fügen Sie auch die erweiterte Beschreibung für das Feld hinzu.</li><li>XDM-Felder zu Interaktionsdetails anzeigen. Fügen Sie auch die erweiterte Beschreibung für das Feld hinzu.</li></ul> |

{style="table-layout:auto"}
