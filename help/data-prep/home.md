---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Datenvorbereitung – Übersicht
description: Dieses Dokument führt in die Datenvorbereitung in Adobe Experience Platform ein.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 73%

---


# Datenvorbereitung – Übersicht

Die Datenvorbereitung ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren. Die Datenvorbereitung wird als „Map“-Schritt in den Datenaufnahmemechanismen, einschließlich des Workflows der CSV-Aufnahme, angezeigt. Dateningenieure können die Datenvorbereitung verwenden, um die folgende Datenbearbeitung während der Aufnahme durchzuführen:

- Definieren einfacher Pass-through-Zuordnungen zur Zuweisung von Eingabeattributen zu XDM-Attributen
- Erstellen von berechneten Feldern, um in der Zeile Berechnungen durchzuführen, die XDM-Attributen zugewiesen werden können.
- Umwandeln von Daten durch Anwenden von Zeichenfolgen-, numerischen oder Datumsbearbeitungsfunktionen
- Erstellen von XDM-Hierarchien mithilfe von hierarchischen Funktionen
- Vorschau der Daten, wie sie in der Datenvorbereitung bearbeitet werden

Die Datenvorbereitung wendet außerdem mehrere intrinsische Datenvalidierungen an, um sicherzustellen, dass die Integrität der Daten bei der Aufnahme erhalten bleibt. Sofern möglich, ordnet die Datenvorbereitung die eingehenden Daten-Schemas automatisch XDM zu. Dateningenieure können die vorgeschlagenen Zuordnungen ändern, korrigieren und löschen und sie gegebenenfalls durch andere Zuordnungen ersetzen.

>[!NOTE]
>
>Sofern die resultierende Nachricht kein ungültiges XDM ist, führen Umwandlungsfehler in der Datenvorbereitung dazu, dass diese Attribute auf `null` gesetzt werden, während der Rest der Zeile erfasst wird. Wenn die Zeile nicht zu ungültigem XDM aufgelöst wird, wird die Zeile **nicht** erfasst. In beiden Fällen wird der Fehler dokumentiert.

## Zuordnung

„Zuordnung“ bezeichnet hier die Zuordnung eines Eingabeattributs oder berechneten Felds zu einem XDM-Attribut. Ein einzelnes Attribut kann mehreren XDM-Attributen zugeordnet werden, indem einzelne Zuordnungen erstellt werden.

Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im [Handbuch zu den Zuordnungsfunktionen](./functions.md).

### Berechnete Felder

Berechnete Felder ermöglichen die Erstellung von Werten anhand der Attribute im Eingabeschema. Diese Werte können dann Attributen im Zielschema zugewiesen und mit einem Namen und einer Beschreibung versehen werden, um eine einfachere Referenz zu ermöglichen. Berechnete Felder haben eine maximale Länge von 4096 Zeichen.

Weitere Informationen zu berechneten Feldern finden Sie im Abschnitt [Handbuch zu berechneten Feldern](./functions.md#calculated-fields).

### Escape-Sonderzeichen {#escape-special-characters}

Sie können Sonderzeichen in einem Feld mit `${...}`. JSON-Dateien mit Feldern mit einem Punkt (`.`) werden von diesem Mechanismus nicht unterstützt. Wenn bei der Interaktion mit Hierarchien ein untergeordnetes Attribut einen Punkt (`.`), müssen Sie einen umgekehrten Schrägstrich (`\`), um Sonderzeichen zu maskieren. Beispiel: `address` ist ein Objekt, das das Attribut enthält `street.name`, kann dies dann als `address.street\.name` anstelle von `address.street.name`.

## Zuordnungssatz

Eine Reihe von Zuordnungen, die ein Schema in ein anderes umwandeln, wird gemeinhin als Zuordnungssatz bezeichnet. Im Rahmen jedes Datenflusses wird ein einzelner Zuordnungssatz erstellt. Ein Zuordnungssatz ist ein integraler Bestandteil der Datenflüsse und wird im Rahmen der Datenflüsse erstellt, bearbeitet und überwacht.

Weitere Informationen zu Zuordnungssätzen, einschließlich der Verwendung von Feldern in einem Zuordnungssatz, finden Sie im [Handbuch für Zuordnungssätze](./mapping-set.md). Informationen zum Erstellen eines Zuordnungssatzes und zum Verwenden anderer API-Aufrufe im Zusammenhang mit Zuordnungssätzen finden Sie im Abschnitt zu den Zuordnungssätzen im [Entwicklerhandbuch](./api/mapping-set.md).

## Verarbeiten von Datenformaten

Datenvorbereitung kann verschiedene Datenformate, die in Platform erfasst werden, zuverlässig verarbeiten. Weitere Informationen zum Verarbeiten verschiedener Datentypen durch die Datenvorbereitung finden Sie in der [Übersicht zur Verarbeitung von Datenformaten](./data-handling.md).

## Teilzeilenaktualisierungen senden mit [!DNL Data Prep]

Streaming-Aktualisierungen in [!DNL Data Prep] ermöglicht es Ihnen, Teilzeilenaktualisierungen an zu senden [!DNL Profile Service] -Daten sowie beim Erstellen und Erstellen neuer Identitätslinks mit einer einzelnen API-Anfrage. Weitere Informationen zum Streamen von Uploads finden Sie in [!DNL Data Prep], siehe das Dokument unter [Teilzeilenaktualisierungen senden](./upserts.md).

## Attributbasierte Zugriffssteuerung in [!DNL Data Prep]

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Attributbasierte Zugriffskontrolle stellt sicher, dass Sie nur die Attribute zuordnen können, auf die Sie Zugriff haben. Attribute, auf die Sie keinen Zugriff haben, können nicht in Passthrough-Zuordnungen und berechneten Feldern verwendet werden. Wenn Sie also keinen Zugriff auf ein erforderliches Feld haben, können Sie eine Zuordnung nicht erfolgreich speichern. Außerdem können Sie keine Objekte oder Objekt-Arrays zuordnen, wenn Sie keinen Zugriff auf eines der untergeordneten Attribute haben. Sie können jedoch andere Elemente innerhalb des Objekt- oder Objekt-Arrays einzeln zuordnen.

Siehe [Attributbasierte Zugriffskontrolle - Übersicht](../access-control/abac/overview.md) für weitere Informationen.

## Nächste Schritte

In diesem Dokument wurden die Grundlagen zur Datenvorbereitung in Adobe Experience Platform behandelt. Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im [Handbuch zu den Zuordnungsfunktionen](./functions.md). Weitere Informationen zum Verarbeiten verschiedener Datentypen durch die Datenvorbereitung finden Sie im [Handbuch zur Verarbeitung von Datenformaten](./data-handling.md#dates). Informationen zur Verwendung der Datenvorbereitungs-API finden Sie im [Entwicklerhandbuch zur Datenvorbereitung](api/overview.md).
