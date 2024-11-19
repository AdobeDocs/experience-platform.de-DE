---
title: Erste Schritte mit der Auditabfrage-API
description: Mit der Auditabfrage-API können Sie Metrikdaten für verschiedene Adobe Experience Platform-Funktionen abrufen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Audit-Abfrage-API durchführen.
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 40%

---

# Erste Schritte mit der Auditabfrage-API

Mit Adobe Experience Platform können Sie Benutzeraktivitäten auf verschiedene Dienste und Funktionen in Form von Audit-Ereignisprotokollen überprüfen. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute für den Aktionstyp angeben.

Mit der Auditabfrage-API können Sie die Benutzeraktivität auf verschiedene Dienste und Funktionen in Form von Audit-Ereignisprotokollen überprüfen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Audit-Abfrage-API durchführen.

## Voraussetzungen

Um Prüfereignisse verwalten zu können, müssen Sie über die Zugriffssteuerungsberechtigung **[!UICONTROL Protokoll zur Benutzeraktivität anzeigen]** verfügen (zu finden unter der Kategorie [!UICONTROL Data Governance] ). Informationen zum Verwalten individueller Berechtigungen für Platform-Funktionen finden Sie in der Dokumentation zur [Zugriffskontrolle](../../../../access-control/home.md) .

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung in Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Für diese Anleitung müssen Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, damit Sie Platform-APIs erfolgreich aufrufen können. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Für alle Anfragen an [!DNL Platform] -APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Für alle Anfragen mit einer Payload (POST, PUT, PATCH) wird eine zusätzliche Kopfzeile benötigt:

* Content-Type: application/json

## Nächste Schritte

Informationen zum Starten von Aufrufen mit der [!DNL Audit Query]-API finden Sie im [Ereignis-Endpunkthandbuch](./events.md) und im [Export-Endpunkthandbuch](./export.md).
