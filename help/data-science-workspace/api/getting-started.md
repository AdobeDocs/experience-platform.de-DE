---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen; Datenwissenschaftsarbeitsbereich; Datenwissenschaft
solution: Experience Platform
title: Handbuch zur Sensei Machine Learning API
description: Mit der Sensei Machine Learning API können Entwickler CRUD-Vorgänge für verschiedene Data Science Workspace-Ressourcen durchführen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 34%

---

# [!DNL Sensei Machine Learning]-API-Handbuch

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Die [!DNL Sensei Machine Learning] -API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von Diensten für maschinelles Lernen, von der Onboarding von Algorithmen über Experimente bis hin zur Bereitstellung von Diensten.

Dieses Entwicklerhandbuch enthält Schritte, die Sie bei der Verwendung der [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) unterstützen, und zeigt API-Aufrufe zur Ausführung von CRUD-Vorgängen für verschiedene Data Science Workspace-Ressourcen.

## Erste Schritte

Sie müssen das Tutorial [Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um Zugriff auf die folgenden Anforderungsheader zu erhalten, um Aufrufe an [!DNL Adobe Experience Platform] -APIs durchführen zu können:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Authentifizierungsberechtigungen gesammelt haben, können Sie in den folgenden Abschnitten dieses Entwicklerhandbuchs API-Beispielaufrufe an die folgenden Endpunktgruppen senden:

* [Engines](./engines.md)
* [Experimente](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Recipes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelle](./models.md)
* [Anhang](./appendix.md)
