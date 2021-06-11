---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Datenvorbereitung – Übersicht
topic-legacy: overview
description: Dieses Dokument führt in die Datenvorbereitung in Adobe Experience Platform ein.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: daefd977cd09bd9cd7f8d6101b45be98f30d24ae
workflow-type: ht
source-wordcount: '437'
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

## Zuordnung

„Zuordnung“ bezeichnet hier die Zuordnung eines Eingabeattributs oder berechneten Felds zu einem XDM-Attribut. Ein einzelnes Attribut kann mehreren XDM-Attributen zugeordnet werden, indem einzelne Zuordnungen erstellt werden.

Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im [Handbuch zu den Zuordnungsfunktionen](./functions.md).

## Zuordnungssatz

Eine Reihe von Zuordnungen, die ein Schema in ein anderes umwandeln, wird gemeinhin als Zuordnungssatz bezeichnet. Im Rahmen jedes Datenflusses wird ein einzelner Zuordnungssatz erstellt. Ein Zuordnungssatz ist ein integraler Bestandteil der Datenflüsse und wird im Rahmen der Datenflüsse erstellt, bearbeitet und überwacht.

Weitere Informationen zu Zuordnungssätzen, einschließlich der Verwendung von Feldern in einem Zuordnungssatz, finden Sie im [Handbuch für Zuordnungssätze](./mapping-set.md). Informationen zum Erstellen eines Zuordnungssatzes und zum Verwenden anderer API-Aufrufe im Zusammenhang mit Zuordnungssätzen finden Sie im Abschnitt zu den Zuordnungssätzen im [Entwicklerhandbuch](./api/mapping-set.md).

## Verarbeiten von Datenformaten

Datenvorbereitung kann verschiedene Datenformate, die in Platform erfasst werden, zuverlässig verarbeiten. Weitere Informationen zum Verarbeiten verschiedener Datentypen durch die Datenvorbereitung finden Sie in der [Übersicht zur Verarbeitung von Datenformaten](./data-handling.md).

## Nächste Schritte

In diesem Dokument wurden die Grundlagen zur Datenvorbereitung in Adobe Experience Platform behandelt. Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im [Handbuch zu den Zuordnungsfunktionen](./functions.md). Weitere Informationen zum Verarbeiten verschiedener Datentypen durch die Datenvorbereitung finden Sie im [Handbuch zur Verarbeitung von Datenformaten](./data-handling.md#dates). Informationen zur Verwendung der Datenvorbereitungs-API finden Sie im [Entwicklerhandbuch zur Datenvorbereitung](api/overview.md).
