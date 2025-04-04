---
title: Handbuch zur Audit Query API
description: Audit Query ist eine RESTful-API, mit der Entwickler sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
role: Developer
feature: Audits, API
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 9%

---

# [!DNL Audit Query]-API-Handbuch

Die [!DNL Audit Query]-API stellt Endpunkte bereit, mit denen Sie Ereignisdaten für verschiedene Adobe Experience Platform-Funktionen programmgesteuert abrufen und überwachen können. Die Endpunkte sind unten beschrieben. Wichtige Informationen [ erforderlichen Kopfzeilen, zum Lesen von Beispiel](./getting-started.md)API-Aufrufen und mehr finden Sie im Handbuch „Erste Schritte“.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge zu sehen, besuchen Sie den [[!DNL Audit Query] API-Swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Ereignisse

Audit-Ereignisse bieten Einblicke in Benutzeraktionen in Experience Platform, einschließlich Aktionstyp, Datum und Uhrzeit, E-Mail-ID der Person, die die Aktion ausgeführt hat, und zusätzliche Attribute, die für den Aktionstyp für verschiedene Funktionen in Adobe Experience Platform relevant sind. Informationen zum Abrufen von Metriken mithilfe der API finden Sie im [Handbuch zu Ereignisendpunkten](./events.md).

## Exportieren

Der Auditexport ermöglicht es Ihnen, Ereignisdaten abzurufen, indem Sie die Ereignisse angeben, die Sie in der Payload abrufen möchten. Informationen zum Abrufen von Metriken mithilfe der API finden Sie im [Handbuch zu Exportendpunkten](./export.md).
