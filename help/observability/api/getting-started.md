---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
solution: Experience Platform
title: Erste Schritte mit der Observability Insights-API
description: Mit der Observability Insights-API können Sie Metrikdaten für verschiedene Adobe Experience Platform-Funktionen abrufen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die Observability Insights-API durchführen.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 51%

---

# Erste Schritte mit der [!DNL Observability Insights]-API

Mit der [!DNL Observability Insights]-API können Sie Metrikdaten für verschiedene Adobe Experience Platform-Funktionen abrufen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen sollten, bevor Sie Aufrufe an die [!DNL Observability Insights]-API durchführen.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation der [!DNL Observability Insights]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum Lesen von Beispiel-API-Aufrufen im [Handbuch zur Fehlerbehebung bei Experience Platform](../../landing/troubleshooting.md).

## Erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll. Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nächste Schritte

Um mit Aufrufen mit der [!DNL Observability Insights]-API zu beginnen, fahren Sie mit dem [Handbuch zu Metriken-Endpunkten](./metrics.md) fort.
