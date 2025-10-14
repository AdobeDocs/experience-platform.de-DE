---
title: Handbuch zur Sandbox-Tooling-API
description: Mit den Sandbox-Tools in Adobe Experience Platform können Sie einen Schnappschuss der Sandbox-Konfigurationen zwischen Sandboxes exportieren und importieren.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 14%

---

# Handbuch zur [!DNL Sandbox] Tooling-API

Die [!DNL Sandbox]-Tooling-API bietet mehrere Endpunkte, mit denen Sie Momentaufnahmen zwischen Sandboxes exportieren und importieren können, die Ihnen in Ihrem Unternehmen zur Verfügung stehen. Alle Interaktionen erfolgen über HTTP-Endpunkte. Die Quell-Sandbox wird vor dem Exportieren eines Schnappschusses auf Artefakte überprüft, bei denen es sich um die in einem Paket enthaltenen Objekte handelt. Wenn eine Importanfrage gestellt wird, wird ein [!DNL Azure Blob]-Schnappschuss abgerufen und als Vorlage verwendet, um fast ähnliche Artefakte für die Ziel-Sandbox zu erzeugen. In der [Sandbox-Tools](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)-Dokumentation finden Sie eine Liste der unterstützten Objekte und Einschränkungen.

Diese Endpunkte werden nachfolgend beschrieben. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

## Packages        {#packages}

Mit dem Sandbox Tooling Packages-Endpunkt können Sie Pakete verwalten. Das Sandbox-Tooling-Paket ist eine Sammlung von Artefaktdefinitionen, einschließlich Paket-ID, Name, Beschreibung, Organisations-ID und Ersteller-ID. Weitere Informationen [&#x200B; Arbeiten mit Paketen in der API finden &#x200B;](./packages.md) im Handbuch zum packages-Endpunkt .

## Tools {#tools}

Mit dem Endpunkt Sandbox-Tools können Sie die JSON-Auftragsdaten unabhängig abrufen. Weitere Informationen zum Abrufen von JSON[Auftragsdaten in der API finden Sie &#x200B;](./tools.md) „tools-Endpunkthandbuch“.

## Nächste Schritte {#next-steps}

Um mit Aufrufen mit der Sandbox-Tooling-API zu beginnen, lesen Sie [Erste Schritte](./getting-started.md) und wählen Sie dann eines der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
