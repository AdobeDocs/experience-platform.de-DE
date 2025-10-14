---
keywords: Experience Platform;Erste Schritte;Attributions-KI;beliebte Themen
feature: Attribution AI
title: Erste Schritte mit Attributions-KI
description: Folgende Handbücher setzen ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die mit der Verwendung von Attribution AI verbunden sind. Bevor Sie mit den Tutorials beginnen, lesen Sie die folgenden Dokumente.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 55%

---

# Erste Schritte mit Attribution AI

Die folgenden Handbücher erfordern ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Services, die mit der Verwendung von Attribution AI verbunden sind. Bevor Sie mit den Tutorials beginnen, lesen Sie folgende Dokumente:

- [Experience-Datenmodell (XDM) - Systemübersicht](../../xdm/home.md): XDM ist das grundlegende Framework, mit dem [!DNL Adobe Experience Cloud] auf der Grundlage von Experience Platform die richtige Botschaft zur richtigen Zeit an die richtige Person auf dem richtigen Kanal senden kann. Das XDM-System nutzt Experience-Datenmodell-Schemas, die Experience Platform Experience Platform-Services zur Verwendung bereitstellen.
- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Dieses Dokument bietet eine Einführung in Experience-Datenmodell(XDM)-Schemata und die Bausteine, Prinzipien und Best Practices zum Erstellen von Schemata, die in [!DNL Adobe Experience Platform] verwendet werden können.
- [Erstellen von Schemata](../../xdm/tutorials/create-schema-ui.md): In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.

Attributions-KI erfordert, dass Datensätze dem Schema Consumer Experience Events (CEE) entsprechen, das eine [Experience-Datenmodell (XDM)-](../../xdm/home.md) ist. Wenden Sie sich bitte unter attributionai-support@adobe.com an den Support von Adobe, um die Daten zu implementieren oder zu ändern. Wenn Daten zu Medienausgaben vorhanden sind, können Sie weitere Analysen durchführen, z. B. zu inkrementellen Umsätzen und ROI. Wenn Kundenprofildaten verfügbar sind, können Sie Guthaben auf der Kundenebene genauer zuordnen.

## Terminologie

- **Konversionsereignis:** Alle digitalen Ereignisse oder Interaktionen, die Kunden ausführen, um einen Meilenstein auf dem Weg zu einem Ziel anzuzeigen, wie z. B. Registrierung für eine Konferenz. Weitere Beispiele sind bezahlte Konversionen, kostenlose Kontoanmeldungen oder Qualifizierungen für ein Merkmal.

- **Touchpoint:** Alle digitalen Ereignisse oder Interaktionen, die Kunden auf dem Weg zu einem Ziel ausführen. Beispiele dafür sind Marketing-Maßnahmen vor dem Kauf, Impressions bei Display-Werbung oder Klicks auf Paid-Suchen.

## Herunterladen von Attribution AI-Bewertungen

>[!NOTE]
>
>Wenn Sie die Rohdaten der Scores nicht herunterladen müssen, können Sie diesen Schritt überspringen und mit den [nächsten Schritten“ &#x200B;](#next-steps).

Der Download von Attribution AI-Scores erfolgt über eine Kombination aus API-Aufrufen. Um Experience Platform-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Experience Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Zugangssteuerung {#access-control}

Bei Verwendung der rollenbasierten Zugriffssteuerung gewähren die Berechtigungen **Attributions-KI anzeigen** und **Attributions-KI**) Zugriff auf verschiedene Funktionen von Attributions-KI. Mit **Attributions-KI verwalten** können Sie **erstellen**, **klonen**, **bearbeiten**, **löschen**, **aktivieren** oder **deaktivieren** eine Instanz, während **Attributions-KI anzeigen** Ihnen **Lesen** oder **Anzeigen** ermöglicht. Die **Erstellen**, **Bearbeiten** und **Löschen** werden in Auditprotokollen aufgezeichnet.

Weitere Informationen finden Sie in der Dokumentation [Zuweisen von Berechtigungen für die Zugriffskontrolle](../../../help/access-control/home.md) oder [Verwenden von Adminprotokollen zur Überwachung von Zugriff und Aktivität](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte {#next-steps}

Sobald alle Ihre Anmeldedaten und Schemata vorhanden sind, befolgen Sie das [Handbuch zur Benutzeroberfläche von Attribution AI](./user-guide.md). Dieses Handbuch führt Sie durch das Erstellen einer Instanz sowie das Übermitteln der Instanz zum Trainieren und Bewerten.
