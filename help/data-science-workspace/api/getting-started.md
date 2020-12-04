---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: Entwicklerleitfaden für Sensei Machine Learning API
topic: Developer guide
description: In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der Sensei-API für maschinelles Lernen Beginn ausführen können. Außerdem werden API-Aufrufe für die Ausführung von CRUD-Vorgängen in verschiedenen Data Science Workspace-Ressourcen veranschaulicht.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 18%

---


# [!DNL Sensei Machine Learning]-API-Entwicklerhandbuch

Die [!DNL Sensei Machine Learning] API bietet Datenwissenschaftlern einen Mechanismus zur Organisation und Verwaltung von Dienstleistungen für maschinelles Lernen, von der Algorithmusüberwachung über Experimente bis zur Dienstbereitstellung.

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der [Sensei-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)für maschinelles Lernen Beginn ausführen können. Außerdem werden API-Aufrufe für CRUD-Vorgänge in verschiedenen Data Science Workspace-Ressourcen veranschaulicht.

## Erste Schritte

Sie müssen das [Authentifizierungs](../../tutorials/authentication.md) -Tutorial abgeschlossen haben, um Zugriff auf die folgenden Anforderungsheader zu haben, um Aufrufe an [!DNL Adobe Experience Platform] APIs durchzuführen:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

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