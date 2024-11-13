---
title: XDM-Feldsuche mit dem AI-Assistenten
description: Lesen Sie dieses Dokument, um zu erfahren, wie Sie die AI Assistant for Experience Data Model (XDM)-Felderkennung verwenden können.
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# XDM-Feldsuche für mit dem AI-Assistenten

>[!AVAILABILITY]
>
>Diese Funktion ist in Alpha verfügbar und steht Ihrem Unternehmen möglicherweise nicht zur Verfügung. Wenden Sie sich an Ihr Adobe-Account-Team, um am Alpha-Programm teilzunehmen und auf diese Funktion zuzugreifen.

Sie können den AI-Assistenten verwenden, um nach Experience-Datenmodell (XDM)-Feldern zu suchen und diese zu entdecken, mit denen Sie dann innerhalb von Experience Platform Zielgruppen erstellen können.

In der folgenden Tabelle finden Sie unterstützte Abfrage- und Eingabemuster für die XDM-Felderkennung im AI-Assistenten.

>[!TIP]
>
>Während Abfrage- und Eingabeaufforderungsmuster in verschiedenen Anwendungsfällen identisch sein können, variiert die genaue Formulierung einer Frage je nach den XDM-Feldern und Schemas, die für eine bestimmte Sandbox verwendet werden.

| Abfragetyp | Abfrage-/Eingabemuster | Beispiele |
| --- | --- | --- |
| XDM-Feldsuche nach Datendomäne oder -bereich | Zeigen Sie mir die XDM-Felder an, die für die Darstellung von {DATA_DOMAIN/AREA} verwendet werden. | <ul><li>Zeigen Sie mir die XDM-Felder an, die zur Darstellung von Einwilligungsdaten verwendet werden.</li><li>Zeigen Sie mir die XDM-Felder an, die zur Darstellung von Informationen über E-Mail-Abonnements verwendet werden.</li></ul> |
| XDM-Feldsuche nach allgemeinen Feldnamen | <ul><li>Zeigen Sie mir die XDM-Felder, die mit {DATA_DOMAIN/AREA} in Verbindung stehen.</li><li>Welche XDM-Felder enthalten {GENERAL_FIELD_NAME}.</li></ul> | <ul><li>Zeigen Sie mir die XDM-Felder, die sich auf Bestellungen beziehen.</li><li>Zeigen Sie mir die XDM-Felder im Zusammenhang mit Interaktionsdetails an.</li><li>Welches XDM-Feld enthält Besucher-IDs?</li><li>Welches XDM-Feld enthält Produktkategorien?</li></ul> |
| XDM-Feldsuche nach Datenmodellherkunft | <ul><li>Zeigen Sie mir alle Felder von {FIELD_GROUP/CLASS_NAME} an, die {GENERAL_FIELD_NAME} enthalten.</li><li>Was ist der {FIELD_GROUP/CLASS_NAME} des XDM-Felds {GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Zeigen Sie mir alle Felder der Feldergruppe an, die Produktdaten enthalten.</li><li>Zeigen Sie mir alle Felder der Feldergruppe an, die Analysedaten enthält.</li><li>Was ist die Klasse des Vornamens des XDM-Felds?</li><li>Welche Klasse haben die E-Mail-Abonnements für das XDM-Feld?</li></ul> |
| Aufforderung zum Abrufen verbesserter Beschreibungen zusammen mit Feldnamen | {FIELD_DISCOVERY_QUERY}. Schließen Sie außerdem erweiterte Beschreibungen ein. | <ul><li>Zeigen Sie mir die XDM-Felder an, die zur Darstellung von Einwilligungsdaten verwendet werden. Schließen Sie außerdem die erweiterte Beschreibung für das Feld ein.</li><li>Zeigen Sie mir die XDM-Felder im Zusammenhang mit Interaktionsdetails an. Schließen Sie außerdem die erweiterte Beschreibung für das Feld ein.</li></ul> |

{style="table-layout:auto"}