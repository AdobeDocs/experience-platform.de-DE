---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Erste Schritte mit Attribution AI
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Erste Schritte mit Attribution AI

Die folgenden Leitfäden erfordern ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die mit der Verwendung von Attribution AI verbunden sind. Bevor Sie mit den Tutorials beginnen, lesen Sie bitte die folgenden Dokumente:

- [Systemübersicht](../../xdm/home.md)zum Erlebnis-Datenmodell (XDM): XDM ist das grundlegende Framework, mit dem Adobe Experience Cloud, powered by Experience Platform, die richtige Botschaft an die richtige Person im richtigen Kanal und genau zum richtigen Zeitpunkt senden kann. Die Methode, auf der Experience Platform aufgebaut ist, XDM-System, operalisiert Experience Data Model-Schema für die Verwendung durch Plattformdienste.
- [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md)des Schemas: Dieses Dokument bietet eine Einführung in Experience Data Model-(XDM-)Schema und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in Adobe Experience Platform verwendet werden sollen.
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Lernprogramm werden die Schritte zum Erstellen eines Schemas mit dem Schema-Editor in Experience Platform beschrieben.

Für die Zuordnung von AI müssen die Datensätze dem Consumer Experience Ereignisses (CEE)-Schema entsprechen, bei dem es sich um eine Mischung im [Experience Data Model](../../xdm/home.md) (XDM) handelt. Wenden Sie sich an den Adobe-Support unter attributionai-support@adobe.com, um diese Daten zu implementieren oder zu ändern. Wenn Daten zu Medienausgaben vorhanden sind, können Sie weitere Analysen durchführen, z. B. inkrementellen Umsatz und ROI. Wenn Kundendaten verfügbar sind, können Sie Gutschriften auch auf Kundenebene zuordnen, wenn Profil-Daten verfügbar sind.

## Terminologie

- **Konversions-Ereignis:** Alle digitalen Ereignisse oder digitalen Interaktionen, die Kunden ausführen, um einen Meilenstein auf dem Weg zu einem Ziel anzuzeigen, wie z. B. Konferenzregistrierungen. Weitere Beispiele sind bezahlte Konversionen, kostenlose Kontoanmeldungen oder Qualifizierungen für eine Eigenschaft.

- **Touchpoint:** Alle digitalen Ereignisse oder digitalen Interaktionen, die Kunden auf dem Weg zu einem Ziel ausführen. Beispiele sind Marketing-Maßnahmen vor dem Kauf, Anzeigen von Anzeigenimpressionen und Klicks auf gebührenpflichtige Suchen.

## Zugreifen auf Ergebnisse und Abfragen

>[!NOTE] Wenn Sie keine Abfrage oder keinen Zugriff auf Rohdaten benötigen, können Sie diesen Schritt überspringen und zum [Benutzerhandbuch](./user-guide.md)wechseln.

Der Zugriff auf und die Abfrage von Ergebnissen für Attribution AI erfolgt über Snowflake. Derzeit müssen Sie den Adobe-Support unter attributionai-support@adobe.com per E-Mail senden, um die Anmeldeinformationen für Ihr Reader-Konto für Snowflake einzurichten und zu erhalten oder Rohdaten stapelweise zu exportieren.

Nachdem der Adobe-Support Ihre Anforderung verarbeitet hat, erhalten Sie eine URL für das Reader-Konto für Snowflake und die entsprechenden Anmeldeinformationen unten:

- Schneeflocken-URL
- Benutzername
- Kennwort

## Nächste Schritte

Sobald Sie alle Ihre Anmeldedaten und Schema installiert haben, folgen Sie dem Benutzerhandbuch zur [Attribution AI, um Beginn zu erhalten](./user-guide.md). Dieser Leitfaden führt Sie durch das Erstellen einer Instanz und das Einreichen zur Schulung und Bewertung.