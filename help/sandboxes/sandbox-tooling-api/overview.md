---
title: Handbuch zur Sandbox Tooling-API
description: Sandbox-Tools in Adobe Experience Platform ermöglichen den Export und Import einer Momentaufnahme von Sandbox-Konfigurationen zwischen Sandboxes.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 14%

---

# [!DNL Sandbox] Handbuch zur Tools-API

Die [!DNL Sandbox] Die Tool-API bietet mehrere Endpunkte, mit denen Sie Momentaufnahmen zwischen Sandboxes exportieren und importieren können, die Ihnen in Ihrer Organisation zur Verfügung stehen. Alle Interaktionen erfolgen über HTTP-Endpunkte. Die Quell-Sandbox wird vor dem Exportieren einer Momentaufnahme auf Artefakte überprüft, bei denen es sich um die in einem Paket enthaltenen Objekte handelt. Bei einer Importanfrage wird ein [!DNL Azure Blob] Momentaufnahmen werden abgerufen und als Vorlage verwendet, um fast ähnliche Artefakte für die Ziel-Sandbox zu erzeugen. Siehe [Sandbox-Tools](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) Dokumentation für eine Liste der unterstützten Objekte und Einschränkungen.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

## Pakete {#packages}

Über den Endpunkt Sandbox-Tooling-Pakete können Sie Pakete verwalten. Das Sandbox-Tooling-Paket ist eine Sammlung von Artefaktdefinitionen, einschließlich Paket-ID, Name, Beschreibung, Organisations-ID und Ersteller-ID. Siehe [Endpunktleitfaden für Pakete](./packages.md) für weitere Informationen zum Arbeiten mit Paketen in der API.

## Tools {#tools}

Über den Endpunkt Sandbox-Tools können Sie die JSON-Auftragsdaten unabhängig voneinander abrufen. Siehe [Tools-Endpunkthandbuch](./tools.md) Weitere Informationen zum Abrufen von Auftrags-JSON-Daten in der API.

## Nächste Schritte {#next-steps}

Um mit der Sandbox-Tool-API Aufrufe zu tätigen, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
