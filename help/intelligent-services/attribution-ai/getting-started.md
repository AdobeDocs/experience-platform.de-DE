---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform, Intelligent Services
title: Erste Schritte mit Attribution AI
topic: Getting started
description: Folgende Handbücher setzen ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die mit der Verwendung von Attribution AI verbunden sind. Bevor Sie mit den Tutorials beginnen, lesen Sie folgende Dokumente.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 77%

---


# Erste Schritte mit Attribution AI

The following guides require an understanding of the various [!DNL Adobe Experience Platform] services involved with using Attribution AI. Bevor Sie mit den Tutorials beginnen, lesen Sie folgende Dokumente:

- [Systemübersicht](../../xdm/home.md)zum Erlebnis-Datenmodell (XDM): XDM ist das Fundament, das es ermöglicht, [!DNL Adobe Experience Cloud]mit Experience Platform die richtige Botschaft an die richtige Person zu senden, am richtigen Kanal, genau zum richtigen Zeitpunkt. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit.
- [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md)des Schemas: Dieses Dokument bietet eine Einführung in Experience Data Model-(XDM-)Schema und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in [!DNL Adobe Experience Platform]verwendet werden sollen.
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.

Für Attribution AI müssen Datensätze dem Schema Consumer Experience Events (CEE) entsprechen; dabei handelt es sich um ein Mixin im [Experience-Datenmodell](../../xdm/home.md) (XDM). Wenden Sie sich bitte unter attributionai-support@adobe.com an den Support von Adobe, um die Daten zu implementieren oder zu ändern. Wenn Daten zu Medienausgaben vorhanden sind, können Sie weitere Analysen durchführen, z. B. zu inkrementellen Umsätzen und ROI. Wenn Kundenprofildaten verfügbar sind, können Sie Guthaben auf der Kundenebene genauer zuordnen.

## Terminologie

- **Konversionsereignis:** Alle digitalen Ereignisse oder Interaktionen, die Kunden ausführen, um einen Meilenstein auf dem Weg zu einem Ziel anzuzeigen, wie z. B. Registrierung für eine Konferenz. Weitere Beispiele sind bezahlte Konversionen, kostenlose Kontoanmeldungen oder Qualifizierungen für eine Eigenschaft.

- **Touchpoint:** Alle digitalen Ereignisse oder Interaktionen, die Kunden auf dem Weg zu einem Ziel ausführen. Beispiele dafür sind Marketing-Maßnahmen vor dem Kauf, Impressions bei Display-Werbung oder Klicks auf Paid-Suchen.

## Herunterladen von Attribution AI-Scores

>[!NOTE]
>
>If you do not need to download raw scores, you can skip this step and proceed to the [next steps](#next-steps).

Das Herunterladen von Attribution AI-Ergebnissen erfolgt über eine Kombination von API-Aufrufen. Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Nächste Schritte {#next-steps}

Sobald alle Ihre Anmeldedaten und Schemas vorhanden sind, befolgen Sie das [Handbuch zur Benutzeroberfläche von Attribution AI](./user-guide.md). Dieses Handbuch führt Sie durch das Erstellen einer Instanz sowie das Übermitteln der Instanz zum Trainieren und Bewerten.