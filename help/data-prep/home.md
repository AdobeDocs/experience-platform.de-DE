---
keywords: Experience Platform;Home;beliebte Themen;Map CSV;Map CSV-Datei;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Übersicht über die Datenvorbereitung
topic-legacy: overview
description: Dieses Dokument führt die Datenvorbereitung in Adobe Experience Platform ein.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: daefd977cd09bd9cd7f8d6101b45be98f30d24ae
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

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

Weitere Informationen zu Zuordnungssätzen, einschließlich der Verwendung der Felder in einem Zuordnungssatz, finden Sie im Handbuch [Zuordnungssatz](./mapping-set.md). Um zu erfahren, wie Sie einen Zuordnungssatz erstellen und andere API-Aufrufe im Zusammenhang mit Zuordnungssätzen verwenden, lesen Sie bitte den Abschnitt &quot;Zuordnungssatz&quot;im [Entwicklerhandbuch](./api/mapping-set.md).

## Verarbeitung von Datenformaten

Data Prep kann verschiedene Datenformate, die in die Plattform aufgenommen werden, mit großem Aufwand handhaben. Weitere Informationen zum Umgang mit verschiedenen Datentypen finden Sie unter [Übersicht über die Verarbeitung von Datenformaten](./data-handling.md).

## Nächste Schritte

In diesem Dokument wurden die Grundlagen zur Datenvorbereitung in Adobe Experience Platform behandelt. Weitere Informationen zu den verschiedenen Zuordnungsfunktionen finden Sie im Handbuch [Zuordnungsfunktionen](./functions.md). Weitere Informationen zum Umgang mit verschiedenen Datentypen finden Sie im Handbuch [Verarbeitung von Datenformaten](./data-handling.md#dates). Informationen zur Verwendung der Data Prep API finden Sie im [Data Prep Developer Guide](api/overview.md).
