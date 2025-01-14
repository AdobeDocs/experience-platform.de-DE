---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen;Datenwissenschafts-Arbeitsbereich;Datenwissenschaft
solution: Experience Platform
title: Handbuch zur API für maschinelles Lernen in Sensei
description: Mit der Sensei Machine Learning-API können Entwickler CRUD-Vorgänge für verschiedene Data Science Workspace-Ressourcen durchführen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
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

Die [!DNL Sensei Machine Learning]-API bietet Datenwissenschaftlern einen Mechanismus zum Organisieren und Verwalten von Services für maschinelles Lernen, von der Einführung von Algorithmen über Experimente bis hin zur Bereitstellung von Services.

Dieses Entwicklerhandbuch enthält Schritte, die Ihnen bei der Verwendung der [Sensei-API für maschinelles Lernen helfen](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) und veranschaulicht API-Aufrufe zum Ausführen von CRUD-Vorgängen für verschiedene Data Science Workspace-Ressourcen.

## Erste Schritte

Sie müssen das Tutorial [Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um Zugriff auf die folgenden Anfragekopfzeilen zu erhalten, über die Aufrufe an [!DNL Adobe Experience Platform] APIs durchgeführt werden können:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Content-Type: application/json

## Nächste Schritte

Nachdem Sie die erforderlichen Authentifizierungsdaten gesammelt haben, können Sie mit den nachfolgenden Abschnitten dieses Entwicklerhandbuchs für Beispiel-API-Aufrufe an die folgenden Endpunktgruppen fortfahren:

* [Engines](./engines.md)
* [Experimente](./experiments.md)
* [Insights](./insights.md)
* [MLInstances (Rezepte)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelle](./models.md)
* [Anhang](./appendix.md)
