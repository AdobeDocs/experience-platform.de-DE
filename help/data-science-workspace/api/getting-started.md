---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen;Datenwissenschaftsarbeitsbereich;Datenwissenschaften
solution: Experience Platform
title: Sensei Machine Learning API
topic-legacy: Developer guide
description: Die Sensei Machine Learning API ermöglicht Entwicklern, CRUD-Vorgänge auf verschiedenen Data Science Workspace-Ressourcen durchzuführen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 16%

---

# [!DNL Sensei Machine Learning] API-Handbuch

Die [!DNL Sensei Machine Learning]-API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von maschinellen Lerndiensten, von der Algorithmusüberwachung über Experimente bis zur Dienstbereitstellung.

In diesem Entwicklerhandbuch finden Sie Anleitungen, die Ihnen beim Beginn mit der [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) helfen. Außerdem werden API-Aufrufe für die Ausführung von CRUD-Vorgängen in verschiedenen Data Science Workspace-Ressourcen veranschaulicht.

## Erste Schritte

Sie müssen das Tutorial [authentication](https://www.adobe.com/go/platform-api-authentication-en) abgeschlossen haben, um Zugriff auf die folgenden Anforderungsheader zu haben, um Aufrufe an [!DNL Adobe Experience Platform]-APIs durchzuführen:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* x-sandbox-name: `{SANDBOX_NAME}`

Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Authentifizierungsberechtigungen gesammelt haben, können Sie in den folgenden Abschnitten dieses Entwicklerhandbuchs Muster-API-Aufrufe für die folgenden Endpunktgruppen ausführen:

* [Engines](./engines.md)
* [Experimente](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Rezepte)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelle](./models.md)
* [Anhang](./appendix.md)
