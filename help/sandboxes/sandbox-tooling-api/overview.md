---
title: Handbuch zur Sandbox Tooling-API
description: Sandbox-Tools in Adobe Experience Platform ermöglichen den Export und Import einer Momentaufnahme von Sandbox-Konfigurationen zwischen Sandboxes.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 14%

---

# Leitfaden zur Tool-API für [!DNL Sandbox]

Die Tool-API [!DNL Sandbox] bietet mehrere Endpunkte, mit denen Sie Momentaufnahmen zwischen Sandboxes exportieren und importieren können, die Ihnen in Ihrer Organisation zur Verfügung stehen. Alle Interaktionen erfolgen über HTTP-Endpunkte. Die Quell-Sandbox wird vor dem Exportieren einer Momentaufnahme auf Artefakte überprüft, bei denen es sich um die in einem Paket enthaltenen Objekte handelt. Wenn eine Importanfrage gestellt wird, wird ein [!DNL Azure Blob] -Schnappschuss abgerufen und als Vorlage verwendet, um fast ähnliche Artefakte für die Ziel-Sandbox zu erzeugen. Eine Liste der unterstützten Objekte und Einschränkungen finden Sie in der Dokumentation zu [Sandbox-Tools](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) .

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

## Packages        {#packages}

Über den Endpunkt Sandbox-Tooling-Pakete können Sie Pakete verwalten. Das Sandbox-Tooling-Paket ist eine Sammlung von Artefaktdefinitionen, einschließlich Paket-ID, Name, Beschreibung, Organisations-ID und Ersteller-ID. Weitere Informationen zum Arbeiten mit Paketen in der API finden Sie im [Paket-Endpunkthandbuch](./packages.md) .

## Tools {#tools}

Über den Endpunkt Sandbox-Tools können Sie die JSON-Auftragsdaten unabhängig voneinander abrufen. Weitere Informationen zum Abrufen von Job-JSON-Daten in der API finden Sie im [Tools-Endpunkthandbuch](./tools.md) .

## Nächste Schritte {#next-steps}

Um Aufrufe mithilfe der Sandbox-Tool-API zu tätigen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eine der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
