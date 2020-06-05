---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Entwicklerleitfaden für Sensei Machine Learning API
topic: Developer guide
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---


# Entwicklerleitfaden für Sensei Machine Learning API

Die Sensei Machine Learning API bietet Datenwissenschaftlern einen Mechanismus zur Organisation und Verwaltung von Dienstleistungen des maschinellen Lernens, von Algorithmus-Onboarding über Experimentierungen bis hin zur Service-Implementierung.

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)Beginn ausführen können. Außerdem werden API-Aufrufe für die Ausführung von CRUD-Vorgängen in verschiedenen Data Science Workspace-Ressourcen veranschaulicht.

## Erste Schritte

Sie müssen das [Authentifizierungs](../../tutorials/authentication.md) -Tutorial abgeschlossen haben, um Zugriff auf die folgenden Anforderungsheader zu haben, um Aufrufe an [!DNL Adobe Experience Platform] APIs durchzuführen:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Authentifizierungsberechtigungen gesammelt haben, können Sie in den folgenden Abschnitten dieses Entwicklerhandbuchs Muster-API-Aufrufe für die folgenden Endpunktgruppen ausführen:

* [Motoren](./engines.md)
* [Experimente](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Rezepte)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelle](./models.md)
* [Anhang](./appendix.md)