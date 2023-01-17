---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Datenvorbereitung – Übersicht
description: Dieses Dokument führt in die Datenvorbereitung in Adobe Experience Platform ein.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 100%

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

Um mehr über berechnete Felder zu erfahren, lesen Sie bitte den [Leitfaden für berechnete Felder](./functions.md#calculated-fields).

### Sonderzeichen mit Escape-Zeichen versehen {#escape-special-characters}

Sie können Sonderzeichen in einem Feld durch die Verwendung von `${...}` mit Escape-Zeichen versehen. Allerdings werden JSON-Dateien, die Felder mit einem Punkt (`.`) enthalten, von diesem Mechanismus nicht unterstützt. Wenn Sie mit Hierarchien arbeiten und ein untergeordnetes Attribut einen Punkt (`.`) enthält, müssen Sie einen Backslash (`\`) verwenden, um Sonderzeichen zu umgehen. Ein Beispiel: `address` ist ein Objekt, das das Attribut `street.name` enthält. Auf dieses kann sich dann durch `address.street\.name` anstelle von `address.street.name` bezogen werden.

## Zuordnungssatz

Eine Reihe von Zuordnungen, die ein Schema in ein anderes umwandeln, wird gemeinhin als Zuordnungssatz bezeichnet. Im Rahmen jedes Datenflusses wird ein einzelner Zuordnungssatz erstellt. Ein Zuordnungssatz ist ein integraler Bestandteil der Datenflüsse und wird im Rahmen der Datenflüsse erstellt, bearbeitet und überwacht.

Weitere Informationen zu Zuordnungssätzen, einschließlich der Verwendung von Feldern in einem Zuordnungssatz, finden Sie im [Handbuch für Zuordnungssätze](./mapping-set.md). Informationen zum Erstellen eines Zuordnungssatzes und zum Verwenden anderer API-Aufrufe im Zusammenhang mit Zuordnungssätzen finden Sie im Abschnitt zu den Zuordnungssätzen im [Entwicklerhandbuch](./api/mapping-set.md).

## Verarbeiten von Datenformaten

Datenvorbereitung kann verschiedene Datenformate, die in Platform erfasst werden, zuverlässig verarbeiten. Weitere Informationen zum Verarbeiten verschiedener Datentypen durch die Datenvorbereitung finden Sie in der [Übersicht zur Verarbeitung von Datenformaten](./data-handling.md).

## Senden Sie partielle Zeilenaktualisierungen mit [!DNL Data Prep]

Das Streamen von Upserts in [!DNL Data Prep] ermöglicht es Ihnen, partielle Zeilenaktualisierungen an [!DNL Profile Service]-Daten zu senden und gleichzeitig neue Identitätsverknüpfungen mit einer einzigen API-Anfrage zu erstellen und herzustellen. Mehr darüber, wie Sie Upserts in [!DNL Data Prep] streamen, erfahren Sie im Dokument zum [Senden von partiellen Zeilenaktualisierungen](./upserts.md).

## Attributbasierte Zugriffssteuerung in [!DNL Data Prep]

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Die attributbasierte Zugriffssteuerung stellt sicher, dass Sie nur die Attribute zuordnen können, auf die Sie Zugriff haben. Attribute, auf die Sie keinen Zugriff haben, können nicht in Passthrough-Zuordnungen und berechneten Feldern verwendet werden. Wenn Sie also keinen Zugriff auf ein erforderliches Feld haben, können Sie eine Zuordnung nicht erfolgreich speichern. Außerdem können Sie keine Objekte oder Objekt-Arrays zuordnen, wenn Sie auf eines der untergeordneten Attribute keinen Zugriff haben. Sie können jedoch andere Elemente innerhalb des Objekts oder Objekt-Arrays einzeln zuordnen.

Weitere Informationen finden Sie in der [Übersicht über die attributbasierte Zugriffssteuerung](../access-control/abac/overview.md).

## Nächste Schritte

In diesem Dokument wurden die Grundlagen zur Datenvorbereitung in Adobe Experience Platform behandelt. Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im [Handbuch zu den Zuordnungsfunktionen](./functions.md). Weitere Informationen zum Verarbeiten verschiedener Datentypen durch die Datenvorbereitung finden Sie im [Handbuch zur Verarbeitung von Datenformaten](./data-handling.md#dates). Informationen zur Verwendung der Datenvorbereitungs-API finden Sie im [Entwicklerhandbuch zur Datenvorbereitung](api/overview.md).
