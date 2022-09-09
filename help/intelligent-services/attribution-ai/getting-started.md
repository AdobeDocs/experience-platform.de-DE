---
keywords: Experience Platform; Erste Schritte; Attribution; beliebte Themen
feature: Attribution AI
title: Erste Schritte mit Attribution AI
topic-legacy: Getting started
description: Folgende Handbücher setzen ein Verständnis der verschiedenen Adobe Experience Platform-Dienste voraus, die mit der Verwendung von Attribution AI verbunden sind. Bevor Sie mit den Tutorials beginnen, lesen Sie folgende Dokumente.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: a14f857f87482e1468211152976530c718d56e38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 62%

---

# Erste Schritte mit Attribution AI

Die folgenden Handbücher erfordern ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] mit der Nutzung von Attribution AI verbundene Dienste. Bevor Sie mit den Tutorials beginnen, lesen Sie folgende Dokumente:

- [Übersicht über das Experience-Datenmodell (XDM)-System](../../xdm/home.md): XDM ist das grundlegende Framework, das Folgendes ermöglicht [!DNL Adobe Experience Cloud], unterstützt von Experience Platform, um genau zum richtigen Zeitpunkt die richtige Nachricht an die richtige Person auf dem richtigen Kanal zu senden. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit.
- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Dieses Dokument bietet eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in verwendet werden sollen [!DNL Adobe Experience Platform].
- [Erstellen von Schemas](../../xdm/tutorials/create-schema-ui.md): In diesem Tutorial werden die Schritte zum Erstellen eines Schemas mit dem Schema Editor in Experience Platform beschrieben.

Attribution AI erfordert, dass Datensätze dem Schema Consumer Experience Events (CEE) entsprechen, bei dem es sich um ein [Experience-Datenmodell (XDM)](../../xdm/home.md) Schemafeldgruppe. Wenden Sie sich bitte unter attributionai-support@adobe.com an den Support von Adobe, um die Daten zu implementieren oder zu ändern. Wenn Daten zu Medienausgaben vorhanden sind, können Sie weitere Analysen durchführen, z. B. zu inkrementellen Umsätzen und ROI. Wenn Kundenprofildaten verfügbar sind, können Sie Guthaben auf der Kundenebene genauer zuordnen.

## Terminologie

- **Konversionsereignis:** Alle digitalen Ereignisse oder Interaktionen, die Kunden ausführen, um einen Meilenstein auf dem Weg zu einem Ziel anzuzeigen, wie z. B. Registrierung für eine Konferenz. Weitere Beispiele sind bezahlte Konversionen, kostenlose Kontoanmeldungen oder Qualifizierungen für eine Eigenschaft.

- **Touchpoint:** Alle digitalen Ereignisse oder Interaktionen, die Kunden auf dem Weg zu einem Ziel ausführen. Beispiele dafür sind Marketing-Maßnahmen vor dem Kauf, Impressions bei Display-Werbung oder Klicks auf Paid-Suchen.

## Herunterladen von Attribution AI-Werten

>[!NOTE]
>
>Wenn Sie keine Rohdaten herunterladen müssen, können Sie diesen Schritt überspringen und mit dem [Nächste Schritte](#next-steps).

Das Herunterladen von Attribution AI-Werten erfolgt über eine Kombination von API-Aufrufen. Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Zugangssteuerung {#access-control}

Bei der Verwendung rollenbasierter Zugriffssteuerung muss die **Attribution AI anzeigen** und **Attribution AI verwalten** -Berechtigungen gewähren Zugriff auf verschiedene Funktionen von Attribution AI. Die **Attribution AI verwalten** ermöglicht **erstellen**, **clone**, **edit**, **delete**, **enable** oder **disable** eine Instanz während **Attribution AI anzeigen** ermöglicht **lesen** oder **Ansicht** es. Die **erstellen**, **edit** und **delete** -Aktionen werden in Auditprotokollen aufgezeichnet.

Weitere Informationen finden Sie in der Dokumentation . [Zuweisen von Berechtigungen für die Zugriffskontrolle](../../../help/access-control/home.md) oder wie [Verwenden Sie Auditprotokolle zur Überwachung von Zugriff und Aktivität.](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Nächste Schritte {#next-steps}

Sobald alle Ihre Anmeldedaten und Schemas vorhanden sind, befolgen Sie das [Handbuch zur Benutzeroberfläche von Attribution AI](./user-guide.md). Dieses Handbuch führt Sie durch das Erstellen einer Instanz sowie das Übermitteln der Instanz zum Trainieren und Bewerten.
