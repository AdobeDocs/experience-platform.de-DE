---
keywords: Experience Platform;Home;beliebte Themen;Map CSV;Map CSV-Datei;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Übersicht über die Datenvorbereitung
topic: Übersicht
description: Dieses Dokument führt die Datenvorbereitung in Adobe Experience Platform ein.
translation-type: tm+mt
source-git-commit: 73bf6abb143c0866a400aafe984f9a553ffc1abf
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# Datenvorgabe - Übersicht

Data Prep ermöglicht es Datenentwicklern, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren. Die Datenvorgabe wird als &quot;Map&quot;-Schritt in den Datenaufnahmemechanismen einschließlich des CSV-Ingestion-Arbeitsablaufs angezeigt. Dateningenieure können Data Prep verwenden, um die folgende Datenbearbeitung während der Erfassung durchzuführen:

- Definieren einfacher Pass-through-Zuordnungen zur Zuweisung von Eingabedateien zu XDM-Attributen
- Erstellen Sie berechnete Felder zur Durchführung von In-Line-Berechnungen, die XDM-Attributen zugewiesen werden können.
- Daten durch Anwendung von Zeichenfolgen-, numerischen oder Datumsbearbeitungsfunktionen umwandeln
- XDM-Hierarchien mithilfe von hierarchischen Funktionen erstellen
- Vorschau der Daten, wie sie in der Datenvorgabe manipuliert werden

Data Prep wendet außerdem mehrere intrinsische Datenvalidierungen an, um sicherzustellen, dass die Datenintegrität bei der Erfassung erhalten bleibt. Sofern möglich, ordnet Data Prep die eingehenden Daten-Schema automatisch XDM zu. Dateningenieure können die vorgeschlagenen Zuordnungen ändern, korrigieren und löschen und sie gegebenenfalls durch die Zuordnungen ersetzen.

## Zuordnung

Eine Zuordnung ist eine Zuordnung eines Eingabedatums oder eines berechneten Felds zu einem XDM-Attribut. Ein einzelnes Attribut kann mehreren XDM-Attributen zugeordnet werden, indem einzelne Zuordnungen erstellt werden.

Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im Handbuch [Zuordnungsfunktionen](./functions.md).

## Zuordnungssatz

Eine Reihe von Zuordnungen, die ein Schema in ein anderes umwandeln, werden kollektiv als Zuordnungssatz bezeichnet. Im Rahmen jedes Datenflusses wird ein einzelner Zuordnungssatz erstellt. Ein Zuordnungssatz ist ein integraler Bestandteil der Datenflüsse und wird im Rahmen der Datenflüsse erstellt, bearbeitet und überwacht.

## Nächste Schritte

In diesem Dokument wurden die Grundlagen zur Datenvorbereitung in Adobe Experience Platform behandelt. Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im Handbuch [Zuordnungsfunktionen](./functions.md). Weitere Informationen zu den verschiedenen Datums-Uhrzeit-Zeichenfolgen finden Sie im Handbuch [Datums-Zeichenfolgen](./dates.md). Informationen zur Verwendung der Data Prep API finden Sie im [Data Prep Developer Guide](api/overview.md).