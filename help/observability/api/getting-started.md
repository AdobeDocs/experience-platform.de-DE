---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
solution: Experience Platform
title: Erste Schritte mit der Observability Insights API
topic-legacy: developer guide
description: Mit der Observability Insights-API können Sie Metrikdaten zu verschiedenen Adobe Experience Platform-Funktionen abrufen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Observability Insights-API durchführen.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 24%

---

# Erste Schritte mit der API[!DNL Observability Insights]

Mit der API [!DNL Observability Insights] können Sie Metrikdaten zu verschiedenen Adobe Experience Platform-Funktionen abrufen. Dieses Dokument bietet eine Einführung in die Kernkonzepte, die Sie kennen müssen, bevor Sie Aufrufe an die [!DNL Observability Insights]-API durchführen.

## Lesen von Beispiel-API-Aufrufen

Die [!DNL Observability Insights]-API-Dokumentation enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum Lesen von Beispiel-API-Aufrufen im Handbuch [Experience Platform Fehlerbehebung](../../landing/troubleshooting.md).

## Erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird. Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nächste Schritte

Um mit dem Aufrufen der API zu beginnen, fahren Sie mit dem [Metriken-Endpunktleitfaden](./metrics.md) fort.[!DNL Observability Insights]
