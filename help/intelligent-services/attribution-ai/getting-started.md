---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Erste Schritte mit Attribution AI
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Erste Schritte mit Attribution AI

Die folgenden Handbücher erfordern ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Verwendung von Attribution AI verbunden sind. Bevor Sie mit den Tutorials beginnen, lesen Sie bitte die folgenden Dokumente:

- [Systemübersicht](../../xdm/home.md)zum Erlebnis-Datenmodell (XDM): XDM ist das Fundament, das es ermöglicht, [!DNL Adobe Experience Cloud]mit Experience Platform die richtige Botschaft an die richtige Person zu senden, am richtigen Kanal, genau zum richtigen Zeitpunkt. Die Methode, auf der Experience Platform aufgebaut ist, XDM-System, operalisiert Experience Data Model-Schema für die Verwendung durch Platform-Services.
- [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md)des Schemas: Dieses Dokument bietet eine Einführung in Experience Data Model-(XDM-)Schema und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in [!DNL Adobe Experience Platform]verwendet werden sollen.
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Lernprogramm werden die Schritte zum Erstellen eines Schemas mit dem Schema-Editor in der Experience Platform beschrieben.

Für die Zuordnung von AI müssen die Datensätze dem Consumer Experience Ereignisses (CEE)-Schema entsprechen, bei dem es sich um eine Mischung im [Experience Data Model](../../xdm/home.md) (XDM) handelt. Wenden Sie sich an den Adobe-Support unter attributionai-support@adobe.com, um diese Daten zu implementieren oder zu ändern. Wenn Daten zu Medienausgaben vorhanden sind, können Sie weitere Analysen durchführen, z. B. inkrementellen Umsatz und ROI. Wenn Kundendaten verfügbar sind, können Sie Gutschriften auch auf Kundenebene zuordnen, wenn Profil-Daten verfügbar sind.

## Terminologie

- **Konversions-Ereignis:** Alle digitalen Ereignisse oder digitalen Interaktionen, die Kunden ausführen, um einen Meilenstein auf dem Weg zu einem Ziel anzuzeigen, wie z. B. Konferenzregistrierungen. Weitere Beispiele sind bezahlte Konversionen, kostenlose Kontoanmeldungen oder Qualifizierungen für eine Eigenschaft.

- **Touchpoint:** Alle digitalen Ereignisse oder digitalen Interaktionen, die Kunden auf dem Weg zu einem Ziel ausführen. Beispiele sind Marketing-Maßnahmen vor dem Kauf, Anzeigen von Anzeigenimpressionen und Klicks auf gebührenpflichtige Suchen.

## Herunterladen von Attribution AI-Ergebnissen

>[!NOTE]
>
>Wenn Sie keine Rohdaten herunterladen müssen, können Sie diesen Schritt überspringen und mit den [nächsten Schritten](#next-steps)fortfahren.

Das Herunterladen von Attributions-AI-Bewertungen erfolgt über eine Kombination von API-Aufrufen. Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung bei Experience Platformen.

## Nächste Schritte {#next-steps}

Sobald Sie alle Ihre Anmeldedaten und Schema installiert haben, folgen Sie dem Benutzerhandbuch zur [Attribution AI, um Beginn zu erhalten](./user-guide.md). Dieser Leitfaden führt Sie durch das Erstellen einer Instanz und das Einreichen zur Schulung und Bewertung.